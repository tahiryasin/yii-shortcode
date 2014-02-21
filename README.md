yii-shortcode
=============

Yii-shortcode is a component for the [Yii PHP framework](http://www.yiiframework.com) that provides ability to create [WordPress](http://codex.wordpress.org/Shortcode) like shortcodes.

## Usage

### Setup

Download the latest release from [Yii extensions](http://www.yiiframework.com/extension/yii-shortcode).

Unzip the component under ***protected/components*** and add the following to your application config:

```php
return array(
  'components' => array(
    'shortcode' => array(
        'class' => 'application.components.ShortCode',
     ),
  ...
  ...
  ),
);
```
***protected/config/main.php***




### Registring Shortcodes

You can register as many shortcodes as you want in base controller or in any custom controller:

```php
public function beforeAction($action)
  {
      Yii::app()->shortcode->add_shortcode('gallery', array($this, 'gallery_callback'));
	  Yii::app()->shortcode->add_shortcode('caption', array($this, 'caption_callback'));
	  return $action;
  }
```
***protected/components/Controller.php***

```php
function gallery_callback($atts)
  {
      return "<div id='gallery'>Gallery #{$atts['id']}</div>";
  }  
function caption_callback($atts, $content)
  {
      return '<span class="caption">' . $content . '</span>';
  }  
```
***protected/controllers/SiteController.php***


#### Rendering ShortCode
```php
$content = 'My Gallery: [gallery id="123"]';
echo Yii::app()->shortcode->parse($content);
```
**The output would be:**
`My Gallery: <div id="gallery">Gallery #123</div>`


```php
$content= 'Hi, check out this caption: [caption]My Caption[/caption]';
echo Yii::app()->shortcode->parse($content);
```
**The output would be:**
`Hi, check out this caption: <span class="caption">My Caption</span>`

***protected/views/site/index.php***


