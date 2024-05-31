# Вывод изображение с БД
[Назад](index.md)

В моделе:
```php
public function getImage()
{
    return ($this->/*Название избражение с БД*/) ? '/all_img/post_car/ - Путь к файлу' . // Берет название изображение в БД и ищет папке такое же название
    $this->/*Название избражение с БД*/: '/all_img/logo_order/no_image.png - Путь к файлу'; // Если изображение пустое, вставляет no_image
}
```
Пример готового кода модели Car:
```php
public function getImage_1()
{
    return ($this->photo_car_1) ? '/all_img/post_car/' . $this->photo_car_1: '/all_img/logo_order/no_image.png';
}
```

В index.php (Где вы хотите выгрузить изображение на странице)
``` php
<img src="<?= /* $название чего-то */ -> getImage(); ?>" alt="post-only-cars"> 
```
Пример готового кода в index.php:
``` php
<img src="<?= $car -> getImage_1(); ?>" alt="post-only-cars"> 
```

[$car](database-query-and-pagination.md) - Запрос к базе данных и пагинация.