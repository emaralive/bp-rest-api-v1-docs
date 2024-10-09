# Groups

## Schema

The schema defines all the fields that exist for a group object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>A unique numeric ID for the Group.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>creator_id</code><p></p><p>integer</p></td><td>The ID of the user who created the Group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>name</code><p></p><p>string</p></td><td>The name of the group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>slug</code><p></p><p>string</p></td><td>The URL-friendly slug for the group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>link</code><p></p><p>string,<br>uri</p></td><td>The permalink to the Group on the site.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>description</code><p></p><p>object</p></td><td>The <code>raw</code> and <code>rendered</code> descriptions of the Group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>status</code><p></p><p>string</p></td><td>The visibility status of the Group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code><br>One of: <code>public</code>, <code>private</code>, <code>hidden</code></td></tr><tr><td><code>enable_forum</code><p></p><p>boolean</p></td><td>Whether the group has a forum or not.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>parent_id</code><p></p><p>integer</p></td><td>ID of the parent Group.<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_created</code><p></p><p>string or null</p></td><td>The date the Group was created, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_created_gmt</code><p></p><p>string or null</p></td><td>The date the Group was created, as GMT.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>types</code><p></p><p>array</p></td><td>The Group Types. See this <a href="https://codex.buddypress.org/developer/group-types/">documentation page</a> for more information about Groupe Types.<br>Read only<br>Context: <code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>admins</code><p></p><p>array</p></td><td>List of <code>WP_User</code> objects for Group administrators.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>mods</code><p></p><p>array</p></td><td>List of <code>WP_User</code> objects for moderators.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>total_member_count</code><br>integer</td><td>Count of all Group members.<br>Read only<br>Context:&nbsp;<code><code>view</code>,&nbsp;<code>edit</code></code></td></tr><tr><td><code>last_activity</code><p></p><p>string or null</p></td><td>The date the Group was last active, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code><code>view</code>,&nbsp;<code>edit</code></code></td></tr><tr><td><code>last_activity_gmt</code><p></p><p>string or null</p></td><td>The date the Group was last active, as GMT.<br>Read only<br>Context:&nbsp;<code><code>view</code>,&nbsp;<code>edit</code></code></td></tr><tr><td><code>last_activity_diff</code><p></p><p>string</p></td><td>The human diff time the Group was last active, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code><code>view</code>,&nbsp;<code>edit</code></code></td></tr><tr><td><code>avatar_urls</code>&nbsp;<em>(1)</em><p></p><p>object</p></td><td>Avatar URLs for the group (Full &amp; Thumb sizes).<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

*(1) Only if Group Avatar uploads are enabled on the community site.*

## List User Groups

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of Groups to be returned in result set.  
Default: `10` |
| search | `string` | Limit results to Group names or descriptions matching a string. |
| type | `string` | Shorthand for certain orderby/order combinations.  
Default: `active`  
One of: `active, newest, alphabetical, random, popular, most-forum-topics, most-forum-posts` |
| order | `string` | Order sort attribute ascending or descending.  
Default: `desc`  
One of : `asc, desc` |
| orderby | `string` | Order Groups by which attribute.  
Default: `date_created`  
One of : `date_created, last_activity, total_member_count, name, random` |
| status | `array` | Group statuses to limit results to.  
Default: `[]`  
One or more of : `public, private, hidden` |
| user\_id | `integer` | Pass a user\_id to limit to only Groups that this user is a member of.  
Default: `0` |
| parent\_id | `array` | Get Groups that are children of the specified Group(s) IDs.  
Default: `[]` |
| meta | `array` | Get Groups based on their meta data information.  
Default: `[]` |
| include | `array` | Ensure result set includes Groups with specific IDs.  
Default: `[]` |
| exclude | `array` | Ensure result set excludes Groups with specific IDs.  
Default: `[]` |
| group\_type | `string` | Limit results set a to certain Group type. See this [documentation page](https://codex.buddypress.org/developer/group-types/) for more information about Group Types.  
One of: The active Group types on the site. |
| enable\_forum | `boolean` | Whether the group has a forum enabled.  
Default: `false` |
| show\_hidden | `boolean` | Whether results should include hidden groups.  
Default: `false` |
| populate\_extras | `boolean` | Whether to fetch extra BP data about the returned groups.  
Default: `false` |

### Definition

`GET /buddypress/v1/groups`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups',
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

## Create a User Group

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| creator\_id | `integer` | The ID of the user who created the Group.  
Default: the logged in user ID |
| name | `string` | The name of the Group.  
**Required** |
| slug | `string` | The URL-friendly slug for the Group. |
| description | `string` | The description of the Group.  
**Required** |
| status | string | The status of the Group.  
Default: `public`  
One of : `public, private, hidden` |
| enable\_forum | `boolean` | Whether the Group has a forum or not. |
| parent\_id | `integer` | ID of the parent Group. |
| types | `array` | The Group Types. See this [documentation page](https://codex.buddypress.org/developer/group-types/) for more information about Group Types. |

### Definition

`POST /buddypress/v1/groups`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups',
  type: 'POST',
  data: {
    context: 'edit',
    creator_id: 4,
    name: 'BuddyPress Group',          // Required.
    description: 'My beautiful group', // Required.
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific User Group

Note: If you want to fetch activities posted in a specific User Group, please use the [Activity Endpoint](https://developer.buddypress.org/bp-rest-api/reference/activity/#arguments) to fetch these using the `group_id` argument set to the ID of the User Group.

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the Group. |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |
| populate\_extras | `boolean` | Whether to fetch extra BP data about the returned group.  
Default: `false` |

### Definition

`GET /buddypress/v1/groups/<group_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/51',
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

## Update a User Group

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the Group. |
| creator\_id | `integer` | The ID of the user who created the Group. |
| name | `string` | The name of the Group. |
| description | `string` | The description of the Group. |
| status | `string` | The status of the Group.  
Default: `public`  
One of : `public, private, hidden` |
| enable\_forum | `boolean` | Whether the Group has a forum or not. |
| parent\_id | `integer` | ID of the parent Group. |
| types | `string` | Assign one or more type to a group. To assign more than one type, use a comma separated list of types. See this [documentation page](https://codex.buddypress.org/developer/group-types/) for more information about Group Types. |
| append\_types | `string` | Append one or more type to a group. To append more than one type, use a comma separated list of types. See this [documentation page](https://codex.buddypress.org/developer/group-types/) for more information about Group Types. |
| remove\_types | `string` | Remove one or more type of a group. To remove more than one type, use a comma separated list of types. See this [documentation page](https://codex.buddypress.org/developer/group-types/) for more information about Group Types. |

### Definition

`PUT /buddypress/v1/groups/<group_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/51',
  type: 'PUT',
  data: {
    context: 'edit',
    name: 'My awesome Group'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Delete a User Group

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the Group. |

### Definition

`DELETE /buddypress/v1/groups/<group_id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/51',
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

## List the User Groups of the logged in member

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| max | `integer` | The maximum amount of groups the user is member of to return. Defaults to all groups. |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |

### Definition

`GET /buddypress/v1/groups/me`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/groups/me',
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