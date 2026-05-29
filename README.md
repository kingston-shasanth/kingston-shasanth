name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"   # runs every 12 hours
  workflow_dispatch:           # allows manual trigger

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark&color_snake=00AEEF&color_dots=0d1117,0d2a4a,0d4a8a,0078D4,00AEEF

      - uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
