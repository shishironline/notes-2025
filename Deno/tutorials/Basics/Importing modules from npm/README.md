# Importing modules form npm

Import the express module from npm using **npm:** prefix

and appending a version number

`import express from "npm:express@4.18.2";`

Create an express server

`const app = express();`

Configure a route to process HTTP GET requests

```
app.get("/", (_req, res) => {
  res.send("Welcome to the Dinosaur API!");
});
```

Start a web server using the express app

`app.listen(3000);`

Run locally using Deno CLI

`deno run --allow-net --allow-read --allow-env https://docs.deno.com/examples/scripts/npm.ts`


---
[copy of raw file](https://github.com/denoland/docs/blob/main/examples/scripts/npm.ts)

/**
 * @title Import modules from npm
 * @difficulty beginner
 * @tags cli
 * @run --allow-net --allow-read --allow-env <url>
 * @resource {https://docs.deno.com/runtime/manual/node} Node.js / npm support in Deno
 * @resource {https://docs.deno.com/runtime/manual/node/npm_specifiers} npm: specifiers
 * @resource {https://www.npmjs.com/package/express} express module on npm
 * @group Basics
 *
 * Use JavaScript modules from npm in your Deno programs with the "npm:"
 * specifier in your imports.
 */

// Import the express module from npm using an npm: prefix, and appending a
// version number. Dependencies from npm can be configured in an import map
// also.
import express from "npm:express@4.18.2";

// Create an express server
const app = express();

// Configure a route that will process HTTP GET requests
app.get("/", (_req, res) => {
  res.send("Welcome to the Dinosaur API!");
});

// Start an HTTP server using the configured Express app
app.listen(3000);