# strict-transport-security

Node.js middleware to add Strict-Transport-Security header according to http://tools.ietf.org/html/rfc6797

## Install
```
$ npm install strict-transport-security --save
```
## Tests
```
$ npm install --dev
$ npm test
```
## Usage
```js
const sts = require('strict-transport-security');
const express = require('express');
const app = express();

const globalSTS = sts.getSTS({'max-age':{'days': 30}});
const localSTS = sts.getSTS({'max-age':{'days': 10}, 'includeSubDomains': true});

// This will apply this policy to all requests
app.use(globalSTS);

app.get('/', (req, res) => {
  res.send('Using global strict transport security policy!');
});

// This will apply the local policy just to this path, overriding the globla policy
app.get('/local', localSTS, (req, res) => {
  res.send('Using path local strict transport security policy!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```
