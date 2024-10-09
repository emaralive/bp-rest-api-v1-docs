# Group Membership

## Schema

The schema defines all the fields that exist for a group member object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>Unique identifier for the member.<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>name</code><p></p><p>string</p></td><td>Display name for the member.<br>Context:&nbsp;<code>embed</code>, <code>view</code>, <code>edit</code></td></tr><tr><td><code>mention_name</code><p></p><p>string</p></td><td>The name used for that user in @-mentions.<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>link</code><p></p><p>string,<br>uri</p></td><td>Profile URL of the member.<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>user_login</code><p></p><p>string</p></td><td>A numeric identifier for the member.<br><strong>Required</strong><br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>member_types</code><p></p><p>array</p></td><td>Member types associated with the member.<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>registered_date</code><p></p><p>string or null</p></td><td>Registration date for the member, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>registered_date_gmt</code><p></p><p>string or null</p></td><td>Registration date for the member, as GMT.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>password</code><p></p><p>string</p></td><td>Password for the member (never included).<br><strong>Required</strong><br>Context:&nbsp;<code>none</code></td></tr><tr><td><code>roles</code><p></p><p>array</p></td><td>Roles assigned to the member.<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>capabilities</code><p></p><p>object</p></td><td>All capabilities assigned to the member.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>extra_capabilities</code><p></p><p>object</p></td><td>All capabilities assigned to the member.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>xprofile</code> <em>(1)</em><p></p><p>array</p></td><td>Member XProfile groups and its fields.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>friendship_status</code>&nbsp;<em>(2)</em><p></p><p>boolean</p></td><td>Whether the logged in user has a friendship relationship with the fetched user.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>friendship_status_slug</code>&nbsp;<em>(2)</em><p></p><p>string</p></td><td>lug of the friendship relationship status the logged in user has with the fetched user.<br>Read only<br>One of:&nbsp;<code>is_friend</code>,&nbsp;<code>not_friends</code>,&nbsp;<code>pending</code>,&nbsp;<code>awaiting_response</code><br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>avatar_urls</code> <em>(3)</em><p></p><p>object</p></td><td>Avatar URLs for the member (Full &amp; Thumb sizes).<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>is_confirmed</code><p></p><p>integer</p></td><td><code>1</code> if the membership of this user has been confirmed, <code>0</code> otherwise.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>One of: <code>0</code>, <code>1</code></td></tr><tr><td><code>is_mod</code><p></p><p>integer</p></td><td><code>1</code> if this member is a Group moderator, <code>0</code> otherwise.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>One of: <code>0</code>, <code>1</code></td></tr><tr><td><code>is_admin</code><p></p><p>integer</p></td><td><code>1</code> if this member is a Group administrator, <code>0</code> otherwise.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>One of: <code>0</code>, <code>1</code></td></tr><tr><td><code>is_banned</code><p></p><p>integer</p></td><td><code>1</code> if this member has been banned from the Group, <code>0</code> otherwise.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>One of: <code>0</code>, <code>1</code></td></tr><tr><td><code>date_modified</code><p></p><p>string or null</p></td><td>The date of the last time the membership of this user was modified, in the site’s timezone.<br>Read only<br>Context: <code>view,</code> <code>edit</code></td></tr><tr><td><code>date_modified_gmt</code><p></p><p>string or null</p></td><td>The date of the last time the membership of this user was modified, as GMT.<br>Read only<br>Context: <code>view,</code> <code>edit</code></td></tr></tbody></table>

*(1) Datas is only fetched if the xProfile component is active  
(2) Data is only fetched if the Friends component is active  
(3) Only if the WordPress discussion settings allow avatars.*

## List the Group Members

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| group\_id | `integer` | A unique numeric ID for the Group.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, embed, edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of Group members to be returned in result set.  
Default: `10` |
| search | `string` | Limit results to members name matching a string. |
| status | `string` | Sort the order of results by the status of the group members.  
Default: `last_joined`  
One of: `last_joined,` `first_joined,` `alphabetical,` `group_activity` *(1)* |
| roles | `array` | Ensure result set includes specific Group roles.  
Default: `[]`  
One or more of: `admin`, `mod`, `member`, `banned` |
| exclude | `array` | Ensure result set excludes specific member IDs.  
Default: `[]` |
| exclude\_admins | `boolean` | Whether results should exclude group admins and mods.  
Default: `true` |
| exclude\_banned | `boolean` | Whether results should exclude banned group members.  
Default: `true` |

*(1) The* `*group_activity*` *status is only available if the Activity BuddyPress component is active.*

### Definition

`GET /buddypress/v1/groups/<group_id>/members`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/4/members',
  type: 'GET',
  data: {
    context: 'view',
    exclude_admins: false
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Add a specific Member into a Group

Note: To make a logged in user **join a public Group**, you need to use the `view` context. In this case the `role` argument is not available and the user is added to the Group as a member.

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| group\_id | `integer` | A unique numeric ID for the Group.  
**Required** |
| user\_id | `integer` | A unique numeric ID for the Member to add to the Group.  
**Required**  
Default: the logged in user ID |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of: `view, embed, edit` |
| role | `string` | Group role to assign the user to.  
Default: `member`  
One of: `admin, mod, member` |

### Definition

`POST /buddypress/v1/groups/<group_id>/members`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/5/members',
  type: 'POST',
  data: {
    context: 'edit',
    user_id: 3
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Promote or demote a specific Group Member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| group\_id | `integer` | A unique numeric ID for the Group.  
**Required** |
| user\_id | `integer` | A unique numeric ID for the Group Member.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of: `view, embed, edit` |
| role | `string` | Group role to assign the user to.  
Default: `member`  
One of: `admin, mod, member` |
| action | `string` | Action used to update a group member.  
Default: `promote`  
One of: `promote, demote, ban, unban` |

### Definition

`PUT /buddypress/v1/groups/<group_id>/members/<user_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/5/members/3',
  type: 'PUT',
  data: {
    context: 'edit',
    role: 'mod',
    action: 'promote'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Remove a specific Group Member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| group\_id | `integer` | A unique numeric ID for the Group.  
**Required** |
| user\_id | `integer` | A unique numeric ID for the Group Member.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of: `view, embed, edit` |

### Definition

`DELETE /buddypress/v1/groups/<group_id>/members/<user_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/5/members/3',
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