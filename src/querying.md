### Pages a user has contributed to

```php
function get_contributed_pages( $user_id ) {
	$query = new WP_Query( array(
		'connected_type' => 'page_contributors',
		'connected_items' => $user_id
	) );

	return $query->posts;
}
```

### Users that contributed to a page

```php
function get_contributing_users( $page_id ) {
	return get_users( array(
		'connected_type' => 'page_contributors',
		'connected_items' => $page_id
	) );
}
```
