---
title: Next.js Integration
description: Seamlessly integrate oRPC with Next.js
---

# Next.js Integration

[Next.js](https://nextjs.org/) is a leading React framework for server-rendered apps. oRPC works with both the [App Router](https://nextjs.org/docs/app/getting-started/installation) and [Pages Router](https://nextjs.org/docs/pages/getting-started/installation). For additional context, refer to the [HTTP Adapter](/docs/adapters/http) guide.

::: info
oRPC also supports [Server Action](/docs/server-action) out-of-the-box.
:::

## App Router

::: code-group

```ts [app/rpc/[[...rest]]/route.ts]
import { RPCHandler } from '@orpc/server/fetch'

const handler = new RPCHandler(router)

async function handleRequest(request: Request) {
  const { response } = await handler.handle(request, {
    prefix: '/rpc',
    context: {}, // Provide initial context if needed
  })

  return response ?? new Response('Not found', { status: 404 })
}

export const GET = handleRequest
export const POST = handleRequest
export const PUT = handleRequest
export const PATCH = handleRequest
export const DELETE = handleRequest
```

:::

::: info
The `handler` can be any supported oRPC handler, such as [RPCHandler](/docs/rpc-handler), [OpenAPIHandler](/docs/openapi/openapi-handler), or another custom handler.
:::

## Pages Router

::: code-group

```ts [pages/rpc/[[...rest]].ts]
import { RPCHandler } from '@orpc/server/node'

const handler = new RPCHandler(router)

export const config = {
  api: {
    bodyParser: false,
  },
}

export default async (req, res) => {
  const { matched } = await handler.handle(req, res, {
    prefix: '/rpc',
    context: {}, // Provide initial context if needed
  })

  if (matched) {
    return
  }

  res.statusCode = 404
  res.end('Not found')
}
```

:::

::: warning
Next.js default [body parser](https://nextjs.org/docs/pages/building-your-application/routing/api-routes#custom-config) blocks oRPC raw‑request handling. Ensure `bodyParser` is disabled in your API route:

```ts
export const config = {
  api: {
    bodyParser: false,
  },
}
```

:::

::: info
The `handler` can be any supported oRPC handler, such as [RPCHandler](/docs/rpc-handler), [OpenAPIHandler](/docs/openapi/openapi-handler), or another custom handler.
:::
