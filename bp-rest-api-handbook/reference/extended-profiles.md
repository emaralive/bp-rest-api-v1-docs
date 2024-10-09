# Extended Profiles

The Extended Profiles allow Administrator to highlight the best of their community **members** by creating an unlimited number of custom Profile Fields and/or groups of custom Profile Fields.

To reflect the data structure of Extended Profiles, 3 endpoints are available to respectively manipulate Group of profile fields, Profile fields and user Data for these profile fields.

Note: The Extended Profiles component is an optional one. This means the following endpoints will only be available if the component is active on the community site.

## Extended Profiles Endpoints

| Resource | Base Route |
| --- | --- |
| [Profile Group](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-group/) | /buddypress/v1/xprofile/groups |
| [Profile Field](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-field/) | /buddypress/v1/xprofile/fields |
| [Profile Data](https://developer.buddypress.org/bp-rest-api/reference/extended-profiles/profile-data/) | /buddypress/v1/xprofile/<field\_id>/data/<user\_id> |