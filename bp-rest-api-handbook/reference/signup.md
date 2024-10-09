# User Signups

The BuddyPress Signups endpoint helps you manage member registrations of your community site.

Note: User registrations must be enabled on your community site to be able to use the following endpoints.

## Schema

The schema defines all the fields that exist for a signup object.

<table><tbody><tr><td><code>id</code><p></p><p>integer</p></td><td>Unique numeric identifier for the signup.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>user_login</code><p></p><p>string</p></td><td>The login of the new user.<br><strong>Required</strong><br>Context:&nbsp;<code>view</code>, <code>edit</code></td></tr><tr><td><code>user_email</code><p></p><p>string</p></td><td>The email of the new member.<br><strong>Required</strong><br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>registered</code><p></p><p>string or null</p></td><td>The registration date for the new member, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>registered_gmt</code><p></p><p>string or null</p></td><td>The registration date for the new member, as GMT.<br>Read only<br>Context:&nbsp;<code>view</code>,&nbsp;<code>edit</code></td></tr><tr><td><code>date_sent</code><p></p><p>string or null</p></td><td>The date the activation email was sent to the pending member, in the site’s timezone.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>date_sent_gmt</code><p></p><p>string or null</p></td><td>The date the activation email was sent to the pending member, as GMT.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>count_sent</code><p></p><p>integer</p></td><td>The number of times the activation email was sent to the pending member.<br>Read only<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>meta</code><p></p><p>object</p></td><td>The signup meta information. BuddyPress uses it to store the password hash of the new member. This password hash is never included into the BP REST API responses.<br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>site_name</code> <em>(1)</em><p></p><p>string</p></td><td>Unique name (slug) of the new member’s child site.<br>Default: <code>''</code><br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>site_title</code> <em>(1)</em><p></p><p>string</p></td><td>Title of the new member’s child site.<br>Default: <code>''</code><br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>site_public</code> <em>(1)</em><p></p><p>boolean</p></td><td>Search engine visibility of the new member’s site. <code>true</code> to be visible, <code>false</code> otherwise.<br>Default: <code>true</code><br>Context:&nbsp;<code>edit</code></td></tr><tr><td><code>site_language</code> <em>(1)</em><p></p><p>string</p></td><td>Language to use for the new member’s site.<br>Default: the Network main site’s locale (eg: <code>en_US</code>)<br>One of: the available locales of the Network.<br>Context:&nbsp;<code>edit</code></td></tr></tbody></table>

*(1) Only available on WordPress Multisite configurations where it is possible to signup with a blog.*

## List Signups

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view`, `edit` |
| number | `integer` | Total number of signups to return.  
Default: `1` |
| offset | `integer` | Offset the result set by a specific number of items.  
Default: `1` |
| include | `array` | Ensure the result set includes specific Signup IDs.  
Default: `[]` |
| user\_login | `string` | Ensure the result set only returns the signup for a specific pending member login.  
Default: `''` |
| orderby | `string` | Order the result set according to a specific parameter.  
Default: `signup_id`  
One of: `signup_id`, `login`, `email`, `registered`, `activated` |
| order | `array` | Order sort type (ascending or descending).  
Default: `desc`  
One of: `asc`, `desc` |

### Definition

`GET /buddypress/v1/signup`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/signup',
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

## Signup a user (with or without a blog)

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| user\_login | `string` | A numeric identifier for the new member.  
**Required** |
| password | `string` | Password for the new member.  
**Required** |
| user\_email | `string` | The email address for the new member.  
**Required** |
| `signup_field_data` *(1)* | `array` | The XProfile field data for the new user. |
| site\_name *(2)* | `string` | Unique name (slug) of the new member’s child site.  
Default: `''` |
| site\_title *(2)* | `string` | Title of the new member’s child site.  
Default: `''` |
| site\_public *(2)* | `boolean` | Search engine visibility of the new member’s site. `true` to be visible, `false` otherwise.  
Default: `true` |
| site\_language *(2)* | `string` | Language to use for the new member’s site.  
Default: the Network main site’s locale (eg: `en_US`) |

*(1) Only available if the BuddyPress xProfile component is active.  
(2) Only available on WordPress Multisite configurations where it is possible to signup with a blog.*

### Definition

`POST /buddypress/v1/signup`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
// Example for a simple signup when the BP xProfile component is active.
bp.apiRequest( {
  path: 'buddypress/v1/signup',
  type: 'POST',
  data: {
    context: 'edit',
    user_login: 'testuser',
    user_email: 'test@user.mail',
    password: 'password' // Always use strong passwords, not like this one!
    "signup_field_data[0][field_id]": "36",
    "signup_field_data[0][value]": "Arabic, English",
    "signup_field_data[1][field_id]": "31",
    "signup_field_data[1][value]": "Sometimes, I never travel",
    "signup_field_data[2][field_id]": "35",
    "signup_field_data[2][value]": "This is some text for my profile.",
    "signup_field_data[3][field_id]": "1",
    "signup_field_data[3][value]": "New Profile",
    "signup_field_data[4][field_id]": "19",
    "signup_field_data[4][value]": "Option 01, Option 03",
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Retrieve a specific Signup

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `string` | Unique identifier for the signup. It can be a signup ID, an email address, or most likely an activation key.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `view`  
One of: `view, edit` |

### Definition

`GET /buddypress/v1/signup/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/signup/1f56ce56bf66ef53', // Activation key.
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

## Activate a specific Signup

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| activation\_key | `string` | Activation key of the signup.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of: `view, edit` |

### Definition

`PUT /buddypress/v1/signup/activate/<activation_key>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/signup/activate/1f56ce56bf66ef53',
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

## Delete a specific Signup

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| id | `string` | Unique identifier for the signup. It can be a signup ID, an email address, or most likely an activation key.  
**Required** |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of: `view, edit` |

### Definition

`DELETE /buddypress/v1/signup/<id>`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/signup/1f56ce56bf66ef53', // Activation key.
  type: 'DELETE',
  data: {
    context: 'edit',
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```

## Resend signup activation email

### Arguments

| Name | Type | Description |
| --- | --- | --- |
| context | `string` | Scope under which the request is made; determines fields present in response.  
Default: `edit`  
One of: `edit` |
| id | `string` | Unique identifier for the signup. It can be a signup ID, an email address, or an activation key.  
**Required** |

### Definition

`POST /buddypress/v1/signup/resend/`

### Example of use

Alert: To use the `bp.apiRequest` function, you need to enqueue the `bp-api-request` JavaScript or use it as a dependency of your script. Refer to [this page](https://developer.wordpress.org/plugins/javascript/enqueuing/) to know more about loading JavaScript files in WordPress.

```javascript
bp.apiRequest( {
  path: 'buddypress/v1/signup/resend/',
  type: 'POST',
  data: {
    context: 'edit',
    id: '1f56ce56bf66ef53',
  }
} ).done( function( data ) {
  return data;
} ).fail( function( error ) {
  return error;
} );
```