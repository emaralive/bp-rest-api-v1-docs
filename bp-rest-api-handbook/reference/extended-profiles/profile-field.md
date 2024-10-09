# Profile Field

## Schema

The schema defines all the fields that exist for a profile field object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>A unique numeric ID for the profile field.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>group_id</code><p></p><p>integer</p></td><td>The ID of the group the profile field is part of.<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>parent_id</code><p></p><p>integer</p></td><td>The ID of the parent field.<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>type</code><p></p><p>string</p></td><td>The form element used by the profile field.<br>Context:&nbsp;<code>view</code>, <code>edit</code><br>One of: <code>checkbox</code>, <code>datebox</code>, <code>multiselectbox</code>, <code>number</code>, <code>url</code>, <code>radio</code>, <code>selectbox</code>, <code>textarea</code>, <code>textbox</code>, <code>telephone</code>, <code>option</code> <em>(1)</em></td></tr><tr><td><code>name</code><p></p><p>string</p></td><td>The name of the profile field.<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>description</code><p></p><p>object</p></td><td>The <code>raw</code> and <code>rendered</code> descriptions of the profile field.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>is_required</code><p></p><p>boolean</p></td><td>Whether the profile field must have a value or not.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>can_delete</code><p></p><p>boolean</p></td><td>Whether the profile field can be deleted or not.<br>Default: <code>true</code><br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>field_order</code><p></p><p>integer</p></td><td>The order of the profile field within the group of profile fields.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>option_order</code><p></p><p>integer</p></td><td>The order of the option within the profile field’s list of options.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>order_by</code><p></p><p>string</p></td><td>How the options of a profile field are sorted.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>Default: <code>asc</code><br>One of: <code>asc</code>, <code>desc</code></td></tr><tr><td><code>is_default_option</code><p></p><p>boolean</p></td><td>Whether the option is the default one for the profile field.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>visibility_level</code><p></p><p>string</p></td><td>Who may see the saved value for this profile field.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>Default: <code>public</code><br>One of: <code>public</code>, <code>adminsonly</code>, <code>loggedin</code>, <code>friends</code> <em>(1)</em></td></tr><tr><td><code>options</code><br>array</td><td>Options of the profile field.<br>Read only.<br>Context: <code>view</code>, <code>edit</code></td></tr><tr><td><code>data</code><p></p><p>object</p></td><td>The <code>raw</code>, <code>unserialized</code> and <code>rendered</code> values for this profile field.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br><a href="https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-data/#field-data-object">More details about the value object</a>.</td></tr></tbody></table>

*(1) This is the list of BuddyPress built-in Profile field types. Please note that BuddyPress plugins can extend this list.*

*(2) The* `*friends*` *visibility level is only available when the Friend Connections component is active.*

## List profile fields

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | string | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of profile fields to be returned in the result set.  
Default: `10` |
| search | `string` | Limit results to those matching a string. |
| profile\_group\_id | `integer` | ID of the profile group that has profile fields. |
| hide\_empty\_groups | `boolean` | Whether to hide profile groups that do not have any profile fields or not.  
Default: `false` |
| user\_id | `integer` | Required if you want to load a specific user’s data.  
Default: the logged in user ID. |
| member\_type | `array` | Limit profile fields to those restricted to a given member type, or array of member types. If the $user\_id is provided, then the value of $member\_type will be overridden by the member types of that user. The special value of ‘any’ will return only those fields that are unrestricted by member type – i.e., those applicable to any type.  
Default: `[]` |
| hide\_empty\_fields | `boolean` | Whether to hide profile fields where the user has not provided data or not.  
Default: `false` |
| fetch\_field\_data | `boolean` | Whether to fetch data for each profile field. Requires a `$user_id`.  
Default: `false` |
| fetch\_visibility\_level | `boolean` | Whether to fetch the visibility level for each field.  
Default: `false` |
| signup\_fields\_only | `boolean` | Whether to only return signup fields.  
Default: `false` |
| exclude\_groups | `array` | Ensure result set excludes specific profile field groups.  
Default: `[]` |
| exclude\_fields | `array` | Ensure result set excludes specific profile fields.  
Default: `[]` |
| update\_meta\_cache | `boolean` | Whether to pre-fetch xprofilemeta for all retrieved groups, fields, and data.  
Default: `true` |

### Definition

`GET /buddypress/v1/xprofile/fields`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/fields',
  type: 'GET',
  data: {
    context: 'view'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Create a profile field

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| group\_id | `integer` | The ID of the group the field is part of.  
**Required** |
| parent\_id | `integer` | The ID of the parent field. |
| type | `string` | The form element of the profile field.  
**Required**  
One of: `checkbox, datebox, multiselectbox, number, url, radio, selectbox, textarea, textbox, telephone, option` |
| name | `string` | The name of the profile field.  
**Required** |
| description | `string` | The description of the profile field. |
| is\_required | `boolean` | Whether the profile field must have a value. |
| can\_delete | `boolean` | Whether the profile field can be deleted or not.  
Default: `true` |
| field\_order | `integer` | The order of the profile field within the group of profile fields. |
| option\_order | `integer` | The order of the option within the profile field’s list of options. |
| order\_by | string | How the options of a profile field are sorted.  
Default: `asc`  
One of: `asc, desc` |
| is\_default\_option | `boolean` | Whether the option is the default one for the profile field. |
| default\_visibility | `string` | Default visibility for the profile field.  
Default: `public`  
One of: `public, adminsonly, loggedin, friends` |
| allow\_custom\_visibility | `string` | Whether to allow members to set the visibility for the profile field data or not.  
Default: `allowed`  
One of: `allowed, disabled` |
| do\_autolink | `string` | Autolink status for this profile field.  
Default: `off`  
One of: `on, off` |

### Definition

`POST /buddypress/v1/xprofile/fields`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/fields',
  type: 'POST',
  data: {
    context: 'edit',
    group_id: 2,                    // Required
    type: 'textbox',                // Required
    name: 'BuddyPress.org username' // Required
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific profile field

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the profile field.  
**Required** |
| user\_id | `integer` | Required if you want to load a specific user’s data.  
Default: `0` |
| fetch\_field\_data | `boolean` | Whether to fetch data for the field. Requires `$user_id`.  
Default: `false` |

### Definition

`GET /buddypress/v1/xprofile/fields/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/fields/5',
  type: 'GET',
  data: {
    context: 'view'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Update a specific profile field

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the profile field.  
**Required** |
| group\_id | `integer` | The ID of the profile group the profile field is part of. |
| parent\_id | `integer` | The ID of the parent profile field. |
| type | `string` | The form element used by the profile field.  
One of: `checkbox, datebox, multiselectbox, number, url, radio, selectbox, textarea, textbox, telephone, option` |
| name | `string` | The name of the profile field. |
| description | `string` | The description of the profile field. |
| is\_required | `boolean` | Whether the profile field must have a value. |
| can\_delete | `boolean` | Whether the profile field can be deleted or not.  
Default: `true` |
| field\_order | `integer` | The order of the profile field within the group of profile fields. |
| option\_order | `integer` | The order of the option within the profile field’s list of options. |
| order\_by | `string` | How the options of a profile field are sorted.  
Default: `asc`  
One of: `asc, desc` |
| is\_default\_option | `boolean` | Whether the option is the default one for the profile field. |
| default\_visibility | `string` | Default visibility for the profile field.  
Default: `public`  
One of: `public, adminsonly, loggedin, friends` |
| allow\_custom\_visibility | `string` | Whether to allow members to set the visibility for the profile field data or not.  
Default: `allowed`  
One of: `allowed, disabled` |
| do\_autolink | `string` | Autolink status for this profile field.  
Default: `off`  
One of: : `on, off` |

### Definition

`PUT /buddypress/v1/xprofile/fields/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/fields/5',
  type: 'PUT',
  data: {
    context: 'edit',
    description: 'The username you used to register on BuddyPress.org'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Delete a specific profile field

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the profile field.  
**Required** |
| delete\_data | `boolean` | Required if you want to delete users data for the field.  
Default: `false` |

### Definition

`DELETE /buddypress/v1/xprofile/fields/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/fields/5',
  type: 'DELETE',
  data {
    context: 'edit',
    delete_data: true
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```