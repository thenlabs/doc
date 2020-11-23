
# Ejemplo 4.

## Introducción.

Con este ejemplo lo que se pretende mostrar es que con el método `setStyle()` de los elementos es posible establecer las propiedades *css* de los elementos del DOM de la página.

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
            </head>
            <body>
                <select s-element="select">
                    <option>Select color</option>
                    <option value="blue">blue</option>
                    <option value="red">red</option>
                    <option value="green">green</option>
                </select>
                <label s-element="label">black</label>
                <button s-element="button">Apply</button>
            </body>
            </html>
        HTML;
    }

    public function onClickButton(): void
    {
        $color = $this->select->value;

        $this->label->textContent = $color;
        $this->label->setStyle('color', $color);
    }
}
```

## Resultado.

![](result.gif)