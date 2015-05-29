**Please don't modify this document unless you are authorized to do so.**

# Roadmap #

This document is always subject to change, but basically covers which version of Classilla will come out when. In keeping with the OS 9-specific motif, initial versions will be numbered according to official Apple versions of OS 9 (while they last).

## Classilla 9.0 ##

This was the first release of Classilla with the updated "Clecko" layout engine. It is roughly the equivalent of Mozilla 1.6, but this is not exact (it lacks some 1.6 features, but also adds features from as late as 1.8). This version had layout and multiple security improvements, along with changes for rebranding and Mac-specific bug fixes.

This version was intentionally unfinished -- since WaMCom is no longer updated, this is the only version of Mozilla for the classic Mac that is even still theoretically maintained, so its release was accelerated to ensure continuity. For that reason, it was released in 'pre-alpha' form on June 30th, 2009.

## Classilla 9.0.4 ##

This was the second release of Classilla. It added additional security and network improvements from Bugzilla, and updates to JavaScript and DOM. Additional layout improvements were also present in this release, along with an experimental fixup rendering mode for sites that cannot be rendered with the standard layout engine, and various other MacOS-specific stability and functionality issues were also repaired. This was the final version to support Chatzilla.

Classilla 9.0.4 was released on October 28th, 2009.

## Classilla 9.1 ##

This was the third release of Classilla. This version restored the layout overflow branch (replacing the 9.0.4 experimental renderer), allowing more advanced rendering and further improvements with site compatibility, roughly somewhere between Mozilla 1.7 and 1.8, though again this is not exact (it lacks some core features of 1.7, but adds code from as late as 1.9). It also repaired the most important regressions caused by 9.0.4.

Classilla 9.1 was released on February 26th, 2010.

## Classilla 9.2 ##

This was the fourth release of Classilla. This version completely rewrote JavaScript, replacing it with the same interpreter used by Firefox 3.0.19, with additional targeted improvements to DOM and layout pending a complete update in 9.3. Although many sites still didn't work completely correctly due to missing DOM elements, many more sites became better supported at some level. The most important regressions caused by 9.1 were also mitigated or repaired, and theming was specifically supported with this release.

Classilla 9.2 was released on June 4th, 2010.

## Classilla 9.2.1 ##

This was the fifth release of Classilla. This version repaired various regressions caused by 9.2, and also introduced Script-B-Gone, a Classilla-specific front-end to NoScript. Various browser bugs were also repaired in this release, and strings were frozen to allow language packs to be officially supported in 9.2.2.

Classilla 9.2.1 was released on August 22nd, 2010.

## Classilla 9.2.2 ##

This was the sixth release of Classilla. This was a bugfix rollup only, repairing interface, system and security bugs; regressions caused by 9.2.1; and new bugs introduced by Script-B-Gone. The only new feature was the official introduction of language packs into the core browser, starting with Japanese and German.

Classilla 9.2.2 was released on March 29th, 2011.

## Classilla 9.2.3 ##

This was the seventh release of Classilla. This was another bugfix rollup covering important and critical issues that occurred between 9.2.2 and 9.3.0 to get these fixes to users while the internal redesign was completed. No new features were introduced with this release.

Classilla 9.2.3 was released on October 11th, 2011.

## Classilla 9.3.0 ##

This was the eighth release of Classilla. Starting with 9.3.0, Classilla will be numbered according to a conventional major-minor-patch scheme. This release converted Classilla into a browser focused on the mobile web, optimized for the slower/smaller systems limited to OS 8.6 and OS 9. This release also introduced Byblos, Classilla's dynamic HTML rewriting engine, and fixed several security and stability issues.

Classilla 9.3.0 was released on January 20th, 2012.

## Classilla 9.3.1 ##

This was the ninth release of Classilla. This was the first of several security rollups, focused on the new layout architecture and bringing the browser to security parity as much as possible, along with fixing the most important regressions introduced with 9.3.0.

Classilla 9.3.1 was released on October 19th, 2012.

## Classilla 9.3.2 ##

This was the tenth release of Classilla. This was the second security rollup, and also included regression fixes from 9.3.1 and Byblos CSS rewriting support.

Classilla 9.3.2 was released on January 6th, 2013.

## Classilla 9.3.3 ##

This is the eleventh release of Classilla. This is a major overhaul of the browser's encryption suite, including SHA-256 certificate support and improvements to TLS. This release also improves Byblos support and fixes several smaller bugs.

Classilla 9.3.3 was released on October 28th, 2014.

## Classilla 9.3.4 ##

This will be the twelfth release of Classilla. This will be the fourth security rollup.

There is no ETA currently for Classilla 9.3.4.