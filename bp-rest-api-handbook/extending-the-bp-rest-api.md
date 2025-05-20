# Extending the BP REST API

You can extend any of the data endpoint responses by registering custom REST fields using the `bp_rest_register_field()` function.

Hooking to `bp_rest_api_init` you first need to register your custom REST field.

<aside class="notice">
Note: Click the <strong>PHP</strong> language tab in the right hand column to see the code examples. 
</aside>

> In the below example code, you’ll notice the `get_callback` parameter, you need to use it to define the function to use to retrieve the value of your custom field and add it to the REST response. Additionally, to update the value of your custom field, you’ll need to code the function you defined as the `update_callback` parameter you had used.

```php
function example_register_activity_rest_field() {
    bp_rest_register_field(
        'activity',      // Id of the BuddyPress component the REST field is about
        'example_field', // Used into the REST response/request
        array(
            'get_callback'    => 'example_get_rest_field_callback',    // The function to use to get the value of the REST Field
            'update_callback' => 'example_update_rest_field_callback', // The function to use to update the value of the REST Field
            'schema'          => array(                                // The example_field REST schema.
                'description' => 'Example of Activity Meta Field',
                'type'        => 'string',
                'context'     => array( 'view', 'edit' ),
            ),
        )
    );
}
add_action( 'bp_rest_api_init', 'example_register_activity_rest_field' );
```
> The function associated with the 'get_callback' parameter.

```php
/**
 * The function to use to get the value of the REST Field.
 *
 * param  array  $array     The list of properties of the BuddyPress component's object.
 * param  string $attribute The REST Field key used into the REST response.
 * return string            The value of the REST Field to include into the REST response.
 */
function example_get_rest_field_callback( $array, $attribute ) {
    // The key of the metadata can be different from the REST Field key.
    $metadata_key = '_example_metadata_key';

    return bp_activity_get_meta( $array['id'], $metadata_key );
}
```
> The function associated with the 'update_callback' parameter.

```php
/**
 * The function to use to update the value of the REST Field.
 *
 * param  object $object    The BuddyPress component's object that was just created/updated during the request.
 *                           (in this case the BP_Activity_Activity object).
 * param  string $attribute The REST Field key used into the REST response.
 * return string $value     The value of the REST Field to save.
 */
function example_update_rest_field_callback( $object, $value, $attribute ) {
    // The key of the metadata can be different from the REST Field key.
    $metadata_key = '_example_metadata_key';

    bp_activity_update_meta( $object->id, $metadata_key, $value );
}
```
