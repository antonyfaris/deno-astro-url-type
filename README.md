# Steps to reproduce

Install dependencies and run deno cache the project:

1. `pnpm i`
1. `deno task cache`
1. Restart Deno Language Server

```ts
import { defineMiddleware } from "astro/middleware";

export const onRequest = defineMiddleware((context, next) => {
  console.log(context.url.pathname);
                            ^ Property 'pathname' does not exist on type 'URL'.deno-ts(2339)
});
```

The types from `URL` are incorrect. Example:
[`./src/middleware.ts`](./src/middleware.ts). It does not work in vscode, and if
you run `deno task check`.

In [`.vscode/settings.json`](./.vscode/settings.json) if you change
`"deno.enable": true,` to false it will work fine with Node. Sometimes, you may
need to run `pnpm i` again and restart the TypeScript server.

If you right-click on `url` (line 4 of
[`./src/middleware.ts`](./src/middleware.ts)), it will navigate to a URL type
coming from esbuild.

> Note: Tested with Deno 1.43.6 and Deno vscode extension 3.37.1

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/antonyfaris/deno-astro-url-type)

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/antonyfaris/deno-astro-url-type)
