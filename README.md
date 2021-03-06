# Workspace ONE Access User and Groups APIs Provisioned-Users
> Author(s): Jiaqi Gao (jiaqig@vmware.com)
>
> Date Created: Jul 7th, 2022

*The following SCIM1.1 APIs have been made available to select IdP partners and customers for local user management of users provisioned by the third-party IdP.*

## Create a provisioned user in other directory 
It allows to create the provisioned users in the other directory when InternalUserType is specified as PROVISIONED and domain is specified, which is used to infer the directory.

The required attributes are: userName, name.givenName, name.familyName, emails (containing one and only one email address), internalUserType, domain and externalId. 

```
POST /SAAS/jersey/manager/api/scim/Users
Host: sva.eng.vmware.com
Accept: application/json
Authorization: Bearer h480djs93hd8
```

```
{
"schemas": [
"urn:scim:schemas:core:1.0",
"urn:scim:schemas:extension:workspace:1.0" 
],
"userName": "cuser1",
"name": {
"givenName": "firstName",
"familyName": "lastName"
},
"displayName": "firstName lastName",
"emails": [
{
  "value": "cuser1@domain.com"
}
],
"externalId":"422e2e25-6904-4443-b979-7c5c46c63175",
"urn:scim:schemas:extension:workspace:1.0": {
"internalUserType": "PROVISIONED",
"domain": "domain.com"
}
}
```
```
HTTP/1.1 201 Created
Content-Type: application/json
Location: https://sva.eng.vmware.com/SAAS/jersey/manager/api/scim/Users/91cfcac4-cca9-4509-bce6-febc0e3b1d7c
ETag: W/"f250dd84f0671c3"

{
"schemas": [
"urn:scim:schemas:extension:workspace:1.0",
"urn:scim:schemas:core:1.0",
"urn:scim:schemas:extension:enterprise:1.0"
],
"id": "91cfcac4-cca9-4509-bce6-febc0e3b1d7c",
"meta": {
"created": "2014-11-20T05:54:34.895Z",
"lastModified": "2014-11-20T05:54:35.089Z",
"location": "https://sva.eng.vmware.com/SAAS/jersey/manager/api/scim/Users/91cfcac4-cca9-4509-bce6-febc0e3b1d7c"
"version":"W\/\"f250dd84f0671c3\""
},
"userName": "cuser1",
"name": {
"givenName": "firstName",
"familyName": "lastName"
},
"displayName": "firstName lastName",
"emails": [
{
  "value": "cuser1@domain.com"
}
],
"groups": [],
"active": true,
"roles": [
{
  "value": "c071da06-84c0-46d3-944b-dd8853cec3fc",
  "display": "User"
}
],
"externalId":"422e2e25-6904-4443-b979-7c5c46c63175",
"urn:scim:schemas:extension:workspace:1.0": {
"userStatus": "1",
"internalUserType": "PROVISIONED",
"domain": "domain.com"
}
}
```

## Find Users: UserResource By externalId
```
GET /SAAS/jersey/manager/api/scim/Users?filter=externalId%20eq%20%223273e0f7-1756-440b-a90b-fa0056a10fa0%22
Host: sva.eng.vmware.com
Authorization: Bearer h480djs93hd8
```

## Delete User Resource 
Delete will currently operate on any user, synchronized or not. It takes only the id as a parameter and does not discriminate based on the user's userStore value.
```
DELETE /SAAS/jersey/manager/api/scim/Users/d24afa39-05a1-433f-8aa9-ad41c9a3d394
Host: sva.eng.vmware.com
Authorization: Bearer h480djs93hd8
```
