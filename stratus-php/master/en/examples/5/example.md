
# Ejemplo 5.

## Introducción.

Con este ejemplo lo que se pretende mostrar es que con los métodos `hasClass()`, `addClass()` y `removeClass()` es posible manipular las clases *css* de los elementos del DOM de la página.

También queremos comentar que de manera similar, existen los métodos `hasAttribute()`, `setAttribute()` y `getAttribute()` para el caso de los atributos.

## Implementación.

```php
<?php
// src/App.php

use ThenLabs\StratusPHP\Plugin\SElements\AbstractApp;

class App extends AbstractApp
{
    public function getView(): string
    {
        return <<<HTML
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>Document</title>

                <style>
                    .hidden {
                        display: none;
                    }
                </style>
            </head>
            <body>
                <label s-element="label">I am the label</label>
                <button s-element="button">Show/Hide</button>
            </body>
            </html>
        HTML;
    }

    public function onClickButton(): void
    {
        if ($this->label->hasClass('hidden')) {
            $this->label->removeClass('hidden');
        } else {
            $this->label->addClass('hidden');
        }
    }
}
```

## Resultado.

![](result.gif)