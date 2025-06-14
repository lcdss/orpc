---
title: Comparison
description: How is oRPC different from other RPC or REST solutions?
---

# Comparison

This comparison table helps you understand how oRPC differs from other popular TypeScript RPC and REST solutions.

- ✅ First-class, built-in support
- 🟡 Lacks features, or requires third-party integrations
- 🛑 Not supported or not documented

| Feature                                      | oRPC docs                                                                                    | oRPC | tRPC | ts-rest |
| -------------------------------------------- | -------------------------------------------------------------------------------------------- | ---- | ---- | ------- |
| End-to-end Typesafe Input/Output             |                                                                                              | ✅   | ✅   | ✅      |
| End-to-end Typesafe Errors                   | [1](/docs/client/error-handling), [2](/docs/error-handling#type%E2%80%90safe-error-handling) | ✅   | 🟡   | ✅      |
| End-to-end Typesafe File/Blob                | [1](/docs/file-upload-download)                                                              | ✅   | 🟡   | 🛑      |
| End-to-end Typesafe Streaming                | [1](/docs/event-iterator)                                                                    | ✅   | ✅   | 🛑      |
| Tanstack Query Integration (React)           | [1](/docs/tanstack-query/react)                                                              | ✅   | ✅   | 🟡      |
| Tanstack Query Integration (Vue)             | [1](/docs/tanstack-query/vue)                                                                | ✅   | 🛑   | 🟡      |
| Tanstack Query Integration (Solid)           | [1](/docs/tanstack-query/solid)                                                              | ✅   | 🛑   | 🟡      |
| Tanstack Query Integration (Svelte)          | [1](/docs/tanstack-query/svelte)                                                             | ✅   | 🛑   | 🛑      |
| Vue Pinia Colada Integration                 | [1](/docs/pinia-colada)                                                                      | ✅   | 🛑   | 🛑      |
| With Contract-First Approach                 | [1](/docs/contract-first/define-contract)                                                    | ✅   | 🛑   | ✅      |
| Without Contract-First Approach              |                                                                                              | ✅   | ✅   | 🛑      |
| OpenAPI Support                              | [1](/docs/openapi/openapi-handler)                                                           | ✅   | 🟡   | 🟡      |
| OpenAPI Support for multiple schema          | [1](/docs/openapi/openapi-handler)                                                           | ✅   | 🛑   | 🛑      |
| OpenAPI Bracket Notation Support             | [1](/docs/openapi/bracket-notation)                                                          | ✅   | 🛑   | 🛑      |
| Server Actions Support                       | [1](/docs/server-action)                                                                     | ✅   | ✅   | 🛑      |
| Lazy Router                                  | [1](/docs/router#lazy-router)                                                                | ✅   | ✅   | 🛑      |
| Native Types (Date, URL, Set, Maps, ...)     | [1](/docs/rpc-handler#supported-data-types)                                                  | ✅   | 🟡   | 🛑      |
| Streaming response (SSE)                     | [1](/docs/event-iterator)                                                                    | ✅   | ✅   | 🛑      |
| Standard Schema (Zod, Valibot, ArkType, ...) |                                                                                              | ✅   | ✅   | 🛑      |
| Built-in Plugins (CORS, CSRF, Retry, ...)    |                                                                                              | ✅   | 🛑   | 🛑      |
| Batch Request/Response                       | [1](/docs/plugins/batch-request-response)                                                    | ✅   | ✅   | 🛑      |
| WebSockets                                   | [1](/docs/adapters/websocket)                                                                | ✅   | ✅   | 🛑      |
| Nest.js integration                          |                                                                                              | 🛑   | 🟡   | ✅      |
