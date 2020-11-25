
# Ejemplo 6.

## Introducción.

Con este ejemplo lo que se pretende mostrar es que StratusPHP permite obtener información del navegador.

Puede verse que al llamar a la función `prompt()` del objeto `Browser`, en el navegador se pedirá que el usuario introduzca un valor a través de una ventana *prompt* nativa y seguidamente el valor estará disponible en el código PHP.

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
                <label s-element="label"></label>
                <button s-element="button">Greet</button>
            </body>
            </html>
        HTML;
    }

    public function onClickButton(): void
    {
        $this->label->textContent = 'Hi ' . $this->getBrowser()->prompt('What is your name?');
    }
}
```

## Resultado.

![](result.gif)