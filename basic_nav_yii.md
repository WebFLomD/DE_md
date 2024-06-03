# Навигатор на Yii без дизайна
[Назад](README.md)

```php
echo Nav::widget([
        'options' => ['class' => 'navbar-nav'],
        'items' => [
//            ['label' => 'Главная', 'url' => ['/site/index']],
            /* Раздел видит только Пользователь и админ */
            ['label' => 'Личный кабинет', 'url' => ['/statement'], 'visible' => !Yii::$app->user->isGuest],
            /* ИЛИ */
            /* Раздел видит только Пользователь */
            ['label' => 'Личный кабинет', 'url' => ['/statement'], 'visible' => !Yii::$app->user->isGuest&&!Yii::$app->user->identity->isAdmin()],
            /* Раздел видит только админ */
            ['label' => 'Панель адмистратора', 'url' => ['/admin'], 'visible' => !Yii::$app->user->isGuest&&Yii::$app->user->identity->isAdmin()],
            /* Раздел видит только гость */
            ['label' => 'Регистрация', 'url' => ['/user/create'], 'visible' => Yii::$app->user->isGuest],

            Yii::$app->user->isGuest
                ? ['label' => 'Войти', 'url' => ['/site/login']]
                : '<li class="nav-item">'
                    . Html::beginForm(['/site/logout'])
                    . Html::submitButton(
                        'Выйти (' . Yii::$app->user->identity->username . ')',
                        ['class' => 'nav-link btn btn-link logout']
                    )
                    . Html::endForm()
                    . '</li>'
        ]
    ]);

    <?php
    NavBar::begin([
        'brandLabel' => Yii::$app->name, /* Логотип только название */
        /* ИЛИ */
        'brandLabel' => Html::img('@web/images/logo.png', ['alt'=>Yii::$app->name, 'style' => 'height:30px;']), /* Логотип изображение */
        'brandUrl' => Yii::$app->homeUrl,
        'options' => ['class' => 'navbar-expand-md navbar-dark bg-dark fixed-top']
    ]);
    echo Nav::widget([
        'options' => ['class' => 'navbar-nav'],
        'items' => [
            ['label' => 'Главная', 'url' => ['/site/index']],
            /* Раздел видит только Пользователь и админ */
            ['label' => 'Личный кабинет', 'url' => ['/statement'], 'visible' => !Yii::$app->user->isGuest],
            /* ИЛИ */
            /* Раздел видит только Пользователь */
            ['label' => 'Личный кабинет', 'url' => ['/statement'], 'visible' => !Yii::$app->user->isGuest&&!Yii::$app->user->identity->isAdmin()],
            /* Раздел видит только админ */
            ['label' => 'Панель адмистратора', 'url' => ['/admin'], 'visible' => !Yii::$app->user->isGuest&&Yii::$app->user->identity->isAdmin()],
            /* Раздел видит только гость */
            ['label' => 'Регистрация', 'url' => ['/user/create'], 'visible' => Yii::$app->user->isGuest],

            Yii::$app->user->isGuest
                ? ['label' => 'Войти', 'url' => ['/site/login']]
                : '<li class="nav-item">'
                    . Html::beginForm(['/site/logout'])
                    . Html::submitButton(
                        'Выйти (' . Yii::$app->user->identity->username . ')',
                        ['class' => 'nav-link btn btn-link logout']
                    )
                    . Html::endForm()
                    . '</li>'
        ]
    ]);
    NavBar::end();
    ?>
```