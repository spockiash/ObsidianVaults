Routes describe how request for given path should be handled. Routes have two main parts: handler and component. A route can have either, or both, but never neither.

The handler defines how request is processed. The component is the template for the page (`JSX`). The handler is passed a `render` function that can render a component.
## Handler
Here is basic handler:
```ts
import { FreshContext, Handlers } from "$fresh/server.ts";

export const handler: Handlers = {
  GET(_req: Request, _ctx: FreshContext) {
    return new Response("Hello World");
  },
  POST(_req: Request, _ctx: FreshContext) {
		return new Response("Posting World");
	},
};
```
To define a handler, one needs to export a `handler` function or object from the route module. If the handler is an object, each key in the object is the name of the HTTP method that the method should be called for.

## Component route
Now, let’s render some HTML using the route component:
```ts
import { PageProps } from "$fresh/server.ts";

export default function Page(props: PageProps) {
  return <div>You are on the page '{props.url.href}'.</div>;
}
```