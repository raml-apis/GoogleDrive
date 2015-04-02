---
site: https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/12164/versions/12574/portal/pages/28943/edit
apiNotebookVersion: 1.1.66
title: About, changes, permissionIds, app
---

```javascript
load('https://github.com/chaijs/chai/releases/download/1.9.0/chai.js')
```

See http://chaijs.com/guide/styles/ for assertion styles

```javascript
assert = chai.assert
```

```javascript
CLIENT_ID = prompt("Please, enter Client ID of your Google application.")
CLIENT_SECRET = prompt("Please, enter Client Secret of your Google application.")
```

```javascript
API.createClient('client', '#REF_TAG_DEFENITION');
```

```javascript
API.authenticate(client,"oauth_2_0",{
  clientId : CLIENT_ID,
  clientSecret : CLIENT_SECRET
  scopes: [ "https://www.googleapis.com/auth/drive", "https://www.googleapis.com/auth/drive.apps.readonly" ]
})
```

Gets the information about the current user along with Drive API settings

```javascript
aboutResponse = client.about.get()
```

```javascript
assert.equal( aboutResponse.status, 200 )
USER_EMAIL = aboutResponse.body.user.emailAddress
```

Lists the changes for a user

```javascript
changesResponse = client.changes.get()
```

```javascript
assert.equal( changesResponse.status, 200 )
ID_CHANGE = changesResponse.body.items[0].id
```

Gets a specific change

```javascript
changeResponse = client.changes.changeId(ID_CHANGE).get()
```

```javascript
assert.equal( changeResponse.status, 200 )
```

Returns the permission ID for an email address

```javascript
permissionIdsEmailResponse = client.permissionIds.email(USER_EMAIL).get()
```

```javascript
assert.equal( permissionIdsEmailResponse.status, 200 )
```

Lists a user's installed apps

```javascript
appsResponse = client.apps.get()
```

```javascript
assert.equal( appsResponse.status, 200 )
ID_APP = appsResponse.body.items[0].id
```

Gets a specific app

```javascript
appResponse = client.apps.appId(ID_APP).get()
```

```javascript
assert.equal( appResponse.status, 200 )
```