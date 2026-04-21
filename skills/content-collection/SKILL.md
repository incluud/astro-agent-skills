---
name: content-collection
description: Set up and evolve Astro content collections with typed schemas and reliable querying patterns.
---

# Astro Content Collections

Use this skill when creating or refactoring structured content in Astro, such as blogs, docs, changelogs, case studies, team data, or other schema-driven content.

If `astro-best-practices` is available, apply it alongside this skill for naming, accessibility, and performance defaults.

## Workflow

### 1. Model the content before coding

Decide:

- which collections exist
- whether each one is `content` or `data`
- which fields are required
- which relationships need references
- whether assets such as images should be validated

Favor a schema that reflects how the site queries content, not just how frontmatter currently looks.

### 2. Define the schema in `src/content/config.*`

Use `defineCollection` and a clear schema. Keep required fields truly required, and add defaults only when they reflect real behavior.

Example:

```ts
import { defineCollection, z } from 'astro:content'

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    description: z.string(),
    publishDate: z.coerce.date(),
    updatedDate: z.coerce.date().optional(),
    tags: z.array(z.string()).default([]),
    draft: z.boolean().default(false),
  }),
})

export const collections = { blog }
```

Useful patterns:

- `z.enum(...)` for controlled values
- `z.coerce.date()` for frontmatter dates
- `reference('collection-name')` for relationships
- `schema: ({ image }) => ...` when image validation matters

### 3. Keep collection structure predictable

Typical layout:

```text
src/content/
  config.ts
  blog/
  docs/
  authors/
```

Prefer a stable folder structure and predictable slugs. Avoid scattering content across route folders if it is logically a collection.

### 4. Query with intent

Use the content APIs that match the job:

- `getCollection()` for lists
- `getEntry()` for a single known entry
- collection filters for draft/published splits

Example:

```astro
---
import { getCollection } from 'astro:content'

const posts = await getCollection('blog', ({ data }) => !data.draft)
---
```

When rendering entries, keep route generation and content rendering separate enough that each part remains easy to reason about.

### 5. Wire routes and rendering carefully

For dynamic routes:

- build paths from collection data
- pass the entry through props cleanly
- render content close to where layout decisions happen

Example:

```astro
---
import { getCollection } from 'astro:content'

export async function getStaticPaths() {
  const posts = await getCollection('blog')
  return posts.map((post) => ({
    params: { slug: post.slug },
    props: { post },
  }))
}

const { post } = Astro.props
const { Content } = await post.render()
---

<article>
  <h1>{post.data.title}</h1>
  <Content />
</article>
```

### 6. Sync and validate

After changing collections:

- run `npx astro sync` or the repo’s normal Astro workflow
- fix schema mismatches instead of weakening types
- validate at least one real entry per collection

## Migration Guidance

When migrating from older content patterns:

1. move content into `src/content/<collection>/`
2. create a schema that matches real fields
3. replace broad file-globbing with collection APIs
4. update routes to derive from collection entries

If the project is crossing Astro versions at the same time, verify version-sensitive content APIs in the current official Astro docs before finalizing.
