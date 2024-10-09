# Group Membership Requests

## Schema

The schema defines all the fields that exist for a group membership request object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>A unique numeric ID for the BP Invitation object.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>user_id</code><p></p><p>integer</p></td><td>The ID of the user who requested a Group membership.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>group_id</code><p></p><p>integer</p></td><td>The ID of the group the user requested a membership for.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_modified</code><p></p><p>string,<br>date-time</p></td><td>The date the object was created or last updated, in the site’s timezone.&nbsp;<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>type</code><p></p><p>string</p></td><td>A request for membership to a private group.&nbsp;<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>Default: <code>request</code><br>One of:&nbsp;<code>invite</code>,&nbsp;<code>request</code></td></tr><tr><td><code>message<br></code>string</td><td>The <code>raw</code> and <code>rendered</code> versions for the content of the message.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

## List the Group Membership Requests

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | string | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of items to be returned in result set.  
Default: `10` |
| group\_id | `integer` | The ID of the group the user requested a membership for. |
| user\_id | `integer` | Return only Membership requests made by a specific user. |

### Definition

`GET /buddypress/v1/groups/membership-requests`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/membership-requests',
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

## Request a Group Membership

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| user\_id | `integer` | The ID of the user who requested a Group membership.  
Default: the logged in user ID |
| group\_id | `integer` | The ID of the group the user requested a membership for.  
**Required** |
| message | `string` | The optional message the user requesting membership to private group sends to the group administrator. |

### Definition

`POST /buddypress/v1/groups/membership-requests`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/membership-requests',
  type: 'POST',
  data: {
    context: 'edit',
    group_id: 30
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific Group Membership Request

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| request\_id | `integer` | A unique numeric ID for the group membership request.  
**Required** |
| context | string | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, edit` |

### Definition

`GET /buddypress/v1/groups/membership-requests/<request_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/membership-requests/12',
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

## Accept a Group Membership Request

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| request\_id | `integer` | A unique numeric ID for the group membership request.  
**Required** |

### Definition

`PUT /buddypress/v1/groups/membership-requests/<request_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/membership-requests/12',
  type: 'PUT',
  data: {
    context: 'edit'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Reject or cancel a Group Membership Request

Note: If the logged in user is the one who requested a Group membership, using this endpoint will cancel it. Otherwise it will reject it.

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| request\_id | `integer` | A unique numeric ID for the group membership request.  
**Required** |

### Definition

`DELETE /buddypress/v1/groups/membership-requests/<request_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/membership-requests/12',
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