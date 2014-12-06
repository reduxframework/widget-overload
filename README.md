widget-overload
===============

register a widget with arguments

Extends the WP_Widget_Factory class by overloading the register method to allow for the passing params.

Place the following in your widget PHP file.

```php
    class Extend_WP_Widget_Factory extends WP_Widget_Factory {
        function register($widget_class, $param = null) {
            $this->widgets[$widget_class] = new $widget_class($param);
        }
    }  
```

Register the widget as follows:

```php
add_action ( 'widgets_init',  'load_widget' , 0 );

function load_widget () {
    $param = array('one' => 'value one', 'two' => 'value 2');

    $extend = new Extend_WP_Widget_Factory();
    $extend->register('MyWidgetName', $param);
}
```


Then to use it:
```php
    class MyWidgetName extends WP_Widget {

        public function MyWidgetName ($param) {
            extract ($param);
       
            echo $one;
            echo $two;

            // do widget set up here, etc, etc.
        }
    }
```
