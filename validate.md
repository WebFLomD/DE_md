# Валлидация
[Назад](README.md)

### Часть кода можно найти в zeal (<u>Core Validators</u>)

```php
# Общая валлидация
[['username', 'fio', 'email', 'phone', 'id_cite', 'password'], 'required', 'message' => 'Заполните поля!'],

# Зарегистрированые данные в БД
[['username'], 'unique', 'message' => 'Такой логин зарегистрирован!'],
[['email'], 'unique', 'message' => 'Такая почта зарегистрирована!'],
[['phone'], 'unique', 'message' => 'Такой телефон зарегистрирован!'],

# Валлидация
['username', 'match', 'pattern' => '/^[A-Za-z0-9]{3,}$/u', 'message' => 'Только латиница'], # Валлидация на "Логин"
['fio', 'match', 'pattern' => '/^[А-Яа-я\s\-]{5,}$/u', 'message' => 'Только кириллица,и пробел'], # Валлидация на "ФИО"
['email', 'email', 'message' => 'Почта должен содержать латинские буквы, @ и точку'], # Валлидация на "Email"
# Валлидация на "Телефон"
['phone', 'string', 'max' => 18], # Максимальная длина номера телефона +7 (999) 999-99-99
['phone', 'match', 'pattern' => '/^\+7 \(\d{3}\) \d{3}-\d{2}-\d{2}$/', 'message' => 'Некорректный формат номера телефона. Используйте формат: +7 (999) 999-99-99.'], # Валлидация на "Телефон"
['password', 'match', 'pattern' => '/^[A-Za-z0-9_-]{6,}$/u', 'message' => 'Пароль должен содержать не менее 6 символов и литница'], # Валлидация на "Пароль"
['passwordRepeat', 'compare', 'compareAttribute' => 'password', 'message' => 'Пароли не совпадают!'], # Валлидация на "Подтверждение пароля"
# Валлидация на "Чек-Бокс"
['check', 'boolean'],
['check', 'compare', 'compareValue' => true, 'message' => 'Необходимо выше согасие!'],
```

Вместо валлидация "Телефон", можно прописать в view/site/login.php
```php
use yii\widgets\MaskedInput;

<?= $form->field($model, 'phone')->widget(MaskedInput::class, [
    'mask' => '+7 (999) 999-99-99',
    'options' =>['maxlength' => true ,
    'class' => 'input-auth-register', # Стизация в css
    'id' => 'phone-register', # Стизация в css
    'placeholder' => '+7 (___) ___-__-__'], # Для дизайна
]) ?>
```