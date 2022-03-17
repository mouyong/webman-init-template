## 安装

**注意: 安装包之前，先移除项目的 composer.lock 文件，避免无法安装 phinx 包的问题 (https://www.workerman.net/q/8016)**

`rm composer.lock && composer require mouyong/webman-init-template:dev-master`

## 启用插件

```
./webman plugin:install zhen-mu/support
./webman plugin:install mouyong/validate
./webman plugin:install mouyong/webman-init-template
rm app/controller/WebmanBaseController.php
```

## 引入的第三方包

|包名|作用|文档|
|---|---|---|
|zhenmu/support|基础支持|https://github.com/mouyong/php-support|
|mouyong/validate|表单验证|https://github.com/mouyong/validate|
|webman/console|web 命令行插件|https://www.workerman.net/plugin/1|
|vlucas/phpdotenv|.env 文件管理|https://github.com/vlucas/phpdotenv|
|illuminate/database|数据库|https://learnku.com/docs/laravel/9.x/database/12245|
|illuminate/pagination|数据分页|https://learnku.com/docs/laravel/9.x/pagination/12247|
|illuminate/events|event 事件|https://learnku.com/docs/laravel/9.x/events/12228|
|robmorgan/phinx|phinx 数据库迁移|https://tsy12321.gitbooks.io/phinx-doc/content/|
|yzh52521/webman-event|webman 基于 laravel event 的事件|https://www.workerman.net/plugin/27|


## 使用

1. 禁用默认路由，并按照文档配置路由信息
https://www.workerman.net/doc/webman/route.html


`config/route.php`

`Route::disableDefaultRoute();`


2. 配置数据库连接信息
https://www.workerman.net/doc/webman/db/tutorial.html

`config/database.php`

```
return [
    // 默认数据库
    'default' => 'mysql',

    // 各种数据库配置
    'connections' => [
        'mysql' => [
            'driver'      => getenv('DB_DRIVER') ?: 'mysql',
            'host'        => getenv('DB_HOST') ?: '127.0.0.1',
            'port'        => getenv('DB_PORT') ?: 3306,
            'database'    => getenv('DB_DATABASE') ?: 'webman',
            'username'    => getenv('DB_USERNAME') ?: 'root',
            'password'    => getenv('DB_PASSWORD') ?: '',
            'unix_socket' => getenv('DB_UNIX_SOCKET') ?: '',
            'charset'     => getenv('DB_CHARSET') ?: 'utf8mb4',
            'collation'   => getenv('DB_COLLATION') ?: 'utf8mb4_bin',
            'prefix'      => getenv('DB_PREFIX') ?: '',
            'strict'      => getenv('DB_STRICT') ?: true,
            'engine'      => getenv('DB_ENGINE') ?: null,
        ],
    ],
];
```

3. 在项目目录下创建 .env 文件，并更具需要配置环境变量

`cp .env.example .env`

```
# database
DB_DRIVER=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=webman
DB_USERNAME=root
DB_PASSWORD=root
```

4. 控制器继承

```
<?php

namespace app\controller;

use support\Request;
use Mouyong\WebmanInitTemplate\Controllers\WebmanBaseController;

class Index extends WebmanBaseController
{
    <...>
}
```

5. 错误处理集成

见文档 README.md 说明: https://github.com/mouyong/php-support

`support/exception/Handle.php`

```
<?php

namespace support\exception;

use Webman\Http\Request;
use Webman\Http\Response;
use Throwable;
use Webman\Exception\ExceptionHandler;
use ZhenMu\Support\Traits\WebmanResponseTrait;

class Handler extends ExceptionHandler
{
    use WebmanResponseTrait;

    <...>
    
    public function render(Request $request, Throwable $exception): Response
    {
        return $this->renderableHandle($request, $exception); // 这里进行调用，做了一些错误捕捉
    }
}
```
