---
title: Fastify Integration
description: Seamlessly integrate oRPC with Fastify
---

# Fastify Integration

[Fastify](https://fastify.dev/) is a web framework highly focused on providing the best developer experience with the least overhead and a powerful plugin architecture. For additional context, refer to the [HTTP Adapter](/docs/adapters/http) guide.

::: warning
Fastify automatically parses the request payload which interferes with oRPC, that apply its own parser. To avoid errors, it's necessary to create a node http server and pass the requests to oRPC first, and if there's no match, pass it to Fastify.
:::

## Basic

```ts
import Fastify from 'fastify'
import { RPCHandler } from '@orpc/server/node'

const fastify = Fastify()

const handler = new RPCHandler(router)

const fastify = Fastify({
  logger: true,
  serverFactory: (serverHandler) => {
    const server = http.createServer(async (req, res) => {
      const { matched } = await handler.handle(req, res, {
        context: {},
        prefix: "/api",
      })

      if (matched) {
        return
      }

      serverHandler(req, res)
    })

    return server
  },
})

try {
  await fastify.listen({ port: 3000 })
} catch (err) {
  fastify.log.error(err)
  process.exit(1)
}
```

## OpenAPI with Zod 4 (experimental)

```ts
import Fastify from 'fastify'
import { RPCHandler } from '@orpc/server/node'
import { OpenAPIHandler } from "@orpc/openapi/node"
import { OpenAPIReferencePlugin } from "@orpc/openapi/plugins"
import {
  experimental_ZodSmartCoercionPlugin as ZodSmartCoercionPlugin,
  experimental_ZodToJsonSchemaConverter as ZodToJsonSchemaConverter,
} from "@orpc/zod/zod4"

const fastify = Fastify()

const openAPIHandler = new OpenAPIHandler(router, {
  plugins: [
    new ZodSmartCoercionPlugin(),
    new OpenAPIReferencePlugin({
      schemaConverters: [new ZodToJsonSchemaConverter()],
      specGenerateOptions: {
        info: {
          title: "API Playground",
          version: "1.0.0",
        },
      },
    }),
  ],
})

const fastify = Fastify({
  logger: true,
  serverFactory: (serverHandler) => {
    const server = http.createServer(async (req, res) => {
      const { matched } = await openAPIHandler.handle(req, res, {
        context: {},
        prefix: "/api",
      })

      if (matched) {
        return
      }

      serverHandler(req, res)
    })

    return server
  },
})

try {
  await fastify.listen({ port: 3000 })
} catch (err) {
  fastify.log.error(err)
  process.exit(1)
}
```

::: info
The `handler` can be any supported oRPC handler, such as [RPCHandler](/docs/rpc-handler), [OpenAPIHandler](/docs/openapi/openapi-handler), or another custom handler.
:::
