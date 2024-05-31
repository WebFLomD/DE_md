# Загрузка файлов в БД
[Назад](index.md)

### Часть кода можно найти в zeal (<u>Uploading Files</u>)

В контролере (функция actionCreate)
``` php
use yii\web\UploadedFile;

// Загрузка избражение в БД
$model -> /*Название избражение с БД*/ = UploadedFile::getInstance($model, 'Название для загрузки избражений в _form'); // Эту строчку можно найти в zeal часть кода

$filename = md5(microtime()) . '.' . $model-> /*Название избражение с БД*/ ->extension; // Эту строчку можно найти в zeal часть кода

$model-> /*Название избражение с БД*/ ->saveAs('all_img/auto_parts/ - Путь загрузки' . $filename); // Эту строчку можно найти в zeal часть кода

$model-> /*Название избражение с БД*/ = $filename;                
```
Пример готового кода:
```php
use yii\web\UploadedFile;


// Загрузка избражение в БД
$model->photo_auto_parts = UploadedFile::getInstance($model, 'photo_auto_parts');
$filename = md5(microtime()) . '.' . $model->photo_auto_parts->extension;
$model->photo_auto_parts->saveAs('all_img/auto_parts/' . $filename);
$model->photo_auto_parts = $filename;
```