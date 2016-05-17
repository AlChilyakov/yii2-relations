Yii2-relations
==========
Модуль дает возможность быстро добавить возможность связывать модели между собой. Пример использования: привязка похожих продуктов.

Установка
---------------------------------
Выполнить команду

```
php composer require pistol88/yii2-relations "*"
```

Или добавить в composer.json

```
"pistol88/yii2-relations": "*",
```

И выполнить

```
php composer update
```

Подключение и настройка
---------------------------------
В конфигурационный файл приложения добавить модуль yii2images
```php
    'modules' => [
        //..
        'relations' => [
            'class' => 'pistol88\relations\Module',
            'fields' => ['code'],
        ],
        //..
    ]
```

*fields - массив доп. полей (по умолчанию в окне выбора показываются только id и название)

Использование
---------------------------------
К модели, которая имплементирует \pistol88\relations\interfaces\Torelate и наследует AR, подключить поведение:

```php
    function behaviors() {
        return [
            'relations' => [
                'class' => 'pistol88\relations\behaviors\AttachRelations',
                'relatedModel' => 'common\models\Product',
                'inAttribute' => 'relations',
            ],
        ];
    }
```

Теперь привязанные модели будет возвращаеть метод $model->getRelations().

Виджеты
---------------------------------
Выбор подключаемых моделей осуществляется через виджет:

<?=\pistol88\relations\widgets\Constructor::widget(['model' => $model]);?>

Его необходимо вызвать внутри формы редактирования вашей модели.
