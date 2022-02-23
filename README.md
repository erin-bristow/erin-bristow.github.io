# erin-bristow.github.io

Personal blog/resume website using samarsault's texture theme for Jekyll.

https://jekyllrb.com/docs/configuration/

###Note on Custom Plugins 
I wanted to use custom plugins (notably, [jekyll-target-blank](https://github.com/keithmifsud/jekyll-target-blank)), but GitHub Pages doesn't allow custom plugins by default, citing security concerns.
For more control over your site, including the use of custom plugins, you can deploy your Jekyll site to GitHub Pages with [GitHub Actions](https://jekyllrb.com/docs/continuous-integration/github-actions/). Below are a few troubleshooting issues I ran into when following the Jekyll documentation for GitHub Actions.
1. After the gh-pages branch is created, you must [switch to the gh-pages branch](https://github.com/jekyll/jekyll/issues/8360#issuecomment-683134170) in the settings for your GitHub Pages repository.
2. In github-pages.yml, [you need to include](https://github.com/jekyllt/jasper2/issues/122) '''target_branch: gh-pages''' but that's the only line I had to change in the documentation's provided github-pages.yml file.
3. 


A final note: Even though GitHub pages is now serving your site off of the gh-pages branch and not master, you still need to be pushing to your master branch. When you push to your master branch, GitHub Actions will automatically build the site in the gh-pages branch. Do not edit the gh-pages branch directly.
