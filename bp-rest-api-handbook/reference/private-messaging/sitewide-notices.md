# Sitewide Notices

The Sitewide Notices feature allows to send notices to the whole site. This feature is currently part of the Private Messages Component.

Note: The Private Messaging component is an optional one. This means the following endpoints will only be available if the component is active on the community site.

## Schema

The schema defines all the fields that exist for a Siteweide Notice object.

<table><tbody><tr><td><code><code>id</code></code><br><br>integer</td><td>A unique numeric ID for the sitewide notice.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>subject</code><br><br>object</td><td>The&nbsp;<code>raw</code>&nbsp;and&nbsp;<code>rendered</code> contents of the sitewide notice subject.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>message</code><br><br>object</td><td>The&nbsp;<code>raw</code>&nbsp;and&nbsp;<code>rendered</code> contents of the sitewide notice.<br><strong>Required</strong><br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date</code><br><br>string or null</td><td>The date of the sitewide notice, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_gmt</code><br><br>string or null</td><td>The date of the sitewide notice, as GMT.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>is_active</code><br><br>bool</td><td>Whether this sitewide notice is active or not.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

## List Sitewide Notices

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |
| page | `integer` | Current page of the sitewide notices collection.  
Minimum: `1`  
Default: `1` |
| per\_page | `integer` | Maximum number of sitewide notices to be returned in result set.  
Minimum: `1`  
Default: `10`  
Maximum: `100` |
| search | `string` | Limit results to those matching a string. |

### Definition

`GET /buddypress/v1/sitewide-notices`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/sitewide-notices',
  type: 'GET',
  data: {
    context: 'view',
    search: 'Sitewide Notices'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific Sitewide Notice

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | ID of a Sitewide Notice.  
**Required** |

### Definition

`GET /buddypress/v1/sitewide-notices/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: '/buddypress/v1/sitewide-notices/5',
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

## Update a specific Sitewide Notice

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | integer | ID of the Sitewide Notice.  
**Required** |
| subject | string | Subject of the Sitewide Notice. |
| message | string | Content of the Sitewide Notice. |
| is\_active | bool | The status of the Sitewide Notice (active or not). |

### Description

`PUT /buddypress/v1/sitewide-notices/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: '/buddypress/v1/sitewide-notices/5',
  type: 'PUT',
  data: {
    context: 'edit',
    subject: 'a new subject for this sitewide notice'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Delete a specific Sitewide Notice

### Arguments

| Name | Description |
| --- | --- |
| id | ID of the Sitewide Notice.  
**Required** |

### Definition

``DELETE /buddypress/v1/`sitewide-notices`/<id>``

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/sitewide-notices/25',
  type: 'DELETE',
  data: {
    context: 'edit',
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Dismiss currently active notice for the current user

When a user requests to dismiss the current active sitewide notice, the notice is dimissed.

Warning: If the user is not logged in or if there is no active notice available, the REST response will be an error object.

### Definition

``PUT /buddypress/v1/`sitewide-notices`/dismiss``

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/sitewide-notices/dismiss',
  type: 'PUT',
  data: {
    context: 'edit',
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```