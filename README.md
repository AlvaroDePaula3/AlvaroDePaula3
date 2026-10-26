![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=AlvaroDePaula3&layout=compact&theme=dracula)


![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

name: Generate Snake



on:

  schedule:

    - cron: "0 0 * * *" # Roda todos os dias à meia-noite (UTC)

  workflow_dispatch: # Permite rodar manualmente



jobs:

  generate:

    runs-on: ubuntu-latest

    timeout-minutes: 10

    permissions:

      contents: write

    

    steps:

      - name: Generate snake SVG

        uses: Platane/snk@v3

        with:

          github_user_name: ${{ github.repository_owner }}

          outputs: |

            dist/github-snake.svg

            dist/github-snake-dark.svg?palette=github-dark

            

      - name: Push to output branch

        uses: crazy-max/ghaction-github-pages@v4

        with:

          target_branch: output

          build_dir: dist

        env:

          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
