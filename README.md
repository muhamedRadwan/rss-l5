# RSS

RSS builder for Laravel 5

## Installation

Add `mayconbordin/rss-l5` to `composer.json`.

```json
"mayconbordin/rss-l5": "~1.1"
```

Run `composer update` to pull down the latest version of RSS.

Now open up `app/config/app.php` and add the service provider to your `providers` array.

```php
'providers' => array(
    'Thujohn\Rss\RssServiceProvider',
)
```

Now add the alias.

```php
'aliases' => array(
    'Rss' => 'Thujohn\Rss\RssFacade',
)
```

## Usage

Returns the feed

```php
Route::get('/', function()
{
	$feed = Rss::feed('2.0', 'UTF-8');
	$feed->channel([
	    'title'       => "Channel's title",
	    'description' => "Channel's description",
	    'link'        => "http://www.test.com/"
    ]);
    
	for ($i=1; $i<=5; $i++) {
		$feed->item([
		    'title' => 'Item '.$i,
		    'description|cdata' => 'Description '.$i,
		    'link' => 'http://www.test.com/article-'.$i
	    ]);
	}

	return response($feed, 200)->header('Content-Type', 'text/xml');
});
```

Save the feed

```php
Route::get('/', function()
{
	$feed = Rss::feed('2.0', 'UTF-8');
	$feed->channel([
	    'title'       => "Channel's title",
	    'description' => "Channel's description",
	    'link'        => "http://www.test.com/"
    ]);
    
	for ($i=1; $i<=5; $i++) {
		$feed->item([
		    'title' => 'Item '.$i,
		    'description|cdata' => 'Description '.$i,
		    'link' => 'http://www.test.com/article-'.$i
	    ]);
	}

	$feed->save('test.xml');
});
```
