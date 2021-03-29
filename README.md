# swagger-schema

swagger-ui schema auto generation and base on [swagger-autogen](https://github.com/davibaltar/swagger-autogen).

[![NPM Version](https://img.shields.io/npm/v/swagger-schemagen.svg?style=flat)](https://www.npmjs.org/package/commander)
[![NPM Downloads](https://img.shields.io/npm/dm/swagger-schemagen.svg?style=flat)](https://npmcharts.com/compare/swagger-schemagen?minimal=true)
[![Known Vulnerabilities](https://snyk.io/test/npm/swagger-schemagen/badge.svg)](https://snyk.io/test/npm/swagger-autogen)

## Installation

This is a [Node.js](https://nodejs.org/en/) module available through the [npm](https://www.npmjs.com/).

```bash
$ npm install --save swagger-schemagen
```

It is loaded using the require() function:

```js
const swaggerSchema = require('swagger-schemagen')
```

## Update

If you already have the module installed and want to update to the latest version, use the command:

```bash
$ npm install --save swagger-schemagen@1.0.1
```

## Usage

[Example express api](https://github.com/whlshy/UsefulExpressAPI)

### Usage

The code below must be inserted in a separate file, for example: *swagger.js*. For example:

**File: swagger.js**

```js
const doc = {
    info: {
        title: "Example API Document",
        description: "Description"
    },
    host: null,
    schemes: ['http'],
    tags: alltags
}

const outputFile = './src/swagger/swagger-output.json'
const endpointsFiles = ['./index.js']

const swaggerschema = require('./src/lib/swaggerschema')
const schematest = require('swagger-schemagen')

const asyncfun = async (outputFile, endpointsFiles, doc, schemaFolder) => {
    await swaggerAutogen(outputFile, endpointsFiles, doc)
    await schematest(outputFile, schemaFolder)
}

const schemaFolder = './src/schema/'
asyncfun(outputFile, endpointsFiles, doc, schemaFolder)
```