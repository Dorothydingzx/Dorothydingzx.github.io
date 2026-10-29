# Dorothy's little world

Source of https://zxding.me — a Jekyll blog (NexT theme) served by GitHub Pages.

## Writing a new post

1. Add a Markdown file to `_posts/` named `YYYY-MM-DD-short-title.md`.
2. Start it with front matter (title, date, categories, tags) — copy any existing post as a template.
3. Put images in `uploads/images/<year>/` and link them as `![](/uploads/images/<year>/name.png)`.
4. Put `<!-- more -->` after the first paragraph to set the preview shown on the home page.
5. Run `./publish.sh` (or `git add -A && git commit -m "New post" && git push`).
