# Hacktober Fest Blog Project 🎃

## Share your knowledge

Not all contributions to open source are code. Open source contributions can take the form of thought-leadership via blog posts, talks, etc.

If you feel most comfortable contributing to open source through your writing, I challenge you to share your knowledge via the Hacktober Fest Blog Project.

The Hacktober Fest Blog Project is a compilation of user contributed blog posts. Blog posts can be about anything: tool tips, productivity tips, tutorials, talk reviews, podcast recommendations. You can even contribute blog posts you've written for your personal blog or other publications.

All of these blog posts will be compiled into a free ebook at the end of the month!

TL;DR Contribute your blog posts. They will be compiled into an awesome free ebook at the end of the month. YAY Hactober Fest!

### How to contribute

This is a Jekyll blog, you don't have to do anything but write your blog post in Markdown :)

If you're unfamiliar with Jekyll, I wrote a [blog post](http://cecycorrea.com/development/2017/02/06/getting-started-with-jekyll.html) on how to get started with Jekyll.

Repo owner (me) will push your post and make it live after approving your PR. You will be sent a link to your blog post as a response to your PR.

**Step 1:** Fork this repo and create a branch on your fork for your post.

**Step 2:** Write a blog post. If you're unfamiliar with Jekyll, don't worry. It's easy. Essentially, all posts go in the `_posts` folders and follow this convention: `YYYY-MM-DD-title-of-your-post.markdown`.

There is a handy rake task you can use to auto generate the file for you. Just type `rake post:new` and follow the prompt.

**Step 3:** Write your post! You can use [Github flavored markdown](https://guides.github.com/features/mastering-markdown/).

Please include your name and twitter / github (some way to identify you) in the [post frontmatter](https://jekyllrb.com/docs/frontmatter/). Example:

```
layout: post
title: My awesome blog post
author: Johnny Joestar
twitter: https://twitter.com/jjoestar
website: https://my-awesome-site.com
github: https://github.com/jjoestar
```

You can either leave blank or omit fields in the frontmatter you don't want. **Do not change the layout though!** Layout and title are required for Jekyll to work.

**Step 4:** Submit your PR!

Once your PR is approved, repo owner (me!) will merge and deploy to Github Pages. The blog, for now, will be hosted on `cecyc.github.io/hacktoberfest-blog`.

### Blog post ideas

* Idea for an app you haven't had a chance to build and how you would build it
* How you could improve the UI / UX or functionality of an existing app or site
* Tech how-to tutorial (how to build a blog in Rails, how to create a to do list app in React, how to get started with PHP, etc)
* A link to a tech talk you really liked and why
* Lessons your learned from learning a new language / skill
* Tips that help you be productive in tech
* App or list of apps that help you in your job as a designer, developer, etc
* Open source projects you like and why
* Tips for developers getting started in tech

Any posts are welcome as long as they are constuctive, helpful, or teach the community something :)
