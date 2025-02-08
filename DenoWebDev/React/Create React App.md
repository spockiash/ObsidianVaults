The best way of creating React app with Deno is using Vite. It is possible to create React app without Vite in Deno but Vite allows for much smoother developer experience. It is also very fast.

When developing react applications with Deno (or Node) we use these frameworks as development servers. Vite is also development server technology. Once we build the application the output is JavaScript content for the browser. There is no React specific back-end component once the React front-end is pushed to production.
# Scaffolding with `create-vite-extra`
To scaffold project we can use `npm` package `create-vite-extra`. We can use [[Deno#CLI|Deno CLI]] with flags to scaffold new project with already prepared run flags:
```sh
deno run --allow-env --allow-read --allow-write npm:create-vite-extra
```
After this command Vite prompts to select scaffolding options, so we can choose what front-end framework we want and what language we want (JavaScript or TypeScript). Then we just `cd` into folder that matches name of the project and run the application with:
```sh
deno task dev
```

