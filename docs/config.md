# Config

## Route

In your codeigniter ```application >> config >> routes.ph``` add the following route.

```php
/**
 * Beats
 */
$route['beats'] = "beats/index";
```

## Controller

Create a controller named ```Beats.php``` and add the following code block.

```php
<?php defined('BASEPATH') or exit('No direct script access allowed');



class Beats extends MY_Controller
{

  private $beats;

  function __construct()
  {
    parent::__construct();
    $this->beats = new \Beats\Beats();
  }



  /**
   * index
   * 
   * @method GET
   * 
   * @return void
   */
  function index()
  {
    echo $this->beats->showLogs();
    return;
  }
}
```