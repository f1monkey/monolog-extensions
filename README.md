# monolog-extensions

Handlers nad other usable (probably) things for monolog.

## Install
```
$ composer require f1monkey/monolog-extensions
```

## Handlers

#### [LogstashHttpHandler](./src/Handler/LogstashHttpHandler.php)

Writes log messages directly to Logstash using [http input](https://www.elastic.co/blog/introducing-logstash-input-http-plugin). It is a default SocketHandler with minor changes.

Usage:

`services.yaml`:
```$yaml
services:
    monolog.handler.logstash_handler:
        class: F1Monkey\MonologExtensions\Handler\LogstashHttpHandler
        arguments:
            $connectionString: '%env(LOGSTASH_HOST)%' #i.e. http://localhost:8080
        calls:
            - ['setFormatter', ['@monolog.formatter.logstash']]
```
`packages/monolog.yaml`:
```yaml
monolog:
    handlers:
        logstash:
            type: service
            id: monolog.handler.logstash_handler
            channels: ["!event", "!doctrine"]
            level: debug
```