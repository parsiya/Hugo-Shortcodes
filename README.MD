## My Hugo Shortcodes

These are shortcodes that I have created for the [Hugo](https://gohugo.io) static blogging engine.

To use them, copy the HTML files into `your-hugo-blog/layouts/shortcodes/` or `your-hugo-blog/themes/current-theme/layouts/shortcodes/`. I do not suggest the second approach. Create the `shortcodes` directory if it does not exist. You can learn more about shortcodes from [Hugo documentation](https://gohugo.io/extras/shortcodes/).

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
This shortcode adds captions to pictures. Due to the way the original css file was organized, this shortcode does not use `<figure>` and `<figcaption>`. `Alt` will also be set to title.

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
I attempted to the re-create the Jekyll Wikipedia link generator by [Keltia](https://github.com/keltia). You can see the source [here](https://github.com/keltia/octopress/commit/17b975067ff86c0c7cddac4ae2c2c975b0790b6e).

You can see the discussion on Hugo forums [here](https://discuss.gohugo.io/t/equivalent-to-jekyll-octopress-theme-named-cleanpress/2953) with my original [gist](https://gist.github.com/parsiya/562f5d2bde3e9060d793).

It has some shortcomings. There are definitely better ways to do this. Personally I prefer the named parameter version because the shortcode is easier to write but this should work for both.

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

It does not remove the underlines from tag to use in title. I have not found a Hugo template function for that yet (perhaps there is one).

## Atom snippets for shortcodes

I use Atom editor these days so I created a couple of snippets to insert these shortcodes while editing Markdown files. In order to read on how to create snippets please refer to [Atom's Snippets package](https://github.com/atom/snippets).

Open your snippets file (on Windows it's `File > Open Your Snippets`) and paste the following in the file:

``` coffee
'.source.gfm':
  'codecaption':
    'prefix': 'codecap'
    'body': """
    {{< codecaption title="$1" lang="$2"  >}}
    $3
    {{< /codecaption >}}
    """
  'imgcap':
    'prefix': 'imgcap'
    'body': '{{< imgcap title="$1" src="/images/2016/$2" >}}'
  'wp':
    'prefix': 'wp'
    'body': '{{< wp tag="$1" lang="$2" title="$3" >}}'
```

My original mistake was to repeat `'.source.gfm'` before the `imgcap` snippet, seems like [cson keys should not be repeated](https://atom.io/docs/latest/using-atom-basic-customization#id-D9ATX).

You can trigger the shortcodes by entering `imgcap` and `codecap` respectively and then pressing enter. You can change these by modifying the `prefix` in the code above. After inserting the shortcode, the cursor will go to the first location which is designated by `$1` which is `title` in both cases. After entering the value you can go to `$2` and `$3` by pressing `tab`.

Hopefully these snippets help in using these shortcodes.

## License
I don't know, [MIT](LICENSE) I guess.
