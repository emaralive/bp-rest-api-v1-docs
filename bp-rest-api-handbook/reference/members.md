# Members

The BuddyPress Members endpoint extends the WordPress Users one to include specific BuddyPress data such as profile fields data *(1)* and use the `BP_User_Query` instead of the `WP_User_Query` to fetch the members.

*(1) If the Extend profiles component is active on the website.*

## Schema

The schema defines all the fields that exist for a member object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>Unique identifier for the member.<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>name</code><p></p><p>string</p></td><td>Display name for the member.<br>Context:&nbsp;<code>embed</code>, <code>view</code>, <code>edit</code></td></tr><tr><td><code>mention_name</code><p></p><p>string</p></td><td>The name used for that user in @-mentions.<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>link</code><p></p><p>string,<br>uri</p></td><td>Profile URL of the member.<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>user_login</code><p></p><p>string</p></td><td>An alphanumeric identifier for the member.<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>member_types</code><p></p><p>array</p></td><td>Member types associated with the member. See this <a href="https://codex.buddypress.org/developer/member-types/">documentation page</a> for more information.<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>registered_date</code><p></p><p>string or null</p></td><td>Registration date for the member.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>registered_date_gmt</code><p></p><p>string or null</p></td><td>The date the member was registered, as GMT.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>password</code><p></p><p>string</p></td><td>Password for the member (never included).<br>Context:&nbsp;<code>none</code></td></tr><tr><td><code>roles</code><p></p><p>array</p></td><td>Roles assigned to the member.<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>capabilities</code><p></p><p>object</p></td><td>All capabilities assigned to the member.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>extra_capabilities</code><p></p><p>object</p></td><td>All capabilities assigned to the member.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>xprofile</code> <em>(1)</em><p></p><p>array</p></td><td>Member xProfile groups and its fields.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>friendship_status</code> <em>(2)</em><p></p><p>boolean</p></td><td>Whether the logged in user has a friendship relationship with the fetched user.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>friendship_status_slug</code> <em>(2)</em><p></p><p>string</p></td><td>Slug of the friendship relationship status the logged in user has with the fetched user.<br>Read only<br>One of: <code>is_friend</code>, <code>not_friends</code>, <code>pending</code>, <code>awaiting_response</code><br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>last_activity</code><p></p><p>object</p></td><td>Last date the member was active on the site (object properties: <code>timediff</code>, <code>date</code> and <code>date_gmt</code>).<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>latest_update</code> <em>(3)</em><p></p><p>object</p></td><td>The content of the latest activity posted by the member (object properties: <code>id</code>, <code>raw</code> and <code>rendered</code>).<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>total_friend_count</code> <em>(2)</em><p></p><p>integer</p></td><td>Total number of friends for the member..<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>avatar_urls</code> <em>(4)</em><p></p><p>object</p></td><td>Avatar URLs for the member (Full &amp; Thumb sizes).<br>Read only<br>Context:&nbsp;<code>embed</code>,&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

*(2) Data is only fetched if the Friends component is active  
(3) Data is only fetched if the Activity component is active  
(4) Only if the WordPress discussion settings allow avatars.*

## List Members

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view`, `embed`, `edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of members to be returned in result set.  
Default: `10` |
| search | `string` | Limit results to those matching a string. |
| exclude | `array` | Ensure result set excludes specific IDs.  
Default: `[]` |
| include | `array` | Ensure result set include specific IDs.  
Default: `[]` |
| type | `string` | Shorthand for certain orderby/order combinations.  
Default: `newest`  
One of: `active, newest, alphabetical, random, online, popular` |
| user\_id | `integer` | Limit results to friends of a user.  
Default: `0` |
| user\_ids | `array` | Pass IDs of users to limit result set.  
Default: `[]` |
| populate\_extras | `boolean` | Whether to fetch extra BP data about the returned members.  
Default: `false` |
| member\_type | `array` | Limit results set to certain type(s). See this [documentation page](https://codex.buddypress.org/developer/member-types/) for more information.  
Default: `[]` |
| xprofile | `array` | Limit results set to a certain XProfile field.  
Default: `[]` |

### Definition

`GET /buddypress/v1/members`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members',
  type: 'GET',
  data: {
    context: 'view',
    'xprofile': {
        relation: 'AND',
        args: [
            {
                field: 'Test field',
                value: 'Hello world',
                compare: '='
            }
        ]
    },
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Create a member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| user\_login | `string` | An alphanumeric identifier for the member.  
**Required** |
| password | `string` | Password for the member.  
**Required** |
| email | `string` | The email address for the member.  
**Required** |
| name | `string` | Display name for the member. |
| roles | `array` | Roles assigned to the member. |
| member\_type | `string` | A comma separated list of Member Types to set for the member. See this [documentation page](https://codex.buddypress.org/developer/member-types/) for more information. |

### Definition

`POST /buddypress/v1/members`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members',
  type: 'POST',
  data: {
    context: 'edit',
    name: 'Test User',
    user_login: 'testuser',
    email: 'test@user.mail',
    password: 'password' // Always use strong passwords, not like this one!
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | Unique identifier for the member. |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, embed, edit` |
| populate\_extras | `boolean` | Whether to fetch extra BP data about the returned member.  
Default: `false` |

### Definition

`GET /buddypress/v1/members/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members/2',
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

## Update a specific member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | Unique identifier for the user. |
| name | `string` | Display name for the member. |
| roles | `array` | Roles assigned to the member. |
| member\_type | `string` | A comma separated list of Member Types to set for the member. See this [documentation page](https://codex.buddypress.org/developer/member-types/) for more information. |

### Definition

`PUT /buddypress/v1/members/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members/2',
  type: 'PUT',
  data: {
    context: 'edit',
    name: 'FirstName LastName',
    roles: 'contributor'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Delete a specific member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | Unique identifier for the member.  
**Required** |
| force | `boolean` | Required to be true, as members do not support trashing. |
| reassign | `integer` | Reassign the deleted member’s posts and links to this user ID.  
**Required** |

### Definition

`DELETE /buddypress/v1/members/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members/2',
  type: 'DELETE',
  data: {
    context: 'edit',
    force: true,
    reassign: 1 // The User ID to reassign the deleted user's post to.
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve the logged in member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, embed, edit` |

### Definition

`GET /buddypress/v1/members/me`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members/me',
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

## Update the logged in member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| name | `string` | Display name for the member. |
| roles *(1)* | `array` | Roles assigned to the member. |
| member\_type | `string` | A comma separated list of Member Types to set for the member. See this [documentation page](https://codex.buddypress.org/developer/member-types/) for more information. |

*(1) To update roles, the logged in member must have the* `*promote_user*` *capability.*

### Definition

`PUT /buddypress/v1/members/me`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members/me',
  type: 'PUT',
  data: {
    context: 'edit',
    name: 'FirstName LastName'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Delete the logged in member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| force | `boolean` | True as users do not support trashing  
**Required** |
| reassign | `integer` | Reassign the deleted member’s posts and links to this user ID.  
**Required** |

### Definition

`DELETE /buddypress/v1/members/me`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/members/me',
  type: 'DELETE',
  data: {
    context: 'edit',
    force: true,
    reassign: 1 // The User ID to reassign the deleted user's post to.
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```