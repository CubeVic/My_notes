>Datamuse is a collection of free websites, mobile apps, and APIs designed to help people create and communicate more effectively.

I will focus in this note sin the [datamuse API](https://www.datamuse.com/api/)

## What is it

the website describe it as: 
*The Datamuse API is a word-finding query engine for developers.*

## For what I can use it?

| To find | end point |
|:------------------------------------------------------------------------|:-----------------------------------------------|
|Meaning similar to a sentence                                             |`/words?ml=[sentence]`                          |
|Related with a word that start with b or ends with a                     |`/words?ml=duck&sp=b*`or `/words?ml=spoon&sp=*a`|
|Word that sound like                                                     |`/words?sl=jirraf`                              |
|A word that start with t has 2 letters between and end k                  |`/words?sp=t??k`                                | 
|Words that are spelled similarly to hippopotamus                          |`/words?sp=hipopatamus`                         |
|Words that rhyme with forgetful                                          |`/words?rel_rhy=forgetful`                      |
|Words that rhyme with grape that are related to breakfast 	              |`/words?ml=breakfast&rel_rhy=grape`             |
|Adjectives that are often used to describe ocean 	                      |`/words?rel_jjb=ocean`                          |
|Adjectives describing ocean sorted by how related they are to temperature|`/words?rel_jjb=ocean&topics=temperature`       |
|Nouns that are often described by the adjective yellow 	              |`/words?rel_jja=yellow`                         |
|Words that often follow "drink" in a sentence, that start with the letter w |`/words?lc=drink&sp=w*`                      |
|Words that are triggered by (strongly associated with) the word "cow"    |`/words?rel_trg=cow`                            |
|Suggestions for the user if they have typed in rawand so far 	          |`/sug?s=rawand`                                 |

## End points

The feacture can be access on: 

* `api.datamuse.com/words`
* `api.datamuse.com/sug`

## `/words` endpoint

>End point return a list of words 

we can device divide it in 3 categories;   
1. Hard constraints results (`rd`,`sl`,`sp`,`rel_[code]` and `v`). 
2. Context hints (`topics`, `lc`, `rc`). 
3. Those that affect the order of the results returned.

### Hard Constraints

#### Means like `ml`

This will give back words or sentence that has similar meaning 

```
https://api.datamuse.com/words?ml=ringing+in+the+ears
or
https://api.datamuse.com/words?ml=Python
```

#### Means like `ml`

#### Sound like `sl`

#### spelled like `sp`

#### Related word `rel_[code]`

#### Vocabulary used `v`