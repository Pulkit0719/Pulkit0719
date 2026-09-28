# GitHub Profile Automation & Maintenance Guide

This document details the automated architecture, visual generators, and GitHub Actions workflows powering the **Pulkit0719** developer profile.

---

## 🛠️ Automated Workflows

All workflows are located in `.github/workflows/` and run on Ubuntu GitHub runners using standard least-privilege tokens (`contents: write`).

| Workflow | File | Daily Schedule (UTC) | Purpose | Output Directory / Branch |
| :--- | :--- | :---: | :--- | :--- |
| **Profile 3D Contrib** | `profile-3d.yml` | `00:30 UTC` | Generates 3D isometric GitHub contribution calendars (night, green, seasonal, rainbow). | `profile-3d-contrib/` on `main` |
| **Snake Animation** | `snake.yml` | `01:00 UTC` | Generates animated SVG snake eating contribution dots using `Platane/snk/svg-only@v3`. | `dist/`, `output/` on `main` & `output` branch |
| **Pac-Man Arcade** | `pacman.yml` | `02:00 UTC` | Generates arcade Pac-Man eating contribution dots via `abozanona/pacman-contribution-graph`. | `dist/`, `output/` on `main` & `pacman` branch |
| **GitArtwork** | `gitartwork.yml` | `03:00 UTC` | Generates animated text raster "PULKIT" from contributions via `jasineri/gitartwork`. | `gitartwork.svg` on `main` |
| **Profile Analytics** | `profile-update.yml` | `04:00 UTC` | Generates comprehensive profile stats, top languages, and activity cards via `lowlighter/metrics`. | `metrics/` on `main` |

> [!NOTE]
> All workflows are scheduled 30–60 minutes apart to prevent concurrent Git push collisions and merge conflicts. Each workflow performs `git pull --rebase` prior to committing.

---

## 🚀 Manual Regeneration (Workflow Dispatch)

Every workflow supports manual execution at any time:
1. Navigate to **Actions** tab in your repository: [GitHub Actions](https://github.com/Pulkit0719/Pulkit0719/actions).
2. Select the workflow you wish to run from the left sidebar (e.g., *Generate Snake Game from GitHub Contribution Grid*).
3. Click the **Run workflow** dropdown button.
4. Select `Branch: main` and click **Run workflow**.

---

## 🎨 Asset Structure & Files

- **`images/`**:
  - `header.svg`: Main hero banner with CSS gradient animation and glowing badges.
  - `header2.svg`, `profile-banner-wide.svg`: Alternative banner variants.
  - `education.svg`: Academic credentials card (PSIT Kanpur, B.Tech).
  - `certificates.svg`: Verified credentials card (Google, IBM, Coursera).
  - `clock.svg`: Pure SVG CSS keyframe-animated analog clock.
  - `animated-waves.svg`: Smooth wave divider with morphing path keyframes.
- **`profile-3d-contrib/`**:
  - `profile-night-view.svg`: Primary dark-mode 3D contribution matrix.
  - `profile-green-animate.svg`: Animated emerald green isometric view.
  - `profile-night-rainbow.svg`: Rainbow colorway.
  - `profile-season-animate.svg`: Seasonal animation.
- **`dist/` & `output/`**:
  - `github-snake-darkBlue.svg`: Dark theme snake animation with electric blue serpent.
  - `github-snake.svg`, `github-snake-dark.svg`: Standard snake variants.
  - `pacman-contribution-graph-dark.svg`: Dark mode Pac-Man arcade.
  - `pacman-contribution-graph.svg`: Light mode Pac-Man arcade.
- **`metrics/`**:
  - `githubstats.svg`: Detailed profile metrics scorecard.
  - `toplangs.svg`: Most-used language breakdown.
  - `activity.svg`: Recent contribution activity log.
- **Root**:
  - `gitartwork.svg`: Contribution text artwork spelling "PULKIT".

---

## 🔐 Required Repository Permissions

For scheduled workflows to commit automatically back to the repository:
1. Go to repository **Settings** -> **Actions** -> **General**.
2. Under **Workflow permissions**, choose **Read and write permissions**.
3. Check the box **Allow GitHub Actions to create and approve pull requests**.
4. Click **Save**.

---

## 🔌 Optional Integrations (WakaTime / Spotify)

If you ever wish to enable optional widgets:
- **WakaTime**: Obtain your API key from [WakaTime](https://wakatime.com/settings/api-key) and add it to repository **Settings** -> **Secrets and variables** -> **Actions** -> **New repository secret** as `WAKATIME_API_KEY`.
- **Spotify**: Configure your Spotify client ID/secret to display currently playing tracks via `spotify-github-profile`.
*(Both integrations remain cleanly omitted until you configure credentials).*
