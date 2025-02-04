Deno provides compatibility layer for Node.js. To do that we need to use `node:` specifier to import statements:
```ts
import * as os from "node:os";
console.log(os.cpus());
```
# Using npm
Deno has native support for importing npm packages:
```ts
import * as emoji from "npm:node-emoji";
console.log(emoji.emojify(`:sauropod: :heart:  npm`));
```