---
site: https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/12164/versions/12574/portal/pages/13375/edit
apiNotebookVersion: 1.1.66
title: About, changes, permissionIds, app, channels
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
API.createClient('client', '/apiplatform/repository/public/organizations/30/apis/12164/versions/12574/definition');
```

```javascript
API.authenticate(client,"oauth_2_0",{
  clientId : CLIENT_ID,
  clientSecret : CLIENT_SECRET
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

Test watch channel id.

```javascript
ID_CHANNEL = "notebookTestChannel"
```

The address where notifications are delivered for this channel.

```javascript
ADDRESS = prompt('Please enter address for watch channel. Example: \'https://yourdomain.com\'')
```

Watch for all changes to a user's Drive

```javascript
watchCreateResponse = client.changes.watch.post({
  "id" : ID_CHANNEL ,
  "type" : "web_hook" ,
  "address" : ADDRESS
})
```

```javascript
assert.equal( watchCreateResponse.status, 200 )
ID_RESOURCE = watchCreateResponse.body.resourceId
```

Stop watching for changes to a resource.
If successful, this method returns an empty response body.

```javascript
channelsStopResponse = client.channels.stop.post({
  "id" : ID_CHANNEL ,
  "resourceId" : ID_RESOURCE
})
```

```javascript
assert.equal( channelsStopResponse.status, 204 )
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