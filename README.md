# GitHub Pages Deployment with GitHub Actions

This repository demonstrates how to deploy a simple "Hello, World!" webpage to GitHub Pages using GitHub Actions.

## Steps to Set Up and Deploy

### 1. Enable GitHub Pages
1. Go to your repository's **Settings > Pages**.
2. Under "Branch", select `gh-pages` (or allow the workflow to create it).
3. Click **Save**.

---

### 2. Create a Personal Access Token (PAT)
A Personal Access Token is needed if the default `GITHUB_TOKEN` doesn't have sufficient permissions (e.g., for private repositories or certain branch restrictions).

#### Steps to Create a PAT:
1. Go to your GitHub account **Settings**.
2. Navigate to **Developer settings > Personal access tokens > Tokens (classic)**.
3. Click **Generate new token**.
4. Select the following scopes:
   - `repo` (for full control of private repositories, if applicable).
   - `workflow` (to manage workflow permissions).
   = `delete_repo` (to delete repositories)
5. Set an expiration date (optional, but recommended).
6. Click **Generate token** and **copy** the token.

---

### 3. Add the Token as a Secret in Your Repository
1. Go to your repository on GitHub.
2. Navigate to **Settings > Secrets and variables > Actions**.
3. Click **New repository secret**.
4. Add a secret with the name `PERSONAL_ACCESS_TOKEN` and paste the PAT you generated.

---

### 4. Update the Workflow
Modify the GitHub Actions workflow to use the PAT for authentication:

```yaml
uses: peaceiris/actions-gh-pages@v3
with:
  personal_token: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
  publish_dir: .
