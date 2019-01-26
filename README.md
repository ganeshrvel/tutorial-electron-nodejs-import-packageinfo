# Import values from package.json into electron/nodejs application.

- Author: [Ganesh Rathinavel](https://www.linkedin.com/in/ganeshrvel "Ganesh Rathinavel")
- License: [MIT](https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo/blob/master/LICENSE "MIT")
- Website URL: [https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo](https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo/ "https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo")
- Repo URL: [https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo](https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo/ "https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo")
- Contacts: ganeshrvel@outlook.com


### Introduction

##### I have seen many users importing 'package.json' directly into the node.js project. This is a programming disaster as it could leak your sensitive information such as "scripts" or private TOKENS into the bundled js files.
##### There is no single clearcut solution to get this done inside an electron app. It has to be handled intelligently using algorithms and fallbacks.
##### I have spent a significant amount of time researching how to get this done. This was originally implemented inside [OpenMTP - Advanced Android File Transfer Application for macOS](https://github.com/ganeshrvel/openmtp "OpenMTP - Advanced Android File Transfer Application for macOS").

### Implementation

- Install npm packages

```shell
$ npm install electron-root-path

or 

$ yarn add electron-root-path
```

- Add the below code inside your *webpack.config.js* file (for both production and development)

```javascript
import { rootPath } from 'electron-root-path';

const pkg = require(join(rootPath, 'package.json'));

plugins: [
    new webpack.DefinePlugin({
      PKG_INFO: {
        productName: JSON.stringify(pkg.productName),
        description: JSON.stringify(pkg.description),
        name: JSON.stringify(pkg.name),
        author: JSON.stringify(pkg.author),
        version: JSON.stringify(pkg.version),
        repository: JSON.stringify(pkg.repository),
        homepage: JSON.stringify(pkg.homepage)
      }
    }),
  ]
```

- Create a file *./app/pkginfo.js* and add the below code

```javascript
'use strict';

import { join } from 'path';
import { readFileSync } from 'fs';
import { rootPath } from 'electron-root-path';

let _pkginfo = {};

// eslint-disable-next-line no-undef
if (typeof PKG_INFO !== 'undefined' && PKG_INFO !== null) {
  // eslint-disable-next-line no-undef
  _pkginfo = PKG_INFO;
} else {
  /* This is a fallback incase the webpack DefinePlugin modules hasn't been initialized yet. */
  /* Developement mode only */
  _pkginfo = JSON.parse(
    readFileSync(join(rootPath, 'package.json'), { encoding: 'utf8' })
  );
}

export const pkginfo = _pkginfo;
```


### Clone
```shell
$ git clone --depth 1 --single-branch --branch master https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo.git

$ cd tutorial-electron-nodejs-import-packageinfo
```

### Contribute
- Fork the repo and create your branch from master.
- Ensure that the changes pass linting.
- Update the documentation if needed.
- Make sure your code lints.
- Issue a pull request!

When you submit code changes, your submissions are understood to be under the same [MIT License](https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo/blob/master/LICENSE "MIT License") that covers the project. Feel free to contact the maintainers if that's a concern.


### Buy me a coffee
Help me keep the app FREE and open for all.
Paypal me: [paypal.me/ganeshrvel](https://paypal.me/ganeshrvel "paypal.me/ganeshrvel")

### Contacts
Please feel free to contact me at ganeshrvel@outlook.com

### More repos
- [Electron React Redux Advanced Boilerplate](https://github.com/ganeshrvel/electron-react-redux-advanced-boilerplate "Electron React Redux Advanced Boilerplate")
- [OpenMTP  - Advanced Android File Transfer Application for macOS](https://github.com/ganeshrvel/openmtp "OpenMTP  - Advanced Android File Transfer Application for macOS")
- [electron-root-path](https://github.com/ganeshrvel/npm-electron-root-path "Get the root path of an Electron Application")

### License
tutorial-electron-nodejs-import-packageinfo is released under [MIT License](https://github.com/ganeshrvel/tutorial-electron-nodejs-import-packageinfo/blob/master/LICENSE "MIT License").

Copyright © 2018 - 2019 Ganesh Rathinavel
