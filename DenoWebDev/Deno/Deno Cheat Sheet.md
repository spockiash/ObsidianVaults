# Initialization
To create new project with Deno only:
```
deno init my_project
```
To create new application using vite:
```
deno run --allow-env --allow-read --allow-write npm:create-vite-extra
```
# Running
To run local file:
```
deno run main.ts
```
Running scripts from URL:
```
deno run https://docs.deno.com/examples/scripts/hello_world.ts
```
Running piped programs:
```shell
cat main.ts | deno run -
```
# Passing arguments
Deno can accept arguments and they can be accessed here:
```ts
console.log(Deno.args);
```
Then arguments can be passed:
```shell
$ deno run main.ts arg1 arg2 arg3
[ "arg1", "arg2", "arg3" ]
```
# Type checking
This if for TypeScript support and it can make the code type safe.
```
deno check module.ts
```
