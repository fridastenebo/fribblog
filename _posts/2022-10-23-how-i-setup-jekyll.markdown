---
layout: post
title:  "How I set up my blog using Jekyll"
date:   2022-10-23 12:30:00 +0200
categories: jekyll code
---

Let's kick this off a little meta before getting into it, I have so many posts I want to publish on here because lately, I've been really missing the wordpress blog I ran for a few years during my gymnasie-years (grade 9-12).

So, I've had this thought for a few months now, where I wish I could just set up a really bare-bones - preferably free - blog based on Markdown files. As a developer, [Markdown](https://www.markdownguide.org/getting-started/) is just the most intuitive way for me to get some formatting without the need to involve too much HTML of JS code. After all, I'd mostly call myself a backend developer rather than full stack or front end 😁

So, when I saw Jekyll being used to generate Docs at my job, I quickly found that this is what I'd been ~~looking for~~ wanting. Or, I guess I will find out eventually if it works out.

## Intro to Jekyll
[Jekyll](https://jekyllrb.com/) is a static site generator built on Ruby. The site can serve many purposes, such as portforlio, docs, landing page or the thing I'm after - a blog. One doesn't have to know Ruby to get started, but it helps to be comfortable with a command line and have some developer experience.

The basic idea is that you create a file for every post or page, and Jekyll generates the HTML for you based on that.

There are several free or paid themes to browse and use, just search `jekyll free themes`


## Intro to Github Pages
I already knew I wanted to host my blog on Github, it's what we use at my job, and it's free to get a subdomain on github.io. And that, is called [Github Pages](https://pages.github.com/). Also, it has [native support for Jekyll!](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

## My setup
I run on a Macbook Pro with an M1 chip, macOS Monterey 12.6. My terminal is set up with zsh.

None of these are must-haves or prerequisits, I'm just specifying it here because I think expecially the M1 chip was cause for some of my troubles.

---

## Let's get started!

### Step 1: Install Ruby

Step 1 in the Github Pages + Jekyll docs is stated as "Install Ruby" and of course, this is where I hit my first roadblock 😅

**What didn't work:**
I referred to Jekyll's own documentation to [install Ruby](https://jekyllrb.com/docs/installation/macos/), and `chruby` was just absolutely not happy with me.

`ruby-install ruby` failed with an error message

```
Undefined symbols for architecture arm64:
  "_rb_arithmetic_sequence_extract", referenced from:
      _arith_seq_s_extract in extract.o
  "_rb_ary_new_capa", referenced from:
      _arith_seq_s_extract in extract.o
  "_rb_ary_store", referenced from:
      _arith_seq_s_extract in extract.o
  "_rb_define_singleton_method", referenced from:
      _Init_extract in extract.o
  "_rb_path2class", referenced from:
      _Init_extract in extract.o
ld: symbol(s) not found for architecture arm64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make[2]: *** [../../../../.ext/arm64-darwin21/-test-/arith_seq/extract.bundle] Error 1
make[1]: *** [ext/-test-/arith_seq/extract/all] Error 2
make: *** [build-ext] Error 2
!!! Compiling ruby 3.1.2 failed!
```

**What worked:**
Installing ruby via Homebrew and making sure the new version is in the beginning of the PATH to make it resolve before the older built-in Ruby that macs are shipped with (this is specified in the ).

`brew install ruby`

`echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc`

[This answer and accompanied video](https://talk.jekyllrb.com/t/need-help-with-chruby-unknown-ruby-ruby-3-1-1/7255/4) was helpul in proceeding.

### Step 2: Install Bundler and Jekyll
Next up was installing the needed *gems* for running Jekyll. They recommended bundler, so that was the first one.

`gem install bundler`

**What didn't work:** 

`gem install jekyll`

Trying to install Jekyll is where I hit my next roadblock, it suceeded but when I did the subsequent steps, `jekyll` wasn't a recognized command

**What worked:**

`sudo gem install -n /usr/local/bin jekyll`

Installing jekyll and specifiying it to be installed at the root seemed to do the trick

### Step 3: Setting up the Github Repository

The next few steps went by exactly as [specified](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-a-repository-for-your-site), there are several branching options here so this is where each person does what fits their needs.

At **Step 18**, [Configure your publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) I went with Github Actions. At this point, it doesn't matter, but in the future it might give me some more flexibility in terms of customizing the compilation steps. *Also, it's in Beta and I want to try out anything that is new and shiny*

### Step 4: Running locally

So if you followed the previous step pretty much according to the tutorial like me, you're currently in a folder for your new site with a Gemfile and some boilerplate markdown files.
[The next step is running locally](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll) before we push to Github.

**What didn't work:** Not to my surprise, I missed the note that explained this step, that I saw just now was actually in the docs.

`bundle exec jekyll serve` failed with a very unhelpful error
```
bundler: failed to load command: jekyll (/opt/homebrew/lib/ruby/gems/3.1.0/bin/jekyll)
```

**What worked:** 

`bundle add webrick`

### It (hopefully) worked!
![Success! Our very own static site, and not a single line of Javascript was needed](../../../../../assets/jekyll-first-look.png)