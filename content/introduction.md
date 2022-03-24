---
title: "Get Started with Obsidian"
metaTitle: "Obsidian | Deno's first native GraphQL caching client and server module"
metaDescription: "Deno's first native GraphQL caching client and server module"
---

Here's how to use Obsidian with your application.

# Quick Start
obsidian is Deno's first native GraphQL caching client and server module. Boasting lightning-fast caching and fetching capabilities alongside headlining normalization and destructuring strategies, obsidian is equipped to support scalable, highly performant applications.

Optimized for use in server-side rendered React apps built with Deno, full stack integration of obsidian enables many of its most powerful features, including optimized caching exchanges between client and server and extremely lightweight client-side caching.

## Docker File for Full Demo
If you would like to see Obsidian in action you can run Docker-Compose to spin our demo server

https://github.com/oslabs-beta/obsidian-demo-docker

## Demo Git Repository
If you would like to explore the git repository of the Obsidian Demo the link is provided below

https://github.com/oslabs-beta/obsidian-demo-3.2

## Adding Obsidian Cacheing tool to a GraphQL server
Obsidian Acts as an extrention to the Oak Router, so implementing Obsidian is as easy as importing the Obsidian Router, and Oak Router and extending the Oak Router with Obsidian.

The Code below will extend the Oak router and will server the /graphql endpoint for any querys.

```javascript
import { Application, Router } from "https://deno.land/x/oak@v6.0.1/mod.ts";
import { ObsidianRouter, gql } from "https://deno.land/x/obsidian/mod.ts";

const PORT = 8000; 
const app = new Application();

interface ObsRouter extends Router {
    obsidianSchema?: any;
    }
          
const GraphQLRouter = await ObsidianRouter<ObsRouter>({
Router,
typeDefs: types,        // declare imported types object here
resolvers: resolvers,   // declare imported resolvers object here
redisPort: 6379,        //Desired redis port
useCache: true,         //Boolean to toggle all cache functionality
usePlayground: true,    //Boolean to allow for graphQL playground
useQueryCache: true,    //Boolean to toogle full query cache
useRebuildCache: true,  //Boolean to toggle rebuilding from normalized data
customIdentifier: ["id", "__typename"]  
    //customIdentifier is by default set to id + typename and is used to
    //create the unique hash for storing data in the cache
    //this can be set by the user to be different feilds that are expected
    //on the response from graphQL server, but must create a unique hash for
    //proper storage and retrieval from cache 
                  
});

// now we attach the graphql router routes to our app
app.use(GraphQLRouter.routes(), GraphQLRouter.allowedMethods());
          

app.addEventListener("listen", () => {
  console.log(`listening on localhost:${PORT}`);
});

await app.listen({ port: PORT });
```

## Lists
- Item 1
- Item 2
- Item 3
- Item 4
- Item 5

## Links

* Relative: [Codeblock](/codeblock)
* Absolute: [Demo](https://learn.hasura.io/graphql/react)