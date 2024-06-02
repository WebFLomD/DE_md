# Авторизация
[Назад](README.md)

### Часть кода можно найти в zeal (<u>IdentityInterface</u> и <u>User (app/models/User)</u>)

В коде models/User.php
```php
use yii\web\IdentityInterface;

class User extends ActiveRecord implements IdentityInterface
{
    ...
    
    public static function findIdentity($id)
    {
        return static::findOne($id);
    }

    public static function findIdentityByAccessToken($token, $type = null)
    {
        return null;
    }

    public function getId()
    {
        return $this->id;
    }

    public function getAuthKey()
    {
        return null;
    }

    public function validateAuthKey($authKey)
    {
        return null;
    }

    /* Поиск пользователя по логину */
    public static function findByUsername($username)
    {
        return User::findOne(['username' => $username]);
    }

    /* Проверка пароля */
    public function validatePassword($password)
    {
        return $this->password === md5($password);
    }

    /* Регистрация нового пользователя пароль в md5 */
    public function beforeSave($insert)
    {
        if ($this -> isNewRecord)
        {
            return $this -> password = md5($this -> password);
        }
        return parent::beforeSave($insert);
    }

    /* Если пользователь администратор */
    public function isAdmin()
    {
        return $this -> role === 1;
    }
}

```