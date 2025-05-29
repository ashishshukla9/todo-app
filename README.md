Continuous Integration / Continuous Deployment ya Continuous Delivery

🚀 Complete Steps: React App + GitHub + CI/CD (GitHub Actions)

1. Create a New React App
   npx create-react-app

2. Initialize Git Repo & First Commit

   git init
   git add .
   git commit -m "Initial commit"


3. Create GitHub Repo & Push Code


  - GitHub pe jaake new repo banao (e.g. todo-app)

  - Fir terminal me run karo:

    git remote add origin https://github.com/<your-username>/todo-app.git
    git branch -M main
    git push -u origin main


4. Setup homepage in package.json

   Open package.json and add:

   "homepage": "https://<your-username>.github.io/todo-app"


5. Install gh-pages

   Then in package.json, scripts ko update karo:

   "scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
   }

6. Create CI/CD Workflow

   Create folder & file:

   mkdir -p .github/workflows
   touch .github/workflows/deploy.yml

   Aur deploy.yml me ye likho:

   name: Deploy React App to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Build the React app
        run: npm run build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build

7. Set GitHub Actions Permission
   
   Go to:

   Repo → Settings → Actions → General
   ➡️ Scroll to "Workflow permissions"
   ✅ Select: Read and write permissions
   ✅ (Optional but helpful) Enable: "Allow GitHub Actions to create and approve pull requests"

   Click Save ✅

8. Push Workflow to Trigger CI/CD

   git add .
   git commit -m "Add CI/CD workflow"
   git push origin main

9. Check CI/CD Run

   Go to your repo on GitHub → Click Actions tab
   ✅ Check:

   Green tick on latest run

   Step: Deploy to GitHub Pages → success

