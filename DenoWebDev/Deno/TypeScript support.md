Typescript i a first class language in Deno. It can be run just with Deno.
## Type checking
Deno allows for code type checking using command `deno check`.
When using `deno run` command the type-checking will be skipped. In order to to do type checking with `run` use the `--check' flag:
```
deno run --check module.ts
```
This will cause type errors to exit before run is executed.