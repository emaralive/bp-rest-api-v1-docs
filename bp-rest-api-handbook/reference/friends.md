# Friend connections

The Friends component allow your members to make connections with other members. The BuddyPress Friendship is a mutually agreed relationship between 2 members.

Note: The Friends component is an optional one. This means the following endpoints will only be available if the component is active on the community site

## Schema

The schema defines all the fields that exist for a friendship object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>A unique numeric ID for the friendship.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>initiator_id</code><p></p><p>integer</p></td><td>The ID of the user who is requesting the Friendship.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>friend_id</code><p></p><p>integer</p></td><td>The ID of the user who is invited to agree to the Friendship request.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>is_confirmed</code><p></p><p>boolean</p></td><td>Whether the friendship has been confirmed. <code>true</code> if it is the case, <code>false</code> otherwise.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_created</code><p></p><p>string or null</p></td><td>The date the friendship was created, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_created_gmt</code><p></p><p>string or null</p></td><td>The date the friendship was created, as GMT.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

## List a Member’s Friendship requests

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of friendships to be returned in result set.  
Default: `10` |
| user\_id | `integer` | ID of the member whose friendships are being retrieved.  
**Required**  
Default: the logged in user ID |
| is\_confirmed | `integer` | Whether the friendship has been confirmed. `1` if it is the case, `0` otherwise.  
Default: `0` |
| id | `integer` | Unique numeric identifier of the friendship.  
Default: `0` |
| initiator\_id | `integer` | The ID of the user who is requesting the Friendship.  
Default: `0` |
| friend\_id | `integer` | The ID of the user who is invited to agree to the Friendship request.  
Default: `0` |
| orderby | `string` | Order Groups by which attribute.  
Default: `date_created`  
One of : `'date_created'`, `'initiator_user_id'`, `'friend_user_id'`, `'id'` |
| order | `string` | Order sort attribute ascending or descending.  
Default: `desc`  
One of : `asc, desc` |

### Definition

`GET /buddypress/v1/friends`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/friends',
  type: 'GET',
  data: {
    context: 'view',
    'user_id': 47,
    'is_confirmed': 1
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Request a new Friendship

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of : `view, edit` |
| initiator\_id | `integer` | The ID of the user who is requesting the Friendship.  
**Required** |
| friend\_id | `integer` | The ID of the user who is invited to agree to the Friendship request.  
**Required** |
| force | `boolean` | Whether to force the friendship agreement.  
**NB**: Only Administrators can force a friendship.  
Default: `false` |

### Definition

`POST /buddypress/v1/friends`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/friends',
  type: 'POST',
  data: {
    context: 'edit',
    'initiator_id': 4, // Required.
    'friend_id': 5     // Required.
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve the Friendship between the logged in Member & another Member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | Numeric identifier for a possible Friendship initiator or for the user who is invited to agree to a Friendship request.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |

### Definition

`GET /buddypress/v1/friends/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/friends/51',
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

## Let the logged in Member accept a Friendship

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | Numeric identifier of the friendship initiator.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of : `view, edit` |

### Definition

`PUT /buddypress/v1/friends/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/friends/131',
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

## Let the logged in Member reject, withdraw or remove a Friendship.

*   The logged in Member is withdrawing a Friendship request when he is the initiator.
*   The logged in Member is rejecting a Friendship request when he is the user who is invited to agree to a Friendship request.
*   The logged in Member is removing an existing Friendship when the `force` argument is used.

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the user who requested a Friendship or who is invited to agree to a Friendship request.  
**Required** |
| force | boolean | Whether to force the removal of an existing Friendship. `true` to remove, `false` otherwise.  
Default: `false` |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of : `view, edit` |

### Definition

`DELETE /buddypress/v1/friends/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/friends/131',
  type: 'DELETE',
  data: {
    context: 'edit',
    force: true
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```