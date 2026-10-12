# Manifesto page

This folder is a small static blog/manifesto for `https://mobneutralizer.com/manifesto/`.

- `index.html` displays the entries and the comment area.
- `posts.json` contains your entries. Add a new object to the `posts` array to publish another post.
- The site reads the JSON in the browser; you do not need to edit the HTML when adding posts.

## Add a post

Open `posts.json` and add a post object inside the `posts` array. Example:

```json
{
  "posts": [
    {
      "title": "A First Principle",
      "slug": "a-first-principle",
      "date": "2026-10-11",
      "category": "Principles",
      "excerpt": "A short summary shown in the entry list.",
      "content": "This is the first paragraph of the post.\n\nA second paragraph. Markdown is supported.\n\n## A heading\n\n- One point\n- Another point\n\n**Bold**, *italic*, and `inline code` all work.\n\n> A blockquote.\n\n[An external link](https://example.com)"
    }
  ]
}
```

You can add multiple objects separated by commas. The site displays newest dates first and gives every post a link like `https://mobneutralizer.com/manifesto/#a-first-principle`.

### Fields

- `title` — required, displayed heading.
- `slug` — required, unique, lowercase URL-safe ID. Use letters, numbers, and hyphens only, such as `why-i-build-things`.
- `date` — recommended, use `YYYY-MM-DD`.
- `category` — optional, such as `Politics`, `Technology`, or `Personal`.
- `excerpt` — optional short description shown in the index.
- `content` — required post body, written as a JSON string. Use `\n\n` for paragraph breaks and escape any literal quotation marks as `\"`.

The Markdown renderer supports headings (`##` to `####`), paragraphs, line breaks, unordered and ordered lists, blockquotes, horizontal rules, fenced code blocks, links, bold, italics, strikethrough, and inline code. Raw HTML is escaped for safety.

**JSON reminder:** Every post except the last needs a comma after its closing `}`. JSON does not allow comments or trailing commas.

## Enable comments (one-time setup)

The page uses [Giscus](https://giscus.app/), a free comments widget backed by GitHub Discussions. Commenters need a GitHub account and must authorize Giscus. Comments can then be moderated in your repository's Discussions. GitHub Pages itself is static and cannot save comments directly.

1. Make sure the GitHub repository hosting your site is **public**.
2. In that repository, go to **Settings → General → Features** and enable **Discussions**.
3. Install the [Giscus GitHub App](https://github.com/apps/giscus) and grant it access to the website repository.
4. Open [giscus.app](https://giscus.app/). Select your website repository, choose the Discussion category you want to use for comments, and configure the widget. A category named `Comments` is a sensible choice if you create one in Discussions.
5. Copy the four values `data-repo`, `data-repo-id`, `data-category`, and `data-category-id` that Giscus generates.
6. Open `index.html` and find `const GISCUS_CONFIG` near the beginning of its JavaScript. Replace the four placeholder values with the values from Giscus. The `repo` must be in `OWNER/REPOSITORY` format; the other IDs must be copied exactly.
7. Commit and deploy the changes.

The code uses a distinct Giscus discussion term (`manifesto-<slug>`) for each post. That lets every entry have its own comments thread. The first comment or reaction on an entry can trigger creation of its matching discussion. Test with one post first.

Until Giscus is configured, posts work normally and the comments area shows setup instructions. Do not put GitHub tokens or other secrets into this file; the Giscus IDs are public configuration values, not passwords.
