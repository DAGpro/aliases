<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://yiisoft.github.io/docs/images/yii_logo.svg" height="100px" alt="Yii">
    </a>
    <h1 align="center">Yii Aliases</h1>
    <br>
</p>

[![Latest Stable Version](https://poser.pugx.org/yiisoft/aliases/v)](https://packagist.org/packages/yiisoft/aliases)
[![Total Downloads](https://poser.pugx.org/yiisoft/aliases/downloads)](https://packagist.org/packages/yiisoft/aliases)
[![Build status](https://github.com/yiisoft/aliases/actions/workflows/build.yml/badge.svg)](https://github.com/yiisoft/aliases/actions/workflows/build.yml)
[![Code Coverage](https://codecov.io/gh/yiisoft/aliases/branch/master/graph/badge.svg)](https://codecov.io/gh/yiisoft/aliases)
[![Mutation testing badge](https://img.shields.io/endpoint?style=flat&url=https://badge-api.stryker-mutator.io/github.com/yiisoft/aliases/master)](https://dashboard.stryker-mutator.io/reports/github.com/yiisoft/aliases/master)
[![Static analysis](https://github.com/yiisoft/aliases/actions/workflows/static.yml/badge.svg?branch=master)](https://github.com/yiisoft/aliases/actions/workflows/static.yml?query=branch%3Amaster)
[![type-coverage](https://shepherd.dev/github/yiisoft/aliases/coverage.svg)](https://shepherd.dev/github/yiisoft/aliases)

The package aim is to store path aliases, i.e. short name representing a long path (a file path, a URL, etc.).
Path alias value may have another value as its part. For example, `@vendor` may store path to `vendor` directory
while `@bin` may store `@vendor/bin`.

## Requirements

- PHP 7.4 or higher.

## Installation

The package could be installed with [Composer](https://getcomposer.org):

```shell
composer require yiisoft/aliases
```

## General usage

A path alias must start with the character '@' so that it can be easily differentiated from non-alias paths.

```php
use Yiisoft\Aliases\Aliases;

$aliases = new Aliases([
    '@root' => __DIR__,
]);
$aliases->set('@vendor', '@root/vendor');
$aliases->set('@bin', '@vendor/bin');

echo $aliases->get('@bin/phpunit');
```

The code about would output "/path/to/vendor/bin/phpunit".

Note that `set()` method does not check if the given path exists or not. All it does is to associate the alias with
the path.

The path could be:

- a directory or a file path (e.g. `/tmp`, `/tmp/main.txt`)
- a URL (e.g. `https://www.yiiframework.com`)
- a path alias (e.g. `@yii/base`). It will be resolved on {@see get()} call.

Any trailing `/` and `\` characters in the given path will be trimmed.

To bulk translate path aliases into actual paths use `getArray()` method:

```php
$aliases = new Aliases([
    '@root' => '/my/app',
]);

// Value will be ['src' => '/my/app/src', 'tests' => '/my/app/tests']
$directories = $aliases->getAll(['src' => '@root/src', 'tests' => '@root/tests']);
```

### Alias priorities

In case multiple aliases are registered with same root (prefix), then the most specific has precedence:

```php
use Yiisoft\Aliases\Aliases;

$aliases = new Aliases([
    '@vendor' => __DIR__ . '/vendor',
    '@vendor/test' => '/special/location'    
]);
echo $aliases->get('@vendor/test');
```

That would output `/special/location` since `@vendor/test` is more specific match than `@vendor`.

### Alias removal

If you need to remove alias runtime:

```php
use Yiisoft\Aliases\Aliases;

$aliases = new Aliases([
    '@root' => __DIR__,
]);
$aliases->remove('@root');
```

## Documentation

- [Internals](docs/internals.md)

If you need help or have a question, the [Yii Forum](https://forum.yiiframework.com/c/yii-3-0/63) is a good place for that.
You may also check out other [Yii Community Resources](https://www.yiiframework.com/community).

## License

The Yii Aliases is free software. It is released under the terms of the BSD License.
Please see [`LICENSE`](./LICENSE.md) for more information.

Maintained by [Yii Software](https://www.yiiframework.com/).

## Support the project

[![Open Collective](https://img.shields.io/badge/Open%20Collective-sponsor-7eadf1?logo=open%20collective&logoColor=7eadf1&labelColor=555555)](https://opencollective.com/yiisoft)

## Follow updates

[![Official website](https://img.shields.io/badge/Powered_by-Yii_Framework-green.svg?style=flat)](https://www.yiiframework.com/)
[![Twitter](https://img.shields.io/badge/twitter-follow-1DA1F2?logo=twitter&logoColor=1DA1F2&labelColor=555555?style=flat)](https://twitter.com/yiiframework)
[![Telegram](https://img.shields.io/badge/telegram-join-1DA1F2?style=flat&logo=telegram)](https://t.me/yii3en)
[![Facebook](https://img.shields.io/badge/facebook-join-1DA1F2?style=flat&logo=facebook&logoColor=ffffff)](https://www.facebook.com/groups/yiitalk)
[![Slack](https://img.shields.io/badge/slack-join-1DA1F2?style=flat&logo=slack)](https://yiiframework.com/go/slack)
