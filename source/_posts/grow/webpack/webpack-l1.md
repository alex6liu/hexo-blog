---
title: webpack l1
date: 2019-05-16 14:59:17
tags: [webpack, l1]
---

[webpack](https://webpack.js.org/concepts)

## Basic features & functionality

### Core concepts (entry, output, loaders, plugins)

At its core, webpack is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph which maps every module your project needs and generates one or more bundles.

#### Entry
An entry point indicates which module webpack should use to begin building out its internal dependency graph. webpack will figure out which other modules and libraries that entry point depends on (directly and indirectly).

By default its value is `./src/index.js`, but you can specify a different (or multiple entry points) by configuring the entry property in the webpack configuration. For example:

webpack.config.js

```js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

#### Output

The output property tells webpack where to emit the bundles it creates and how to name these files. It defaults to `./dist/main.js` for the main output file and to the ./dist folder for any other generated file.

You can configure this part of the process by specifying an output field in your configuration:

webpack.config.js

```js
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

In the example above, we use the `output.filename` and the `output.path` properties to tell webpack the name of our bundle and where we want it to be emitted to. In case you're wondering about the path module being imported at the top, it is a core Node.js module that gets used to manipulate file paths.

#### Loaders

Out of the box, webpack only understands JavaScript and JSON files. Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application and added to the dependency graph.

At a high level, loaders have two properties in your webpack configuration:

- The test property identifies which file or files should be transformed.
- The use property indicates which loader should be used to do the transforming.

webpack.config.js

```js
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};
```

The configuration above has defined a rules property for a single module with two required properties: `test` and `use`.

#### Plugins

While loaders are used to transform certain types of modules, plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

In order to use a plugin, you need to `require()` it and add it to the `plugins` array. Most plugins are customizable through options. Since you can use a plugin multiple times in a config for different purposes, you need to create an instance of it by calling it with the `new` operator.

webpack.config.js

```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

In the example above, the `html-webpack-plugin` generates an HTML file for your application by injecting automatically all your generated bundles.

#### Mode

By setting the `mode` parameter to either `development`, `production` or `none`, you can enable webpack's built-in optimizations that correspond to each environment. The default value is `production`.

```js
module.exports = {
  mode: 'production'
};
```

### Entry points (single entry, syntax & etc.)

#### Single Entry (Shorthand) Syntax

Usage: `entry: string|Array<string>`

webpack.config.js

```js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

The single entry syntax for the entry property is a shorthand for:

webpack.config.js

```js
module.exports = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};
```

#### Object Syntax

Usage: `entry: {[entryChunkName: string]: string|Array<string>}`

webpack.config.js

```js
module.exports = {
  entry: {
    app: './src/app.js',
    adminApp: './src/adminApp.js'
  }
};
```

### Output

webpack.config.js

```js
module.exports = {
  output: {
    filename: 'bundle.js',
  }
};
```

This configuration would output a single `bundle.js` file into the `dist` directory.

#### Multiple Entry Points

If your configuration creates more than a single "chunk" (as with multiple entry points or when using plugins like CommonsChunkPlugin), you should use substitutions to ensure that each file has a unique name.

```js
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
};
```

## Support and extend solution

### Loaders (using, config, features & etc.)

#### Using Loaders

There are three ways to use loaders in your application:

- Configuration (recommended): Specify them in your `webpack.config.js` file.
- Inline: Specify them explicitly in each `import` statement.
- CLI: Specify them within a shell command.

#### Configuration

`module.rules` allows you to specify several loaders within your webpack configuration. This is a concise way to display loaders, and helps to maintain clean code. It also offers you a full overview of each respective loader.

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          // style-loader
          { loader: 'style-loader' },
          // css-loader
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          },
          // sass-loader
          { loader: 'sass-loader' }
        ]
      }
    ]
  }
};
```

#### Loader Features

- Loaders can be chained. Each loader in the chain applies transformations to the processed resource. A chain is executed in reverse order. The first loader passes its result (resource with applied transformations) to the next one, and so forth. Finally, webpack expects JavaScript to be returned by the last loader in the chain.
- Loaders can be synchronous or asynchronous.
- Loaders run in Node.js and can do everything that’s possible there.
- Loaders can be configured with an options object (using query parameters to set options is still supported but has been deprecated).
- Normal modules can export a loader in addition to the normal main via package.json with the loader field.
- Plugins can give loaders more features.
- Loaders can emit additional arbitrary files.

Loaders allow more power in the JavaScript ecosystem through preprocessing functions (loaders). Users now have more flexibility to include fine-grained logic such as compression, packaging, language translations and more.

### Plugins (config, usage & etc.)

#### Usage

Since plugins can take arguments/options, you must pass a `new` instance to the `plugins` property in your webpack configuration.

Depending on how you are using webpack, there are multiple ways to use plugins.

#### Configuration

webpack.config.js

```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

### Configuration

#### Simple Configuration

webpack.config.js

```js
var path = require('path');

module.exports = {
  mode: 'development',
  entry: './foo.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'foo.bundle.js'
  }
};
```

### Modules

#### What is a webpack Module

In contrast to Node.js modules, webpack modules can express their dependencies in a variety of ways. A few examples are:

- An ES2015 `import` statement
- A CommonJS `require()` statement
- An AMD `define` and requ`ire statement
- An `@import` statement inside of a css/sass/less file.
- An image url in a stylesheet (`url(...)`) or html (`<img src=...>`) file.

## Advanced features
### Module Resolution (resolving rules, paths)

**Resolving rules in webpack**
Using enhanced-resolve, webpack can resolve three kinds of file paths:

#### Absolute paths

```js
import '/home/me/file';

import 'C:\\Users\\me\\file';
```

Since we already have the absolute path to the file, no further resolution is required.

#### Relative paths

```js
import '../src/file1';
import './file2';
```

In this case, the directory of the resource file where the `import` or `require` occurs is taken to be the context directory. The relative path specified in the `import/require` is joined to this context path to produce the absolute path to the module.

#### Module paths

```js
import 'module';
import 'module/lib/file';
```

Modules are searched for inside all directories specified in `resolve.modules`. You can replace the original module path by an alternate path by creating an alias for it using `resolve.alias` configuration option.

Once the path is resolved based on the above rule, the resolver checks to see if the path points to a file or a directory. If the path points to a file:

- If the path has a file extension, then the file is bundled straightaway.
- Otherwise, the file extension is resolved using the resolve.extensions option, which tells the resolver which extensions (eg - .js, .jsx) are acceptable for resolution.

If the path points to a folder, then the following steps are taken to find the right file with the right extension:

- If the folder contains a package.json file, then fields specified in resolve.mainFields configuration option are looked up in order, and the first such field in package.json determines the file path.
- If there is no package.json or if the main fields do not return a valid path, file names specified in the resolve.mainFiles configuration option are looked for in order, to see if a matching filename exists in the imported/required directory .
- The file extension is then resolved in a similar way using the resolve.extensions option.

### Dependency graph
### Targets
### Hot module replacement