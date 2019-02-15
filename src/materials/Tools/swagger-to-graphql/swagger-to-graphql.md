---
path: '/materials/swagger-to-graphql'
type: 'GitHub'
img: './screenshot.png'
material:
  title: 'swagger-to-graphql'
  url: 'https://medium.com/@raxwunter/moving-existing-api-from-rest-to-graphql-205bab22c184'
  github_url: 'https://github.com/yarax/swagger-to-graphql'
  subscribers_count: '20'
  stargazers_count: '439'
  tags: ['']
  subtitle: 'Swagger to GraphQL API adapter'
  clone_url: 'https://github.com/yarax/swagger-to-graphql.git'
  ssh_url: 'git@github.com:yarax/swagger-to-graphql.git'
  pushed_at: '2019-02-13T12:09:38Z'
  updated_at: '2019-02-14T16:40:58Z'
  author:
    name: 'yarax'
    avatar: 'https://avatars3.githubusercontent.com/u/1425951?v=4'
    github_url: 'https://github.com/yarax'
  latestRelease:
    tag_name: '1.4.0'
    name: 'Fix odd character issues and GraphQL 0.13'
    url: 'https://github.com/yarax/swagger-to-graphql/releases/tag/1.4.0'
    created_at: '2018-06-30T14:24:29Z'
---
# Swagger2GraphQL

Swagger2GraphQL converts your existing Swagger schema to GraphQL types where resolvers perform HTTP calls to certain real endpoints.
It allows you to move your API to GraphQL with nearly zero effort and maintain both REST and GraphQL APIs.

<a href='https://medium.com/@raxwunter/moving-existing-api-from-rest-to-graphql-205bab22c184'>Why?</a>

*Looking for contributors!*

# Usage

## Basic server

```js
const express = require('express');
const app = express();
const graphqlHTTP = require('express-graphql');
const graphQLSchema = require('swagger-to-graphql');

const proxyUrl = 'http://petstore.swagger.io/v2';
const pathToSwaggerSchema = './petstore.json';
const customHeaders = {
  // Authorization: 'Basic YWRkOmJhc2ljQXV0aA=='
}

graphQLSchema(pathToSwaggerSchema, proxyUrl, customHeaders).then(schema => {
  app.use('/graphql', graphqlHTTP(() => {
    return {
      schema,
      graphiql: true
    };
  }));

  app.listen(3009, 'localhost', () => {
    console.info('http://localhost:3009/graphql');
  });
}).catch(e => {
  console.log(e);
});
```

Constructor (graphQLSchema) arguments:
* `pathToSwaggerSchema` (string) is a path to your local swagger schema file. *required*
* `proxyUrl` (string) base URL which will be used to hit your HTTP API. Can be taken either from Swagger schema `baseUrl` configuration or from this parameter.
* `customHeaders` (object) key value object of custom headers, which should be included to the HTTP request. Can be used for example for authorization (look at the example above)

## CLI usage

You can use the library just to convert schemas without actually running server

```
npm i -g swagger-to-graphql
swagger-to-graphql --swagger=/path/to/swagger_schema.json > ./types.graphql
```

## Video from O.J. Sousa Rodrigues at Vienna.JS
<a href='https://www.youtube.com/watch?v=551gKWJEsK0&feature=youtu.be&t=1269' target='_blank'><img src='https://s3.eu-central-1.amazonaws.com/yarax-public-assets/2019-02-13_13-01-45.png'/></a>


![Build Status](https://travis-ci.org/yarax/swagger-to-graphql.svg?branch=master)