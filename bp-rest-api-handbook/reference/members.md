# Members Endpoint

The BuddyPress Members endpoint extends the WordPress Users one to include specific BuddyPress data such as profile fields data *(1)* and use the `BP_User_Query` instead of the `WP_User_Query` to fetch the members.

*(1) If the Extend profiles component is active on the website.*

## Members Schema

The schema defines all the fields that exist for a member object.

| Attribute | Type | Description |
|:--- |:--- | :---- |
|id | `integer` |Unique identifier for the member.<br><br>Read only<br><br>**Context**: embed, view, edit|
|name| `string` |Display name for the member.<br><br>**Context**: embed, view, edit|
|mention_name| `string` |The name used for that user in @-mentions.<br><br>**Context**: embed, view, edit|
|link| `string`, `uri`|Profile URL of the member.<br><br>Read only<br><br>**Context**: embed, view, edit|
|user_login| `string` |An alphanumeric identifier for the member.<br><br>**Context**: embed, view, edit|
|member_types| `array` |Member types associated with the member. See this documentation page for more information.<br><br>Read only<br><br>**Context**: embed, view, edit|
|registered_date| `string` or `null` |Registration date for the member.<br><br>Read only<br><br>**Context**: edit|
|registered_date_gmt| `string` or `null` |The date the member was registered, as GMT.<br><br>Read only<br><br>**Context**: edit|
|password| `string` |Password for the member (never included).<br><br>**Context**: none|
|roles| `array` |Roles assigned to the member.<br><br>**Context**: edit|
|capabilities| `object` |All capabilities assigned to the member.<br><br>Read only<br><br>**Context**: edit|
|extra_capabilities| `object` |All capabilities assigned to the member.<br><br>Read only<br><br>**Context**: edit|
|xprofile (1)| `array` |Member xProfile groups and its fields.<br><br>Read only<br><br>**Context**: view, edit|
|friendship_status (2)| `boolean` |Whether the logged in user has a friendship relationship with the fetched user.<br><br>Read only<br><br>**Context**: view, edit|
|friendship_status_slug (2)| `string` |Slug of the friendship relationship status the logged in user has with the fetched user.<br><br>Read only<br><br>One of: is_friend, not_friends, pending, awaiting_response<br><br>**Context**: view, edit|
|last_activity| `object` |Last date the member was active on the site (object properties: timediff, date and date_gmt).<br><br>Read only<br><br>**Context**: view, edit|
|latest_update (3)| `object` |The content of the latest activity posted by the member (object properties: id, raw and rendered).<br><br>Read only<br><br>**Context**: view, edit|
|total_friend_count (2)| `integer` |Total number of friends for the member..<br><br>Read only<br><br>**Context**: view, edit|
|avatar_urls (4)| `object` |Avatar URLs for the member (Full & Thumb sizes).<br><br>Read only<br><br>**Context**: embed, view, edit|

*(2) Data is only fetched if the Friends component is active  
(3) Data is only fetched if the Activity component is active  
(4) Only if the WordPress discussion settings allow avatars.*

## List Members

### Arguments

| Attribute | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.<br><br>**Default**: `view`<br><br>**One of**: `view`, `embed`, `edit` |
| page | `integer` | Current page of the collection. <br><br>**Default**: `1` |
| per\_page | `integer` | Maximum number of members to be returned in result set. <br><br>**Default**: `10` |
| search | `string` | Limit results to those matching a string. |
| exclude | `array` | Ensure result set excludes specific IDs. <br><br>**Default**: `[]` |
| include | `array` | Ensure result set include specific IDs.<br><br>**Default**: `[]` |
| type | `string` | Shorthand for certain orderby/order combinations.<br><br>**Default**: `newest` <br><br>**One of**: `active, newest, alphabetical, random, online, popular` |
| user\_id | `integer` | Limit results to friends of a user.<br><br>**Default**: `0` |
| user\_ids | `array` | Pass IDs of users to limit result set.<br><br>**Default**: `[]` |
| populate\_extras | `boolean` | Whether to fetch extra BP data about the returned members.<br><br>**Default**: `false` |
| member\_type | `array` | Limit results set to certain type(s). See this [documentation page](https://codex.buddypress.org/developer/member-types/) for more information.<br><br>**Default**: `[]` |
| xprofile | `array` | Limit results set to a certain XProfile field.<br><br>**Default**: `[]` |

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

| Attribute | Type | Description |
| --- | --- | --- |
| user\_login | `string` | An alphanumeric identifier for the member.<br><br>**Required** |
| password | `string` | Password for the member.<br><br>**Required** |
| email | `string` | The email address for the member.<br><br>**Required** |
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

| Attribute | Type | Description |
| --- | --- | --- |
| id | `integer` | Unique identifier for the member. |
| context | `string` | Scope under which the request is made; determines fields present in response.<br><br>**Default**: `view`<br><br>**One of**: `view, embed, edit` |
| populate\_extras | `boolean` | Whether to fetch extra BP data about the returned member.<br><br>**Default**: `false` |

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

| Attribute | Type | Description |
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

| Attribute | Type | Description |
| --- | --- | --- |
| id | `integer` | Unique identifier for the member.<br><br>**Required** |
| force | `boolean` | Required to be true, as members do not support trashing. |
| reassign | `integer` | Reassign the deleted member’s posts and links to this user ID.<br><br>**Required** |

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

| Attribute | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.>br><br>**Default**: `view`<br><br>**One of**: `view, embed, edit` |

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

| Attribute | Type | Description |
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

| Attribute | Type | Description |
| --- | --- | --- |
| force | `boolean` | True as users do not support trashing.<br><br>**Required** |
| reassign | `integer` | Reassign the deleted member’s posts and links to this user ID.<br><br>**Required** |

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
