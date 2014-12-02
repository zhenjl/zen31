+++
date = "2013-08-18T21:22:22-08:00"
title = "Migrating 40,000 Posts from Wordpress to Octopress"
categories = [ "octopress" ]

+++

I just spent the weekend migrating several of my blogs, including this one ([zhen.org](http://zhen.org)), [Cloudfeed](http://cloudfeed.net), [Mobileaware](http://mobileaware.net), [Dataaware](http://dataaware.net), and [TrustPath News](http://news.trustpath.com), from [wordpress](http://wordpress.org) to [octopress](http://octopress.org). 

I have one more, [Cloudaware](http://cloudaware.net), that I need to migrate but that one will take a bit of work. I'll explain why a bit later.

### tl;dr

#### The Bad

* If you are not familiar with git, don't use Octopress. I almost want to say if you don't use git on other development projects on a fairly regular basis, don't use Octopress because you will run into issues that you may not be able to resolve. 
* If you have a very large site and need fast updates, don't use Octopress. Large sites with 1000's of posts will take a long time to generate. There's no incremental update currently. Everytime you update a post or create a new post you need to re-generate the whole site. 
* If you are not comfortable with the command line (terminal windows), don't use Octopress. Most of everything you do with Octopress is in the terminal so be prepare to type. :)
* If your site uses a lot of wordpress plugins, you may not want to use Octopress. Octopress is still new so it may not have the plugins you are using. Do an inventory prior to determine feasibility.
* If your site uses a special theme you may want to investigate the effort of migrating the theme. There's not a large selection like Wordpress. If you want your own theme then prepare to get your hands dirty or pay someone to do it. Good thing is octopress themes are much simpler than wordpress.

#### The Good

* If you are a developer and have a blog with mostly static content, Octopress is for you.
* If you want a high performance static content site, Octopress is for you.
* If you free blog hosting with a reputable service (e.g., github), Octopress is for you.
* If you don't want to keep updating wordpress versions, Octopress is for you.

### The Reasons

So what caused me to make the jump all of a sudden?

#### #1: I am lazy but I need better security

Due to family, work, and side project reasons, I've been not been paying much attention to these blogs. Some of them are automated but even the automation scripts are failing as I have not kept up with the APIs. This blog especially has been dormant since June 2009. Well, until now at least. This is my first blog post using Octopress.

Not only have I not kept the blogs fresh, I have also not kept Wordpress versions up to date. I've upgraded wordpress a couple of times for these blogs over the years. The last update was April 6th, 2012 and the wordpress version was 3.3.1. The latest I checked is 3.6.

You are probably wondering why I haven't been hacked given the [long list of Wordpress vulnerabilities](http://www.cvedetails.com/vulnerability-list/vendor_id-2337/product_id-4096/). Well, the fact is I have been hacked once before due to a wordpress xmlrpc way back when. I lost a bunch of files that time. I vowed to keep wordpress updated but as you can tell I have not been successful. So I consider myself lucky.

So a static site hosted by someone else completely seems like the perfect approach.

#### #2 and #3: I am cheap but I want flexibility and performance

For the past several years I've been keeping a VPS just to run my blogs. I like to use my own domains and I don't feel like paying wordpress.com for mapping a custom domain and customizing themes. Not to mention you can't even customize the themes all that much. On top of that, I want to server my own ads, not pay wordpress.com NOT to display ads on my blog.

I pay $10/month for my VPS, and I can host any number of blogs I want on it. A single blog on wordpress.com can cost me more than $100 (custom domain, premium theme, custom design, no ads). For the 6 blogs I would be paying $700/year. And every blog I add will cost me another $100+.

Granted, the little VPS I have is barely sufficient to handle the load but it has been ok so far. However, I could really use a bit more horsepower.

So the static site will give me the performance I need and I want the ability to customize the heck out of the site (not that I do it all that much, but the perception of flexibility is still good.)

### The Process

Another name for this post could be: Migrate From Wordpress to Octopress in 9 Not-So-Simple Steps

1. Clone Octopress
2. Export wordpress posts
3. Convert using Exitwp
4. Set up the Octopress Theme
5. Generate the Static Site
6. Preview the Site
7. Prepare for Publishing
8. Publish the Site
9. Commit your source

I've been seeing experimenting hosting static sites with Github gh-pages recently, see [Top Clouds](http://topclouds.org), so I thought that's a good way to host sites that don't change a whole lot. I've also been seeing quite a few mentions of Octopress recently so I've been tempted to check it out.

So with these reasons/excuses, I decided to take the plunge. I checked out many of the recent migrant blogs, including

* [Jason McCreary](http://jason.pureconcepts.net/2013/01/migrating-wordpress-octopress/)
* [Joel Hooks](http://joelhooks.com/blog/2012/07/25/fresh-start-migrating-wordpress-octopress/)
* [Praveen Vijayan](http://decodize.com/html/moving-from-wordpress-to-octopress/)
* [Greg Baugues](http://blog.baugues.com/moving-from-wordpress-to-octopress)
* [Fabrizio (Fritz) Stelluto](http://gotofritz.net/blog/weekly-challenge/migrating-wordpress-blogs-to-octopress/)
* [Matt Gemmell](http://mattgemmell.com/2011/09/12/blogging-with-octopress/)

These are just a few that I read. There's [a ton more](https://www.google.com/search?q=migrate+from+wordpress+to+octopress&oq=migrate+from+wordpress+to+octo) you can browse.

Many of these blogs explained how they migrated and were tremendously helpful. I can't thank these folks enough for sharing their experiences.

### The Details

For each of the blogs I migrated, I did the following. 

#### 1. Clone Octopress

You need to do this once for each blog, so replace cloudfeed with the blog name.

`git clone https://github.com/imathis/octopress cloudfeed`

This will make a copy of octopress in a directory called "cloudfeed" for you. From there, you can run these git commands to save the copy in your own git repo.

```
git config remote.origin.url https://git@github.com/zhenjl/cloudfeed
git push origin master
```

Github sets the first branch you push to in a new repo the default branch. So make sure you do this step before you publish to, say, the gh-pages branch. 

I would highly recommend anyone starting with Octopress to do clone instead of fork on Github. If you fork it on Github, you will end up getting all the branches as well. You really don't need the extra branches. Plus, it will confuse the heck out of you if you didn't realize you got all the branches and you want to use the gh-pages branch to host your blog. 

But if for whatever reason you did fork octopress, you can run these commands after you `git clone` your fork

```
git push origin :2.5
git push origin :2.5-simplify-rakefile
git push origin :3.0
git push origin :commander
git push origin :gh-pages
git push origin :guard
git push origin :linklog
git push origin :migrator
git push origin :refactor_with_tests
git push origin :rubygemcli
git push origin :site
git push origin :site-2.1
```

These commands will remove all the extra branches from your fork.

#### 2. Export wordpress posts 

Do this once for each blog you are converting.

This step is pretty simple. Just go to wordpress blog admin -> Tools -> Export, and you are golden.

However, make sure you run `xmllint` on the exported XML and fix any issue you see. However, watch out for any malformed HTML inside the CDATA section. Not exactly sure how to catch that but just remember exitwp requies parsing of the HTML to convert into markdown. 

#### 3. Convert using Exitwp

You only need to do this step once.

`git clone https://github.com/thomasf/exitwp`

[Exitwp](https://github.com/thomasf/exitwp) is 

> a tool for making migration from one or more wordpress blogs to the jekyll blog engine as easy as possible.
> 
> By default it will try to convert as much information as possible from wordpress but can also be told to filter the amount of data it converts.

There are some dependencies, so make sure you read through the README.rst before moving forward.

Exitwp works by first parsing the **WHOLE** exported wordpress xml, then write out all the markdown files. The problem with that is if you have a very large site ([Dataaware](http://dataaware.net) has over 12K entries, and [Cloudaware](http://cloudaware.net) has over 25K posts), it will take a ton of memory. Not to mention you have no feedback on what's going on until the end.

I had one blog post that had some malformed HTML inside the CDATA section, and that somehow caused the parser to spin forever (still not sure what the deal is). I let exitwp run over night not knowing what's going on, but finally I updated exitwp to write out jekyll files one at a time instead of all at the end. I also outputed the blog title so I know which blog is getting stuck. 

The following diff (sorry not patch format but that was too long) shows the differences. 

```
95,96d94
<     header = parse_header()
<
164,165d161
<             write_jekyll({'header': header, 'items': export_items}, target_format)
<             export_items = []
366a362
>     write_jekyll(data, target_format)
```

In any case, exitwp is an awesome, and required, tool for migrating from wordpress to octopress. Learn to love it.

Put the final XML, from step #2, into wordpress-xml directory under exitwp, and you can run `python exitwp.py` to convert it. 

One of the blogs above mentioned that you may need to fix up the image tags manually, but I didn't check the result as I didn't have many images in my blogs.

After exitwp finishes, you can copy the build/jekyll/<name>/_posts to the source directory under octopress.

`cp -r build/jekyll/cloudfeed/_posts ../cloudfeed/source/_posts`

#### 4. Set up the Octopress Theme

You need to do this for each blog you are migrating.

There are a list of themes on [Opthemes](http://opthemes.com) you can download for Octopress. Most of them are pretty simple. The ones I used are [Pageturner](https://github.com/elisehein/Pageturner) and [Greyshade](https://github.com/shashankmehta/greyshade) with minor modifications.

One caveat to remember, after you `git clone` the theme into `.themes` directory, is you need to remove the .git directory for that theme, or else you won't be able to save a copy to your own repo. So `rm -rf .themes/<theme_name>/.git`.

Another caveat to remember is some of the themes have missing files, most likely they expect the Octopress classis theme to be installed. For example, there's a bunch of files missing from Greyshade if you haven't previously installed classic. So the best way to install the theme is

```
rake install
rake "install[greyshade]"
```

Personally I don't really like it as it adds unncessary files to the source and sass directories, so I just copied the necessary files over to the new theme. You may not want to go through that level of pain.

#### 5. Generate the Static Site

You need to do this for each blog you are migrating, and each time you update the site.

`rake generate`

This command will generate the site for you. It is an easy step but could take forever. For [Dataaware](http://dataaware.net) I have over 12K posts. It takes **1 hour** to generate the site on my Macbook Air (1.8 GHz i5, 4GB memory, SSD). For [Cloudfeed](http://cloudfeed.net) with 5700+ posts, it takes 20-25 minutes. For [Cloudaware](http://cloudaware.net) with over 25K posts, I would expect the generation process to take well over 2 hours.

Hopefully at some point jekyll can do incremental generation coz this really sucks (yes it's a technical word.)

#### 6. Preview the Site

To preview the site before publishing, you can run `rake preview`. It will start a web server on port 4000, so you can go to "http://localhost:4000" to see what your site looks like before publishing. It's great for reviewing new posts.

#### 7. Prepare for Publishing

If you are publishing to github, you need to run the following command to setup the github repo. Read the [Deploying to Github Pages](http://octopress.org/docs/deploying/github/) page very carefully and follow the instructions there.

One thing to note is that octopress will do a git pull on the repo at the beginning of the deploy process. Most of the time this isn't a problem because the git repo in the \_deploy directory aren't tracking any remotes. However if you had checked out the branch (probably because you are trying to fix some git push issues), AND you have a very large site, the git pull will take a long time to finish.

In any case, run the following command `rake setup_github_pages` to set the git repo to publish to.

#### 8. Publish the Site

`rake deploy`

Octopress will copy all the files to the \_deploy directory and push the site to the repo you setup in step #7.

The problem is sometimes you will run into git merge problems and octopress will complain 

```
## Pushing generated \_deploy website
To ssh://git@github.com/zhenjl/trustpath.news.web
! [rejected]        gh-pages -> gh-pages (non-fast-forward)
error: failed to push some refs to 'ssh://git@github.com/zhenjl/trustpath.news.web'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

To fix this, I had to

```
cd _deploy
git pull origin gh-pages
git commit -a -m "merging"
```

This will at least get git to settle down. Then I do a `rake deploy` again which will overwite all the files and finally it will push successfully.

You can also combine this and step #5 (generate) using ``rake gen_deploy``.

#### 9. Commit your source

By now you have reviewed your spanking new website and are probably pretty happy you have gotten this far. But don't forget the last thing which is to save your site's source. 

In step #1 you had setup the remote origin for this octopress clone. You should now add all the files you have created and commit them to github.

```
git add .
git commit -a -m "first commit after conversion"
git push origin master
```

Oh one last thing, if you use vim, be sure to add these to .gitignore.

```
*.swp
*.un~
```

---

So finally after all this we have a working site. I can tell immediately that pages are served up much faster (sorry no data/numbers). I am sure it has to do with both 1) the site is all static pages, and 2) it's served by github rather than the little VPS.

I am not quite ready to delete all the wordpress setups yet as the Octopress site generation takes hours. I will have to see if this painful step will become a deal breaker. Will keep you all posted on that.


---

[Comments](https://news.ycombinator.com/item?id=6236080)
