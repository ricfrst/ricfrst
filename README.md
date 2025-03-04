[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=ricfrst&theme=radical)](https://github.com/anuraghazra/github-readme-stats)



                      
                      
  name: generate monkeytype readme svg
    
   on:
    schedule:
        - cron: "0 */6 * * *" # every 6 hours
    workflow_dispatch:
    
  jobs:
    download-svg:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
            uses: actions/checkout@v3
          - name: Set up Node.js
            uses: actions/setup-node@v3
            with:
            node-version: '16.x'
        - name: Download SVG
            run: |
            mkdir public
            curl -o public/monkeytype-readme.svg https://monkeytype-readme.com/generate-svg/rfurst/bento
            curl -o public/monkeytype-readme-lb.svg https://monkeytype-readme.com/generate-svg/rfurst/bento?lb=true
            curl -o public/monkeytype-readme-pb.svg https://monkeytype-readme.com/generate-svg/rfurst/bento?pb=true
            curl -o public/monkeytype-readme-lb-pb.svg https://monkeytype-readme.com/generate-svg/rfurst/bento?lbpb=true
        - name: push monkeytype-readme.svg to the monkeytype-readme branch
            uses: crazy-max/ghaction-github-pages@v2.5.0
            with:
            target_branch: monkeytype-readme
            build_dir: public
            env:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
                
