## Installing mkdocs

Install using pip:

```shell
pip install mkdocs
```

and to check the installation 

```shell
$ mkdocs --version
mkdocs, version 0.15.3
```

## Installing Material for mkdocs

Install using pip:

```shell
pip install mkdocs-material
```

and int the project's mkdocs.yml we need to add:

```yml
theme:
  name: 'material' 
```

## Useful MkDocs Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Useful commands

* `![Name of the image](/images/nameImage.png)` -  to add an image 
* `[text](URL)` to add a link to a text 

## Launch Mkdocs in specific ip

```bash
mkdocs serve --dev-addr=[IP_Address:Port]
```

## Deploy the MKDocs

The project pages site will be deploy in other branch called 'gh-deploy', run the following command:

```bash
mkdocs gh-deploy
```

That's it! Behind the scenes, MkDocs will build your docs and use the ghp-import tool to commit them to the gh-pages branch and push the gh-pages branch to GitHub.

## Math

* To add inline math you can use `$` and close it `$`, like `$...$`
* To add a block of math we use `$$$` and close with `$$$`
* In case that you need to add a white space inside this blocks you will need to escape it, example `training\ batch`

## extra.css

This is a file to customize the theme without modify the original files, I modify the following:

### 1. Center the image

To center the images first, I added the `markdown extension` called `attr_list`, later create the following modification on the `extra.css`

```css
/*
///////////////////////
// To center images////
///////////////////////
*/

.center {
    display: block;
    margin: 0 auto;
}
```

now to center the image I just need to add "{: .center}" at the end of the statement, for example:

`![Name of the image](/images/nameImage.png).{: .center}`

### Modification to footnote strings color

To change the color of the footnotes i made a change in the css

```css
.md-typeset div.footnote {
  color: #808080;
}
```

### Callout

To create a callout put the content in between `<aside>` tags.

```html
<aside>
    This is a Callout
</aside>
```

<aside>
    This is a Callout
</aside>

>"To every man upon this earth, death cometh soon or late, And how can man die better, Than facing fearful odds, for the ashes of his fathers, And the temples of his gods."
