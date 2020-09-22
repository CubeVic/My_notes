## Installing mkdocs

Install using pip:

```
pip install mkdocs
```
and to check the installation 
```
$ mkdocs --version
mkdocs, version 0.15.3
```
## Installing Material for mkdocs

Install using pip:

```
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

### 2. Modification to the dark theme

#### TOC visited links
I made a modification on the **extra.css** to overwrite **dark_theme.css**

```css
/*
/////////////////////////////
/// visited links on toc ////
////////////////////////////

Modification by: Victor Fernandez
Description: modification of the visited links on TOC to 
              solve contrast issue
*/

.md-nav__link:visited{
  color: #808080;
}

.md-nav__link[data-md-state=blur] {
    color: #808080;
}
```
This modification wants to change the color of the visited links in the TOC, by default this visited link ( or permalinks) are black, this black color against black background present low contrast, thus it is difficult to read, therefore the modification.

#### Blockquote 

block quote has the same problem with the contrast, like the visited link in toc, thus these changes in the **extra.css** to overwrite **dark_theme.css** file

```css
/*
////////////////////
/// Blockquote/////
///////////////////

Modification by: Victor Fernandez
Description: modification of the blockquote to 
              solve contrast issue
*/

.md-typeset blockquote {
  color: #808080;
  border-left-width: 0.2rem;
  border-left-style: solid;
  border-left-color: #808080;
}
```

### Modification color of the `nav` and size of the icon

Again the modification was done on the `extra.css` file 

```css
/* 
///////////////////////////////////////////
// Modification Nav color and icon size////
///////////////////////////////////////////
*/
[data-md-color-primary=deep-purple] .md-header, [data-md-color-primary=deep-purple] .md-hero {
    background-color: #4f3378;
}

[data-md-color-primary=deep-purple] .md-tabs {
    background-color: #4f3378;
}

a.md-header-nav__button.md-logo img{
  width: 48px;
  height: 48px;
}
```

## Modifications to codehilite.css (extra.css)

In order to change how the inline code ( `this` in line code ) and solve the contrast problems ( before was black) I made a change in **extra.css** that overwrite the original **codehilite.css** code, as follow:

```css
/*
/////////////////
// Inline Code //
/////////////////
*/
.md-typeset code {
  color: #ae81ff !important;
  background-color: #313131 !important;
  box-shadow: 0.29412em 0 0 rgba(0,0,0,.07), -0.29412em 0 0 rgba(0,0,0,.07);
}
```


### Modification to footnote strings color

To change the color of the footnotes i made a chang ein the css

```css
.md-typeset div.footnote {
  color: #808080;
}
```


>"To every man upon this earth, death cometh soon or late, And how can man die better, Than facing fearful odds, for the ashes of his fathers, And the temples of his gods." 
