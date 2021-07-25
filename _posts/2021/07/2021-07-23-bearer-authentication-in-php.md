---
title: Request using bearer authentication in PHP
---

Making a `GET` request in PHP is not as simple as doing it in Python using
the `request` module. After looking over multiple resources over the internet
I found the following code to work well.

```php
try {
    $curl = curl_init($);
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
    $headers = array(
        "Accept: application/json",
        sprintf("Authorization: Bearer %s", $auth_token),
    );
    curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
    $response = curl_exec($curl);
    if ($response === false) {
        throw new Exception(curl_error($ch), curl_errno($ch));
    }
    curl_close($curl);
} catch(Exception $e) {
    trigger_error(sprintf(
        'Curl failed with error #%d: %s',
        $e->getCode(), $e->getMessage()),
        E_USER_ERROR);
}
```

The [PHP | cURL post on GFG](https://www.geeksforgeeks.org/php-curl/) summarises
used curl methods in brief. It is better to have error handling because if the
request fails, the value of `$response` will be just `false` which is not
very helpful for debugging.

In other news
-------------

Today, I gave my last evaluation for my bachelor's degree. 🎉
