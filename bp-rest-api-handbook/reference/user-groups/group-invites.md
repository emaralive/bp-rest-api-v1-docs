# Group Invites

## Schema

The schema defines all the fields that exist for a group invite object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>A unique numeric ID for the BP Invitation object.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>user_id</code><p></p><p>integer</p></td><td>The ID of the user who is invited to join the Group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>invite_sent</code><p></p><p>boolean</p></td><td>Whether the invite has been sent to the invitee.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>inviter_id</code><p></p><p>integer</p></td><td>The ID of the user who made the invite.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>group_id</code><p></p><p>integer</p></td><td>The ID of the group to which the user has been invited.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_modified</code><p></p><p>string or null</p></td><td>The date the object was created or last updated, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_modified_gmt</code><p></p><p>string or null</p></td><td>The date the object was created or last updated, as GMT.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>type</code><p></p><p>string</p></td><td>Invitation or request.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>Default: <code>invite</code><br>One of:&nbsp;<code>invite</code>,&nbsp;<code>request</code></td></tr><tr><td><code>message</code><p></p><p>object</p></td><td>The <code>raw</code> and <code>rendered </code>versions for the content of the message.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

## List the Group Invites

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | string | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of items to be returned in result set.  
Default: `10` |
| group\_id | `integer` | ID of the group to limit results to.  
Default: `0` |
| user\_id | `integer` | Return only invitations extended to this user.  
Default: `0` |
| inviter\_id | `integer` | Return only invitations extended by this user.  
Default: `0` |
| invite\_sent | string | Limit result set to invites that have been sent, not sent, or include all.  
Default: `sent`  
One of : `draft, sent, all` |

### Definition

`GET /buddypress/v1/groups/invites`

### Example of Use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/invites',
  type: 'GET',
  data: {
    context: 'view',
    group_id: 3
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Invite a user to join a Group

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| user\_id | `integer` | The ID of the user who is invited to join the Group.  
**Required** |
| inviter\_id | `integer` | The ID of the user who made the invite.  
Default: the current logged in user ID. |
| group\_id | `integer` | The ID of the group to which the user has been invited.  
**Required** |
| message | `string` | The optional message to send to the invited user. |
| send\_invite | `boolean` | Whether the invite should be sent to the invitee.  
Default: `true` |

### Definition

`POST /buddypress/v1/groups/invites`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/invites',
  type: 'POST',
  data: {
    context: 'edit',
    user_id: 13,
    group_id: 7,
    message: 'Join the BuddyPress Contributors Group'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific Group Invite

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| invite\_id | `integer` | A unique numeric ID for the group invitation.  
**Required** |
| context | string | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |

### Definition

`GET /buddypress/v1/groups/invites/<invite_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/invites/5',
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

## Accept a specific Group Invite

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| invite\_id | `integer` | A unique numeric ID for the group invitation.  
**Required** |

### Definition

`PUT /buddypress/v1/groups/invites/<invite_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/invites/5',
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

## Reject or remove a specific Group Invite

Note: If the invited user is the logged in user then the Group Invite will be rejected. Otherwise the uninvite action will be used.

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| invite\_id | `integer` | A unique numeric ID for the group invitation.  
**Required** |

### Definition

`DELETE /buddypress/v1/groups/invites/<invite_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/components',
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