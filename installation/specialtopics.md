# Special Topics

Some specific system software combinations may require some additional configurations to work
 with XOOPS. Here are some details of known issues and guidance for dealing with them.

## SELinux Environments

Certain files and directories need to be writable during install, upgrade and normal operation
of XOOPS. In a traditional Linux environment, this is accomplished by ensuring that the
system user that the web server runs under has permissions on the XOOPS directories, usually by 
setting the appropriate group for those directories.

SELinux enabled systems (such as CentOS and RHEL) have an additional, a security context, that
can restrict a processes ability to change the file system. These systems may require 
changes to the security context for XOOPS to function correctly.

XOOPS expects to be able to freely write to certain directories during normal operation. 
Additionally, during XOOPS installs and upgrades, certain files must be writable as well.
 
During normal operation, XOOPS expects to be able to write files and create sub directories 
in these directories:

- `uploads` in the main XOOPS web root
- `xoops_data` wherever it is relocated during the install

During an install or upgrade process XOOPS will need to write to this file:

- `mainfile.php` in the main XOOPS web root

For a typical CentOS Apache based system, the security context changes might be 
accomplished with these commands:

```
chcon -Rv --type=httpd_sys_rw_content_t /path/to/web/root/uploads/
chcon -Rv --type=httpd_sys_rw_content_t /path/to/xoops_data/
```

You can make mainfile.php writable with:

```
chcon -v --type=httpd_sys_rw_content_t /path/to/web/root/mainfile.php
```

Note: When installing, you can copy an empty mainfile.php from the *extras* directory.

You should also allow httpd to send mail:

```
setsebool -P httpd_can_sendmail=1
```

Other settings you might need include:

Allow httpd to make network connections, i.e. fetch rss feeds or make an API calls:

```
setsebool -P httpd_can_network_connect 1
```

Enable network connection to a database with:

```
setsebool -P httpd_can_network_connect_db=1
```

For more information consult your system documentation and/or systems administrator.

## MySQL 8.0 Environments

MySQL 8.0 is not fully supported in PHP versions before 7.1.16, or PHP 7.2 versions before 7.2.4. In earlier versions, 
issues with the  PHP *mysqlnd* library may require the MySQL server's *default-authentication-plugin* to be set to 
*mysql_native_password* to function correctly.
 
Additional background may be found here: 

https://www.php.net/manual/en/mysqli.requirements.php

https://mysqlserverteam.com/upgrading-to-mysql-8-0-default-authentication-plugin-considerations/