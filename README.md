# rollup-plugin-flow-entry

If you are writing a library using the [Flow type system](https://flow.org/), you might want to make your library's types available to your end users. One way to do this is to place a file with a `.js.flow` extension alongside your bundled source code. Flow knows to look inside files like this for type information.

This Rollup plugin will create one of these `.js.flow` files alongside each of your output files. The `.js.flow` file will simply `export *` from your un-bundled input file, allowing Flow to find your original type information.

## Usage

Here is an example `rollup.config.js` file using this plugin:

```js
import flowEntry from 'rollup-plugin-flow-entry'

export default {
  input: './src/index.js',
  output: { file: './lib/index.js', format: 'cjs' },
  plugins: [
    flowEntry()
    // You will also need rollup-plugin-babel or rollup-plubin-flow
    // in here to strip your type annotations...
  ]
}
```

This will produce a file called `lib/index.js.flow` alongside the normal `lib/index.js` output file. The output file will look like this:

```js
// @flow

export * from '../src/index.js'
```

This plugin doesn't take any configuration options.

If you use [rollup-plugin-multi-entry](https://github.com/rollup/rollup-plugin-multi-entry), this plugin will properly handle the multiple entry points. You must place rollup-plugin-flow-entry before rollup-plugin-multi-entry in the plugins array for this to work.
