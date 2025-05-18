# Reference

Just like the WordPress REST API, the BP REST API is organized around [REST](http://en.wikipedia.org/wiki/Representational_state_transfer), and is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. The API uses built-in HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and supports cross-origin resource sharing to allow you to interact securely with the API from a client-side web application.

The BP REST API uses JSON exclusively as the request and response format, including error responses.

The BP REST API provides public data accessible to any client anonymously, as well as private data only available after [authentication](https://developer.buddypress.org/bp-rest-api/#about-authentification). Once authenticated the BP REST API supports most BuddyPress community actions, allowing you to enhance your plugins with more responsive management tools, or build complex single-page applications.

This API reference provides information on the specific endpoints available through the API, their parameters, and their response data format.

## Developer Endpoint Reference

| Resource | Base Route |
| --- | --- |
| [Components](https://developer.buddypress.org/bp-rest-api/reference/components/) | `/buddypress/v1/components` |
| [Members](https://developer.buddypress.org/bp-rest-api/reference/members/) | `/buddypress/v1/members` |
| [Activity](https://developer.buddypress.org/bp-rest-api/reference/activity/) | `/buddypress/v1/activity` |
| [Extended Profiles](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/): |  | 
| – [Profile Group](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-group/) | `/buddypress/v1/xprofile/groups` | 
| – [Profile Field](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-field/) | `/buddypress/v1/xprofile/fields` |  
| – [Profile Data](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-data/) | `/buddypress/v1/xprofile/<field_id>/data/<user_id>` |   
| [User Groups](https://developer.buddypress.org/bp-rest-api/reference/user-groups/): |  | 
| – [Groups](https://developer.buddypress.org/bp-rest-api/reference/user-groups/groups/) | `/buddypress/v1/groups` | 
| – [Group Membership](https://developer.buddypress.org/bp-rest-api/reference/user-groups/group-membership/) | `/buddypress/v1/groups/<group_id>/members` |  
| – [Group Membership Requests](https://developer.buddypress.org/bp-rest-api/reference/user-groups/group-membership-requests/) | `/buddypress/v1/groups/<group_id>/membership-request` |  
| – [Group Invites](https://developer.buddypress.org/bp-rest-api/reference/user-groups/group-invites/) | `/buddypress/v1/groups/<group_id>/invites` |   
| [Private Messaging](https://developer.buddypress.org/bp-rest-api/reference/private-messaging/):  
– [Sitewide Notices](https://developer.buddypress.org/bp-rest-api/reference/private-messaging/sitewide-notices/) | `/buddypress/v1/messages`  
`/buddypress/v1/sitewide-notices` |
| [Screen Notifications](https://developer.buddypress.org/bp-rest-api/reference/screen-notifications/) | `/buddypress/v1/notifications` |
| [Attachments](https://developer.buddypress.org/bp-rest-api/reference/attachments/)  
– [Member Avatar](https://developer.buddypress.org/bp-rest-api/reference/attachments/member-avatar/)  
– [Member Cover Image](https://developer.buddypress.org/bp-rest-api/reference/attachments/member-cover-image/)  
– [Group Avatar](https://developer.buddypress.org/bp-rest-api/reference/attachments/group-avatar/)  
– [Group Cover Image](https://developer.buddypress.org/bp-rest-api/reference/attachments/group-cover-image/)  
– [Blog Avatar](https://developer.buddypress.org/bp-rest-api/reference/attachments/blog-avatar/) | `/buddypress/v1/members/<user_id>/avatar`  
`/buddypress/v1/members/<user_id>/cover`  
`/buddypress/v1/groups/<group_id>/avatar`  
`/buddypress/v1/groups/<group_id>/cover`  
`/buddypress/v1/blogs/<id>/avatar` |
| [User Blogs](https://developer.buddypress.org/bp-rest-api/reference/blogs/) | `/buddypress/v1/blogs` |
| [User Signups](https://developer.buddypress.org/bp-rest-api/reference/signup/) | `/buddypress/v1/signup` |
| [Friend Connections](https://developer.buddypress.org/bp-rest-api/reference/friends/) | `/buddypress/v1/friends` |
