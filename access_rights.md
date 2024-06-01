# Права доступа
[Назад](README.md)


В контролере
```php
public function behaviors()
    {
         return array_merge(
            parent::behaviors(),
            [
                'access' => [
                    'class' => AccessControl::className(),
                    'only' => ['create', 'profile', 'update', 'delete'], /*Страницы*/
                    'rules' => [

                        /* Права доступа для определного пользователя (личный кабинет) */
                        [
                            'actions' => ['profile', 'update'], /*Страницы*/
                            'allow' => true,
                            'roles' => ['@'],
                            'matchCallback' => function ($rule, $action) {
                                return Yii::$app->user->id == Yii::$app->request->get('id');
                            },
                        ],

                        /* Прада доступа только для администратора */
                        [
                            'actions' => ['update', 'delete'], /*Страницы*/
                            'allow' => true,
                            'roles' => ['@'],
                            'matchCallback' => function ($rule, $action) {
                                return Yii::$app->user->identity->isAdmin();
                            },
                        ],

                        /* Права доступа только для гостя */
                        [
                            'actions' => ['create'], /*Страница*/
                            'allow' => true,
                            'roles' => ['?'], /* Гость */
                        ],
                    ],
                ],

                ...
            ]);
    }
```