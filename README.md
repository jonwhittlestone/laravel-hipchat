Hipchat Notifier for Laravel 4
==============================

Quickly and easily send messages to Hipchat rooms, backgrounding via the Laravel queue by default. Uses v1 of the Hipchat API, with auth keys (as opposed to v2 with OAuth).

A couple of usage examples:

```php
$user = 'Taylor';

HipchatNotifier::message("A new account [{$user}] signed up!");
```

Specifying some options:

```php
$message = 'Warning, system is down!';
$options = [
	'notify' => true, 
	'color' => 'red',
	'from' => 'System Monitor',
	'room' => 'Emergency Notifications',
];

HipchatNotifier::message($message, $options);
```

Installation
------------

Install into your Laravel app via composer:

```
"opb/laravel-hipchat": "dev-master",
```

`composer update` and then publish the config file:

```
php artisan publish:config opb/laravel-hipchat
```

You should then find the config file at `app/config/packages/opb/laravel-hipchat/config.php`.

Register the service provider in `app.php`:

```
\Opb\LaravelHipchat\HipchatNotifierServiceProvider
```

The `HipchatNotifier` facade is registered automatically and does **not** need to be added to the `aliases` array in `app.php`.

Options
-------

There are several options which can (and some which must) be provided to the package. Most options can be specified at instantiation (via the config file) and optionally overridden when a message is sent.

| Option | Required? | Default | Override with message? | Info |
|--------|-----------|---------|------------------------|------|
| apiToken | Yes | *none* | No |  |
| room | Yes | *none* | Yes | Name of the room, not ID |
| color | No | 'yellow' | Yes | See available options below |
| from | No | 'Notification' | Yes | The message sender name |
| notify | No | false | Yes | Make Hipchat app notify |
| queue | No | true | Yes | Background to Laravel queue |
| format | No | 'auto' | Yes | Message format - **html**, **text** or **auto** |


- Color options - **yellow**, **red**, **gray**, **green**, **purple**, **random**
- Message format - HipChat can format basic html structures (lists, paragraphs, bold, italic, etc) when set to **html** format. Emoticons are only rendered when **text** format is used. **auto** will check for any html tags in your message and decide automagically which to use.

Usage
-----
Using the `HipchatNotifier` facade allows you to quickly and easily send messages. The simplest is to send a message using all the default options within the package, or using those that were overridden in the config file:

```php
HipchatNotifier::message('Test message with all default options');
```

You can override options on a per-message basis:

```php
$message = 'Warning, system is down!';
$options = [
	'notify' => true, 
	'color' => 'red',
	'from' => 'System Monitor',
	'room' => 'Emergency Notifications',
];

HipchatNotifier::message($message, $options);
```

If you're not going to use the facade, and resolver directly out of the IOC container, the key is `hipchat-notifier`. For example:

```php
$notifier = App::make('hipchat-notifier');
```

Roadmap
-------

- Support Laravel 5
- Support HipChat API v2


 

