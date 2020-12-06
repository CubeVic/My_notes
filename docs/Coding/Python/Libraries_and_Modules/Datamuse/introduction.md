# Python-Datamuse

![datamuse](images/datamuse_logo.png){: .center}

##Description

Python wrapper for [Datamuse API](https://www.datamuse.com/api/)

## Installation
```
pip3 install python-datamuse
```
## Example

```python
from datamuse import datamuse
api = datamuse.Datamuse()
ninth_rhymes = api.words(rel_rhy='ninth', max=5)
#ninth_rhymes
#[]
orange_rhymes = api.words(rel_rhy='orange', max=5)
#orange_rhymes
#[{'word': 'door hinge', 'score': 74, 'numSyllables': 2}]
yellow_things = api.words(rel_jja='yellow', max=5)
#yellow_things
#[{'word': 'fever', 'score': 1001}, {'word': 'color', 'score': 1000}, {'word': 'flowers', 'score': 999}, {'word': 'light', 'score': 998}, {'word': 'colour', 'score': 997}]
foo_complete = api.suggest(s='foo', max=10)
#foo_complete
#[{'word': 'food', 'score': 3888}, {'word': 'foot', 'score': 3041}, {'word': 'fool', 'score': 1836}, {'word': 'football', 'score': 1424}, {'word': 'footage', 'score': 1328}, {'word': 'footprint', 'score': 1082}, {'word': 'foolish', 'score': 967}, {'word': 'foof', 'score': 930}, {'word': 'footing', 'score': 786}, {'word': 'foolproof', 'score': 697}]
```
> Note that the default number of results is set to 100. You can set the default max to something else using the `set_max_default` method, e.g. `api.set_max_default(300)`. Datamuse only returns 1000 results max.

## Parameters for `word` methods
Description of the method
> This endpoint returns a list of words (and multiword expressions) from a given vocabulary that match a given set of constraints. See <https://www.datamuse.com/api/> for the official Datamuse API documentation for the `/words` endpoint.  
**:param `**kwargs`:** Query parameters of constraints and hints.
**:return:** A list of words matching that match the given constraints.

*	Means like `ml`
*	Sounds like `sl`
*	Spelled like `sp`
*	Related word `rel_[code]`
	*	`jja` Popular nouns modified by the given adjective. (gradual → increase)
	*	`jjb` Popular adjectives used to modify the given noun. (beach → sandy)
	*	`syn` Synonyms (ocean → sea)
	*	`trg` "Triggers" (words that are statistically associated with the query word in the same piece of text.) (cow → milking)
	*	`ant` Antonyms (late → early)
	*	`spc` "Kind of" direct hypernyms (gondola → boat)
	*	`gen` "More genaral than" direct hyponyms (boat → gondola)
	*	`com` "Comprises" direct holonyms (car → accelerator)
	*	`par` "part of" direct meronyms (trunk → tree)
	*	`bga` Frequent followers (wreak → havoc)
	*	`bgb` Frequent predecessors (havoc → wreak)
	*	`rhy` Rhymes (spade → aid)
	*	`nry` Approximate rhymes (forest → chorus)
	*	`hom` Homophones, sound-alike (course → coarse)
	*	`cns` Consonant match (sample → simple)
*	Identifier for the vocabulary to use, `v`, if none is provided will use $550,000$ term from English. the value `es` specify $500,000$ term, the value `enwiki` specifies and approximately 6 millions-term.
*	Topic words `topics` (An optional hint to the system about the theme of the document being written)
*	Left context `lc` An optional hint to the system about the word that appears immediately to the left of the target word in a sentence.
*	Right context `rc` An optional hint to the system about the word that appears immediately to the right of the target word in a sentence.
*	Maximum `max`
* 	Metadata flag `md` A list of single-letter codes (no delimiter) requesting that extra lexical knowledge be included with the results.   

	| Letter  | Description    |
	| :------:| ---------------|
	| `d`     | Definitions    |
	| `p`     | Parts of speech|
	| `s`     | Syllable count |
	| `r`     | Pronunciation  |
	| `f`     | word frequency |

*	Query echo `qe` This is useful for looking up metadata about specific words. For example, `/words?sp=flower&qe=sp&md=fr` can be used to get the pronunciation and word frequency for flower.

## Parameters for `suggest` methods

*	`s` Prefix hint string; typically, the characters that the user has entered so far into a search box.  
*	`max` Maximum number of results to return.  
*	`v` 	Identifier for the vocabulary to use.  

