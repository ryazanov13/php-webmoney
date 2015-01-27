WebMoney API PHP Library
========================
Get transparent object-oriented interaction with WebMoney API.

If you just need to sign your requests to the API, use [WebMoney Signer](https://github.com/baibaratsky/php-wmsigner), a native PHP implementation of the WMSigner authentication module. 

XML-interfaces supported
------------------------
- [X2](https://github.com/baibaratsky/php-webmoney/wiki/X2): transferring funds from one purse to another
- [X3](https://github.com/baibaratsky/php-webmoney/wiki/X3): receiving transaction history, checking transaction status
- [X6](https://github.com/baibaratsky/php-webmoney/wiki/X6): sending message to any WM-identifier via internal mail
- [X8](https://github.com/baibaratsky/php-webmoney/wiki/X8): retrieving information about purse ownership, searching for system user by his/her identifier or purse
- [X9](https://github.com/baibaratsky/php-webmoney/wiki/X9): retrieving information about purse balance
- [X11](https://github.com/baibaratsky/php-webmoney/wiki/X11): retrieving information from client’s passport by WM-identifier
- [X14](https://github.com/baibaratsky/php-webmoney/wiki/X14): fee-free refund
- [X17](https://github.com/baibaratsky/php-webmoney/wiki/X17): operations with arbitration contracts
- [X18](https://github.com/baibaratsky/php-webmoney/wiki/X18): getting transaction details via merchant.webmoney
- [X19](https://github.com/baibaratsky/php-webmoney/wiki/X19): verifying personal information for the owner of a WM identifier

Megastock interfaces supported
------------------------------
- Interface for [adding Payment Integrator's merchants](https://github.com/baibaratsky/php-webmoney/wiki/Adding-Payment-Integrator%27s-merchant)
- Interface for [check status of merchant](https://github.com/baibaratsky/php-webmoney/wiki/Check-status-of-merchant)

Requirements
------------
The library requires PHP 5.3 compiled with [cURL extension](http://www.php.net/manual/en/book.curl.php) (but you can override cURL dependencies).

Installation
------------
0. Install [Composer](http://getcomposer.org/):

    ```
    curl -sS https://getcomposer.org/installer | php
    ```

0. Add the php-webmoney dependency:

    ```
    php composer.phar require baibaratsky/php-webmoney:0.9.*
    ```

Usage
-----
**There are more usage examples in [the project wiki](https://github.com/baibaratsky/php-webmoney/wiki).**
```php
require_once(__DIR__ . '/vendor/autoload.php'); // Require autoload file generated by composer

use baibaratsky\WebMoney;

$webMoney = new WebMoney\WebMoney(new WebMoney\Request\Requester\CurlRequester);

$request = new WebMoney\Api\X\X9\Request;
$request->setSignerWmid('YOUR WMID');
$request->setRequestedWmid('REQUESTED WMID');

$request->sign(new Signer('YOUR WMID', 'FULL PATH TO KEY FILE', 'KEY FILE PASSWORD'));

if ($request->validate()) {
    /** @var WebMoney\Api\X\X9\Response $response */
    $response = $webMoney->request($request);

    if ($response->getReturnCode() === 0) {
        echo $response->getPurseByName('Z000000000000')->getAmount();
    }
}
```
