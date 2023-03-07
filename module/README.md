# Session Debloater

## Description
**Session Debloater** is an extension that designed to fix a known OC 3.x (up to and including 3.0.3.6) issue [#7094](https://github.com/opencart/opencart/issues/7094) and prevents the `oc_session` table from being bloated.  
Compatible with OpenCart 3.x versions up to and including 3.0.3.6.

## Features
* Removes old session entries (session lifetime is defined in file `php.ini` by parameter `session.gc_maxlifetime` in seconds).
* Does not modify system files (OCMOD).

## Additional information
OpenCart versions up to and including 3.0.3.6 don't clear expired customer sessions, so the size of the `oc_session` table can grow to gigabytes. Session lifetime is defined in file `php.ini` by parameter `session.gc_maxlifetime` in seconds (1440 by default). This issue was finally solved in version 3.0.3.8 - records of expired sessions are deleted randomly at the start of each new session with a probability of about 1 in 100.
So there are two types of the fix to download:
1. [session-debloater--default.ocmod.zip](../addons/default/zip/session-debloater--default.ocmod.zip) - the trigger (customer login) fires randomly about 1/100 (default OC 3.0.3.8 behaviour).  
2. [session-debloater--instant.ocmod.zip](../addons/instant/zip/session-debloater--instant.ocmod.zip) - expired sessions delete every time a new session starts.

## Issues
Deleting too many entries can cause some errors like `Fatal error: Uncaught Exception: Error: Lock wait timeout exceeded; try restarting transaction`. To avoid this, it is best to clear the table manually before installing the extension using, for example, phpMyAdmin

## License
Licensed under the [MIT License](https://raw.githubusercontent.com/ocmod-space/ocmod-session-debloater/main/LICENSE.txt)

## Download
[Opencart Marketplace](https://www.opencart.com/index.php?route=marketplace/extension/info&extension_id=38580)
