# Components Endpoint

BuddyPress chose a modular approach using components to organize its features. Two components are loaded by default (eg: BuddyPress Core and Community Members) while the majority are optionals. BuddyPress comes with 8 built-in optional components (Account Settings, Activity Streams, Extended Profiles, Friend connections, Notifications, Private messaging, User groups and Site Tracking).

<aside class="warning">
<strong>Note</strong>: It’s important to note there can be more optional components regarding the BuddyPress plugins installed on the website : these plugins can use the BP Component API to incorpore the lists of active or inactive BuddyPress components.
</aside>

## Components Schema

The schema defines all the fields that exist for BuddyPress components.

| Attribute | Type | Description |
| :--- | :--- | :--- |
| name | `string` | Name of the component. <br><br>**Context**: `view`, `edit` |
| status | `string` | Whether the component is active or inactive. <br><br>**Context**: `view`, `edit`. <br><br>**One of**: `active`, `inactive` |
| title | `string` | HTML title of the component. <br><br>**Context**: `view`, `edit` |
| description | `string` | HTML description of the component. <br><br>**Context**: `view`, `edit` |

## List the BuddyPress components

### Arguments - List Components

| Attribute | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.<br><br>**Default**: `view`<br><br>**One of**: `view`, `edit` |
| page | `integer` | Current page of the collection.<br><br>**Default**: `1` |
| per_page | `integer` | Maximum number of components to be returned in result set.<br><br>**Default**: `10` |
| search | `string` | Limit results to those matching a string. |
| status | `string` | Limit result set to components with a specific status.<br><br>**Default**: `all`<br><br>**One of**: `all`, `active`, `inactive` |
| type | `string` | Limit result set to components with a specific type.<br><br>**Default**: `all`<br><br>**One of**: `all`, `optional`, `retired`, `required` |

### Definition - List Components

`GET /buddypress/v1/components`

### Example - List Components

<aside class="success">
<strong>Alert</strong>: To use the <code>wp.apiRequest</code> function, you need to enqueue the <code>wp-api-request</code> JavaScript or use it as a dependency of your script. Refer to <a href="https://developer.wordpress.org/plugins/javascript/enqueuing/">this page</a> to know more about loading JavaScript files in WordPress.
</aside>

<aside class="notice">
<strong>Note</strong>: Click a language tab at the top of the righthand column to view a code example for that language. 
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

## Activate/Deactivate a BuddyPress Component

### Arguments - Activate/Deactivate Component

| Name | Type | Description |
| --- | --- | --- |
| name | `string` | Name of the component.<br><br>**Required**. |
| action | `string` | Whether to activate or deactivate the component.<br><br>**Required**<br><br>**One of**: `activate`, `deactivate` |

### Definition - Activate/Deactivate Component

`PUT /buddypress/v1/components`

### Example - Activate/Deactivate Component

<aside class="success">
<strong>Alert</strong>: To use the <code>wp.apiRequest</code> function, you need to enqueue the <code>wp-api-request</code> JavaScript or use it as a dependency of your script. Refer to <a href="https://developer.wordpress.org/plugins/javascript/enqueuing/">this page</a> to know more about loading JavaScript files in WordPress.
</aside>

<aside class="notice">
<strong>Note</strong>: Click a language tab at the top of the righthand column to view a code example for that language. 
</aside>

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
