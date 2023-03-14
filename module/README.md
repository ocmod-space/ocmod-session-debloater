# Session Debloater

## Description
**Session Debloater** is an extension that designed to fix a known OpenCart 3.x issue [#7094](https://github.com/opencart/opencart/issues/7094) and prevent bloat of the `oc_session` table.  
The extension is compatible with OpenCart versions 3.x up to and including 3.0.3.6. In these versions, expired customer sessions are not removed from the database, so the `oc_session` table size can grow up to gigabytes. This issue was only finally fixed in version 3.0.3.8 - expired sessions are deleted at the start of a new session, but with a probability of about 1 in 100 (to reduce the load on the server). In version 3.0.3.7 there was a bug and sessions were cleared frequently - every 99 times out of 100.  
Session lifetime is defined in file `php.ini` by parameter `session.gc_maxlifetime` in seconds (1440 by default).

> **Warning**  
> DON'T INSTALL THE EXTENSION IF YOU CAN'T RESTORE THE DB AND FILES IN CASE OF ERRORS!  
> YOU ARE FULLY RESPONSIBLE FOR ANY DAMAGE TO YOUR STORE FILES OR LOSS OF DATA, SO START ALL THE CHANGES BY BACKING UP THE DB AND FILES!

## Features
* Removes old session entries from the `oc_session` table.
* Has two types of implementation (see below).
* Does not modify system files (OCMOD).

So there are two types of this fix to download:
1. [session-debloater--default.ocmod.zip](../addons/default/zip/session-debloater--default.ocmod.zip) - the trigger (customer login) will fire randomly about 1/100 (default OC 3.0.3.8 behaviour).  
2. [session-debloater--instant.ocmod.zip](../addons/instant/zip/session-debloater--instant.ocmod.zip) - expired sessions will delete every time a new session starts.

## Issues
Deleting too many records can take a long time and the query execution will be interrupted, which in turn will cause an error message, something like:
```
Fatal error: Uncaught Exception: Error: Lock wait timeout exceeded; try restarting transaction.
```
This is not an extension error! To avoid this, it is best to clear the `oc_session` table manually before installing the extension using, for example, *phpMyAdmin*.

## License
Licensed under the [MIT License](https://raw.githubusercontent.com/ocmod-space/ocmod-session-debloater/main/LICENSE.txt)

## Links
[Opencart Marketplace](https://www.opencart.com/index.php?route=marketplace/extension/info&extension_id=38580)  
[Homepage](https://www.ocmod.space/session-debloater/)  
