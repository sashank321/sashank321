# Sashank's Profile Repository Setup Guide

This guide details the repository structure, automation instructions, and GitHub secret configurations required to make your premium profile live.

---

## 📂 Repository Structure

Your profile repository is set up with the following production-ready layout:

```text
sashank321/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   └── config.yml             # Directs general networking/questions to LinkedIn
│   ├── profile/
│   │   └── github-metrics.svg     # Compiled Developer Metrics SVG (workflow output)
│   ├── workflows/
│   │   ├── metrics.yml            # Automates developer stats collation (runs 12h)
│   │   └── snake.yml              # Automates contribution snake generation (runs daily)
│   └── FUNDING.yml                # Optional Sponsorship configs
├── assets/
│   ├── background.svg             # Abstract geometric vector graphic
│   ├── banner.svg                 # Spotlight banner with centered typography
│   ├── divider.svg                # Minimal cubic Bezier wave divider
│   └── footer.svg                 # Signature footer card
├── icons/
│   ├── ai.svg                     # Custom monochrome Artificial Intelligence icon
│   ├── dsa.svg                    # Custom monochrome Data Structures & Algorithms icon
│   ├── fullstack.svg              # Custom monochrome Full Stack Development icon
│   └── ui.svg                     # Custom monochrome UI Engineering icon
├── LICENSE                        # MIT License
├── README.md                      # Redesigned premium landing page profile
└── SETUP.md                       # Setup and automation instructions (this file)
```

---

## 🔑 GitHub Secret Configuration

To automate the compilation of stats via **GitHub Metrics (`metrics.yml`)**, you must configure a Personal Access Token (PAT). The default `GITHUB_TOKEN` does not have sufficient permissions to query external user statistics across all your repositories.

### Step 1: Generate a Personal Access Token (Classic)
1. Go to your GitHub profile settings: Click your profile picture (top-right) -> **Settings**.
2. Scroll to the bottom of the sidebar and click **Developer settings**.
3. Select **Personal access tokens** -> **Tokens (classic)**.
4. Click **Generate new token** -> Select **Generate new token (classic)**.
5. Configure the token details:
   - **Note**: `GitHub Metrics Token - Profile`
   - **Expiration**: Select either 90 days or *No expiration* (if you do not want to rotate it).
   - **Scopes**: Select the following checkboxes:
     - [x] **repo** (all options: repo:status, repo_deployment, public_repo, etc.)
     - [x] **read:user**
     - [x] **read:org**
6. Click **Generate token** (at the bottom) and **copy the generated token immediately**. (You will not be able to see it again).

### Step 2: Add Token to Repository Secrets
1. Navigate to your profile repository: `https://github.com/sashank321/sashank321`.
2. Go to **Settings** (top tab bar).
3. In the left sidebar under *Security*, expand **Secrets and variables** and click **Actions**.
4. Click **New repository secret** (green button, top right).
5. Input the following configuration:
   - **Name**: `METRICS_TOKEN`
   - **Secret**: Paste the Personal Access Token you copied in Step 1.
6. Click **Add secret**.

---

## ⚙️ Workflow Permissions

To allow the automation workflows to push the compiled graphics back into your repository, you need to ensure the action runners have read/write access.

1. In your repository settings, go to the left sidebar and click **Actions** -> **General**.
2. Scroll down to the **Workflow permissions** section.
3. Select **Read and write permissions**.
4. Click **Save**.

---

## 🚀 Triggering Workflows for the First Time

Although the workflows are scheduled to run automatically (Metrics every 12 hours, Snake daily at midnight), you can force-trigger them immediately to render your live stats right away.

1. Go to your repository `sashank321/sashank321` on GitHub.
2. Select the **Actions** tab.
3. In the left sidebar:
   - Click **GitHub Metrics** -> Click the **Run workflow** dropdown on the right -> Click the green **Run workflow** button.
   - Click **Generate Contribution Snake** -> Click the **Run workflow** dropdown on the right -> Click the green **Run workflow** button.
4. After a few minutes, the workflows will complete successfully:
   - The **GitHub Metrics** workflow will save the updated file at `.github/profile/github-metrics.svg` on your `main` branch.
   - The **Contribution Snake** workflow will create a new branch named `output` containing `github-contribution-grid-snake-dark.svg`.

Once these run, your profile will reflect your real-time developer statistics and a beautiful monochrome contribution snake!
