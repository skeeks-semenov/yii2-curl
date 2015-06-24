yii2-curl extension
===================
Cool working curl extension for Yii2, including RESTful support:

 - POST
 - GET
 - HEAD
 - PUT
 - DELETE
 - PATCH
 - OPTIONS

Requirements
------------
- Yii2
- PHP 5.4+
- Curl and php-curl installed


Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

```bash
php composer.phar require --prefer-dist skeeks/yii2-curl "*"
```


Usage
-----

Once the extension is installed, simply use it in your code. The following example shows you how to handling a simple GET Request.

```php
<?php
/**
 * Yii2 test controller
 *
 * @category  Web-yii2-example
 * @package   yii2-curl-example
 * @license   http://opensource.org/licenses/MIT MIT Public
 *
 */

namespace app\controllers;

use yii\web\Controller;
use skeeks\yii2\curl;

class TestController extends Controller
{

    /**
     * Yii action controller
     */
    public function actions()
    {
        return [
            'error' => [
                'class' => 'yii\web\ErrorAction',
            ],
        ];
    }


    /**
     * cURL GET example
     */
    public function actionGetExample()
    {
        //Init curl
        $curl = new curl\Curl();

        //get http://example.com/
        $response = $curl->get('http://example.com/');
    }


    /**
     * cURL POST example with post body params.
     */
    public function actionPostExample()
    {
        //Init curl
        $curl = new curl\Curl();

        //post http://example.com/
        $response = $curl->setOption(
                CURLOPT_POSTFIELDS,
                http_build_query(array(
                    'myPostField' => 'value'
                )
            ))
            ->post('http://example.com/');
    }


    /**
     * cURL multiple POST example one after one
     */
    public function actionMultipleRequest()
    {
        //Init curl
        $curl = new curl\Curl();


        //post http://example.com/
        $response = $curl->setOption(
            CURLOPT_POSTFIELDS,
            http_build_query(array(
                'myPostField' => 'value'
                )
            ))
            ->post('http://example.com/');


        //post http://example.com/, reset request before
        $response = $curl->reset()
            ->setOption(
                CURLOPT_POSTFIELDS,
                http_build_query(array(
                    'myPostField' => 'value'
                )
            ))
            ->post('http://example.com/');
    }


    /**
     * cURL advanced GET example with HTTP status codes
     */
    public function actionGetAdvancedExample()
    {
        //Init curl
        $curl = new curl\Curl();

        //get http://example.com/
        $response = $curl->post('http://example.com/');

        // List of status codes here http://en.wikipedia.org/wiki/List_of_HTTP_status_codes
        switch ($curl->responseCode) {

            case 200:
                //success logic here
                break;

            case 404:
                //404 Error logic here
                break;
        }
    }
}
```

