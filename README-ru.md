# Laravel улучшенная конфигурация

[![Лицензия](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Версия Laravel](https://img.shields.io/badge/laravel-5-orange.svg?style=flat-square)](http://laravel.com)

![Laravel Conf](conf.png)

Отдельная редактируемая конфигурация для Laravel 5.

Данный пакет позволяет хранить дополнительную редактируемую конфигурацию в отдельном хранилище.

По-умолчанию для хранения используется JSON-файл

Это удобно, если вам нужно использовать конфигурацию, которую необходимо редактировать внутри кода пользователем. Например, настройки сайта.

## Внимание!

Будьте осторожны! Это вторая версия пакета. функция fallback была удалена.

Если она вам все еще нужна, установите [версию 1.*](https://github.com/gaaarfild/laravel-conf/tree/v1.2.2)

## Установка

Добавьте в файл `composer.json` в секцию `require` следующую строчку

``` JSON
"gaaarfild/laravel-conf": "2.*"
```

Далее, наберите в консоли

``` BASH
$ composer update
```

После окончания обновления, добавьте следующую строку в файл `config/app.conf` в раздел `providers`

``` php
  Gaaarfild\LaravelConf\LaravelConfServiceProvider::class,
```

Если вы хотите использовать фасад `Conf`, добавьте в этот же файл в раздел `aliases` следующую строку:

``` php
  'Conf' => Gaaarfild\LaravelConf\ConfFacade::class,
```

### Публикация файлов конфигурации

Чтобы иметь возможность изменить располодение файла, используйте следующую команду в консоли:

`php artisan vendor:publish --provider="Gaaarfild\LaravelConf\LaravelConfServiceProvider" --tag="config"`

Теперь вы сможете отредактировать файл `config/laravel-conf.php` чтобы задать необходимый путь хранения файла настроек.


## Использование

### Получить значение

``` php
Conf::get('key.to.retrieve', 'default_value');
```

Если нет такого ключа, вернется значение по-умолчанию, указанное вторым параметром.

Could be used 'dot' notation

### Задать значение для ключа

``` PHP
Conf::set('key', 'value_to_save');
```

Можно использовать нотацию разделения точками как в стандартной конфигурации.

Так же можно использовать метод `put` Чтобы сохранить сразу несколько значений, задав их в виде массива

``` PHP
$config = [
    'key1' => 'value1',
    'key2.subkey' => `value2`,
];
Conf::put($config);
```

### Удаление ключа из настроек

``` PHP
Conf::forget('key');
```

Можно использовать нотацию разделения точками как в стандартной конфигурации.

### Получить всю конфигурацию в виде массива.

``` PHP
Conf::all();
```

### Получить всю конфигурацию в виде JSON.

``` PHP
Conf::toJson();
```

### Проверить, существует ли данный ключ

``` PHP
Conf::has('key.to.check');
```

Можно использовать нотацию разделения точками как в стандартной конфигурации.

### Хэлпер

Так же доступен хэлпер `conf()` для более удобного использования.

Использование идентично использованию стандартного хэлпера `config()`.

``` php
conf()->set('key.subkey', 'myValue');

conf('key.subkey') // вернет 'myValue'

conf('non.existing.key', 'myDefaultValue') // вернет 'myDefaultValue'

$config = [
    'key1' => 'value1',
    'key2.subkey' => `value2`,
];

conf($config)
```

## Помощь в разработке

Мы будем рады любой помощи в разработке.

Присылайте ваши пулл реквесты в ветку `master`.


## Лицензия

Лицензия MIT. Ознакомиться можно [здесь](https://github.com/gaaarfild/laravel-conf/blob/master/LICENSE).
