
yaml
learning:
  - Advanced React Patterns
  - Backend API Design Best Practices
building:
  - Personal Full Stack Web Application
exploring:
  - New Frontend and Backend Frameworks
openTo:
  - Full Stack / Frontend / Backend Developer Roles
name: Daily Profile README Update

on:
  schedule:
    - cron: '0 0 * * *' # runs daily at 00:00 UTC (change if needed)
  workflow_dispatch:

permissions:
  contents: write

jobs:
  update-readme:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          persist-credentials: true

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: pip install --upgrade pip openai requests

      - name: Run README updater
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }} # optional, required only if you want AI-generated content
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: python scripts/update_readme.py
