###Forked from [vinelab/http on github.org](https://github.com/Vinelab/http)

# http://Client

A smart and simple HTTP client for sending and recieving JSON and XML.

## Installation

### Composer

- `"jenchik/http": "dev-master"` for the latest version installation instructions.

```php
// change this to point correctly according
// to your folder structure.
require './vendor/autoload.php';

use Spc\Http\Client as HttpClient;

$client = new HttpClient;

$response = $client->get('echo.jsontest.com/key/value/something/here');

var_dump($response->json());
```

### Laravel

Edit **app.php** and add ```'Spc\Http\HttpServiceProvider',``` to the ```'providers'``` array.

It will automatically alias itself as **HttpClient** so no need to alias it in your **app.php**, unless you would like to customize it - in that case edit your **'aliases'** in **app.php** adding ``` 'MyHttp'	  => 'Spc\Http\Facades\Client',```

## Usage

### GET

#### Simple

```php

	$response = HttpClient::get('http://example.org');

	// raw content
	$response->content();

```

#### With Params

```php

	$request = [
		'url' => 'http://somehost.net/something',
		'params' => [

			'id'     => '12350ME1D',
			'lang'   => 'en-us',
			'format' => 'rss_200'
		]
	];

	$response = HttpClient::get($request);

	// raw content
	$response->content();

	// in case of json
	$response->json();

	// XML
	$response->xml();

```

### POST

```php

	$request = [
		'url' => 'http://somehost.net/somewhere',
		'params' => [

			'id'     => '12350ME1D',
			'lang'   => 'en-us',
			'format' => 'rss_200'
		]
	];

	$response = HttpClient::post($request);

	// raw content
	$response->content();

	// in case of json
	$response->json();

	// XML
	$response->xml();
```

### Headers

```php
$response = HttpClient::get([
	'url' => 'http://some.where.url',
	'headers' => ['Connection: close', 'Authorization: some-secret-here']
]);

// The full headers payload
$response->headers();
```

### Enforce HTTP Version

```php
HttpClient::get(['version' => 1.1, 'url' => 'http://some.url']);
```

### Raw Content

```php
HttpClient::post(['url' => 'http://to.send.to', 'content' => 'Whatever content here may go!']);
```

#### Custom Query String

The content passed in the `content` key will be concatenated to the *URL* followed by a *?*

```php
HttpClient::get(['url' => 'http://my.url', 'content' => 'a=b&c=d']);
```

> It is pretty much the same process with different HTTP Verbs. Supports ``` GET, POST, PUT, DELETE, PATCH, OPTIONS, HEAD ```

#### TODO
- Improve tests to include testing all the methods of response (like statusCode...)
- Include tests for handling bad data / errors
- Improve tests to include testing for all HTTP Verbs
