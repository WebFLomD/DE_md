# Запрос к базе данных и пагинация
[Назад](README.md)

### Часть кода можно найти в zeal (<u>Pagination</u>)

В контролере где будет пагинация и запрос к БД, чтобы на странице отображались что-то
```php
use app\models\Brandcar;
use app\models\Car;
use yii\data\Pagination;

public function actionIndex()
{
    $brand_cars = BrandCar::find()->all(); # Запрос данные к БД "Бренд"

    $query = Car::find(); # Запрос данные к БД "Автомобили"
    $count = $query->count(); # Подсчет общего количества записей
    $pagination = new Pagination(['totalCount' => $count, 'pageSize' => 20]); # Создание объекта пагинации. 'totalCount' => общее количество записе и 'pageSize' => количество записей на одной странице
    $cars = $query->offset($pagination->offset)
        ->where(['id_status' => 2]) # Показывает что-то где есть статус = 2. Его можно убрать
        ->limit($pagination->limit)
        ->all();

    return $this->render('index',
    [
        'cars' => $cars,
        'brand_cars' => $brand_cars,
        'pagination' => $pagination,
    ]);
}
```
На странице вставить:
```php
use yii\helpers\Html;
use yii\helpers\Url;
use yii\widgets\LinkPager;

<div class="index-main-info">

    <div class="car-brand">
        <?php foreach ($brand_cars as $brand_car): ?>
        <div class="brand">
            <?= Html::a(Html::encode($brand_car->name) .
                ' (' . $brand_car->getCarsCount() . ')',
                Url::toRoute(['site/brand_car', 'id' => $brand_car->id]),
                ['class' => 'kakoytoclass']); ?>
        </div>
        <?php endforeach;?>
    </div>

    <div class="post-all-cars">

        <?php foreach ($cars as $car): ?>

        <div class="post-only-cars">
            <div class="photo-cars">
                <img src="<?= $car -> getImage_1();?>" alt="post-only-cars">
            </div>
            <div class="info-car-post">
                <div class="price-car-post-index">
                    <p class="kakoytoclass"><?= $car -> price ?> рублей</p>
                </div>
                <div class="title-car-index">
                    <p><?= $car -> name_car?></p>
                </div>
                <div class="additionally">
                    <p>2024 /</p>
                    <p class="kakoytoclass" id="probeg-text"><?= $car -> mileage?> км</p>
                </div>
            </div>
            <div class="btn-post-car">
                <a href="<?= Url::toRoute(['/car/post', 'id' => $car-> id]) ?>">Подробнее</a>
            </div>
        </div>

        <?php endforeach;?>

    </div>

    <!-- Пагинация -->
    <?= LinkPager::widget(['pagination' => $pagination]) ?>
</div>

```
