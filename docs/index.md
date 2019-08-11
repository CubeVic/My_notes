# My Notes

This is where I store all notes about the different topics im learning, the idea is to have easy access to the notes from anywhere, initially will be locally and in github eventually to a personal server
I'm using MkDocs to generate this "documentation" more information visit [mkdocs.org](https://mkdocs.org).


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

## Modification to the dark theme

### TOC visited links
I made a modification on the **dark_theme.css**

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

### Blockquote 

block quote has the same problem with the contrast, like the visited link in toc, thus these changes in the **dark_theme.css** file

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

## Modifications to codehilite.css

In order to change how the inline code ( `this` in line code ) and solve the contrast problems ( before was black) I made a change in  Codehilite.css, as follow:

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

>"To every man upon this earth, death cometh soon or late, And how can man die better, Than facing fearful odds, for the ashes of his fathers, And the temples of his gods." 
