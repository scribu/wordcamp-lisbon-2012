### Defining Connection Types

```php
p2p_register_connection_type( array(
	'name' => 'posts_to_users',
	'from' => 'post',
	'to'   => 'user'
) );
```

### Querying For Connected Posts

```php
$query = new WP_Query( array(
	'connected_type' => 'posts_to_users',
	'connected_items' => get_current_user_id(),
) );
```
