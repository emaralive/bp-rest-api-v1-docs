# BP REST API Handbook

Just like the WordPress REST API does it for content data types the BP REST API provides API endpoints for BuddyPress community actions data types that allow developers to interact with sites remotely by sending and receiving [JSON](https://en.wikipedia.org/wiki/JSON) (JavaScript Object Notation) objects. JSON is an open standard data format that is lightweight and human-readable, and looks like Objects do in JavaScript; hence the name.

When you send content to or make a request to the API, the response will be returned in JSON. This enables developers to create, read and update BuddyPress user generated content from client-side JavaScript or from external applications, even those written in languages beyond PHP.

## Why use the BP REST API?

The BP REST API makes it easier than ever to use BuddyPress in new and exciting ways, such as creating Single Page Applications on top of BuddyPress. You could create a Template Pack to provide an entirely new front-end experience for BuddyPress, create brand new & interactive community features, or great BuddyPress blocks for the Block Editor.

The BP REST API can also serve as a strong replacement for the WordPress admin-ajax API. By using the BP REST API, you can more easily structure the way you want to get data into and out of BuddyPress. AJAX calls can be greatly simplified by using the BP REST API, enabling you to improve the performance of your custom features.

## About authentification

**Cookie authentication** is the standard authentication method included with WordPress, the **BP REST API** utilizes it.

### The REST API Nonce

The WordPress REST API includes a technique called [nonces](https://developer.wordpress.org/apis/security/nonces/) to avoid [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) issues. This prevents other sites from forcing you to perform actions without explicitly intending to do so. This requires slightly special handling for the API.

The API uses nonces with the action set to `wp_rest`. To generate it and pass it to your script you can use the `wp_localize_script()`function.

```php
<?php
// Using wp_localize_script()
function example_enqueue_script() {
  wp_enqueue_script( 'my-script-handle', 'url-to/my-script.js', array( 'jquery' ) );
  wp_localize_script( 'my-script-handle', 'bpRestApi', array(
    'nonce' => wp_create_nonce( 'wp_rest' ),
  ) );
}
add_action( 'bp_enqueue_scripts', 'example_enqueue_script' );
```

### Sending the nonce

For developers making their own Ajax requests, the nonce will need to be passed with each request. The recommended way to send the nonce value is in the request header. Below is an example using jQuery.

```javascript
jQuery.ajax( {
  url: '/wp-json/buddypress/v1/components',
  beforeSend: function( xhr ) {
    xhr.setRequestHeader( 'X-WP-Nonce', bpRestApi.nonce );
  },
  success: function( data ) {
    console.log( data )
  }
} );
```

### Using the BP API Request script as a dependency

We advise you to use the `bp-api-request` JavaScript we’ve built to make sure to be compatible with our WordPress minimum required version: `4.7.0`.

That’s why, you’ll find into each endpoint of the [Developer Endpoint Reference](#developer-endpoint-reference) examples of use relying on this dependency.

To enjoy it, you simply need to include it as a dependency of your JavaScript when [registering/enqueueing](https://developer.wordpress.org/plugins/javascript/enqueuing/) your script into WordPress. For example, our `example_enqueue_script()` function becomes:

```
<?php
// Using 'bp-api-request' as a dependency.
function example_enqueue_script() {
  wp_enqueue_script( 'my-script-handle', 'url-to/my-script.js', array( 'bp-api-request' ) );
}
add_action( 'bp_enqueue_scripts', 'example_enqueue_script' );
```

Then into the `my-script.js` file we can directly use the `bp.apiRequest()` function:

```
bp.apiRequest( {
	path: 'buddypress/v1/components',
	type: 'GET',
} ).done( function( data ) {
	console.log( data );
} ).fail( function( error ) {
	console.log( error );
} );
```
