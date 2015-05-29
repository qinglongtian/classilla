## You suck, there's no code repository! ##

One specific problem that classic Mac OS development has relative to other operating systems is that resource forks are not preserved with current revision control systems. Yes, you can use encodings like AppleSingle, but this is an extra step which slows things down, and fraught with peril if you forget to do the conversion because many tools won't warn you if there are no valid resources.

Until this issue is resolved to our satisfaction (and believe me we'll take any and all suggestions), there is no externally accessible code repository and thus you can't do checkins from outside Floodgap. This document talks about how to work around this problem.

## House style ##

When writing your code, please observe the following conventions:

  * Indent according to the file you are working on. Mozilla themselves weren't always consistent about this and indents change from file to file, but whatever the indent is with _this_ file, please use it.

  * Line length is not generally a big deal as long as it's not something unreasonable.

  * When patching code, since there is currently no outside revision control system, keeping "metadata" in the file is preferred for outsiders without tree access (that means pretty much everyone except leads). This means patches can be backed out manually by anyone for testing locally.
    * Tag **all** your changes with a unique, consistent identifier. For example, if this was based on a Bugzilla patch, use the bug number: `// bug 7654321` Or, if this is a specific Classilla issue number, use that: `// issue 1234567` If you had to modify the patch for Classilla, you might want to annotate that in the identifier.
    * If the change is a single line, tag the line with a tail comment using the identifier.
    * If you are deleting a block and replacing it with a new block, place the identifier at the beginning of the block, **comment out** the original code with `#if 0` and `endif` and add your changes immediately after, and then close the change with `// end bug`
    * If you are adding multiple lines of code, put the identifier at the beginning of the block, followed by your code, and then close the change with `// end bug`
    * If you used backported code, include the original code commented out so it can be compared. This is particularly important for complex reCOMtamination where sometimes people make mistakes.

Here is an example of such a code block:

```
// bug 234851 modified for 1.3
#if(0)
  PRBool isScrollable = IsScrollable(aPresContext, display);
  nsCOMPtr<nsIPrintPreviewContext> printPreviewContext(do_QueryInterface(aPresCo
ntext));
#endif
  // The document root should not be scrollable in any paginated context,
  // even in print preview.
  PRBool isPaginated = PR_FALSE;
  aPresContext->IsPaginated(&isPaginated);
  PRBool propagatedScrollToViewport = // added aPresShell to original patch
         (PropagateScrollToViewport(aPresContext, aPresShell) == aDocElement);
  PRBool isScrollable = IsScrollable(aPresContext, display)
                        && isPaginated
                        && !propagatedScrollToViewport;
// end bug
```

Eventually this chaff will be removed. Even if future versions still don't have an RCS, we will remove the old code for changes that are well tested. Don't do this yourself however; let a lead decide.

## How to properly submit code changes ##

All checkins are done on your behalf by a lead (currently this is Cameron) from your submissions into a private internal source tree. Your submission should obey the following constraints:

  * Please make sure your code builds! Openly defective code is not nice!

  * Please verify that you are not modifying actively worked on code (for example layout and DOM code are always at risk of being obsoleted by something else somebody else is working on). If you don't know, ask a lead.

  * Actual, full files are easier to work with than `diff`ed patches. Although there is an MPW tool for Larry Wall-ified `patch`es, it can be a little fiddly to work with, much like the Unix `patch` ;-) That said, if you are working on actively developed code, a true patch may be requested instead of a full file to integrate better into changes other people are making. Ask a lead if you don't know what to do.

  * Resource forks (if any) and type/creator codes must be sane and must be preserved. For example, keep all C/C++ header and source files owned by CodeWarrior (CWIE). For other things such as style sheets, DTDs, JavaScript, XUL, etc., we'd prefer them be TEXT/R\*ch so that they open up in BBEdit, but as long as they're TEXT/something, that is acceptable. Resource files should open in ResEdit. Files that should be owned/opened by Classilla should always be creator MOZZ. For all other files, use your judgment.

  * Include a minimum of files, with context. For example, if you only need to change two files in a source folder, tell us (either in the filename or in your comments on the submission) where the files should go, and _include only those files._

  * Compress and archive your patch with an approved archiving method. Even though Mactar is resource-fork aware, this requires a lot of fiddling to do proper conversion, so please don't use it. The best choice is StuffIt 5-format; if you don't have StuffIt Standard or Deluxe to do this, DiskCopy 4.2 is also acceptable, or an SMI (using a tool like MakeSMI). **Do not use ZIP!** You may, however, choose to zip up or gzip the resulting disk image, and that is fine.

  * Attach your patch to the issue in question, along with a description of the files and where they go. The bug owner will (if a lead) review and check in your patch, or (if not a lead) notify a lead for a code review once they have confirmed the patch builds.