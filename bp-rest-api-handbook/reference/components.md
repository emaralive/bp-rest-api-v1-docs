# Components Endpoit

BuddyPress chose a modular approach using components to organize its features. Two components are loaded by default (eg: BuddyPress Core and Community Members) while the majority are optionals. BuddyPress comes with 8 built-in optional components (Account Settings, Activity Streams, Extended Profiles, Friend connections, Notifications, Private messaging, User groups and Site Tracking).

Note: It’s important to note there can be more optional components regarding the BuddyPress plugins installed on the website : these plugins can use the BP Component API to incorpore the lists of active or inactive BuddyPress components.

## Components Schema

The schema defines all the fields that exist for BuddyPress components.

| Attribute | Type | Description |
| :--- | :--- | :--- |
| name | `string` | Name of the component. <br><br>**Context**: `view`, `edit` |
| status | `string` | Whether the component is active or inactive. <br><br>**Context**: `view`, `edit`. <br><br>**One of**: `active`, `inactive` |
| title | `string` | HTML title of the component. <br><br>**Context**: `view`, `edit` |
| description | `string` | HTML description of the component. <br><br>**Context**: `view`, `edit` |

## List the BuddyPress components

### Arguments

| Attribute | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.<br><br>**Default**: `view`<br><br>**One of**: `view`, `edit` |
| page | `integer` | Current page of the collection.<br><br>**Default**: `1` |
| per_page | `integer` | Maximum number of components to be returned in result set.<br><br>**Default**: `10` |
| search | `string` | Limit results to those matching a string. |
| status | `string` | Limit result set to components with a specific status.<br><br>**Default**: `all`<br><br>**One of**: `all`, `active`, `inactive` |
| type | `string` | Limit result set to components with a specific type.<br><br>**Default**: `all`<br><br>**One of**: `all`, `optional`, `retired`, `required` |

### Definition

`GET /buddypress/v1/components`

### Example of use

<aside class="success">
<strong>Alert</strong>: To use the `wp.apiRequest` function, you need to enqueue the `wp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.
</aside>

<aside class="notice">
<strong>Note</strong>: The code example in the righthand column are in the <strong>PHP</strong> language. 
</aside>

```javascript
wp.apiRequest( {
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

## Activate or Deactivate a BuddyPress component

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| `name` | `string` | Name of the component.  
**Required**. |
| `action` | `string` | Whether to activate or deactivate the component.  
**Required**.  
One of: `activate`, `deactivate`. |

### Definition

`PUT /buddypress/v1/components`

### Example of use

Alert: To use the `wp.apiRequest` function, you need to enqueue the `wp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
wp.apiRequest( {
  path: 'buddypress/v1/components',
  type: 'PUT',
  data: {
    context: 'edit',
    name: 'activity',
    action: 'activate'
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```
