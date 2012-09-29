### Defining Connection Types

```php
p2p_register_connection_type( array(
	'name' => 'page_contributors',
	'from' => 'page',
	'to'   => 'user',
	'duplicate_connections' => true,
	'fields' => array(
		'description' => 'Description'
	)
) );
```
