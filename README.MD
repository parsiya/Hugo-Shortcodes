## My Hugo Shortcodes

These are shortcodes that I have created for the [Hugo](https://gohugo.io)
static blogging engine.

To use them, copy the HTML files into `your-hugo-blog/layouts/shortcodes/` or
`your-hugo-blog/themes/current-theme/layouts/shortcodes/`. I do not suggest the
second approach. Create the `shortcodes` directory if it does not exist. You can
learn more about shortcodes from
[Hugo documentation](https://gohugo.io/extras/shortcodes/).

- [My Hugo Shortcodes](#my-hugo-shortcodes)
  - [Codecaption (codecaption.html)](#codecaption-codecaptionhtml)
  - [Image Caption (imgcap.html)](#image-caption-imgcaphtml)
  - [Wikipedia Link Generator (wp.html)](#wikipedia-link-generator-wphtml)
  - [Octopress blockquote (blockquote.html)](#octopress-blockquote-blockquotehtml)
  - [Year (year.html)](#year-yearhtml)
  - [abbr HTML Tag (abbr.html)](#abbr-html-tag-abbrhtml)
  - [mark HTML Tag (mark.html)](#mark-html-tag-markhtml)
  - [Table of Contents (toc.html)](#table-of-contents-tochtml)
  - [xref (xref.html)](#xref-xrefhtml)
    - [Path](#path)
    - [Anchor](#anchor)
    - [Title](#title)
- [Editor Snippets](#editor-snippets)
  - [Sublime Text Completions](#sublime-text-completions)
  - [VS Code Snippets](#vs-code-snippets)
  - [Atom Snippets - Archived](#atom-snippets---archived)
- [License](#license)

### Codecaption (codecaption.html)
Adds title to code blocks.

**Usage:**

``` html
{{< codecaption lang="html" title="Code caption shortcode" >}}
<figure class="code">
  <figcaption>
    <span>{{ .Get "title" }}</span>
  </figcaption>
  <div class="codewrapper">
    {{ highlight .Inner (.Get "lang") "linenos=true" }}
  </div>
</figure>
{{< /codecaption >}}
```

Results in:

![Captioned codeblock](/images/codecaption1.png)

### Image Caption (imgcap.html)
This shortcode adds captions to pictures. Due to the way the original css file
was organized, this shortcode does not use `<figure>` and `<figcaption>`. `Alt`
will also be set to title.

**Usage:**

    {{< imgcap title="Sample caption" src="/images/2016/thetheme/1.png" >}}

Results in HTML:

``` html
<span class="caption-wrapper">
  <img class="caption" src="/images/2016/thetheme/1.png" title="Sample caption" alt="Sample caption">
  <span class="caption-text">Sample caption</span>
</span>
```

### Wikipedia Link Generator (wp.html)
I attempted to the re-create the Jekyll Wikipedia link generator by
[Keltia](https://github.com/keltia). You can see the source
[here](https://github.com/keltia/octopress/commit/17b975067ff86c0c7cddac4ae2c2c975b0790b6e).

You can see the discussion on Hugo forums
[here](https://discuss.gohugo.io/t/equivalent-to-jekyll-octopress-theme-named-cleanpress/2953)
with my original [gist](https://gist.github.com/parsiya/562f5d2bde3e9060d793).

It has some shortcomings. There are definitely better ways to do this.
Personally I prefer the named parameter version because the shortcode is easier
to write but this should work for both.

**Usage:**

You can either use named parameters:

* {{< wp tag="VIC_cipher" >}}
* {{< wp tag="VIC_cipher" lang="fr" >}}
* {{< wp tag="VIC_cipher" lang="fr" title="" >}}
* {{< wp tag="VIC_cipher" title="VIC Cipher" >}}
* {{< wp tag="VIC_cipher" lang="en" title="VIC Cipher" >}}

Rendered to:

``` html
<a href="https://en.wikipedia.org/wiki/VIC_cipher">VIC_cipher</a>
<a href="https://fr.wikipedia.org/wiki/VIC_cipher">VIC_cipher</a>
<a href="https://fr.wikipedia.org/wiki/VIC_cipher">VIC_cipher</a>
<a href="https://en.wikipedia.org/wiki/VIC_cipher">VIC Cipher</a>
<a href="https://en.wikipedia.org/wiki/VIC_cipher">VIC Cipher</a>
```

Or positional:

* {{< wp VIC_cipher >}}
* {{< wp VIC_cipher fr >}}
* {{< wp VIC_cipher "" fr >}}
* {{< wp VIC_cipher "VIC Cipher" >}}
* {{< wp VIC_cipher "VIC Cipher" fr >}}

``` html
<a href="https://en.wikipedia.org/wiki/VIC_cipher">VIC_cipher</a>
<a href="https://fr.wikipedia.org/wiki/VIC_cipher">VIC_cipher</a>
<a href="https://fr.wikipedia.org/wiki/VIC_cipher">VIC_cipher</a>
<a href="https://en.wikipedia.org/wiki/VIC_cipher">VIC Cipher</a>
<a href="https://fr.wikipedia.org/wiki/VIC_cipher">VIC Cipher</a>
```

It does not remove the underlines from tag to use in title. I have not found a
Hugo template function for that yet (perhaps there is one).

### Octopress blockquote (blockquote.html)
Port of the Octopress `blockquote` plugin at
http://octopress.org/docs/plugins/blockquote/.

It supports author, link, source and title. If title is not provided and link is
longer than 32 characters, it is cut at the last forward slash similar to the
original plugin.

It can be used as follows (also in `tests/wp-test.markdown`):

    Normal quote:
    {{< blockquote >}}
      This is a simple quote.
    {{< /blockquote >}}

    Quote with author
    {{< blockquote author="Author2" >}}
      This is a quote with only an Author named Author2.
    {{< /blockquote >}}

    Quote with author and source
    {{< blockquote author="Author3" source="Source" >}}
      This is a quote from Author3 and source "source."
    {{< /blockquote >}}

    Quote with author and link
    {{< blockquote author="Author4" link="https://www.google.com" >}}
      This is a quote from Author4 and links to https://www.google.com.
    {{< /blockquote >}}

    Quote with author, link and title
    {{< blockquote author="Author5" link="https://www.google.com" title="Google" >}}
      This is a quote from Author5 and links to https://www.google.com with title "Google."
    {{< /blockquote >}}

    Quote with author and a link longer than 32 characters, string is first cut at 32 characters then everything after the last forward slash is removed
    {{< blockquote author="Author6" link="https://twitter.com/CryptoGangsta/status/716427930126196737" >}}
      This is a quote from Author5 and links to https://twitter.com/CryptoGangsta/status/716427930126196737 which is longer than 32 characters.
      <br>And this is a new line in the quote with the HTML br tag.
    {{< /blockquote >}}

    Test from the Octopress blockquote page at: http://octopress.org/docs/plugins/blockquote/
    {{< blockquote author="@allanbranch" link="https://twitter.com/allanbranch/status/90766146063712256" >}}
      Over the past 24 hours I've been reflecting on my life & I've realized only one thing. I need a medieval battle axe.
    {{< /blockquote >}}

Results in:

![blockquote-test](images/blockquote.png)

### Year (year.html)
Displays the current year - based on the shortcode tutorial at
https://gohugo.io/templates/shortcode-templates/#single-word-example-year.

Usage: `{{< year >}}`.

### abbr HTML Tag (abbr.html)
Creates an `abbr` HTML tag. The structure for this tag looks like:

```html
<abbr title="World Health Organization">WHO</abbr>
```

Which is created by the following shortcode:

`{{< abbr title="World Health Organization" text="WHO" >}}`

### mark HTML Tag (mark.html)
Creates a `mark` HTML tag to highlight text.

Usage: `{{< mark text="highlighted text" >}}` results in the following HTML:

`<mark>highlighted text</mark>`

### Table of Contents (toc.html)
Use it to insert a table of contents anywhere in your page. For more information
about Hugo's table of contents please see
https://gohugo.io/content-management/toc/.

Usage: `{{< toc >}}`.

**Note for Goldmark users:** 

Starting with Hugo 0.60 (I think?), the configuration file has a new section
named `markup`. We can specify the minimum and maximum heading levels in the
table of contents. The defaults are as follows which are not that useful. Be
sure to override them in your site's config file:

```yaml
markup:
  tableOfContents:
    endLevel: 3
    ordered: false
    startLevel: 2
```

For more information please see
https://gohugo.io/getting-started/configuration-markup/#table-of-contents.

### xref (xref.html)
Adds text to the input params to create a relref link for my blog. It adds
hardcoded strings to the path to work with the way I organize my paths. It might
not be useful for you.



This way I can write

```
{{< xref title="Brief Recon of the Nordpass Password Manager"
  path="/post/2021/2021-04-30-testing-extensions-edge/" anchor="brief-recon" >}}
```

instead of 

```
[Brief Recon of the Nordpass Password Manager]
  ({{< relref "/post/2021/2021-04-30-testing-extensions-edge/index.markdown#brief-recon" >}}
  "Brief Recon of the Nordpass Password Manager") 
```

We can also use positional arguments.

```
{{< xref "path" "anchor" "title" >}}

{{< xref "/post/2021/2021-04-30-testing-extensions-edge/" "brief-recon"
  "Brief Recon of the Nordpass Password Manager" >}}
```

With positional arguments, we can only include path, or path and anchor, but we
cannot use path and title.

```
{{< xref "/post/2021/2021-04-30-testing-extensions-edge/" >}}

{{< xref "/post/2021/2021-04-30-testing-extensions-edge/" "brief-recon" >}}
```

#### Path

* Path is passed to the relref link so it will panic if the path does not exist.
* If the path does not end in `.md` or `.markdown` it adds `/index.markdown` to
  the end of it to support page bundles.
* Don't worry about including `/` at the beginning or in the end, the shortcode
  removes them and adds its own.

#### Anchor

* Anchor is optional.
* No need to include `#` but if included it will not introduce a bug. The
  shortcode trims it and adds its own.

#### Title

* Title is optional.
* If not provided, the title will be the same as the link. I.e.,
  `.Site.BaseURL/$relreflink`.

----------

## Editor Snippets
I have created snippets for Atom, Sublime and VS Code.

### Sublime Text Completions
[Sublime text completions](http://docs.sublimetext.info/en/latest/reference/completions.html)
are stored in a `.sublime-completion` file in the `User` directory.

### VS Code Snippets
[VS Code snippets](editor-snippets/vs-code-markdown.json) can be added to
`File > Preferences > User Snippets > markdown.json`. For more information
please see:

* https://code.visualstudio.com/docs/editor/userdefinedsnippets

### Atom Snippets - Archived
~~I use Atom editor these days so~~ I created a couple of snippets to insert
these shortcodes while editing Markdown files. In order to read on how to create
snippets please refer to
[Atom's Snippets package](https://github.com/atom/snippets).

Open your snippets file (on Windows it's `File > Open Your Snippets`) and paste the `editor-snippets\atom-snippets.cson` into it.

My original mistake was to repeat `'.source.gfm'` before the `imgcap` snippet,
seems like
[cson keys should not be repeated](https://atom.io/docs/latest/using-atom-basic-customization#id-D9ATX).

For more information please see:

* https://flight-manual.atom.io/using-atom/sections/snippets/

## License
I don't know, [MIT](LICENSE) I guess.
