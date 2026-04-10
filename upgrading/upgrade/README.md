# Upgrading

The XOOPS Upgrader examines your XOOPS installation and applies any needed patches to make it compatible with the new XOOPS code. Patches may include database changes, adding default settings for new configuration items, file and data updates, and more.

The upgrader is tested against a variety of XOOPS installations, both old and new, but the process is smoothest with the most recent XOOPS releases. If you are upgrading an older system and need help, please visit our support forums at [https://xoops.org/modules/newbb/](https://xoops.org/modules/newbb/)

## About XOOPS 2.7.0 Upgrades

XOOPS 2.7.0 introduces **Smarty 4** as its templating engine (XOOPS 2.5.x used Smarty 3). Smarty 4 is stricter than Smarty 3 about template syntax, and some custom themes and module templates may need adjustments before they will work correctly on 2.7.0.

For this reason, XOOPS 2.7.0 ships with a **preflight scanner** that examines your existing themes and module templates for known Smarty 4 incompatibilities. You should run this scanner _before_ launching the main upgrader. See the [Preflight Check](preflight.md) page for details.

Another welcome change in 2.7.0: copying the new distribution over your existing site **no longer overwrites existing configuration files** such as `mainfile.php` and `xoops_data/data/secure.php`. You still need to be careful with customized themes and other files you may have edited — those are not protected by this behaviour, and the guidance in [Preparations for Upgrade](ustep-01.md) about preserving customizations still applies.

## Quick Overview

1. Make a full backup of site files and database.
2. It may be helpful to enable debugging in System Options → Preferences → General Settings.
3. It is wise to turn your site off in System Options → Preferences → General Settings.
4. Copy the contents of the distribution `htdocs` directory into your web root directory. In XOOPS 2.7.0, existing configuration files will not be overwritten.
5. Copy the contents of `htdocs/xoops_lib` to your relocated/renamed `xoops_lib` as applicable.
6. Copy the contents of `htdocs/xoops_data` to your relocated/renamed `xoops_data` as applicable.
7. Copy the distribution `upgrade` directory into your web root directory.
8. **Run `/upgrade/preflight.php`** and follow the [Preflight Check](preflight.md) guidance until the scan is clean.
9. Point your browser to _your-site-url_/upgrade/ and follow the prompts.
10. Log in and step through any needed updates with the "Continue" button.
11. At the end, upgrade the System module.
12. Also update `pm`, `profile` and `protector` modules if installed.
13. **Delete the `upgrade` directory** from your web root. Also delete the `install` directory if one is present.
14. Don't forget to turn your site back on.
