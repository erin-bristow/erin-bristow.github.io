---
layout: post
title:	"Creating Your Jekyll Site and Using Custom Plugins on GitHub Pages"
date:	2022-06-01 
categories: Jekyll
---

This writeup will cover setting up a Jekyll site in GitHub Pages and then (optional!) deploying it with GitHub Actions so you can use custom plugins.

My personal blog website was built using [samarsault's texture theme](https://github.com/samarsault/texture) for [Jekyll](https://jekyllrb.com/). I chose Jekyll because there were many free, minimalist themes that I liked. I also thought that the free GitHub Pages hosting would be easier than dealing with a cPanel backend, but I was most definitely wrong about that - continue reading for a hands-on, involved method of creating a site for your blog! 

## Setting Up Your Site

I won't go into details here because good guides can be easily found online, but I'll link the pages I found most useful. You'll likely want to choose a Jekyll theme before you get started - I found the biggest collection of free ones on [jekyll-themes.com](https://jekyll-themes.com/free/).

### Steps

1. Installation link for Jekyll on Windows via [RubyInstaller](https://jekyllrb.com/docs/installation/windows/).
2. [Guide](https://dev.to/azukacchi/setting-up-github-pages-site-with-jekyll-tutorial-1l60) I used to run Jekyll locally. I did run into some issues with the guide:
	- Silly problem that cost me some time, but when typing ```jekyll new```, you [also need to make a folder to put it in](https://github.com/jekyll/jekyll-help/issues/175), like ```jekyll new blog```.
	- Fixed a problem I ran into when trying to run on localhost: [Stack Overflow post](https://stackoverflow.com/questions/65989040/bundle-exec-jekyll-serve-cannot-load-such-file)
	- When running ```bundle upgrade``` again, I ran an issue where the "bundler could not find compatible versions for gem" and this fixed it: [Stack Overflow post](https://stackoverflow.com/questions/7144846/bundler-could-not-find-compatible-versions-for-gem)
3. Don't remember exactly which of these guides helped me use a custom domain on GitHub Pages (i.e. [https://ebristow.com](https://ebristow.com) not [https://erin-bristow.github.io](https://erin-bristow.github.io)), but think it was one of these: [Medium link](https://hossainkhan.medium.com/using-custom-domain-for-github-pages-86b303d3918a) or [freeCodeCamp link](https://www.freecodecamp.org/news/hosting-custom-domain-on-github-pages-8c598248d2bc/).
4. Deploy with GitHub Actions (see Custom Plugins section). Troubleshooting this was one of the more difficult things I had to do.

### Pre-Requisite Knowledge

You'll need familiarity with Git to successfully create a site on GitHub Pages. Knowing how to pull, push, and commit should be enough, but understanding how branches work is also useful. Commands for viewing all branches (```git branch -a```), switching to another branch (```git checkout <branch>```), and deleting a branch locally (```git branch -d <branch>```) may be needed.

To write posts for your site, you'll want to learn [Markdown](https://www.markdownguide.org/basic-syntax/).

### Other Notes

<img src="/assets/post2jekyllplugins/running-locally.PNG" alt="Showing the command line when running locally"/>

Deploying your Jekyll site locally within a command line:
- If you add a new gem (like ```gem "jekyll-target-blank```) to the Gemfile you'll need to do ```bundle install``` to fetch the new gem
- When you've made changes to ```_config.yml```, you'll need to run ```bundle exec jekyll serve``` again to re-build your site
- If you make changes to a Markdown blog post when running the site locally, you don't need to re-build your site. Just save the markdown file and refresh the locally running site within the browser. In the command line above, see how this blog post "regenerates" when I refresh the browser.

For editing and configuring your site, I recommend referencing the [Jekyll Configuration Docs](https://jekyllrb.com/docs/configuration/).

## Custom Plugins 
I wanted to use custom plugins (notably, [jekyll-target-blank](https://github.com/keithmifsud/jekyll-target-blank)), but GitHub Pages doesn't allow custom plugins by default, citing security concerns.

For more control over your site, including the use of custom plugins, you can deploy your Jekyll site to GitHub Pages with [GitHub Actions](https://jekyllrb.com/docs/continuous-integration/github-actions/). Below are a few issues I ran into when following the linked Jekyll documentation for GitHub Actions. Hopefully this can help you with troubleshooting your own site.

1. After the gh-pages branch is created, you must [switch to the gh-pages branch](https://github.com/jekyll/jekyll/issues/8360#issuecomment-683134170) in the settings for your GitHub Pages repository. 

	<img src="/assets/post2jekyllplugins/point1.PNG" alt="Screenshot of https://github.com/forestryio/jekyll-menus/issues/19#issuecomment-683131856"/>

2. In ```github-pages.yml```, [you need to include](https://github.com/jekyllt/jasper2/issues/122) ```target_branch: gh-pages``` but that's the only line I had to change in the documentation's provided ```github-pages.yml``` file.

	<img src="/assets/post2jekyllplugins/point2.PNG" alt="Screenshot of https://github.com/jekyllt/jasper2/issues/122"/>

3. There can be issues with custom domains. The CNAME record will not be automatically placed in the new gh-pages branch, and you cannot manually create the CNAME record file in the gh-pages branch because it will be overwritten every time your site is rebuilt. In your Jekyll ```_config.xml``` file you need to add ```include: CNAME``` to [force Jekyll to include that record](https://github.com/criptowiki/criptowiki/issues/15#issuecomment-886890153) in the gh-pages branch. 

	<img src="/assets/post2jekyllplugins/point3.PNG" alt="Screenshot of https://github.com/criptowiki/criptowiki/issues/15#issuecomment-886890153"/>

A final note: Even though GitHub pages is now serving your site off of the gh-pages branch and not master, you still need to be pushing to your master branch. When you push to your master branch, GitHub Actions will automatically build the site in the gh-pages branch. Do not edit the gh-pages branch directly because your changes will not persist when your site is rebuilt.