# Blog Avatar

The Blog Avatar is by default the Member Avatar of the Blog Administrator. If the `site_icon` WordPress feature is supported, then the Blog Avatar will use it.

## Schema

The schema defines all the fields that exist for a blog avatar object.

<table><tbody><tr><td><code>full</code><p></p><p>string,<br>uri</p></td><td>Full size of the image file.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>thumb</code><p></p><p>string,<br>uri</p></td><td>Thumb size of the image file.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr></tbody></table>

## Retrieve the Avatar of a Blog

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `integer` | A unique numeric ID for the Blog.  
**Required** |
| context | string | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of : `view, edit` |
| html | `boolean` | Whether to return an <img> HTML element, vs a raw URL to a group avatar.  
Default: `false` |
| alt | `string` | The custom alt attribute for the <img> element.  
Default: `''` |
| no\_user\_gravatar | `boolean` | Whether to disable the default Gravatar Admin user fallback. `true` to disable, `false` otherwise.  
Default: `false` |

### Definition

`GET /buddypress/v1/blogs/<id>/avatar`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/blogs/1/avatar',
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