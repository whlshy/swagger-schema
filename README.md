# swagger-schema

swagger-ui schema auto generation and base on [swagger-autogen](https://github.com/davibaltar/swagger-autogen).

[![NPM Version](https://img.shields.io/npm/v/swagger-schemagen.svg?style=flat)](https://www.npmjs.org/package/commander)
[![NPM Downloads](https://img.shields.io/npm/dy/swagger-schemagen.svg?style=flat)](https://npmcharts.com/compare/swagger-schemagen?minimal=true)

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
$ npm install --save swagger-schemagen@last
```

## Usage

[Example express api](https://github.com/whlshy/UsefulExpressAPI)

### Usage

Function signature:

```js
const swaggerSchema: (outputFile: <string>, schemaFolder: <Array of string>) => Promise <any>
```

**outputFile:** (Required*). Output file. It will be the file generated by the module containing the documentation in the format identified by Swagger.

**schemaFolder:** (Required*). This Folder is saving all of schema json file, and the parameter's type for mssql will update in Swagger file.

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

### Example Document

Json file in schema folder

**Note.json:**

```json
[
    { "attr": "vid", "type": "Int" },
    { "attr": "currenttime", "type": "Float" },
    { "attr": "nid", "type": "Int" },
    { "attr": "title", "type": "NVarChar" },
    { "attr": "content", "type": "NVarChar" }
]
```

### Notice

**Swagger schema json file and swagger tag should be give in same name!!!**

Like your router's swagger tag is 'Note', and your schema name should be 'Note.json'.

## Compare Use

### Before Using swagger-schema

**controller -> Note.js:**

```js
router.delete('/note', async (req, res, next) => {
    // #swagger.tags = ['Note']
    // #swagger.summary = '刪除單個筆記'
    const { nid } = req.body // declare parameter's in body
    sqlcode = "update Note set bDel = 1 where NID = @nid and OwnerMID = @mid";
    let response = await runSQL(sqlcode, req, schema);
    res.json(response ? { message: "success" } : { message: "failed" });
});

router.put('/note/title', async (req, res, next) => {
    // #swagger.tags = ['Note']
    // #swagger.summary = '編輯筆記標題'
    const { nid, title } = req.body // declare parameter's in body
    sqlcode = "update Note set Title = @title, LastModifiedDT = getdate() where NID = @nid and OwnerMID = @mid";
    let response = await runSQL(sqlcode, req, schema);
    res.json(response ? { message: "success" } : { message: "failed" });
});
```

![image](https://user-images.githubusercontent.com/49122960/112843076-cc4d0c00-90d4-11eb-9312-95a18be76414.png)

### After Using swagger-schema

**schema file:**
![image](https://user-images.githubusercontent.com/49122960/112843629-5c8b5100-90d5-11eb-9fc9-9b4b3c3cd3ec.png)

![image](https://user-images.githubusercontent.com/49122960/112843468-2fd73980-90d5-11eb-935e-8846bd5b025b.png)