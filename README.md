# api documentation for  [dependency-check (v2.8.0)](https://github.com/maxogden/dependency-check)  [![npm package](https://img.shields.io/npm/v/npmdoc-dependency-check.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-dependency-check) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-dependency-check.svg)](https://travis-ci.org/npmdoc/node-npmdoc-dependency-check)
#### checks which modules you have used in your code and then makes sure they are listed as dependencies in your package.json

[![NPM](https://nodei.co/npm/dependency-check.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/dependency-check)

[![apidoc](https://npmdoc.github.io/node-npmdoc-dependency-check/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-dependency-check/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-dependency-check/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-dependency-check/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "max ogden"
    },
    "bin": {
        "dependency-check": "cli.js"
    },
    "bugs": {
        "url": "https://github.com/maxogden/dependency-check/issues"
    },
    "dependencies": {
        "async": "^2.1.4",
        "builtins": "^1.0.0",
        "debug": "^2.2.0",
        "detective": "^4.0.0",
        "is-relative": "^0.2.1",
        "minimist": "^1.2.0",
        "read-package-json": "^2.0.4",
        "resolve": "^1.1.7"
    },
    "description": "checks which modules you have used in your code and then makes sure they are listed as dependencies in your package.json",
    "devDependencies": {
        "standard": "^8.6.0"
    },
    "directories": {
        "test": "test"
    },
    "dist": {
        "shasum": "ca1e08a78f6ca2dc4c7dad33e43a9040b0c23b68",
        "tarball": "https://registry.npmjs.org/dependency-check/-/dependency-check-2.8.0.tgz"
    },
    "gitHead": "656bd94862edc5363cc74a11a7aa1261a665153d",
    "homepage": "https://github.com/maxogden/dependency-check",
    "license": "BSD-3-Clause",
    "main": "index.js",
    "maintainers": [
        {
            "name": "blakeembrey"
        },
        {
            "name": "maxogden"
        },
        {
            "name": "voxpelli"
        }
    ],
    "name": "dependency-check",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git+https://github.com/maxogden/dependency-check.git"
    },
    "scripts": {
        "test": "standard && node cli.js test/ && node cli.js . && node cli.js . --extra --no-dev"
    },
    "version": "2.8.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module dependency-check](#apidoc.module.dependency-check)
1.  [function <span class="apidocSignatureSpan"></span>dependency-check (opts, cb)](#apidoc.element.dependency-check.dependency-check)
1.  [function <span class="apidocSignatureSpan">dependency-check.</span>extra (pkg, deps, options)](#apidoc.element.dependency-check.extra)
1.  [function <span class="apidocSignatureSpan">dependency-check.</span>missing (pkg, deps, options)](#apidoc.element.dependency-check.missing)
1.  [function <span class="apidocSignatureSpan">dependency-check.</span>toString ()](#apidoc.element.dependency-check.toString)



# <a name="apidoc.module.dependency-check"></a>[module dependency-check](#apidoc.module.dependency-check)

#### <a name="apidoc.element.dependency-check.dependency-check"></a>[function <span class="apidocSignatureSpan"></span>dependency-check (opts, cb)](#apidoc.element.dependency-check.dependency-check)
- description and source-code
```javascript
dependency-check = function (opts, cb) {
  var pkgPath = opts.path
  readPackage(pkgPath, function (err, pkg) {
    if (err && err.code === 'EISDIR') {
      pkgPath = path.join(pkgPath, 'package.json')
      return readPackage(pkgPath, function (err, pkg) {
        if (err) return cb(err)
        parse({
          path: pkgPath,
          package: pkg,
          entries: opts.entries,
          noDefaultEntries: opts.noDefaultEntries,
          builtins: opts.builtins,
          extensions: opts.extensions,
          detective: opts.detective
        }, cb)
      })
    }
    parse({
      path: pkgPath,
      package: pkg,
      entries: opts.entries,
      noDefaultEntries: opts.noDefaultEntries,
      builtins: opts.builtins,
      extensions: opts.extensions,
      detective: opts.detective
    }, cb)
  })
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.dependency-check.extra"></a>[function <span class="apidocSignatureSpan">dependency-check.</span>extra (pkg, deps, options)](#apidoc.element.dependency-check.extra)
- description and source-code
```javascript
extra = function (pkg, deps, options) {
  var missing = []
  var config = configure(pkg, options)

  config.allDeps.map(function (dep) {
    if (deps.indexOf(dep) === -1 && config.ignore.indexOf(dep) === -1) {
      missing.push(dep)
    }
  })

  return missing
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.dependency-check.missing"></a>[function <span class="apidocSignatureSpan">dependency-check.</span>missing (pkg, deps, options)](#apidoc.element.dependency-check.missing)
- description and source-code
```javascript
missing = function (pkg, deps, options) {
  var missing = []
  var config = configure(pkg, options)

  deps.map(function (used) {
    if (config.allDeps.indexOf(used) === -1 && config.ignore.indexOf(used) === -1) {
      missing.push(used)
    }
  })

  return missing
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.dependency-check.toString"></a>[function <span class="apidocSignatureSpan">dependency-check.</span>toString ()](#apidoc.element.dependency-check.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
