# Koa RBAC

Role-Based Access Control for [Koa](https://github.com/koajs/koa)


## Install

```
npm install koa-rbac --save
```


## Usage

```javascript
var rbac = require('koa-rbac');
var koa = require('koa');
var app = koa();


rbac.addRoles({
  'guest': [],
  'reader': ['read'],
  'writer': ['write'],
});

// parent -> child
rbac.setRoleRelationship('reader', 'guest');
rbac.setRoleRelationship('writer', 'reader');


app.use(rbac.middleware({
  loadUserAccess: loadUserAccess
}));

app.use(rbac.allow('read'));

app.use(function * (next) {
  this.body = "Allowed reading!";
});


function * loadUserAccess() {
  return ['guest', 'reader'];
}
```


## Contribution

All contributions welcome! Every PR **must** be accompanied by their associated
unit tests!


## License

The MIT License (MIT)

Copyright (c) 2014 Mind2Soft <yanick.rochon@mind2soft.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.