[![Deploy to now](https://deploy.now.sh/static/button.svg)](https://deploy.now.sh/?repo=https://github.com/johnymontana/NODES2019-GRANDstack&env=NEO4J_USER&env=NEO4J_URI&env=NEO4J_PASSWORD)

# GraphQL Summit Graph

[GraphQL Summit](https://summit.graphql.com/) is the world's largest conference dedicated to GraphQL. This repo contains a simple demo GRANDstack app to explore the conference sessions and show personalized recommendations using:

**GRANDstack**

* GraphQL
* React
* Apollo
* Neo4j Database

## Neo4j

![](images/neo4j.png)

The data for the app is stored in Neo4j graph database. You can download Neo4j locally or spin up a Neo4j Sandbox. The Python [import script in `/import`](import/scrape_schedule.ipynb) will scrape the GraphQL Summit speakers page and load the data into Neo4j.


## GraphQL API

![](images/graphql.png)

A GraphQL API fetches data from Neo4j using the [`neo4j-graphql.js`](https://grandstack.io/docs/neo4j-graphql-js.html)

*Install dependencies*

```
(cd ./api && npm install)
```

*Start API server*
```
cd ./api && npm start
```

## React UI

The React app uses Apollo Client to query the GraphQL API and render search results and recommendations.

*Start UI server*
```
cd ./ui && npm install 
npm start
```

## Deployment

### Zeit Now v2

Zeit Now v2 can be used with monorepos such as grand-stack-starter. [`now.json`](https://github.com/grand-stack/grand-stack-starter/blob/master/now.json) defines the configuration for deploying with Zeit Now v2.

1. Set the now secrets for your Neo4j instance:

```
now secret add NEO4J_URI bolt+routing://<YOUR_NEO4J_INSTANCE_HERE>
now secret add NEO4J_USER <YOUR_DATABASE_USERNAME_HERE>
now secret add NEO4J_PASSWORD <YOUR_DATABASE_USER_PASSWORD_HERE>
```

2. Run `now`

### Zeit Now v1

1. Run `now` in `/api` and choose `package.json` when prompted.
1. Set `REACT_APP_GRAPHQL_API` based on the API deployment URL from step 1 in `ui/.env`
1. Run `now` in `/env` and choose `package.json` when prompted.