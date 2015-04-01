---
site: https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/12164/versions/12574/portal/pages/28961/edit
apiNotebookVersion: 1.1.66
title: Watch
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
})
```

Insert a new file

```javascript
filesCreateResponse = client.files.post({
  "title" : "NotebookTestFile" ,
  "description" : "testDescription" ,
  "labels" : {
    "starred": false,
    "hidden": false,
    "trashed": false,
    "restricted": false,
    "viewed": false
   } ,
  "writersCanShare" : true})
```

```javascript
assert.equal( filesCreateResponse.status, 200 )
ID_FILE = filesCreateResponse.body.id
USER_EMAIL = filesCreateResponse.body.owners[0].emailAddress
```

Test watch channel id.

```javascript
ID_CHANNEL = "notebookTestWatchChannel"
```

The address where notifications are delivered for this channel.

```javascript
ADDRESS = prompt('Please enter address for watch channel. Example: \'https://yourdomain.com\'')
```

Start watching for changes to a file

```javascript
watchCreateResponse = client.files.fileId(ID_FILE).watch.post({
  "id" : ID_CHANNEL ,
  "type" : "web_hook" ,
  "address" : ADDRESS
})
```

```javascript
assert.equal( watchCreateResponse.status, 200 )
```

Test watch channel id.

```javascript
ID_CHANNEL = "notebookTestChannel"
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

Deleting temporary files

```javascript
client.files.fileId(ID_FILE).delete()
```