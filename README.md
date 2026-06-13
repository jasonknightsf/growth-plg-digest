# Growth & PLG Intelligence Digest

A fully automated daily digest of the best product-led growth content on the internet — articles, podcasts, and Substack posts — curated by AI and deployed to a live site every morning.

**Live site:** [growth-plg-digest.vercel.app](https://growth-plg-digest.vercel.app)

---

## What it does

Every morning at 8:00 AM, an AI agent runs 22 targeted searches across top PLG publications (Lenny's Newsletter, OpenView, Reforge, Kyle Poyar, a16z, and more), categorizes the results, and generates a fresh `index.html`. Twenty minutes later, the file is automatically pushed to GitHub, triggering a Vercel deploy.

No manual steps. No CMS. No backend.

---

## Stack

- **AI agent** — Claude (Claude Code scheduled task) generates and writes the HTML
- **Content** — Web search across articles, podcasts/YouTube, and Substack
- **Hosting** — Vercel, auto-deployed on every push to `main`
- **Automation** — macOS LaunchAgent triggers the GitHub push at 8:20 AM

---

## Pipeline

```
8:00 AM  Claude agent runs -> writes index.html
8:20 AM  LaunchAgent (push-digest.sh) commits & pushes to GitHub
~8:22 AM Vercel detects push -> deploys updated site
```

---

## Repo structure

```
index.html          # The digest -- regenerated daily by the AI agent
push-digest.sh      # Shell script: commits and pushes index.html to GitHub
com.jasonknight.plg-digest-push.plist  # macOS LaunchAgent definition
setup-push-digest.command              # One-time setup script for the LaunchAgent
```

---

## Content categories

| Tab | What's in it |
|-----|-------------|
| PLG Strategy | Product-led growth frameworks and case studies |
| Onboarding & UX | Time-to-value, activation, and UX patterns |
| Conversion & PQLs | Free trial conversion, PQL definitions, benchmarks |
| Growth Loops | Flywheels, virality, and compounding growth |
| Podcasts & Video | Episodes from Lenny's, Growth Unhinged, SaaStr, YouTube |
| Substack | Posts from Elena Verna, Aakash Gupta, Kyle Poyar, and others |

---

## Local setup

1. Clone the repo
2. Run `setup-push-digest.command` to install and load the LaunchAgent
3. Ensure the Claude Code scheduled task `daily-growth-plg-digest` is active
4. Verify your GitHub remote is set and authenticated

The LaunchAgent only pushes if `index.html` has changed, so there's no noise on days the agent doesn't run.
