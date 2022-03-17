## 引入的第三方包

|包名|作用|
|---|---|
|zhenmu/support|基础支持|
|mouyong/validate|表单验证|
|webman/console|web 控制台插件|
|illuminate/database|数据库|
|illuminate/pagination|数据分页|
|illuminate/events|event 事件|
|vlucas/phpdotenv|.env 文件管理|

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
            'driver'      => getenv('DB_DRIVER', 'mysql'),
            'host'        => getenv('DB_HOST', '127.0.0.1'),
            'port'        => getenv('DB_PORT', 3306),
            'database'    => getenv('DB_DATABASE', 'webman'),
            'username'    => getenv('DB_USERNAME', 'root'),
            'password'    => getenv('DB_PASSWORD', ''),
            'unix_socket' => getenv('DB_UNIX_SOCKET', ''),
            'charset'     => getenv('DB_CHARSET', 'utf8mb4'),
            'collation'   => getenv('DB_COLLATION', 'utf8mb4_bin'),
            'prefix'      => getenv('DB_PREFIX', ''),
            'strict'      => getenv('DB_STRICT', true),
            'engine'      => getenv('DB_ENGINE', null),
        ],
    ],
];
```

3. 在项目目录下创建 .env 文件，并更具需要配置环境变量

`.env`

```
# database
DB_DRIVER=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=webman
DB_USERNAME=root
DB_PASSWORD=root
```