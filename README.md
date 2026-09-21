<div align="center">

# 🌐 The Modern Web Triad: A Developer's Blog
### Content-First Technical Publishing Engine Built on Astro

[![Astro](https://img.shields.io/badge/Astro-5.0+-FF5D01?style=for-the-badge&logo=astro&logoColor=white)](https://astro.build)
[![Markdown](https://img.shields.io/badge/Content-MDX_&_Markdown-083344?style=for-the-badge&logo=markdown&logoColor=white)](https://mdxjs.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![Lighthouse Score](https://img.shields.io/badge/Lighthouse-100%2F100-00CC66?style=for-the-badge&logo=lighthouse&logoColor=white)](https://pagespeed.web.dev/)

<br />

<p align="center">
  <b>An ultra-performant, zero-JavaScript-by-default publication dedicated to mastering the building blocks of the web: HTML5, CSS3, and Modern JavaScript.</b>
  <br />
  Designed for readability, technical precision, and sub-second load times using Astro's Content Collections.
</p>

[Explore Pillars](#-the-three-pillars) • [Screenshots](#-visual-walkthrough) • [Content Architecture](#-content-collections-architecture) • [Getting Started](#-getting-started)

---

</div>

## 📖 About the Publication

**The Modern Web Triad** was created to bring focus back to the fundamental cornerstones of the open web. Rather than chasing ephemeral framework trends, this publication provides deep technical dives, interactive recipes, and best practices for:

1. **Semantic & Accessible HTML**
2. **Modern Layouts & Next-Gen CSS**
3. **Vanilla ECMAScript & Browser APIs**

Harnessing **Astro's static compilation**, every single article renders to clean, static HTML without client-side hydration unless strictly requested—achieving a flawless 100/100 Lighthouse performance rating across all metrics.

---

## 🏛 The Three Pillars

| Pillar | Focus Areas | Key Topics Covered |
| :--- | :--- | :--- |
| **🏗️ Semantic HTML** | Structure & Standards | Custom Elements, Web Accessibility (ARIA/WCAG), Microformats, Web Components |
| **🎨 Modern CSS** | Visual Architecture | Grid & Subgrid, Container Queries, Color Spaces (`oklch`), Cascading Layers (`@layer`) |
| **⚡ Native JavaScript** | Execution & Web APIs | ESNext Syntax, Async Patterns, Streams API, Mutation/Intersection Observers |

---

## 📸 Visual Walkthrough

### 1. The Publication Index (Home & Featured Feed)
*A clutter-free landing dashboard presenting curated weekly deep dives and reading-time estimations.*

<div align="center">
  <br />
  <!-- IMAGE SLOT 1: REPLACE WITH YOUR HOME / HERO SCREENSHOT -->
  <img src="/public/interfaz_principal.png" alt="Blog Homepage and Featured Post Feed" width="90%" style="border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.12); box-shadow: 0 20px 40px -15px rgba(255, 93, 1, 0.25);" />
  <p><sub><b>Figure 1:</b> The home feed showing categorised post chips for HTML, CSS, and JS alongside dark mode toggles.</sub></p>
  <br />
</div>

---

### 2. Article Reader View (Typography & Code Blocks)
*Distraction-free reading experience enhanced with Shiki syntax highlighting and interactive copy buttons.*

<div align="center">
  <br />
  <!-- IMAGE SLOT 2: REPLACE WITH YOUR ARTICLE VIEW SCREENSHOT -->
  <img src="/public/uso_menu.png" alt="Article Reading View with Syntax Highlighting" width="90%" style="border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.12); box-shadow: 0 20px 40px -15px rgba(0, 122, 204, 0.25);" />
  <p><sub><b>Figure 2:</b> Deep reading mode showcasing responsive typography, code highlighting, and auto-generated Table of Contents.</sub></p>
  <br />
</div>

---

### 3. Interactive Topic Explorer & Tag Filtering
*Instantaneous client-side filtering letting developers navigate posts by difficulty level, syntax tags, and specs.*

<div align="center">
  <br />
  <!-- IMAGE SLOT 3: REPLACE WITH YOUR SEARCH / FILTER SCREENSHOT -->
  <img src="/public/Individual.png" alt="Topic Filter and Search Screen" width="90%" style="border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.12); box-shadow: 0 20px 40px -15px rgba(56, 178, 172, 0.25);" />
  <p><sub><b>Figure 3:</b> The real-time tag index filtering entries by category (`#html`, `#css-grid`, `#esmodules`).</sub></p>
  <br />
</div>

---

## 📂 Content Collections Architecture

Astro's built-in **Content Collections** provide type-safe frontmatter validation powered by `zod`.

```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string().max(80),
    description: z.string(),
    pillar: z.enum(['HTML', 'CSS', 'JavaScript']),
    tags: z.array(z.string()),
    publishDate: z.date(),
    readingTime: z.string(),
    draft: z.boolean().default(false),
  }),
});

export const collections = { blog };
```

### Static Page Generator Pattern

```astro
---
// src/pages/blog/[...slug].astro
import { getCollection } from 'astro:content';
import PostLayout from '../../layouts/PostLayout.astro';

export async function getStaticPaths() {
  const posts = await getCollection('blog', ({ data }) => !data.draft);
  return posts.map(post => ({
    params: { slug: post.slug },
    props: { post },
  }));
}

const { post } = Astro.props;
const { Content, headings } = await post.render();
---

<PostLayout frontmatter={post.data} headings={headings}>
  <Content />
</PostLayout>
```

---

## ⚡ Performance Highlights

- **0kB JavaScript default bundle** for purely informational articles.
- **Pre-computed RSS feed & XML sitemaps** generated upon every build.
- **Native responsive images** using Astro's `<Image />` component with automated WebP/AVIF conversions.
- **Built-in open graph banner generation** for seamless sharing on social media.

---

## 🚀 Getting Started

### Local Setup

1. **Clone the project:**
   ```bash
   git clone https://github.com/your-username/web-dev-triad-blog.git
   cd web-dev-triad-blog
   ```

2. **Install project dependencies:**
   ```bash
   npm install
   ```

3. **Start the local Astro server:**
   ```bash
   npm run dev
   ```

4. **Add a new article:**
   Create a new `.md` or `.mdx` file under `src/content/blog/`:
   ```markdown
   ---
   title: "Mastering CSS Container Queries"
   description: "Write truly modular UI components independent of viewport widths."
   pillar: "CSS"
   tags: ["css", "responsive", "webdev"]
   publishDate: 2026-09-20
   readingTime: "6 min read"
   ---

   # Deep dive into @container...
   ```

---

## 📜 License

Distributed under the **MIT License**. Refer to [LICENSE](LICENSE) for terms and permissions.
