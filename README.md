# egg-mongoose-multiple

fork from [egg-mongoose](https://github.com/eggjs/egg-mongoose),but it`s different in two points like 
this:

* add the  support for mulitple mongodb sources. 

* becase i haven`t commite this plug to npm center,you should use it by real file path.

## Usage

```js
// {app_root}/config/plugin.js
exports.mongoose = {
  enable: true,
  //package: 'egg-mongoose',
  path:"/Users/cly/Desktop/nodeProject/egg-mongoose-multiple",
};
```


## Multi-mongos support

```js
// {app_root}/config/config.default.js
exports.mongoose = {
  url: [{dbA:"mongodb://urlA"},
  		{dbB:"mongodb://urlB},
  		...],
  options: {}
};
```

## Example
connection dbA

```js
// app/model/userA.js
module.exports = app => {
  const mongoose = app.mongoose.dbA;
  const Schema = mongoose.Schema
  const UserSchema = Schema({
    userName: { type: String  },
    password: { type: String  }
  });

  return mongoose.model('User', UserSchema);
}
// app/controller/userA.js
exports.index = function* (ctx) {
  ctx.body = yield ctx.model.UserA.find({});  // you should use upper case to access mongoose model
}

```
connection dbB

```
// app/model/userB.js
module.exports = app => {
  const mongoose = app.mongoose.dbB;
  const Schema = mongoose.Schema
  const UserSchema = Schema({
    userName: { type: String  },
    password: { type: String  }
  });

  return mongoose.model('User', UserSchema);
}

// app/controller/userB.js
exports.index = function* (ctx) {
  ctx.body = yield ctx.model.UserB.find({});  // you should use upper case to access mongoose model
}

```

## License

[MIT](LICENSE)
