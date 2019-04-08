---
layout: post
title:  "Creating a blog with Jekyll and Github"
---
This blog is made using [Jekyll](https://jekyllrb.com/) and hosted using [Github pages](https://pages.github.com/). You can do it yourself using the [Github Pages Basics](https://help.github.com/en/categories/github-pages-basics) documentation, however as a professional programmer I insist on making things hard for myself so I did it a different way.

The main advantage of doing it my way is that I have a local development environment that is separate from the public site hosted on GitHub so that <strike>my mistakes are made in private</strike> I can experiment locally and only publish content that I consider worth sharing.

## Setup a Ruby development environment

Jekyll is written in Ruby, so you will need to be able to run Ruby to use Jekyll locally. You may already have Ruby available with your operating system, but using the system Ruby has a few drawbacks when using it for development, so lets set up a user install instead.

Install rbenv using [the rbenv install documentation](https://github.com/rbenv/rbenv#installation). I used the GitHub checkout manual method, but do what works for you.

Install ruby-build using [the ruby-build documentation](https://github.com/rbenv/ruby-build#readme). I installed as an rbenv plugin.

Check [https://pages.github.com/versions/](https://pages.github.com/versions/) to see which version of Ruby is required. At time of writing it was version `2.5.3`. Run `rbenv install 2.5.3` to install the required version of ruby. If this step fails then the output from `rbenv install` should tell you how to fix it. I had to run `sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev` to install some missing libraries.

Create a folder to hold your site. To avoid confusion the folder name should match your github username. In my case `mkdir urcheraus`. Don't worry if you haven't created a GitHub account yet - use whatever folder name you want, you can rename the folder later if that account name was taken.

Change into that folder `cd urcheraus` and tell rbenv to use the required version of Ruby in this folder `rbenv local 2.5.3`

Congratulations you have set up a Ruby development environment

## Install Jekyll and generate a site

Ruby libraries are distributed as [gems](https://rubygems.org/). The gems for a project can be managed using [bundler](https://bundler.io/). Run `gem install bundler` to install bundler. Run `gem install github-pages` to install all the dependencies available to Jekyll when built by Github Pages. If this step fails inspect the output to see what went wrong. I had to run `sudo apt install g++` to install a compiler needed for building one of the gems.

Run `jekyll new .` to generate a new site in the current directory.

Edit file `Gemfile` to uncomment (remove the # at the start of the line) the `gem github-pages` line.

Run `bundle exec jekyll serve` to start Jekyll. While this is running you can view ithe generated site at [http://localhost:4000/](http://localhost:4000/)

## Customise your site and write some content

The generated site includes instructions on which files provide which content, but you should start with:

- **`_config.yml`** - To set the title, description, and social links. Set `baseurl` to `yourreponame/` otherwise your site won't load properly on GitHub.
- **`about.md`** - To write the about page.
- **The markdown file in `_posts/`** - This will be your first blog post.

You will need to stop and re-run `bundle exec jekyll serve` to see changes in `_config.yml`, but reloading the page is enough to see changes to the other files.

## Put it on Github

If you don't have an account on [GitHub](https://github.com/) go and create one. You account name will be part of the URL of your blog (unless you pay for a custom domain), so choose wisely.

Make a repository with the same name as your account, in my case `urcheraus`.

In your site directory (which you should rename if it doesn't match your GitHub account and repository name) run:

- `git init` to make the directory into a git repository.
- `git add .` To tell git you care about all the files in the current directory.
- `git commit -m 'OMG my first blog post'` (with a meaningful commit message) to "commit" your changes.
- `git remote add origin git@github.com:urcheraus/urcheraus.git` (with your repository URL) to tell git that you want to be able to send (and receive) commits to GitHub.
- `git push -u origin master` to send your commit to GitHub.

On github.com go to your repositories settings page and set the GitHub pages source to your master branch.

That's it. Your site is now available at https://reponame.github.io/reponame/

If the text of your site loads but the style is broken and none of the links work then you probably forgot to set the `basename` to `reponame/` in `_config.yml`.

## Blog more

To make another blog post create a file in `_posts/` named YYYY-MM-DD-this-is-the-post-url.markdown (with the current date and the name of your post). Add your post with `git add .`. Commit with `git commit -m 'YAFP (Yet Another Fine Post)'`. Send it to GitHub with `git push master`.

## Next steps

Write more blog posts. Share them on social media. Bask in the glory. Tweet at me to let me know how much you like my guide.

Have a look at the [Jekyll documentation](https://jekyllrb.com/docs/) to see what else you can change about your site (hint: everything). Try the [GitHub Pages Basics](https://help.github.com/en/categories/github-pages-basics) documentation to see what you can change about how your site is hosted (hint: not so much).

But above all else: have fun.
