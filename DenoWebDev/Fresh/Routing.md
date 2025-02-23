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
# Route groups
Each route group can have only one `_layout.tsx` file. For example the default Fresh app creates `_app.tsx` as the layout file.
```
└── routes
    ├── (marketing)
    │   ├── _layout.tsx  # only applies to about.tsx and career.tsx
    │   ├── about.tsx
    │   └── career.tsx
    └── (info)
        ├── _layout.tsx  # only applies to archive.tsx and contact.tsx
        ├── archive.tsx
        └── contact.tsx
```
To create route groups use folder that has name put in parentheses like `(marketing`.
## Co-location
We can use similar technique to put islands closer to their route location. Inside each group we can put `(_islands)` or `(_components)`:
```
└── routes
    ├── (marketing)
    │   ├── _layout.tsx
    │   ├── about.tsx
    │   ├── career.tsx
    │   ├── (_components)
    │   │   └── newsletter-cta.tsx
    │   └── (_islands)
    │       └── interactive-stats.tsx # Fresh treats this as an island
    └── shop
        ├── (_components)
        │   └── product-card.tsx
        └── (_islands)
            └── cart.tsx # Fresh treats this as an island
```