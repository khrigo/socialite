# Socialite

[![Build Status](https://travis-ci.org/overtrue/wechat.svg?branch=master)](https://travis-ci.org/overtrue/wechat)
[![Latest Stable Version](https://poser.pugx.org/overtrue/wechat/v/stable.svg)](https://packagist.org/packages/overtrue/wechat)
[![Latest Unstable Version](https://poser.pugx.org/overtrue/wechat/v/unstable.svg)](https://packagist.org/packages/overtrue/wechat)
[![Total Downloads](https://poser.pugx.org/overtrue/wechat/downloads)](https://packagist.org/packages/overtrue/wechat)
[![License](https://poser.pugx.org/overtrue/wechat/license)](https://packagist.org/packages/overtrue/wechat)

Socialite is a collection of OAuth 2 packages that extracts from [laravel/socialite](https://github.com/laravel/socialite). You can easily use it without Laravel.

# Install

```shell
$ composer require overtrue/socialite
```

# Usage

`authorize.php`:

```php
<?php

use Overtrue\Socialite\SocialiteManager;

include __DIR__.'/vendor/autoload.php';

$config = [
    'weibo' => [
        'client_id'     => 'your-app-id',
        'client_secret' => 'your-app-secret',
        'redirect'      => 'http://localhost/socialite/callback.php',
    ],
];

$socialite = new SocialiteManager($config);

$response = $socialite->driver('weibo')->redirect();

echo $response;// or $response->send();
```

`callback.php`:

```php
<?php

// ...
$user = $socialite->driver('weibo')->user();

var_dump($user);
// 'id' => int 2193182644
// 'nickname' => null
// 'name' => string '安正超' (length=9)
// 'email' => null
// 'avatar' => string 'http://tp1.sinaimg.cn/2193182644/180/40068307042/1' (length=50)
```

### Scope

Before redirecting the user, you may also set "scopes" on the request using the scope method. This method will overwrite all existing scopes:

```php
$response = $socialite->driver('github')
                ->scopes(['scope1', 'scope2'])->redirect();

```

### Additional parameters

To include any optional parameters in the request, call the with method with an associative array:

```php
$response = $socialite->driver('google')
                    ->with(['hd' => 'example.com'])->redirect();
```

### User interface

```php

$user = $socialite->driver('weibo')->user();

$user->getId();
$user->getNickname();
$user->getName();
$user->getEmail();
$user->getAvatar();
```

# License

MIT