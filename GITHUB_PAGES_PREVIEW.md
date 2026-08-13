# GitHub Pages Static Preview

This repository now includes a GitHub Actions workflow that publishes a visual-only preview to GitHub Pages whenever changes are pushed to `main`.

## Verified organization links

The project is now owned by the **St-John-s-Hackfinity-2026** GitHub organization. Use these links when sharing or administering the static preview:

| Resource | Link |
|---|---|
| GitHub Pages visual preview | https://st-john-s-hackfinity-2026.github.io/hackfinity-26-pages-preview/ |
| GitHub Pages repository | https://github.com/St-John-s-Hackfinity-2026/hackfinity-26-pages-preview |
| Organization-managed website source | https://github.com/St-John-s-Hackfinity-2026/hackfinity-26-website-source |

## Activate it on GitHub

Open the repository, choose **Settings → Pages**, and select **GitHub Actions** as the publishing source. Then open the **Actions** tab and run **Deploy GitHub Pages Preview** once, or push a commit to `main`. When the workflow finishes, GitHub shows the published URL in the workflow summary and on **Settings → Pages**.

## Important limitation

GitHub Pages hosts static files only. The preview preserves the visual website, animation, countdown, FAQ, prizes, and registration layout, but it deliberately does not submit registrations or provide the organizer dashboard, login, database, live squads count, or Google Sheets sync. Use the full deployed site for those features.

| Feature | GitHub Pages preview | Full deployment |
|---|---|---|
| Website design and motion | Available | Available |
| Countdown and visual form | Available | Available |
| Registration submission | Not available | Available |
| Organizer dashboard | Not available | Available |
| Database and Google Sheets sync | Not available | Available |
