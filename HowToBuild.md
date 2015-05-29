This is mostly based on http://www-archive.mozilla.org/build/mac_cfm.html with my own notes. I'm trying to remember all the gotchas I encountered initially getting this running; please make comments as you encounter your own glitches.

**Changes have occurred in this document as of 9.0.4.**

## Prerequisites ##

### Hardware/OS ###
The build environment is currently only supported on OS 9.0.4 and higher (9.1 or 9.2 recommended). It will probably build on OS 8.6 but this is considered serendipitous. I haven't tested trying to build on OS X and it would probably require some radical changes anyway.

You should have ample RAM and CPU: a G4 and at least 256MB is recommended. Currently the binary builds are made on an FW400 MDD Power Mac with dual Sonnet 1.8GHz G4 7447A processors, the most powerful Power Mac that can boot OS 9 directly, with 2GB of RAM (1.5GB available to OS 9). A simple relinking takes about 15 minutes; a complete build from utter scratch needs around 80 minutes. Do the math for your own box.

### Software ###

Classilla is built with Metrowerks CodeWarrior 7.1, with a portion using the Macintosh Programmer's Workshop (MPW). It will probably build with later versions of CW, but almost certainly not with earlier ones without converting the MCPs (and possibly not even then). The reason CW 7.1 was chosen is it is fairly easy to find/purchase used.

You should not have multiple copies of MPW on your build system; only use the one that comes with CodeWarrior. If you install multiple MPWs, you will have multiple ToolServers which can cause your build to fail inexplicably.

To properly install the CodeWarrior environment,
  * Run the installer(s) and select a stock full Mac C/C++ installation (Mach-O is not required; you can install that and/or Win32 if you want). Make sure that PowerPlant, the CodeWarrior Plugin SDK and CodeWarrior MPW are installed.
  * Unpack the Classilla source. **This is in the ballpark of 30,000 files. It is strongly recommended you do this on a separate, HFS+-formatted partition or disk other than your boot volume.**
  * In `mozilla:build:mac`, find RunTSScript and make sure it is a CodeWarrior plugin with Get Info (if not, drop it on StuffIt Expander and rename the resulting AppleDouble file back to RunTSScript). Put it in `CodeWarrior Plugins:Compilers`. Later versions of the Classilla source have this already converted for you; the source for original 9.0 doesn't.
  * Enable the ToolServer menu (it looks like the Amiga window gadget) in the CodeWarrior IDE preferences. Make sure it can start ToolServer. Make sure all the ToolServer tools show up (in particular MakeStubs and DumpPEF). If not, chase down all the Tools folders, remove extraneous ones, and alias them to point to a central folder. This is critical for stubs.
  * The following libraries are needed if you don't already have them:
    * Menu Sharing Toolkit. This is a part of [MacBird](http://macbird.userland.com/download). Unpack MacBird, then copy the MST portion into `MacOS Support:Menu Sharing Toolkit:`
    * ICProgKit. Unpack into `MacOS Support:ICProgKit1.4:` Later versions may work. If you can't find one, the 1.4 I use is on the Google Code site.
    * AEGizmos 1.4.2. Unpack into `MacOS Support:AEGizmos 1.4.2:` If you can't find this, the 1.4.2 I use is on the Google Code site. This used to be required, and may still be required for building direct from Mozilla code, so you may still want to install it.
    * Universal Interfaces. 3.4.1 should already be under `MacOS Support:Universal:` but if not, [ftp://ftp.apple.com/developer/Development_Kits/](ftp://ftp.apple.com/developer/Development_Kits/)
    * WASTE should already be under `MacOS Support:(Third Party Support):WASTE 2.0 Distribution:`
    * You do not need to install GUSI, `zlib` or `libpng` separately; Classilla already comes with its own copy of what it requires. Do not link Classilla against any other version of these libraries that you might have on your system (the project files by default will prevent this).

I also suggest installing a copy of Make SMI or some similiar drag-and-compress tool for running off complete builds, as it makes packaging for distribution much easier.

Build automation is operated with a complex MacPerl script which functions essentially as the _make_ system. This requires some setup:

  * MacPerl 5.2.0r4; get it from http://www.cpan.org/ports/index.html#macosclassic . I haven't tried 5.6.1 but I don't see any reason why it wouldn't work. There is no 5.8 or 5.10 for classic MacOS.
  * If you use 5.2.0r4 you will also need cpan-mac 0.50 or higher from http://sourceforge.net/projects/cpan-mac/ . This is allegedly not required for MacPerl 5.6.1, but YMMV.
  * Configure your Perl as instructed by the documentation (if needed). In particular, I recommend going to MacPerl's preferences and selecting Run scripts from the Finder, instead of Edit them. It's a lot more convenient and you should probably do your editing in BBEdit anyway.
  * Next, install the following modules from http://backpan.perl.org/authors/id/C/CN/CNANDOR/ and http://www.cpan.org/modules/by-module/Archive/ . **Do not attempt to unpack them.** Drop them onto the CPAN installer applet instead (see the documentation) and they will be properly CRLF-ed and installed into the library directory. The parenthesized version is the one in use on the build system; otherwise use the latest available.
    * Compress::Zlib built for MacPerl (1.04)
    * Archive::Zip built for MacPerl (0.11)
    * Mac::AppleEvents::Simple
    * Mac::Apps::Launch
  * Find your `site_perl` folder. From the Classilla source, look in `mozilla:build:mac:build_scripts`. Copy the `Moz` folder into your Perl's `site_perl` folder (you could also put it in `lib` but this is non-standard and not recommended). This installs the Mozilla-specific Perl modules needed to talk to CodeWarrior and automate the build.
  * Find the `Mozilla build prefs` folder (this should be in the root, _not_ under `mozilla`). Drag this folder into your `System Folder:Preferences` folder. This is preconfigured for the options still supported in the Classilla build system.
  * Run `ClassillaFixAliases.pl` in the root folder. Ignore files it can't find for now. Resolve any ambiguous duplicates. This ensures that the current header files are in sync with their aliases.

## How to compile ##

If you did all this right, go into `mozilla:build:mac:build_scripts` and double-click `BuildMozilla.pl`. Perl will start up and start CodeWarrior in the background, and then do the following:

  * Manifest stage, where it determines what will be copied where.
  * Builds the `xpidl` tools to compile IDLs and headers. These are automatically installed for you under CodeWarrior. **The very first time you try to do a build, it will die after this point because CodeWarrior won't register the tool without a restart. Quit CodeWarrior and MacPerl, then restart the build script. You should never see this again.** If you can't get past this point, your CodeWarrior is not set up right and you should go through the directions above again to figure out why.
  * Compiles the IDLs and headers. If you can't get past this point, there is something wrong with the `xpidl` project file, or you didn't install the Plugin SDK.
  * Compiles the OS stub library. This is a critical and somewhat iffy step. If you have multiple ToolServers, or your ToolServer cannot see all the tools it needs, you may fail at this point (or possibly slightly later when CodeWarrior tries to link against the defective stub). If ToolServer doesn't even start, you probably blew it installing RunTSScript, or failed to convert it into a proper plugin that CodeWarrior will recognize. You might also have forgotten PowerPlant or have incomplete libraries.
  * Compiles the runtime. If this fails, it may also be the stub.
  * Compiles the crossplatform code. This is the longest part of the build process. If the first few shlbs come off like winners, you are likely to complete the build successfully.
  * Compiles the actual application ("apprunner").
  * Links in and jars chrome resources. If this bugs out, make sure you installed all the proper Perl extensions (particularly Archive::Zip or the build script will be unable to make the jar files).

Test your build by going to `mozilla:dist:viewer` and double-clicking Classilla. If it starts, congratulations. You might want to try running it in the CodeWarrior debugger by opening the `_apprunner.mcp` project, choosing the `apprunner` Target and selecting Debug from there if you are not sure that it will be stable on your system.

When you do future builds with a partially built system, you don't need to wait the full 90+ minutes to do the build; only the parts that need to be updated will be done. You can also build shared libraries directly from their own individual CodeWarrior projects without invoking the entire build process, which is much quicker, and they will be incorporated into your test Classilla simply by quitting and restarting the browser.

Old Mozilla hands will wonder where the part that converted the exported XML project files into MCPs went. It's still there, but the MCPs now come pre-converted since everything is only being built on Mac CodeWarrior. Eventually this will be removed from the build process also, since it's just unnecessary bulk.

## Running off a standalone build ##

To make a Classilla that can run on a different computer, it is not sufficient to merely copy the Classilla executable as the shlbs must come along with it. To make this process easier, Classilla includes `ClassillaGenerateDist.pl` that finds all the dependencies, copies them and groups them into a folder that you can immediately copy away. The only problem is that this can mess up your alias structure if you're not careful. I recommend:

  * When preparing to run off a standalone build, run `ClassillaFixAliases.pl` and make sure that all aliases are valid and pointing to valid files. Fix any ambiguities and make sure aliases that were not found are corrected before proceeding.
  * Run `ClassillaGenerateDist.pl`. In the `mozilla:dist:` folder will be a `_RTM Package` (formerly `Classilla` -- the `_` is a space) folder containing a completely standalone set of files. You can rename and drop this folder on Make SMI or DropStuff to create an archive, or copy it to another system. As of 9.0.4, the folder contains the Classilla readme, and Classilla itself in an enclosing folder (the readme comes from the `Classilla Dist Resources` folder; you can put other things in there too you want rolled in).
  * When this is done, **delete the Classilla standalone distribution folder**, empty the Trash and re-run `ClassillaFixAliases.pl` to make sure the aliases are still correct and have not been tainted to mistakenly point into the Classilla standalone directory which you just deleted.

9.0.4 also adds `ClassillaPackageDist.pl` which tries to make a CFM application package that is compatible with OS 9. This package seems to have trouble running on OS X, however, which is why it is still not the default build and should be considered experimental. It also won't work on OS 8.6, but should still open and be executable with the alias inside.

## Troubleshooting ##

**Debug builds don't work.**

Yup, they definitely don't. Don't try to run `BuildMozillaDebug.pl` yet. I intend to get this fixed again for a future version.

**Carbon builds don't work.**

Yup, they probably don't. I don't have any plans to support Carbon builds, but I have received some requests to maintain the targets even if they do not build currently. This might be examined later, but it is low priority.

**The build script can't find CodeWarrior.**

Trash `CodeWarrior IDE Path.txt` and see if the script can re-detect it.

**I want the build to start over but it keeps starting in the middle.**

There is a build progress file dropped in the root source directory enclosing `mozilla`. Delete that.

**During the manifest stage, I see several spurious errors.**

This is normal for the Mac OS 9 build. They are harmless.

**MacPerl freezes when starting CodeWarrior for the first time.**

Switch to CodeWarrior and keep it in the foreground. MacPerl's event handling gets a little daft if it's foregrounded. It's also a lot faster if you keep CodeWarrior front, at least until you get to Stubs (see below).

**CodeWarrior freezes while building stubs.**

Make sure RunTSScript got installed correctly, but even if it is, CodeWarrior sometimes can't start ToolServer if it's the front process. Switch to the Finder and it should start up or go clicking around the screen to prime the Apple Events chain. You might need to do this again even after ToolServer starts, because to build the stubs ToolServer has to run _twice_. A tool like LiteSwitch is perfect for this, btw; just go switching into random other apps to flush Events and unstick the process.

Alternatively, this sometimes happens if you have ToolServer running before the script expects to start it up. Stop the script, stop ToolServer, and restart the build.

In general, I find that the stubs build most reliably if you start the build script and then _don't touch anything_ until stubs are built.

When you get stubs built properly for the first time, you might want to comment `BuildStubs()` out of the build .pm so that you don't have to build it again; they are unlikely to ever change and just represent the most likely way the build process can go wrong.

**The runtime will not build (compiler or linker errors).**

This usually means the stubs are defective. Look in `mozilla:dist:client_stubs` and check the size of NSStdLibStubs (should be around 24K) and InterfacesStubs (should be around 300K). An abnormally small NSStdLibStubs (8K or less) usually indicates a bad stub and means ToolServer probably did not run. Use ToolServer to try to dump the stub with DumpPEF if you're not sure. Ignore InterfacesXStubs, this is a holdover from Fizzilla and will disappear in the future. Make sure that you installed RunTSScript, PowerPlant and any other libraries correctly as well.

Also, some people have reported problems with 3.4.1 Universal Interfaces' ContextualMenu
stub library. If your NSStdLibStubs and InterfacesStubs appear good and look valid to
DumpPEF, replace it with the one from 3.3.2 and see if that helps. You may need to completely rebuild the stub libraries for this to take.

**CodeWarrior can't find a lot of .h files but they are there.**

Usually means (a) bad alias(es). Run `ClassillaFixAliases.pl` and make sure everything points where it should. This typically occurs the **second** time around.

**CodeWarrior freezes up while building large shlbs.**

It's probably not frozen actually. For things like the layout shared library, the optimization step may take as long as several minutes on slower or more memory-impaired systems. During this process your computer may appear to lock up. Just be patient.

_Btw, this is **not** improved by giving CodeWarrior more RAM in Get Info._ In fact, you may make this **worse** by taking away temporary memory from the system, which is what CodeWarrior grabs during the compile process. However, you may get more oomph out of this by putting in more _physical_ RAM and turning off Virtual Memory.

**There sure are a lot of warnings.**

There sure are. (The record is layout: from a fresh build you may see nearly 3000 warnings, and even from a simple relinking you get a minimum 2k.) When I have nothing to do, I'll fix them. (/me smiles sweetly)