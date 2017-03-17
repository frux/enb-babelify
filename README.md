# enb-babelify
ENB Babel techs

Process JavaScript file by Babel.

```
@param {Object}    [options]                              Options
@param {String}    [options.target='?.browser.es5.js']    Path to compiled file.
@param {String}    [options.sourceTarget]                 Path to a source Javascript code
@param {String}    [options.babelOptions={}]              Options provided to Babel
```

```js
var babelBrowserTech = require('enb-babelify/techs/browser-js'),
	fileProvideTech = require('enb/techs/file-provider'),
	bemTechs = require('enb-bem-techs');
 
module.exports = function(config) {
  config.node('bundle', function(node) {
    // get FileList
    node.addTechs([
		[fileProvideTech, { target: '?.bemdecl.js' }],
		[bemTechs.levels, levels: ['blocks']],
		[bemTechs.deps],
		[bemTechs.files]
    ]);
    
    // build browser.js file
    node.addTech([ babelBrowserTech, { sourceTarget: '?.browser.js' } ]);
    node.addTarget('?.browser.es5.js');
  });
};
```
