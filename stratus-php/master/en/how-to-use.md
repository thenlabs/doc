
# How to use StratusPHP?.

**Install StratusPHP.**

    $ composer require thenlabs/stratus-php 1.0.x-dev

**Create a controller that instantiate the application, persist it and returns the view of the page.**

```php
<?php
// public/index.php

require_once __DIR__.'/../vendor/autoload.php';
require_once __DIR__.'/../src/App.php';

use function Opis\Closure\serialize as s;

// Creates the app instance specifying the url where will be processing the requests.
$app = new App('/ajax.php');

// persists the instance on the session(in this case).
session_start();
$_SESSION['app'] = s($app);

// returns the view of the page.
echo $app;
```

**Create the controller that will handle asynchronous requests.**

```php
<?php
// public/ajax.php

require_once __DIR__.'/../vendor/autoload.php';
require_once __DIR__.'/../src/App.php';

use ThenLabs\StratusPHP\Request;
use function Opis\Closure\{serialize as s, unserialize as u};

// Gets the persisted app instance.
session_start();
$app = u($_SESSION['app']);

// Do process the request.
$request = Request::createFromJson($_REQUEST['stratus_request']);
$result = $app->run($request);

// If the processing was successful, persist the app again.
if ($result->isSuccessful()) {
    $_SESSION['app'] = s($app);
}

die();
```

**Create the application class.**

[See examples](examples/index.md)