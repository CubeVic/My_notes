
Here some notes about the material Mkdocs extensions
more information in the [documentation](https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown/)

## Icons

To add custom Icons we need to use [Icons+Emojis](https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/)
We star with the configuration that give use access to some basic icons and emojies, later we explore the addition of
customized icons.

### Configuration 
add the following lines to `mkdocs.yml`
```yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:materialx.emoji.twemoji
      emoji_generator: !!python/name:materialx.emoji.to_svg
```
#### emojis :smile: 
it is recommended to use the shortcodes at [Emojipedia](https://emojipedia.org/twitter/)
we have the example of
```
:smile:
```
:smile:

#### Using icons :faces-one-up:
We can use icons too, in some case we need to make some extra modifications to the `mkdocs.yml`
```yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:materialx.emoji.twemoji
      emoji_generator: !!python/name:materialx.emoji.to_svg
      options:
        custom_icons:
          - overrides/.icons
```
and in the root directory next to `mkdocs.yml` we create a new folder called `overrides` and inside other call `.icons`
and inside we put the svg of the icons.

Now to call that icons we replace the `/` of the path for `-` like
```
:faces-guy-fawkes-mask:
```
:faces-guy-fawkes-mask:

We can find more icons here [materialdesignicons](https://materialdesignicons.com/)

Color can be added to the icons, we will need to add some CSS rules to later reference next to the icon, like this 
```CSS
.purple{
    color: #512DA8;
}
```
```
:faces-panda:{ .purple }
```
:faces-panda:{ .purple }

???important "colors for icons"
    .purple: #6745c2    
    .dark-purple: #6745c2  
    .royal-blue: #000062  
    .orange: #E66C10  
    .light-green: #629749   
    .dark-green: #003d00  
    .green: #32681

## [Admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/#supported-types)

These are basically call-outs. 

### Configuration
```yaml
markdown_extensions:
  - admonition
```

They are enabled by putting `!!!` later a key word
and bellow indented the content, like this 

```
!!!note
    this is an admonition
```

!!!note
    this is an admonition

We can modify the name by putting a different key word ( see [admonitions documentation](https://squidfunk.github.io/mkdocs-material/reference/admonitions/#supported-types))
or by adding the title in `"`.

```
!!!note "this is the title"
    this is an admonition
```
!!!note "This is the title"
    this is an admonition

we can make a dropdown close by default 

```
???note "This is az dropdown admonition"
    this is an admonition
```

???note "This is a dropdown admonition"
    this is an admonition

and open by adding "+"

```
???+ note "This is a dropdown call-out"
    this is an admonition
```

???+note "This is a dropdown call-out"
    this is an admonition

Here some example of other admonitions

```
!!! warning
    This is a warning 
```
!!! warning
    This is a warning 


<!--- 
TODO: add extensions
1. definition list  useful for projects
2. Footnotes.
3. Metadata.
4. pymdownx.details.
5. attr_list.
6. smarty.
7. md_in_html.
--->

## [Definition List](https://squidfunk.github.io/mkdocs-material/reference/lists/)

## [Footnotes](https://squidfunk.github.io/mkdocs-material/reference/footnotes/#adding-footnote-references)

##[Metadata]()
##[pymdownx.details]()
##[attr_list]()
##[smarty]()
##[md_in_html]()