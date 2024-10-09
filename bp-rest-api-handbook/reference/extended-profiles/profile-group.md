# Profile Group

## Schema

The schema defines all the fields that exist for a profile group object.

<table><tbody><tr><td><code>id</code><br><br>integer</td><td>A unique numeric ID for the group of profile fields.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>name</code><br><br>string</td><td>The name of the group of profile fields.<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>description</code><br><br>object</td><td>The <code>raw</code> and <code>rendered</code> descriptions of the group of profile fields.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>group_order</code><br><br>integer</td><td>The order of the group of profile fields.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>can_delete</code><br><br>boolean</td><td>Whether the group of profile fields can be deleted or not.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>fields</code><br><br>array</td><td>The list of profile fields object attached to the group of profile fields.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

## List groups of profile fields

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, edit` |
| page | `integer` | Current page of the collection of groups of profile fields.  
Default: `1` |
| per\_page | `integer` | Maximum number of groups of profile fields to be returned in result set.  
Default: `10` |
| search | `string` | Limit results to those matching a string. |
| profile\_group\_id | `integer` | ID of the group of profile fields that has fields. |
| hide\_empty\_groups | `boolean` | Whether to hide profile groups that do not have any profile fields or not.  
Default: `false` |
| user\_id | `integer` | Needed if you want to load a specific user’s data.  
Default: the logged in user ID. |
| member\_type | `array` | Limit fields by those restricted to a given member type, or array of member types. If `$user_id` is provided, the value of `$member_type` will be overridden by the member types of the provided user. The special value of ‘any’ will return only those fields that are unrestricted by member type – i.e., those applicable to any type.  
Default: `[]` |
| hide\_empty\_fields | `boolean` | Whether to hide profile fields of profile groups that do not have any content or not.  
Default: `false` |
| fetch\_fields | `boolean` | Whether to fetch the profile fields for each profile group.  
Default: `false` |
| fetch\_field\_data | `boolean` | Whether to fetch data for each profile field. Requires a `$user_id`.  
Default: `false` |
| fetch\_visibility\_level | `boolean` | Whether to fetch the visibility level for each profile field.  
Default: `false` |
| signup\_fields\_only | `boolean` | Whether to only return signup fields.  
Default: `false` |
| exclude\_groups | `array` | Ensure result set excludes specific groups of profile fields.  
Default: `[]` |
| exclude\_fields | `array` | Ensure result set excludes specific profile fields.  
Default: `[]` |
| update\_meta\_cache | `boolean` | Whether to pre-fetch xprofile metadata for all retrieved groups, fields, and data.  
Default: `true` |

### Definition

`GET /buddypress/v1/xprofile/groups`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/groups',
  type: 'GET',
  data: {
    context: 'view',
    fetch_fields: true,
    signup_fields_only: true
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Create a group of profile fields

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the group of profile fields.  
**Required** |
| description | `string` | The description of the group of profile fields. |
| can\_delete | `boolean` | Whether the group of profile fields can be deleted or not.  
Default: `true` |

### Definition

`POST /buddypress/v1/xprofile/groups`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/groups',
  type: 'POST',
  data: {
    context: 'edit',
    name: 'Skills',
    description: 'Information about your skills'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific group of profile fields

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the group of profile fields.  
**Required** |

### Definition

`GET /buddypress/v1/xprofile/groups/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/groups/3',
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

## Update a specific group of profile fields

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the group of profile fields.  
**Required** |
| name | `string` | The name of the group of profile fields. |
| description | `string` | The description of the group of profile fields. |
| group\_order | `integer` | The order of the group of profile fields. |
| can\_delete | `boolean` | Whether the group of profile fields can be deleted or not. |

### Definition

`PUT /buddypress/v1/xprofile/groups/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/groups/3',
  type: 'PUT',
  data: {
    context: 'edit',
    group_order: 1
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Delete a group of profile fields

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the group of profile fields.  
**Required** |

### Definition

`DELETE /buddypress/v1/xprofile/groups/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/xprofile/groups/3',
  type: 'DELETE',
  data: {
    context: 'edit'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```