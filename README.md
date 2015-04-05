#phalcon-volt-filter-translate
[![Phalconist](http://phalconist.com/ta-tikoma/phalcon-volt-filter-translate/default.svg)](http://phalconist.com/ta-tikoma/phalcon-volt-filter-translate)
##Preparation
**Add to app/config.php:**
```php
<?php

return new \Phalcon\Config(array(
...
    'application' => array(
      ...
        'messagesDir'    => __DIR__ . '/../../app/messages/',
      ...
    )
));
```
**Add to app/services.php**
+ Add translate service (for example, I set only one file for translate, you can add switch):
```php
...
/**
 * Translate
 */
$di->set('translate', function() use ($config) {
    require $config->application->messagesDir."ru.php";

    return new \Phalcon\Translate\Adapter\NativeArray(array(
        "content" => $messages
    ));
});
...
```
+ Add translate filter for volt [in file](https://github.com/ta-tikoma/phalcon-volt-translate/blob/master/app/config/services.php#L57):
```php
...
$volt->getCompiler()->addFilter('t', function($resolvedArgs, $exprArgs) use ($di) {
  return '$this->getDI()->get("translate")->_(' . $resolvedArgs . ')';
});
...
```
##Use
Now, in views file you can use: 
```twig
...
{% set aa = "test" %}
{{ aa|t }}
...
```
