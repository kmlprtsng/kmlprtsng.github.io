Use [prose.io](http://prose.io/) to add or edit files instead of doing it directly on GitHub, it can be a little easier that way.

#### Letting users leave comments

If you want to enable comments on your site, Beautiful Jekyll supports the [Disqus](https://disqus.com/) comments plugin.  To use it, simply sign up to Disqus and add your Disqus shortname to the `disqus` parameter in the `_config.yml`.

If the `disqus` parameter is set in the configuration file, then all blog posts will have comments turned on by default. To turn off comments on a particular blog post, add `comments: false` to the YAML front matter. If you want to add comments on the bottom of a non-blog page, add `comments: true` to the YAML front matter.

#### Adding Google Analytics to track page views

Beautiful Jekyll lets you easily add Google Analytics to all your pages. This will let you track all sorts of information about visits to your website, such as how many times each page is viewed and where (geographically) your users come from.  To add Google Analytics, simply sign up to [Google Analytics](http://www.google.com/analytics/) to obtain your Google Tracking ID, and add this tracking ID to the `google_analytics` parameter in `_config.yml`.  

#### Page types

- **post** - To write a blog post, add a markdown or HTML file in the `_posts` folder and assign `layout: post` in the YAML front matter. Look at the existing blog post files to see examples of how to use YAML parameters in blog posts.
- **page** - To add a non-blog page, add a markdown or HTML file in the root directory and assign `layout: page` in the YAML front matter. Look at `aboutme.md` and `index.html` as examples.
- **minimal** - To add a random page with minimal styling (ie. without the bulky navigation bar and footer), assign `layout: minimal`.
- To write your own HTML page and completely bypass the Jekyll engine, simply omit the YAML front matter. Only do this if you know what you're doing.

#### YAML front matter parameters

These are the main parameters you can place inside a page's YAML front matter that **Beautiful Jekyll** supports.

Parameter   | Description
----------- | -----------
layout      | What type of page this is (recommended options are `page`, `post`, or `minimal`)
title       | Page or blog post title
subtitle    | Short description of page or blog post
comments    | If you want do add Disqus comments to a specific page, use `comments: true`. Comments are automatically enabled on blog posts, to turn comments off for a specific post, use `comments: false`. Comments only work if you set your Disqus id in the _config.yml file.
js          | List of local JavaScript files to include in the page (eg. `/js/mypage.js`)
ext-js      | List of external JavaScript files to include in the page (eg. `//cdnjs.cloudflare.com/ajax/libs/underscore.js/1.8.2/underscore-min.js`)
css         | List of local CSS files to include in the page
ex-css      | List of external CSS files to include in the page
googlefonts | List of Google fonts to include in the page (eg. `["Monoton", "Lobster"]`)
fb-img      | If you want to share a page on Facebook, by default Facebook will use the first image it can find on the page.  If you want to specify an image to use when sharing the page on Facebook, then provide the image's URL here

### RSS feed

Beautiful Jekyll automatically generates a simple RSS feed of your blog posts, to allow others to subscribe to your posts.  If you want to add a link to your RSS feed in the footer of every page, find the `rss: false` line in `_config.yml` and change it to `rss: true`.

### More advanced features

I wrote [a blog post](http://deanattali.com/2015/03/12/beautiful-jekyll-how-to-build-a-site-in-minutes/) describing some more advanced features that I used in my website that are applicable to any Jekyll site.  It describes how I used a custom URL for my site (deanattali.com instead of daattali.github.io), how to add a Google-powered search into your site, and provides a few more details about having an RSS feed. 

### Advanced: Local development

Beautiful Jekyll is meant to be so simple to use that you can do it all within the browser. However, if you'd like to develop locally on your own machine, that's possible too if you're comfortable with command line. Folow these simple steps to do that with Vagrant:

1. Install [VirtualBox](http://virtualbox.org) and [Vagrant](https://www.vagrantup.com)
2. Clone your fork `git clone git@github.com:yourusername/yourusername.github.io.git`
3. Inside your repository folder, run `vagrant up`
4. View your website at `http://0.0.0.0:4000` on *nix or `http://127.0.0.1:4000` on Windows. 
5. Commit any changes and push everything to the master branch of your GitHub repository. GitHub Pages will then rebuild and serve your website automatically.

### Credits

This template was not made entirely from scratch. I would like to give special thanks to:
- [Barry Clark](https://github.com/barryclark) and his project [Jekyll Now](https://github.com/barryclark/jekyll-now), from whom I've taken several ideas and code snippets, as well as some documenation tips.
- [Iron Summit Media](https://github.com/IronSummitMedia) and their project [Bootstrap Clean Blog](https://github.com/IronSummitMedia/startbootstrap-clean-blog), from which I've used some design ideas and some of the templating code for posts and pagination.

I'd also like to thank [Dr. Jekyll's Themes](http://drjekyllthemes.github.io/), [Jekyll Themes](http://jekyllthemes.org/), and another [Jekyll Themes](http://jekyllrc.github.io/jekyllthemes/) for featuring Beautiful Jekyll in their Jekyll theme directories.

### Known limitations

- If you have a project page and you want a custom 404 page, you must have a custom domain.  See https://help.github.com/articles/custom-404-pages/.  This means that if you have a regular User Page you can use the 404 page from this theme, but if it's a website for a specific repository, the 404 page will not be used.
