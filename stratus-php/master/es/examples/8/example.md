
# Ejemplo 8.

## Introducción.

Este ejemplo es muy similar al anterior y solo se pretende mostrar que también es posible especificar el código JavaScript del manejador de evento frontal en una función de la clase.

Este manera puede ser más apropiada cuando el *script* tenga un tamaño considerable ya que como puede verse, cuando se usa la sintaxis HEREDOC(<<<JAVASCRIPT...JAVASCRIPT), muchos IDEs y editores de código mostrarán un resaltado de sintaxis.

## Implementación.

```php
<?php
// src/App.php

use ThenLabs\StratusPHP\Plugin\SElements\AbstractApp;
use ThenLabs\StratusPHP\Annotation\EventListener;

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
                <input s-element="myInput" type="text">
                <label s-element="myLabel"></label>
            </body>
            </html>
        HTML;
    }

    public function myFrontListener(): string
    {
        return <<<JAVASCRIPT
            if (! (eventData.keyCode >= 97 && eventData.keyCode <= 122)) {
                myLabel.textContent = 'Only lower letters they are accepted.';
                event.backListener = false;
            }
        JAVASCRIPT;
    }

    /**
     * @EventListener(
     *     fetchData={"key", "keyCode"},
     *     frontListener="myFrontListener"
     * )
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