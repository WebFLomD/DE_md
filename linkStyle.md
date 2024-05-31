# Подколючение css и js к Yii
[Назад](README.md)

Файл с css и js надо закинуть в папку web. Затем в коде можно новую создать (PublicAssets.php) или стрый оствить(AppAssets.php) assets/PublicAssets.php:
```php
/**
 * @link https://www.yiiframework.com/
 * @copyright Copyright (c) 2008 Yii Software LLC
 * @license https://www.yiiframework.com/license/
 */

namespace app\assets;

use yii\web\AssetBundle;

/**
 * Main application asset bundle.
 *
 * @author Qiang Xue <qiang.xue@gmail.com>
 * @since 2.0
 */
class PublicAsset extends AssetBundle
{
    public $basePath = '@webroot';
    public $baseUrl = '@web';
    public $css = [
        'public/css/form-auth-register.css', # Путь к css файлам

    ];
    public $js = [
        'public/js/password.js', # Путь к js файлам
    ];
    public $depends = [
    ];
}
```

Пример готового кода PublicAssets.php

```php
namespace app\assets;

use yii\web\AssetBundle;

class PublicAsset extends AssetBundle
{
    public $basePath = '@webroot';
    public $baseUrl = '@web';
    public $css = [
        'public/css/form-auth-register.css', #Регистрация и авторизация
        'public/css/error.css', # Ошибка/сообщение (меняет обычного на нужный цвет текста в авторизации и регистрации)
        'public/css/fontawesome-free-6.5.2-web/css/all.min.css',

    ];
    public $js = [
        'public/js/password.js', # Скрывает и показывает пароль
        'public/js/the-gap-between-thousands.js', # Автопробел больших чисел (1 000, 100 000)
        'public/js/slider.js', # Слайдер
    ];
    public $depends = [
    ];
}
```
Если вы только в старом годе довабивили/заменили, то дальше делать не надо. Если создали новый файл и назвали как-то (PublicAssets.php) и добавили, то что надо, то надо отрыть код views/layouts/main.php, заменить и готово:
```php
/*У вас будет так */
use app\assets\AppAsset;

AppAsset::register($this);
```
****
```php
/* Надо сделать так */
use app\assets\PublicAsset;

PublicAsset::register($this);
```
