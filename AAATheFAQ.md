**Please don't modify this document unless you are authorized to do so.**

# FAQ #

This page will be for frequent user questions. Some of these are also answered on the main site, but are also here for convenient reference.

Questions answered in the FAQ are generally pertinent only to the **most current version of Classilla** although notes about earlier versions are also included for reference.


## What is Classilla? ##
Classilla is an updated open-source Mozilla-based web browser for the classic Macintosh OS (not Mac OS X, although it will run under Classic through 10.4). It is targeted for Mac OS 9, but will include 8.6 compatibility where possible.

The name is, naturally, a portmanteau of _Classic_ (for the classic MacOS) and _Mozilla_.

## What is Mozilla? ##
Mozilla is the force behind the Gecko layout engine, which powers (among others) Mozilla Firefox, currently the second most popular web browser in the world behind Microsoft Internet Explorer. This makes it a very popular foundation for building other browsers and browser-like software upon.

## What is Clecko? ##
Clecko is the fork of Gecko used in Classilla. Mozilla ended official Mac OS 9 support with 1.2, although versions through 1.3.1 would still generally build if the patches for OS X (the old Fizzilla build) were removed.

Because Mozilla 1.4 and up include so much OS X specific code that won't work with the CarbonLib available for Mac OS 9, the decision was made to split Gecko off at 1.3.1 (using the Gecko that was maintained in the venerable old WaMCom build) and backport later changes to it rather than use the Mozilla code base directly, which won't build. This version of Gecko thus has a significantly different lineage despite having a common ancestor, and while its sources are similar, its provenance and feature set are therefore necessarily different. To avoid confusion with the main Gecko, even though this forked Gecko is still mostly official Mozilla code, Classilla's version of Gecko was renamed Clecko.

## What was WaMCom? ##
[WaMCom](http://wamcom.kuix.de/) was Kai Engert's maintained version of Mozilla 1.3.1; the Mac build of WaMCom is the direct ancestor of Classilla. It is no longer supported or developed.

## Why patching? Why not simply port something like WebKit? ##
Although things like the WebKit-based Origyn Web Browser have had huge success on alternative operating systems such as MorphOS and AmigaOS, those operating systems have the advantage of maintained toolchains whereas Mac OS 8 and 9 haven't had such support in years, and are not well-suited to them. Such a port would require extensive groundwork just to begin the conversion. On the other hand, Mozilla for Mac OS 9 already exists, already works, and just needs to be made more up-to-date. (It also has the benefit of building on existing tools, and is well-known for being cross-platform and well-tested.) It's the old battle between the new hotness which will solve all our problems but might never get released, and the old and busted which exists now and can be used now even if it's not fully functional. To create a new port out of whole cloth is a huge amount of work, even if the payoff is obvious. For practical reasons, this is what we're sticking with.

## Does Mozilla support Classilla or Clecko? ##
No, and [Mozilla has no plans to support Mac OS 9](http://groups.google.com/group/mozilla.dev.planning/msg/567792b17859a038) again given the niche user base. For this reason, **you should not ask Mozilla for support of Classilla/Clecko, nor should you file Bugzilla entries about bugs in Classilla.** If there is a specific issue that merits Bugzilla notation, let the Classilla project leads determine that on your behalf.

## When will new versions of Classilla come out? ##
See [Roadmap](Roadmap.md).

## What is Bugzilla? What are Bugzilla numbers? ##
Strictly speaking [Bugzilla](http://bugzilla.mozilla.org/) refers to either the Bugzilla software package, or Mozilla's own Bugzilla installation which is used for tracking Mozilla bugs. In our usage, we almost always mean the latter sense. A Bugzilla number refers to the ID number of a specific issue in the Bugzilla database, with its associated patch(es), if any. **If your bug report corresponds to a specific Bugzilla number, including that in your report helps immensely as there may already be a patch that can be adapted.**

Again, you should **not** file Bugzilla issues for Classilla.

## Can I run Classilla on OS X? ##
Yes. In fact, Classilla may be the best browser option for you if you are running Rhapsody or a very old version of OS X such as 10.0 or 10.1, but you must run it in Classic (or OS X Server/Rhapsody's Blue Box) as it is not Carbonized. Reports from 10.2 users also indicate that it performs better than SeaMonkey 1.1.x in some circumstances, so a combination may be your best best for Jaguar.

If you are looking for a general OS X browser for PPC, however, there are better choices in later versions. For 10.3, Camino 1.6.11 (though EOL) still performs relatively well, and 10.4-10.5 have a maintained PowerPC Firefox branch with [TenFourFox](http://www.tenfourfox.com/), our sister project.

Nevertheless, each version of Classilla is tested on 10.4 Classic before release and is fully compatible. Please note that depending on your version of OS X, the Classic environment may (in some cases noticibly) degrade Classilla's performance. Classilla is naturally always fastest in a native, non-emulated environment.

To run Classilla on an Intel Macintosh or on 10.5 or later, since neither support Classic, you must use an emulator such as SheepShaver. Although it is not officially supported, people have used Classilla on SheepShaver and demonstrated that it runs well. SheepShaver on BeOS is also compatible. Again, its performance under emulation may be significantly impacted. Classilla does not run under Basilisk II, because that is a 68K Mac emulator (see the next question).

## Can I run Classilla on a 68K Macintosh? ##
Not natively. Classilla is currently built with a version of CodeWarrior that only supports PowerPC, and relies on certain specific features of OS 8.5 and later such as Unicode support (see the next question). It is possible to backport these features to OS 8.1 or possibly earlier and/or adjust the portions of the browser that depend on them (again, see the next question for more), but that task is demonstrably non-trivial, and the memory demands may seriously restrict which machines could run Classilla even if those constraints were otherwise met.

However, if you have **a 68K Mac with a PowerPC card** such as any of the 601-based PDS cards out there, those Macs _can_ run Classilla as long as you have sufficient memory and can boot 8.6 on them (the Sonnet PPC cards can with their enabler, for example). Please note that their performance will be, at best, pedestrian.

## Can I run Classilla on 7.x, 8.0 or 8.1? ##
No, for the same reasons as above; Classilla's runtime depends on certain features of Mac OS 8.5 and higher such as ATSUI and Unicode support. Again, there has been some talk of disabling the portions of Classilla that depend on these features or backporting the needed OS libraries, but this work is unlikely to be done in the near future and such a modification would also severely limit its usefulness for multilingual pages. Likewise also, many of the Macintoshes limited to these OS versions have significant memory pressure and Classilla has never been particularly thrifty with RAM. In short, while such a "Classilla 7" is theoretically possible, a fair amount of work would be needed to get it mounted, it would not be as functional as standard Classilla, and it would detract from our top priority which is to be as compatible with modern websites as possible.

## Classilla says I don't have the Contextual Menu Extension and won't start. ##
That's because you don't. The Contextual Menu Extension is a standard part of Mac OS 8.6 and 9, and should have come with your operating system. However, it is possible that it may have been inadvertently disabled (check the `Extensions (Disabled)` folder) or deleted. If so, consider reinstalling your OS, or copying the extension from another computer. Classilla requires this extension to run and cannot start without it.

## Is Classilla localized or available in other languages? ##
Yes. Classilla as of 9.2.2 comes with Japanese (日本語) and German (Deutsch) translations. You can select the translation for your profile by going to Preferences > Language/Content, and selecting your desired language and/or region. Remember, restart immediately after changing the language, or the interface may behave incorrectly.

If you'd like to try creating your own, see [How to localize Mozilla](http://www-archive.mozilla.org/projects/l10n/mlp_howto.html) (which will also work for the older code in Classilla). If you would like to contribute to the project as a translator, see [issue 151](https://code.google.com/p/classilla/issues/detail?id=151).

## When I use Classilla, I get mobile sites, not full sites. ##
Starting in 9.3.0, Classilla pretends to be a mobile browser to sites by default (a whitelist internally keeps exceptions). This gives pages that are smaller, simpler to render and faster to process, and surprisingly give you nearly all the functionality you got on the full desktop site. Try it. You'll like it.

But, if you don't, you have two options. Many sites will let you set a cookie to disable the mobile site such as Wikipedia; the mobile page will have a link to let you turn it off. To go back to the mobile version, delete that cookie or select the mobile option again.

For sites where even _that_ doesn't work, you can choose a desktop user agent from Preferences, Navigator, User Agent. This setting persists even if you navigate to a different site or quit the browser, but because this is non-standard, you will get a warning when you boot the browser with a non-standard user agent selected because Classilla may not support all the features the site may think it does.

## Does Classilla support TLS or SSL? ##
Classilla supports TLSv1, SSLv2 and SSLv3. Of the three, TLS is the most preferred and highest level of security, while SSL is an older encryption technology predating TLS. SSLv2 is no longer secure and should no longer be used; it is disabled by default starting in Classilla 9.3.3 and will be removed completely in a future version. SSLv3 is still available but is considered deprecated due to intrinsic flaws in the protocol and will be disabled by default in a future version. In addition, "export-only" low-key-length symmetric ciphers are also considered deprecated and will be disabled by default in a future version.

Classilla does support TLSv1, but versions prior to 9.3.3 did not support certain features which may cause sites to renegotiate SSLv3. In 9.3.3, support for Server Name Indication (SNI) was added, which improves verification of certain secure websites.

Classilla's encryption package does not currently include higher performance elliptic curve support, but does support regular Diffie-Hellman exchange for forward secrecy. For example, DHE-RSA-AES256-SHA is fully supported.

## Some secure websites give me an error -8182. ##
These sites use SHA-256 certificates for TLS. This support was added in Classilla 9.3.3.

## Some secure websites give me a dialogue box saying the site could not be verified. ##
Classilla allows you to override certain checks on certificate identity when you know or trust that the network and site you're connecting to have not been compromised. For example, if the domain name is slightly different, or the certificate is recently expired, you may receive this box but the certificate may still be perfectly safe to accept temporarily. You receive this box if the certificate name differs, the certificate is expired, it is signed by a certificate authority you don't currently accept, or, starting in 9.3.3, if the certificate is signed with an algorithm that Classilla does not yet understand.

With the added support in 9.3.3 and later versions, this situation should be much less common. If it occurs, you should examine the certificate carefully and decide what to do and how long you want the exception to last. There is no good rule of thumb on when this is safe to do, although **a site that used to work and suddenly fails to work, especially on a different network, should be considered an indication your connection is _not_ safe.** Remember: if you override a certificate check, you are telling Classilla that verification is not required or possible, which may cause you to send information to an unauthorized third party which is masquerading as the trusted site. Be cautious when approving these requests.

## Will Classilla support HTML 5? ##
Certain portions will be supported (and some actually already are invisibly). The most visible features such as CANVAS tags, however, will require extensive work for Clecko's non-Cairo-based graphics architecture, and features such as VIDEO and AUDIO tags may never be supported due to poor codec availability for OS 9. Networking support may also be difficult to integrate with the older Clecko codebase. There are no promises, let alone an ETA, for any of these features. On the other hand, most document-based tags are easy to incorporate into Classilla's parser and many of these are or will be supported.

Currently, however, the highest priority is making sure that HTML 4.01 and CSS 2 are supported to a functional level; this is incomplete, but improving.

## Some pages render really slowly. ##
There are several layout glitches that can cause Classilla to slow down dramatically on sites with complex or pathologic layouts. You can all-stop the browser by holding Cmd-Period down until you get control back. Note that when you do this, everything in layout stops and the current executing script (if any) stops as well, so the page might not appear correctly. However, this is safer than Force Quit, so try using all-stop first if Classilla seems to have stopped responding for awhile.

**If you were using JavaScript on this page, see "JavaScript makes my computer freeze" for an important consideration.**

## Some pages look awful when they scroll. ##
A few pages are not compatible with the way Classilla currently scrolls the screen. **You can use an alternative (though possibly slower) method of scrolling by holding down the Command key as you scroll.** If you are on a site where you have to do this frequently, you can toggle the default setting by going to View > Use Slow Scroll, or pressing Cmd-Shift-S. This setting is sticky and stays until you turn it off.

## JavaScript doesn't work in Classilla. ##
Classilla uses Script-B-Gone, its own special front end to NoScript, to help reduce possible security and stability problems.

By default, **Script-B-Gone is configured to block all JavaScript** except on certain pages where it must be enabled. Script-B-Gone appears in your Classilla window as a little "S" at the lower right (the NoScript logo) which you can click to change its settings: either add the current website to the white list, or, if you are adventurous or reckless, allow it on all pages by clicking Options for advanced settings. For more information, see the [Release Notes](http://www.classilla.org/releases/).

## When JavaScript is on, clicking on certain links doesn't work. ##
There are two possible reasons:

  * The links themselves are in JavaScript that Classilla can't understand. You must disable JavaScript to navigate that particular site. There should be very few of these sites now with the updated interpreter. If you find one, please send it to Report-A-Bug.

  * Sites using Microsoft ASP do not recognize Classilla as a Mozilla-based browser, and fail to insert the correct JavaScript code for their links. To fix that, go to (in 9.0.4 and up) Preferences and change the User-Agent to Firefox, then reload the page and the links should start to function. Remember to change the User-Agent back when you're done. You can recognize these links because they look something like this:
```
javascript:__doPostBack('something', 'something else')
```

## JavaScript makes my computer freeze. ##
Certain scripts take a very long time to execute on slower Macs, and some may inadvertently trip bugs in layout or DOM. These bugs may make Classilla appear to have stopped responding or render very, very slowly.

**You can cancel a script the same way you cancel layout by using the all-stop command (Command-Period ".").** However, this may prevent the page from completing its initialization, and may leave event handlers on the page in an indeterminate state. If you all-stop a page with JavaScript on, you should close that page's window or tab when you get control of the browser, and reload it with JavaScript disabled.

Note that touching certain elements of the page or moving your mouse may also cause scripts to resume execution. Classilla cannot control this individually.

## Will Classilla's JavaScript and layout/DOM support be updated? ##
Starting with Classilla 9.2, Classilla now uses a minimally modified version of SpiderMonkey, the exact same JavaScript interpreter Mozilla uses in Firefox 3.0.19. This interpreter is much faster and more stable than the one in previous versions of Classilla or WaMCom, and repairs many inadequacies.

That said, the Document Object Model (the piece that connects JavaScript to the web page) is still fairly out-of-date and many sites relying on very current features still won't work completely. This can only be upgraded to a certain point. Fortunately, mobile content is much less demanding and generally equally functional, and Classilla now fetches mobile content by default anyway (see above). For those sites that are still difficult to get working, you can use Byblos -- see the next question.

## What is Byblos? How can I write my own Byblos site translators? ##
Byblos is (in Classilla 9.3.0 and up) Classilla's own HTML rewriting engine. Similar to Firefox Greasemonkey, but at a much lower level, Byblos allows you to write JavaScript snippets called _stelae_ that can take the HTML for a page and dynamically insert, change or even cut out portions of it dynamically. Byblos stelae can get many sites that can't render at all to function, and you can write them yourself with just a text editor. See ByblosSteleDocs for how.

## Does Classilla support plugins? ##
Classilla runs most NPAPI plugins, but most OS 9 compatible plugins are no longer updated and many have security issues (see the question on Flash below). That said, they may still be useful if you require their capabilities, **but using these old versions is at your own risk.** George Serban maintains a list of Classilla-compatible plugins at http://cherwally.webs.com/Classilla/Plugins.html

## Does Classilla support Flash? ##
Yes, but OS 9 support was dropped after Flash 7. **There are known security problems in that version of Adobe Flash Player and its use is strongly discouraged.** Still, this is enough to surf many sites and even view many videos, although people have reported synchronization issues with certain codecs. Your humble author, however, does not use it.

## Flash (and other plugins) make Classilla flicker really badly sometimes. ##
This is a known and unfortunately unfixable bug due to the way plugins in general work in Mac OS 9. See [issue 14](https://code.google.com/p/classilla/issues/detail?id=14).

If this really bugs you, you can disable plugins completely by going to Preferences > Advanced > Performance and checking Disable plugins.

## Does Classilla support Java? ##
Yes, but only the version of Macintosh Runtime for Java that Apple provides with your version of Mac OS. **There are known security problems in all classic Mac OS versions of the MRJ and its use is strongly discouraged.** By default, Java is forced off in new profiles. You can turn it on from the preferences panel, but you should only use it on trusted sites. You will need to have plugins enabled and ensure that the MRJ Plugin is in your plugins folder (it comes with Classilla 9.2.1 and later).

## Does Classilla support theming? ##
Yes, but due to its roots in Mozilla 1.3, it only supports Mozilla 1.3-compatible themes. That said, there are a lot of these still around which work just great with Classilla, and several Classilla-specific themes. Themes require at least Classilla 9.2 due to installation bugs that were fixed in that version. Tim Grissom maintains his custom theme and others at http://www.transcorp.com/AutoIndex/HTML/classilla.shtml .

## Classilla disables Sherlock 2 on my non-English Mac. ##
If you are using a non-English keyboard and running Sherlock 2 and Classilla at the same time, your keyboard will not work in Sherlock 2 (it will work fine elsewhere). This can be solved by temporarily switching to an English keyboard layout. It is currently being debated whether this is a Mozilla or Mac OS/Sherlock bug.

## Non-Roman character sets don't appear right under Mac OS 9.2. ##
The Unicode converter built into Mac OS 9.2 is not fully compatible with Classilla. It works correctly with OS 9.1. This is a known bug and is being investigated.

## Why doesn't Classilla support Chatzilla? ##
Chatzilla's final release under Classilla was with 9.0.4. It no longer appears in 9.1 and versions thereafter due to multiple known security flaws and difficulty integrating later versions with Classilla's older code base. There are many better IRC clients for Mac OS 9; you should use one of those instead. If you must use Chatzilla, you are limited to 9.0 and 9.0.4 (or WaMCom, etc.).

## How do I get Classilla set up to use Gmail's POP server? ##
The short answer is, right now you don't. Instead, use IMAP. The long answer is POP on Gmail for some reason causes Classilla to hang up when you quit. POP works fine on other servers, so it is not clear why and this is being investigated. In the meantime ...

## How do I get Classilla set up to use Gmail's IMAP server then? ##
The [standard settings that Google recommends](http://mail.google.com/support/bin/answer.py?answer=78799) will work, but here they are for reference:

  * Use `imap.gmail.com` port 993 for incoming IMAP. Enable SSL. Use your account name for your user name (the part before the @).
  * Use `smtp.gmail.com` port 587 for outgoing SMTP. Use STARTTLS.

Whenever Classilla prompts for your password, enter your Gmail password. Remember, you must enable IMAP in your Gmail settings before you can access it with IMAP.

## Will Classilla still support mail and news? ##
Currently, yes. There are enough users and enough user demand that Classilla will continue to support it for the immediate future. However, we do need testers to find and report bugs, as well as regular user reports. **You can help!**

## Will Classilla ever be as up-to-date as Firefox? ##
That depends on the devotion and hardwork of the maintainers, leads and programmers. We're always looking for a few good Mac nerds.

## How can I help with Classilla? I only know HTML. ##
You can still be a big help as a distiller. See [BeAPart](BeAPart.md).

## How can I help with Classilla? I'd like to code and build my own. ##
To build your own Classilla on your own system, you need to set up a sane build environment. See HowToBuild.

Once you have Classilla built and want to do your own stuff to send in, you have to obey certain conventions for code (and to ensure that resource forks are not trampled upon). See [BeAPart](BeAPart.md) and HowToSubmit.

## My question is not answered by this document. ##
If you have a specific issue with Classilla which you think is a bug, look under the Issues tab for what the coders are currently working on.

If you don't see a bug listed and you're sure you've found one, please use Report-A-Bug (don't file bugs here unless you are authorized to do so; [Report-A-Bug](http://www.classilla.org/report) allows a reviewer to triage your bug so that the worklist is more efficiently updated).

If you have questions about Classilla or how it is administered, see http://www.classilla.org/ or send a message to classilla at floodgap dawt com.