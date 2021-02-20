
# Ejemplo 11.

## Introducción.

Con este ejemplo se pretende mostrar que con las funciones `alert()`, `confirm()` y `prompt()` es posible mostrar y tomar información del navegador usando las equivalentes funciones nativas.

## Implementación.

```php
<?php
// src/MyPage.php

use ThenLabs\StratusPHP\Plugin\SElements\AbstractPage;

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
                <label s-element="myLabel"></label>
                <button s-element="alertButton">Show Alert</button>
                <button s-element="confirmButton">Show Confirm</button>
                <button s-element="promptButton">Show Prompt</button>
            </body>
            </html>
        HTML;
    }

    public function onClickAlertButton(): void
    {
        $this->browser->alert('My Alert');
    }

    public function onClickConfirmButton(): void
    {
        $this->myLabel->textContent = $this->browser->confirm('Do you confirm this?') ?
            'Accepted' : 'Cancelled'
        ;
    }

    public function onClickPromptButton(): void
    {
        $this->myLabel->textContent = 'Hello ' . $this->browser->prompt('What is your name?');
    }
}
```

## Resultado.

![](result.gif)

<a class="float-left" href="../10/example.html">Anterior</a>