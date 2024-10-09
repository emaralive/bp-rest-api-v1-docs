# User Groups

The Groups component allow your users to organize themselves into specific public, private or hidden sections of your community site with separate activity streams and member listings.

4 endpoints are available to let you manage groups, manage group members, manage memberships requests and group invites.

Note: The User Groups component is an optional one. This means the following endpoints will only be available if the component is active on the community site.

### User Groups Endpoints

| Resource | Base Route |
| --- | --- |
| [Groups](https://developer.buddypress.org/bp-rest-api/reference/user-groups/groups/) | `/buddypress/v1/groups` |
| [Group Membership](https://developer.buddypress.org/bp-rest-api/reference/user-groups/group-membership/) | `/buddypress/v1/groups/<group_id>/members` |
| [Group Membership Requests](https://developer.buddypress.org/bp-rest-api/reference/user-groups/group-membership-requests/) | `/buddypress/v1/groups/<group_id>/membership-request` |
| [Group invites](https://developer.buddypress.org/bp-rest-api/reference/user-groups/group-invites/) | `/buddypress/v1/groups/<group_id>/invites` |