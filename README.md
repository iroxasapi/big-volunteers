# Deploying to GitHub Pages

1. Create a repo (e.g. `big-volunteers`) and push these files, keeping this structure:
   ```
   index.html
   volunteers.html
   css/site.css
   images/  (add your volunteer photos here, e.g. images/MariaChasapi.png)
   ```
2. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
3. Your site goes live at `https://<username>.github.io/<repo-name>/`
   (or `https://<username>.github.io/` if the repo is named `<username>.github.io`).

## What changed from the .NET project
- Removed all Razor syntax (`@page`, `@model`, `asp-page`, `RenderBody`, etc.) — GitHub Pages
  only serves static HTML/CSS/JS, it can't run C#.
- `_Layout.cshtml` had no static equivalent, so its header/footer markup is now duplicated
  directly inside `index.html` and `volunteers.html`.
- The `@foreach` loops over volunteer data in `Volunteers.cshtml` are unrolled into plain
  static `<div>` cards.
- The "Request to Join" form used `method="post"` to a C# handler, which can't run here.
  It now links out to the same Google Form (`forms.gle/...`) already used for "Join Us"
  elsewhere on the site. If you'd rather keep a real embedded form, a service like
  Formspree or Google Forms embed can capture submissions from a static page.
- Dropped the jQuery/Bootstrap `<script>` includes from the layout — nothing in the markup
  actually uses Bootstrap components or jQuery, only the vanilla-JS mobile nav toggle, which
  is kept.
- `asp-append-version="true"` cache-busting was removed (no build step to generate it);
  add `?v=1` manually to `css/site.css` if you want a similar effect after updates.

You'll need to add your own volunteer photos into `images/` with the exact filenames
referenced in `volunteers.html` (e.g. `EleniAplakidou.png`).
