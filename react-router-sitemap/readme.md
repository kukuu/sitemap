# React Router Sitemap



Module for generating sitemaps using [React Router](https://www.npmjs.com/package/react-router) configuration. Also it can filter paths and replace params (like a `:paramName`) in dynamic paths.

## Install

`npm i --save react-router-sitemap`

## Usage

You need to have a module with the router configuration. For example:

`router.jsx`
```js
import React from 'react';
import { Route } from 'react-router';

export default (
	<Route>
		<Route path='/' />
		<Route path='/about' />
		<Route path='/projects' />
		<Route path='/contacts' />
		<Route path='/auth' />
	</Route>
);
```
If you are using v4 `react-router`, your `router.jsx` might be:
```js
import React from 'react';
import { Switch, Route } from 'react-router';

export default (
	// Switch is added in v4 react-router
	<Switch>
		<Route path='/' />
		<Route path='/about' />
		<Route path='/projects' />
		<Route path='/contacts' />
		<Route path='/auth' />
		<Route /> // No-match case
	</Switch>
);
```
And you need to create a script which will run from the command line or on the server.

_Please note that in this case you need a module 'babel-register' to work with the ES2105 syntax and `.jsx` format._

`sitemap-builder.js`

```js
require('babel-register');

const router = require('./router').default;
const Sitemap = require('../').default;

(
	new Sitemap(router)
		.build('http://my-site.ru')
		.save('./sitemap.xml')
);
```

It's a minimal example. After running the script, a `sitemap.xml` file will be created, which includes all paths, described in the configuration of `react-router`.

A more detailed example can be found in the `example` directory. 


