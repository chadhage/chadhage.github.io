# Chad Hage's Microsite

A small, responsive personal homepage for **<https://chadhage.github.io/>**.
Plain HTML and CSS, with a small script to select the color theme. No package
manager, build step, or local server is required.

## Preview

Open [site/index.html](site/index.html) in your browser. On Windows, from the
repository directory:

```powershell
Start-Process .\site\index.html
```

The page follows your operating system's light/dark preference on load. Append
`?clawpilotTheme=light` or `?clawpilotTheme=dark` to the page URL to preview either
theme. The avatar loads from GitHub and requires an internet connection; the
rest of the page works offline.

## Publish

**The GitHub repository must be named `chadhage.github.io` and owned by
`chadhage` to serve the root URL `https://chadhage.github.io/`.** A repository
named `chadhage` would normally publish to `https://chadhage.github.io/chadhage/`
instead. The local folder can remain named `chadhage`.

1. While signed in as `chadhage`, create a **public**, empty repository named
   `chadhage.github.io` on GitHub. Do not initialize it with a README, license,
   or gitignore. If that repository already exists, inspect its contents before
   connecting this folder; do not overwrite an existing site or force-push.
2. This local repository currently has no remote or commits. From its root,
   commit the site and connect the new empty repository:

   ```powershell
   git add site .github README.md
   git commit -m "Add personal microsite and GitHub Pages deployment"
   git remote add origin https://github.com/chadhage/chadhage.github.io.git
   git push -u origin main
   ```

3. In the GitHub repository, open **Settings > Pages**. Under **Build and
   deployment**, set **Source** to **GitHub Actions**. No custom domain or DNS
   changes are needed.
4. Open **Actions > Deploy GitHub Pages > Run workflow**, select `main`, and
   run it. The initial push may fail if Pages was not enabled yet; running the
   workflow after step 3 resolves that prerequisite.
5. Wait for the build and deploy jobs to succeed, then visit
   **<https://chadhage.github.io/>**. First publication may take up to 10 minutes.

After this one-time setup, every push to `main` republishes the site. Manual
runs are also available. Nothing has been committed, pushed, or published by
the local setup itself.

## Customize

- Edit the name, intro, links, and styles in [site/index.html](site/index.html).
- The current image is your GitHub avatar. Replace its URL with a relative
  image path under `site/` to host a photo yourself.
- Put additional public pages and assets inside `site/`. Use relative links
  for local previews and portable hosting.
- Update the canonical URL and Open Graph metadata if the site's address changes.

The [Pages workflow](.github/workflows/pages.yml) publishes only `site/`, not
this README or repository configuration. Everything inside `site/` is public;
never put credentials or private material there. The `.nojekyll` marker also
allows these files to be served without Jekyll processing.

## Project Gallery

The homepage's **Projects & experiments** link opens
[site/projects.html](site/projects.html). The gallery is static HTML: its cards
and navigation work without JavaScript, a server, or GitHub API requests.

The initial catalog contains 17 public projects, including the microsite.
The separate GitHub profile repository is excluded to avoid duplicating the
microsite. Titles and summaries were curated from the public sites and
repositories on September 21, 2026; new repositories are not added automatically.

To add a project, duplicate an `<article class="project">` in the gallery and
update its heading, description, GitHub Pages URL, and repository URL. Give the
heading a unique `id`, use that value in the article's `aria-labelledby`, and
update both link labels to identify the project. Keep one card per project.
For a project with no published Pages site, use the existing `unpublished`
text pattern instead of a placeholder link. Replace it with a real link once
the site is published.

Open either HTML file directly to preview. The existing Pages workflow already
publishes the gallery because it uploads all of `site/`. To publish future
committed updates to the configured website remote, use `git push pages main`.

## Checks

Before publishing, open the page at desktop and narrow mobile widths, check
both themes, confirm the GitHub links and avatar load, and use Tab to check
keyboard focus and the skip link. No dependency installation is needed.

Follow **Projects & experiments**, check the gallery at desktop and mobile
widths, and use **Home** to return. Verify each card's two destinations (or its
unpublished label), both color themes, and keyboard focus on every link.

If the published URL returns 404, verify the repository name and owner, confirm
that Pages uses **GitHub Actions**, and inspect the latest workflow run. The
deployment artifact must contain `index.html` at its root, which the supplied
workflow achieves by uploading `site/` directly.
