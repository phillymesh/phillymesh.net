# phillymesh.net
This is the repository for the `phillymesh.net` website!

This site is built with the open-source [Hugo](https://gohugo.io/) static site generator, which converts Markdown posts and pages into HTML. 

## Making Changes & New Content

Anyone is welcome to submit updates to this site via [pull request](https://github.com/phillymesh/phillymesh.net/pulls).
GitHub maintains a [great guide for creating a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) if you've never made one before.
Note that if you are part of the Philly Mesh organization you can make a pull request utilizing the [shared repository mode](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/getting-started/about-collaborative-development-models#shared-repository-model) which is easy, fast, and great for collaboration.
If you are outside of the org you must [create a pull request from a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork).

After submitting a PR, someone in the organization will review the changes and either approve them or request updates.

Merged updates will go live automatically via a GitHub Actions workflow.

### New Post

New posts are incredibly easy! Make a new page in the [content/post](https://github.com/phillymesh/phillymesh.net/tree/master/content/post) directory in the format `YYYY-MM-DD-your-post-slug.md`. The resulting rendered URL will be `phillymesh.net/YYYY/MM-DD/your-post-slug`. The `YYYY-MM-DD` should be the date you start working on the post or intend to have it published.

At the top of your `.md` file you need to include *front matter* that acts as metadata about the post. Here is an example:

```yaml
---
title: Station G2 Node Installation
author: Mike Dank (Famicoman)
type: post
date: 2025-03-24T00:00:01+00:00
url: /2025/03/24/station-g2-node-installation/
categories:
  - Philly Mesh
tags:
  - meshtastic
  - stationg2
#cspell:ignore stationg2
---
```

This format is pretty self-explanatory and as long as you have a sensible `title`, your preferred name for the `author`, the proper `date`, and a `url` that matches your filename, you should be good. Currently, most posts use `Philly Mesh` as the category and include some `tags` that pertain to the content of the most. For a full explanation of front matter fields, you can consult [this reference](https://gohugo.io/content-management/front-matter/).
the `#cspell:ignore` line is explained below in the Spell Checking section

Posts are written in Markdown, and a quick reference is available [here](https://www.markdownguide.org/tools/hugo/).

If your post needs images, you can make a new folder in the [static/images/uploads](https://github.com/phillymesh/phillymesh.net/tree/master/static/images/uploads) directory with the same name as your post file, such as `YYYY-MM-DD-your-post-slug`. In this directory you can upload any images (or other files really) that you would like to include in the post. Pictures can be referenced in your post in a variety of ways, with the most popular being [a markdown approach](https://alexwlchan.net/2021/markdown-image-syntax/). However, if you need more control over your images there are a few options. **NOTE:** We highly encourage alt text for accessibility!

This figure shortcode is great if you want to include captions with your images:

```
{{< figure src="/images/uploads/YYYY-MM-DD-your-post-slug/your-cool-photo.png" caption="Your cool caption." alt="Describe the picture" link="/images/uploads/YYYY-MM-DD-your-post-slug/your-cool-photo.png">}}
```

If you need control over styling and width/height, you can add html attributes with braces on the next line

```
![Describe the picture](/images/uploads/YYYY-MM-DD-your-post-slug/your-cool-photo.png)
{width="50%"}
```

**NOTE:** Due to the way paths are set up in Hugo, your images will not preview properly because the `src` is set to an absolute path starting with `/images`. For drafting a new post you may want to use `../../static/images` instead but this will not work properly after the page is rendered for the site. Please make sure to switch back to the absolute path before committing.

### Spell Checking
In an effort to reduce typos across the site, we are making use of [CSpell](https://cspell.org/), a spell checker for code.

If you're editing in a VSCode or fork, I'd recommend installing the [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) extension to highlight unrecognized words using the cspell engine.
Otherwise you can run it from the command line with
`npx cspell your-file-name.md` which requires you to have node installed.

If you want to check all the files for spelling issues, you can run
`npx cspell` and check the output


If your post includes some proper nouns or other words that aren't likely to be in the dictionary, you can suppress spellcheck errors by adding that word to the "ignore" list in the "front matter" with the `cspell:ignore` command as a comment

For example:
```yaml
---
title: A new Post
author: Your name
#cspell:ignore ProperNoun
---
```

This isn't a requirement, but saves maintainers time if you can preemptively fix the spelling issue.

## Local Development

If you want to run the site locally to test changes, you can do the following on a Debian Linux host. Hugo maintains a [getting started guide](https://gohugo.io/getting-started/quick-start/) if you use a different operating system, though many steps will be similar.

First, install `git` and grab Hugo extended:

```
sudo apt install git
wget https://github.com/gohugoio/hugo/releases/download/v0.147.8/hugo_extended_0.147.8_Linux-64bit.tar.gz
tar -xzf hugo_*.tar.gz && rm hugo_*.tar.gz
chmod +x hugo
```

Now, clone the `phillymesh.net` repo and pull down the theme via submodule update:

```
git clone https://github.com/phillymesh/phillymesh.net.git
cd phillymesh.net
git submodule update --init --recursive
```

Finally, run `hugo` and build the site, hosting it on a live webserver:

```
hugo server
```

You now have a live server of the site running at <http://127.0.0.1:1313>
