Light_Bullsheet
===========
2019-08-14



A service for the [Light](https://github.com/lingtalfi/Light) framework to help generate fake data for a database.


This is a [Light framework plugin](https://github.com/lingtalfi/Light/blob/master/doc/pages/plugin.md).

This is part of the [universe framework](https://github.com/karayabin/universe-snapshot).


Install
==========
Using the [uni](https://github.com/lingtalfi/universe-naive-importer) command.
```bash
uni import Ling/Light_Bullsheet
```

Or just download it and place it where you want otherwise.






Summary
===========
- [Light_Bullsheet api](https://github.com/lingtalfi/Light_Bullsheet/blob/master/doc/api/Ling/Light_Bullsheet.md) (generated with [DocTools](https://github.com/lingtalfi/DocTools))
- [Services](#services)
- [Example](#example)




Services
=========


This plugin provides the following services:

- bullsheet


The service accepts bullsheeter instances. Each bullsheeter being its own stand-alone generator. 



Here is the content of the service configuration file:

```yaml
bullsheet:
    instance: Ling\Light_Bullsheet\Service\LightBullsheetService
    methods:
        setContainer:
            container: @container()
        setSilentMode:
            mode: true



```




Example
=========

From the Light_UserDatabase plugin, we want to allow the developer to generate fake users.

So we register to the bullsheet service like this (from the service configuration file of Light_UserDatabase):


```yaml
# ... some previous Light_UserDatabase configuration...
# ... some previous Light_UserDatabase configuration...
# ... some previous Light_UserDatabase configuration...

$bullsheeter.methods_collection:
    -
        method: registerBullsheeter
        args:
            identifier: Light_UserDatabase.lud_user
            bullsheeter:
                instance: Ling\Light_UserDatabase\Bullsheet\LightWebsiteUserDatabaseBullsheeter
                methods:
                    setApplicationDir:
                        dir: ${app_dir}
                    setAvatarImgDir:
                        dir: ${app_dir}/www/img/some/dir

```

And then we can call the bullsheeter like this:

```php
/**
 * @var $bull LightBullsheetService
 */
$bull = $container->get("bullsheeter");
$bull->generateRows("Light_UserDatabase.lud_user", 50);

```









History Log
=============

- 1.0.0 -- 2019-08-14

    - initial commit