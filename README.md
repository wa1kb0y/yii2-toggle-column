Toggle data column for Yii2
===========================
Provides a toggle data column and action

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist pheme/yii2-toggle-column "*"
```

or add

```
"pheme/yii2-toggle-column": "*"
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply use it in your code by  :

```php
// In your Controller
use pheme\grid\actions\ToggleAction;

public function actions()
{
	return [
		'toggle' => [
			'class' => ToggleAction::className(),
			'modelClass' => 'path\to\your\Model',
			// Uncomment to enable flash messages
			//'setFlash' => true,
		]
	];
}

// In your view
use yii\grid\GridView;
use yii\widgets\Pjax;

Pjax::begin();

GridView::widget(
	[
		'dataProvider' => $dataProvider,
		'filterModel' => $searchModel,
		'columns' => [
			'id',
			[
				'class' => '\pheme\grid\ToggleColumn',
				'attribute' => 'active',
				// Uncomment if  you don't want AJAX
				// 'enableAjax' => false,
				// Uncomment if you want to hide it by some model's attribute
				// 'hideAttribute' => 'is_toggle_hidden',
				// 'onIcon' => 'glyphicon glyphicon-ok',
                // 'offIcon' => 'glyphicon glyphicon-remove',
			],
			['class' => 'yii\grid\ActionColumn'],
		],
	]
);

Pjax::end();
```

### Button icon redefine
You can redefine button icons by setting `onIcon` and `offIcon` in global params of Yii application.

add in your 'params.php' or 'params-local.php:
```php
[
    'toggleColumn.iconOn' => 'glyphicon glyphicon-ok',
    'toggleColumn.iconOff' => 'glyphicon glyphicon-remove',
]
```