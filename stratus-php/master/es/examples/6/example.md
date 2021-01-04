
# Ejemplo 6.

## Introducción.

Con este ejemplo lo que se pretende mostrar es que con la ayuda de la anotación `ThenLabs\StratusPHP\Annotation\EventListener` es posible especificar los datos del evento que se van a necesitar en el servidor.

Cuando en el navegador, se introduce un caracter en el cuadro de texto, sobre este se producirá un evento del tipo `keypress` el cual contendrá(entre muchos otros) los datos `key` y `keyCode`. El ejemplo muestra la manera de especificar los datos del evento del navegador que se necesitarán en el servidor para el procesamiento de dicho evento.

## Implementación.

```php
<?php
// src/MyPage.php

use ThenLabs\StratusPHP\Plugin\SElements\AbstractPage;
use ThenLabs\StratusPHP\Annotation\EventListener;

class MyPage extends AbstractPage
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
                <input s-element="myInput" type="text">
                <label s-element="myLabel"></label>
            </body>
            </html>
        HTML;
    }

    /**
     * @EventListener(fetchData={"key", "keyCode"})
     */
    public function onKeypressMyInput($event): void
    {
        $eventData = $event->getEventData();

        $this->myLabel->textContent = "key: {$eventData['key']}, keyCode: {$eventData['keyCode']}";
    }
}
```

## Resultado.

![](result.gif)