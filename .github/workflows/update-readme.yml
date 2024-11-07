name: Update README Stats

on:
  schedule:
    - cron: '0 0 * * *'  # Runs daily at midnight UTC
  workflow_dispatch:       # Allows manual triggering

jobs:
  update-readme:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Fetch Top Languages SVG
        env:
          ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
        run: |
          curl -o top-langs.svg -L "https://github-readme-stats.vercel.app/api/top-langs?username=suyashwaghmare&show_icons=true&layout=compact&theme=radical&token=${{ secrets.ACCESS_TOKEN }}"

      - name: Fetch GitHub Stats SVG
        env:
          ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
        run: |
          curl -o github-stats.svg -L "https://github-readme-stats.vercel.app/api?username=suyashwaghmare&show_icons=true&theme=radical&token=${{ secrets.ACCESS_TOKEN }}"

      - name: Update README with latest stats
        run: |
          sed -i '/<!-- Top Languages Start -->/,/<!-- Top Languages End -->/c\![Top Languages](top-langs.svg)' README.md
          sed -i '/<!-- GitHub Stats Start -->/,/<!-- GitHub Stats End -->/c\![GitHub Stats](github-stats.svg)' README.md
          git add README.md
          git commit -m "Update README with latest stats"
          git push
