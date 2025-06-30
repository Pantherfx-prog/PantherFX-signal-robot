name: Build and Deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [20.x]

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}

      # Build frontend
      - name: Install frontend dependencies
        working-directory: ./frontend
        run: npm install

      - name: Build frontend
        working-directory: ./frontend
        run: npm run build

      # Build backend
      - name: Install backend dependencies
        working-directory: ./backend
        run: npm install

      # You can add backend build steps here if needed

      # Deploy frontend to Vercel (optional)
      # Uncomment and configure the following if you use Vercel
      # - name: Deploy to Vercel
      #   uses: amondnet/vercel-action@v25
      #   with:
      #     vercel-token: ${{ secrets.VERCEL_TOKEN }}
      #     vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
      #     vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
      #     working-directory: ./frontend
      #     prod: true

      # Deploy frontend to Netlify (optional)
      # Uncomment and configure the following if you use Netlify
      # - name: Deploy to Netlify
      #   uses: nwtgck/actions-netlify@v3.0
      #   with:
      #     publish-dir: ./frontend/build
      #     production-deploy: true
      #     github-token: ${{ secrets.GITHUB_TOKEN }}
      #     deploy-message: "Deployed from GitHub Actions"
      #     netlify-auth-token: ${{ secrets.NETLIFY_AUTH_TOKEN }}
      #     netlify-site-id: ${{ secrets.NETLIFY_SITE_ID }}

      # Add your backend deploy step here (e.g. Render, Railway, Heroku)
      # See provider docs for GitHub Actions deploy steps# PantherFX-signal-robot
