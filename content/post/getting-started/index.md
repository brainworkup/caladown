---
output: hugodown::md_document
title: "Tutorial part 1: Getting started"
type: "post"
author: "Danielle Navarro"
date: "2020-06-10"
slug: getting-started
tags: ["tutorial"]
header:
  caption: "A caption"
  image: 'header/banner.png'
  profile: 'header/profile.png'
rmd_hash: 35d400cbbf65a261

---

The aim of caladown is to provide a simple Hugo template suitable for R users who want to build a website or start a blog, and is designed to be compatible with both [blogdown](https://github.com/rstudio/blogdown) and [hugodown](https://github.com/r-lib/hugodown). In this tutorial, I'll show you how to get started. The assumed reader for this tutorial is an R user who has some experience with [R Markdown](https://rmarkdown.rstudio.com/), but is unfamiliar with blogdown, hugodown, or Hugo itself.

## Blogdown or Hugodown?

The first decision you need to make is which R package to use, blogdown or hugodown? Both allow you to design and manage static websites within R, and both allow you to write pages/posts as R markdown documents. However, there are differences: blogdown blurs the roles played by Hugo and R, which can lead to some degree of messiness. In contrast, hugodown tries to maintain a clean separation: the role of hugodown is to translate your R markdown files into a "plain" markdown format that Hugo knows how to read, and then leaves the rest of the process to Hugo. To me, the cleaner separation in hugodown is highly desirable: but it is currently an experimental package, so some caution is warranted!

To make things as easy as possible, the caladown package contains installer functions for both hugodown and blogdown. If you want to use blogdown, you can create a new site with the following command. Just change `"path_to_blog_folder"` to something suitable:

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span><span class='nf'>caladown</span><span class='nf'>::</span><span class='nf'><a href='https://rdrr.io/pkg/caladown/man/create_blogdown_calade.html'>create_blogdown_calade</a></span><span class='o'>(</span><span class='s'>"path_to_blog_folder"</span><span class='o'>)</span></span></code></pre>

</div>

Blogdown will download the calade template and generate the example site (i.e., this one!), and you are ready to get started. The `create_blogdown_calade()` command is just a very thin wrapper around [`blogdown::new_site()`](https://pkgs.rstudio.com/blogdown/reference/hugo_cmd.html), so if you want to customise the install you can pass arguments to `new_site()` via the dots `...`.

If you want to use hugodown, the installation command is this:

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span><span class='nf'>caladown</span><span class='nf'>::</span><span class='nf'><a href='https://rdrr.io/pkg/caladown/man/create_hugodown_calade.html'>create_hugodown_calade</a></span><span class='o'>(</span><span class='s'>"path_to_blog_folder"</span><span class='o'>)</span></span></code></pre>

</div>

Note that because hugodown makes different choices to blogdown regarding what is and is not automated, you may need to install the appropriate version of Hugo first. The command for this is:

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span><span class='nf'>hugodown</span><span class='nf'>::</span><span class='nf'><a href='https://rdrr.io/pkg/hugodown/man/hugo_install.html'>hugo_install</a></span><span class='o'>(</span><span class='s'>"0.66.0"</span><span class='o'>)</span></span></code></pre>

</div>

Once you have installed Hugo and called the `create_hugodown_calade()` function, hugodown will download the calade template, configure the site appropriately and then knit all the R markdown files to "Hugo flavoured markdown". Please note that the success of this knitting may depend on the version of pandoc you have installed, which you can check with [`rmarkdown::pandoc_version()`](https://pkgs.rstudio.com/rmarkdown/reference/pandoc_available.html). For versions prior to 2.1 the knitting may not be successful, and `create_hugodown_calade()` may produce an error. If this happens it may be useful to note that the you can call this function setting `knit = FALSE` and it will set up the blog without attempting to knit the R markdown files.

Regardless of whether you choose to use blogdown or hugodown, if you are using RStudio you will end up with a new project opened in a new session. To create a preview of the site use one of the following two commands:

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span><span class='nf'>blogdown</span><span class='nf'>::</span><span class='nf'><a href='https://pkgs.rstudio.com/blogdown/reference/serve_site.html'>serve_site</a></span><span class='o'>(</span><span class='o'>)</span></span>
<span><span class='nf'>hugodown</span><span class='nf'>::</span><span class='nf'><a href='https://rdrr.io/pkg/hugodown/man/hugo_start.html'>hugo_start</a></span><span class='o'>(</span><span class='o'>)</span></span></code></pre>

</div>

## Initial configuration

Most of the settings that you'll initially want to play with are in the `config.toml` file. The file is (I hope) fairly well documented, so you can see what most of the settings do and how to configure them. For example, here's a snippet:

    # These settings specify the title for your blog, 
    # and the name of the Hugo theme that it uses.
    title = "A minimal Hugo website"
    theme = "calade"

The snippet above is what you should see if you are using hugodown. If you are using blogdown it will be slightly different: the theme folder will have been automatically renamed from `"calade"` to `"hugo-calade"`, and this will be reflected in the `config.toml` file. Either way, take a look at the config file, change a couple of things if you like, and then you're ready to start blogging!

## Your first post

Creating posts or pages is (usually) pretty straightfoward in both blogdown and hugodown. In blogdown, you can use the `new_post()` function to create a post, and all you need to do is specify the title:

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span><span class='nf'>blogdown</span><span class='nf'>::</span><span class='nf'><a href='https://pkgs.rstudio.com/blogdown/reference/hugo_cmd.html'>new_post</a></span><span class='o'>(</span>title <span class='o'>=</span> <span class='s'>"My new post"</span><span class='o'>)</span></span></code></pre>

</div>

In hugodown, the `use_post()` function is similar but not quite identical. The main thing you need to do is specify the `path` that you'd like the new page to have. So if I want my website to create a page at `https://myfancywebsite.com/post/my-new-post` or whatever, the command I would need is this:

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span><span class='nf'>hugodown</span><span class='nf'>::</span><span class='nf'><a href='https://rdrr.io/pkg/hugodown/man/use_post.html'>use_post</a></span><span class='o'>(</span>path <span class='o'>=</span> <span class='s'>"post/my-new-post"</span><span class='o'>)</span></span></code></pre>

</div>

Either way, whether you are using blogdown or hugodown, you should now be looking at a new R markdown document that you can start editing!

