# configstore-plain

> Easily load and persist config without having to think about where and how

Fork of https://github.com/yeoman/configstore to add new plain key methods (see https://github.com/yeoman/configstore/issues/39)

Config is stored in a JSON file located in `$XDG_CONFIG_HOME` or `~/.config`.<br>
Example: `~/.config/configstore/some-id.json`

See options below to modify storage location.


## Usage

```js
const Configstore = require('configstore');
const pkg = require('./package.json');

// Init a Configstore instance with an unique ID e.g.
// package name and optionally some default values
const conf = new Configstore(pkg.name, {foo: 'bar'});

conf.set('awesome', true);

console.log(conf.get('awesome'));
//=> true

console.log(conf.get('foo'));
//=> bar

// use dot notation to access nested properties (provided by `dot-prop` module)
conf.set('bar.baz', true);

console.log(conf.get('bar'));
//=> { baz: true }

console.log(conf.all);
//=> { foo: 'bar', awesome: true, bar: { baz: true } }

conf.del('awesome');

console.log(conf.get('awesome'));
//=> undefined
```


## API

### Configstore(packageName, [defaults], [options])

Create a new Configstore instance `config`.

#### packageName

Type: `string`

Name of your package.

#### defaults

Type: `object`

Default content to init the config store with.

#### options

Type: `object`

##### globalConfigPath

Type: `boolean`<br>
Default: `false`

Store the config at `$CONFIG/package-name/config.json` instead of the default `$CONFIG/configstore/package-name.json`. This is not recommended as you might end up conflicting with other tools, rendering the "without having to think" idea moot.

##### configFile

Type: `string`<br>

Store the config file at the absolute location instead of the default (see above). Useful if (a) you want full control, (b) if you're using it for storing data other than 'config' data, or (c) to keep things together for a 'portable' installation.

### config.set(key, value)

Set an item.

### config.setPlain(key, value)

Set an item (does not turn periods in key into nested object properties).

### config.set(object)

Set multiple items at once.

### config.get(key)

Get an item.

### config.getPlain(key, value)

Get an item (does not turn periods in key into nested object properties).

### config.del(key)

Delete an item.

### config.clear()

Delete all items.

### config.all

Get all items as an object or replace the current config with an object:

```js
conf.all = {
	hello: 'world'
};
```

### config.size

Get the item count.

### config.path

Get the path to the config file. Can be used to show the user where the config file is located or even better open it for them.


## License

[BSD license](http://opensource.org/licenses/bsd-license.php)<br>
Copyright Google
