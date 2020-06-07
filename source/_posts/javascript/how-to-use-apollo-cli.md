---
title: How work with Apollo CLI
tags: [vue, javascript, es6]
date: 2020-05-20 21:35:09
categories: [IT]
---

Apollo CLI is a productive tool when integrate Apollo into your application. It can: 


1. service:push - Publish Schema to https://engine.apollographql.com, share among your team.
2. client:codegen - Generate TypeScript interface definition from GraphQL schema.


## Install Apollo CLI
```
npm i -g apollo
```

## Publish Schema： service:push

Here we assume you've already started Apollo Server(Started on port 4000). Open https://engine.apollographql.com in browser, create a bucket named `magic-mooc`， Then run :

```bash
 apollo service:push --graph=magic-mooc --key=user:gh.guoguolong:vKOUWxxp71eyns94RnorPg --endpoint=http://localhost:4000 
```
it'll publish schema to engine.apollographql.com. Let your other team members check it.

You can also move the command arguments into the file .env and apollo.config.js, then simply use `apollo service:push` to publish it.

**# apollo.config.js**
```
module.exports = {
    service: {
        name: 'magic-mooc',
        endpoint: {
            url: 'http://localhost:4000/graphql'
        }
    }
}
```

**# .env**
```
APOLLO_KEY=user:gh.guoguolong:vKOUWxxp71eyns94RnorPg
```

Try `aplollo service:push` again.

## Generate TypeScript definition file：client:codegen

We often develop ReactJS with TypeScript for type check. `apollo client:codegen` can check all the source code under src folder and it's sub-folder. If find any gql definition, it'll generate TypeScript interface into the __generated__ folder for subsequent use.

Unfortunately, I only succeed it by the file way(schema.gql). below is the sample I made:

### Step 1. Create apollo.config.js
Move to project root folder(You should have src sub-folder and some of the gql definitions), create apollo.config.js like this:
```
module.exports = {
    client: {
        service: {
            localSchemaFile: "./schema.gql"
        }
    }
}
```
### Step 2. Download schema.gql

Open Graph Endpoint in browser: http://localhost:4000, easily find the gql definitions then download it as schema.gql

### Step 3. Generate TypeScript Interface

```
apollo client:codegen --target typescript --watch
```

>Reference：[Configuring Apollo projects](https://www.apollographql.com/docs/devtools/apollo-config)
