# api documentation for  [merge-stream (v1.0.1)](https://github.com/grncdr/merge-stream#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-merge-stream.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-merge-stream) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-merge-stream.svg)](https://travis-ci.org/npmdoc/node-npmdoc-merge-stream)
#### Create a stream that emits events from multiple other streams

[![NPM](https://nodei.co/npm/merge-stream.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/merge-stream)

[![apidoc](https://npmdoc.github.io/node-npmdoc-merge-stream/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-merge-stream/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-merge-stream/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-merge-stream/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Stephen Sugden"
    },
    "bugs": {
        "url": "https://github.com/grncdr/merge-stream/issues"
    },
    "dependencies": {
        "readable-stream": "^2.0.1"
    },
    "description": "Create a stream that emits events from multiple other streams",
    "devDependencies": {
        "from2": "^2.0.3",
        "istanbul": "^0.3.2"
    },
    "directories": {},
    "dist": {
        "shasum": "4041202d508a342ba00174008df0c251b8c135e1",
        "tarball": "https://registry.npmjs.org/merge-stream/-/merge-stream-1.0.1.tgz"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "1b33da64b219dcc8bf33645953c32a6fd9e3b36d",
    "homepage": "https://github.com/grncdr/merge-stream#readme",
    "license": "MIT",
    "maintainers": [
        {
            "name": "grncdr"
        },
        {
            "name": "shinnn"
        }
    ],
    "name": "merge-stream",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git+https://github.com/grncdr/merge-stream.git"
    },
    "scripts": {
        "test": "istanbul cover test.js && istanbul check-cover --statements 100 --branches 100"
    },
    "version": "1.0.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module merge-stream](#apidoc.module.merge-stream)
1.  [function <span class="apidocSignatureSpan"></span>merge-stream ()](#apidoc.element.merge-stream.merge-stream)
1.  [function <span class="apidocSignatureSpan">merge-stream.</span>toString ()](#apidoc.element.merge-stream.toString)



# <a name="apidoc.module.merge-stream"></a>[module merge-stream](#apidoc.module.merge-stream)

#### <a name="apidoc.element.merge-stream.merge-stream"></a>[function <span class="apidocSignatureSpan"></span>merge-stream ()](#apidoc.element.merge-stream.merge-stream)
- description and source-code
```javascript
merge-stream = function () {
  var sources = []
  var output  = new PassThrough({objectMode: true})

  output.setMaxListeners(0)

  output.add = add
  output.isEmpty = isEmpty

  output.on('unpipe', remove)

  Array.prototype.slice.call(arguments).forEach(add)

  return output

  function add (source) {
    if (Array.isArray(source)) {
      source.forEach(add)
      return this
    }

    sources.push(source);
    source.once('end', remove.bind(null, source))
    source.once('error', output.emit.bind(output, 'error'))
    source.pipe(output, {end: false})
    return this
  }

  function isEmpty () {
    return sources.length == 0;
  }

  function remove (source) {
    sources = sources.filter(function (it) { return it !== source })
    if (!sources.length && output.readable) { output.end() }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.merge-stream.toString"></a>[function <span class="apidocSignatureSpan">merge-stream.</span>toString ()](#apidoc.element.merge-stream.toString)
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
