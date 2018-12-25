PHPKoa Static
=================

安装
=======
```
composer require naka1205/phpkoa_static
```

使用
=======

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>PHPkoa Static</title>
    <link rel="stylesheet" href="/css/default.css">
</head>
<body>
    <img src="/images/20264902.jpg" />
</body>
</html>
```
```php
<?php
require __DIR__ . '/vendor/autoload.php';

defined('DS') or define('DS', DIRECTORY_SEPARATOR);

use Naka507\Koa\Application;
use Naka507\Koa\Context;
use Naka507\Koa\Error;
use Naka507\Koa\Timeout;
use Naka507\Koa\NotFound;
use Naka507\Koa\Router;
use Naka507\Koa\StaticFiles;

$app = new Application();
$app->υse(new Error());
$app->υse(new Timeout(5));
$app->υse(new NotFound()); 
$app->υse(new StaticFiles(__DIR__ . DS .  "static" )); 

$router = new Router();

$router->get('/index', function(Context $ctx, $next) {
    $ctx->status = 200;
    yield $ctx->render(__DIR__ . "/index.html");
});

$app->υse($router->routes());

$app->listen(3000);
```