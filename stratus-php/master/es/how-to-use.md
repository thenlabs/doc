
# ¿Cómo usar StratusPHP?.

**Instale StratusPHP.**

    $ composer require thenlabs/stratus-php 1.0.x-dev

**Cree un controlador que instancie la página, la persista y devuelva su vista.**

```php
<?php
// public/index.php

require_once __DIR__.'/../vendor/autoload.php';
require_once __DIR__.'/../src/MyPage.php';

use function Opis\Closure\serialize as s;

// Creates the page instance specifying the url where will be processing the requests.
$page = new MyPage('/ajax.php');

// persists the instance on the session(in this case).
session_start();
$_SESSION['page'] = s($page);

// returns the view of the page.
echo $page;
```

**Cree el controlador que se encargará de procesar las solicitudes asíncronas.**

```php
<?php
// public/ajax.php

require_once __DIR__.'/../vendor/autoload.php';
require_once __DIR__.'/../src/MyPage.php';

use ThenLabs\StratusPHP\Request;
use function Opis\Closure\{serialize as s, unserialize as u};

// Gets the persisted page instance.
session_start();
$page = u($_SESSION['page']);

// Do process the request.
$request = Request::createFromJson($_REQUEST['stratus_request']);
$result = $page->run($request);

// If the processing was successful, persist the page again.
if ($result->isSuccessful()) {
    $_SESSION['page'] = s($page);
}

die();
```

**Cree la clase de la página.**

[Ver ejemplos](examples/index.md)