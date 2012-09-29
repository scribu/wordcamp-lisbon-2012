### Defining Connection Types

```php
function page_contributors_ctype() {
	p2p_register_connection_type( array(
		'name' => 'page_contributors',
		'from' => 'page',
		'to'   => 'user',
		'duplicate_connections' => true,
		'fields' => array(
			'contribution' => 'Contribution'
		)
	) );
}

add_action( 'p2p_init', 'page_contributors_ctype' );
```
