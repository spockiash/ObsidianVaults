Routing in [[Fresh Framework]] provides an  way of handling requests to the server. It combines URL path with file-system based approach.
Here is a table of file names, which route patterns they map to, and which paths they might match:

| File name                   | Route pattern          | Matching paths                          |     |
| --------------------------- | ---------------------- | --------------------------------------- | --- |
| `index.ts`                  | `/`                    | `/`                                     |     |
| `about.ts`                  | `/about`               | `/about`                                |     |
| `blog/index.ts`             | `/blog`                | `/blog`                                 |     |
| `blog/[slug].ts`            | `/blog/:slug`          | `/blog/foo`, `/blog/bar`                |     |
| `blog/[slug]/comments.ts`   | `/blog/:slug/comments` | `/blog/foo/comments`                    |     |
| `old/[...path].ts`          | `/old/:path*`          | `/old/foo`, `/old/bar/baz`              |     |
| `docs/[[version]]/index.ts` | `/docs{/:version}?`    | `/docs`, `/docs/latest`, `/docs/canary` |     |
|                             |                        |                                         |     |
source: https://fresh.deno.dev/docs/concepts/routing

## Overriding default routing
Custom URL patterns can be specified in the routing configuration:
`routes/x.ts`:
```ts
import { RouteConfig } from "$fresh/server.ts";

export const config: RouteConfig = {
  routeOverride: "/x/:module@:version/:path*",
};

// ...
```
