# User Blogs

The Site Tracking components comes, on WordPress Multisite configurations, with a directory page listing all public user Blogs of your network of sites. Thanks to the BP Blogs REST Endpoint, you can fetch these public blogs into your Application.

Note: The User Blogs component is an optional one. This means the User Blogs endpoint will only be available if the component is active on the community site.

## Schema

The schema defines all the fields that exist for a Blog object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>Unique identifier for the Blog.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>user_id</code><p></p><p>integer</p></td><td>A unique numeric ID for the Blog’s administrator.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>name</code><p></p><p>string</p></td><td>The Blog’s name.<br>Read only<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>permalink</code><p></p><p>string,<br>uri</p></td><td>The Blog’s permalink.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>description</code><p></p><p>string</p></td><td>The Blog’s description.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>path</code><p></p><p>string</p></td><td>The Blog’s relative path to the network’s domain (when Multisite is using sub-directories for blogs)<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>domain</code><p></p><p>string</p></td><td>The Blog’s domain (or the network’s domain when Multisite is using sub-directories for blogs).<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>last_activity</code><p></p><p>string or null</p></td><td>The last activity date from the Blog, in the network’s timezone.<br>Read only<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>last_activity_gmt</code><p></p><p>string or null</p></td><td>The last activity date from the Blog, as GMT.<br>Read only<br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>avatar_urls</code> <em>(1)</em><p></p><p>object</p></td><td>Avatar URLs for the Blog (Full &amp; Thumb sizes). It uses the WordPress site icon feature if supported, and falls back on the Administrator’s avatars.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

*(1) Only if the WordPress discussion settings allow avatars.*

## List Blogs

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view`, `edit` |
| page | `integer` | Current page of the collection.  
Default: `1` |
| per\_page | `integer` | Maximum number of members to be returned in result set.  
Default: `10` |
| search | string | Limit results to site titles, domains, descriptions matching the searched terms. |
| user\_id | `integer` | The unique numeric identifier of the user having publishing capabilities on the Blog. |
| include | `array` | Ensure result set include specific Blog IDs.  
Default: `[]` |
| type | `string` | Shorthand for certain orderby/order combinations.  
Default: `active`  
One of: `active, newest, alphabetical, random` |

### Definition

`GET /buddypress/v1/blogs`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/blogs',
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

## Create a Blog

Note: This route requires the Blogs signup option to be active into the WordPress Network Administration settings.

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| name | `string` | The new site’s name (used for the site URL).  
**Required** |
| title | `string` | The new site’s title.  
**Required** |
| site\_id | `integer` | The new site’s network ID. (Only relevant on multi-network installations).  
Default: `1` |
| user\_id | `integer` | The user ID of the new site’s admin.  
Default: the logged in user ID. |
| meta | `array` | Set initial Blog options.  
Default: `[]` |

### Definition

`POST /buddypress/v1/blogs`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/blogs',
  type: 'POST',
  data: {
    context: 'edit',
    name: 'buddypress',
    title: 'BuddyPress',
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific Blog

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | Unique identifier for the Blog. |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, edit` |

### Definition

`GET /buddypress/v1/blogs/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/blogs/2',
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