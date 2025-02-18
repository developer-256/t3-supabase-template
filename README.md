## Quick Start

In Supabase dashboard:

1. Goto Authentication and then click on Emails on sidebar
2. Replace {{ .ConfirmationURL }} with {{ .SiteURL }}/auth/confirm?token_hash={{ .TokenHash }}&type=email
3. Goto Home and click on connect in navbar
4. Copy the connection string for nextjs within framework and add to .env
5. Copy Direct connection from connection string and add to DATABASE_URL in .env
6. Copy Session pooler from connection string and add to DIRECT_URL in .env

# Next.js + tRPC + Prisma + Supabase

This is a project template that sets you up with all of the basics required to build an interesting full stack app. It combines these frameworks into a setup that should empower you to build with sensible defaults.

It is based on the [T3 Stack](https://create.t3.gg/).

Things that this template comes with

- Next.js App Router
- Postgres database
- Auth (via Supabase)
- Type-safe API
- UI library in ShadCN/UI

This is everything you need to start building an advanced app.

## Overview

I can't possibly explain the systems better than they explain themselves, but if you're new to any of this tech, I'll do my best to explain the overall picture. But first, some links to each of the projects involved here.

- [Next.js](https://nextjs.org)
- [Supabase](https://supabase.com/docs)
- [Prisma](https://prisma.io)
- [tRPC](https://trpc.io) with [TanStack Query](https://tanstack.com/query/latest)
- [Tailwind CSS](https://tailwindcss.com) with [ShadCN UI](https://ui.shadcn.com/)

Generally speaking, here's how things click together:

- Next.js at its core. This is the web server framework that will return a React app.
- tRPC as the server API. It provides type safety end-to-end at its core. We use this as the main way to talk to the database to make sure we get authorized queries.
  - Note: this template does not take full advantage of Supabase's RLS (row-level security) as an auth strategy. It instead creates
- Supabase as the auth, database, and storage provider. Supabase auth was implemented via their most recent guide with Next.js [here](https://supabase.com/docs/guides/auth/server-side/nextjs?queryGroups=router&router=app).

This template doesn't enforce an opinion on data fetching strategies, but you do have basically two options

- Use the TanStack query hooks from the `trpc` component to fetch data in the React Lifecycle. This is the pre- React Server Components way to fetch data.
- Use the `trpc` client to fetch data in React Server Components. You can take full advantage of Suspense and have the first response from the server return interesting HTML.

There is lengthy debate on what the right approach will be for each use case. I encourage you to think critically about what one is best for you. If you're not sure, try starting with the TanStack query option and try pre-fetching queries in the server component for the page.

You can see examples in `prefetch/page.tsx`, `server-only-fetch/page.tsx`, and `client-only-fetch/page.tsx`. It's also worth noting that you can pre-fetch data in the initial SSR render of client components too, but I digress.
