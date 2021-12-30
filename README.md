
# Goal

This repository aims to standardize the creation of Flashcards and cards for Spaced Repetition in Markdown files.

## Use Cases

- Create Portable decks of flashcards and cards for spaced repetition.
- Include flashcards and spaced repetition cards in notes (in tools like [Obsidian](https://obsidian.md/))
- Non intrusive flashcards in GitHub README.md files to facilitate the retention of key concepts.

## Quick Example

How many people are bitten by snakes each year? : 5.3M ⚡️

How many people die each year from snake bites? : ~130k ⚡️

See gif below for an example review of 👆 cards in [NeuraCache](https://neuracache.com/)

![](images/neuracache-example.gif "Example Review in NeuraCache")

## NeuraCache Support

| Type  | Supported |
| ------------- | ------------- |
| One-Line Flashcards  | ✅ |
| One-Line Spaced Repetition  | ✅ |
| Micro-Cards | ✅ |
| Regular Flashcards | ✅ |
| Regular Spaced Repetition | ✅ |
| Two-Sided Flashcards | ✅ |
| Tag Groups | ✅ |

Full documentation with examples: 

https://wiki.neuracache.com/markdown-flashcards

🎥  Videos: 

One-Line and Micro Cards

https://www.youtube.com/watch?v=6L3Zcm7HqDw

Regular Cards

https://www.youtube.com/watch?v=RsV3qMUkgoA

## Example .MD file

See this .md file, which is ready to use with NeuraCache.

[example_note.md](example_note.md)

It contains all types of supported cards.

# Specification

## One-Line Cards

### One-Line Flashcards
```
question : answer #flashcard #optionaltag1 #optionaltag2
```

**Example:**
```
⌥⏎ : follow link #flashcard #intellij #shortkeys
```
### One-Line Spaced Repetition
```
content #spaced #optionaltag1 #optionaltag2
```
**Example:**
```
"We are what we repeadetly do" #spaced
```
## Micro Cards

Same as "One-Line Flashcards" but instead of a #flashcard you can use ⚡️ or 🧠
This is great for Github README.md files where a #flashcard could look strange.

**Example:**
```
⌥⏎: follow link ⚡️
```
## Regular Cards

Regular cards allow creating cards with images, latex, lists, etc.

A horizontal rule is used to mark the end of the card.

You can use: 

\-\-\-, \- \- \-, \*\*\*, \* \* \*

### Regular Flashcards
```
question #flashcard #optionaltag1 #optionaltag2 

answer

- - -
```
**Example:**
```
Radii of stable orbits in the Bohr model #flashcard 

$a_0  = \frac{{ \hbar ^2}}{{m_e ke^2}}$

$\Delta E = h\nu$

$c = \lambda \nu$

- - -
```
### Regular Spaced Repetition
```
#spaced #optionaltag1 #optionaltag2 

content

- - -
```
**Example:**
```
#spaced #quotes

"We are what we repeatedly do. Excellence, then, is not an act, but a habit."

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/The_collection_of_11_volumes_of_the_Story_of_Civilization_by_Will_and_Ariel_Durant.jpg/220px-The_collection_of_11_volumes_of_the_Story_of_Civilization_by_Will_and_Ariel_Durant.jpg)

- - -
```
## Two-Sided Flashcards
```
#flashcard #optionaltag1 #optionaltag2 

question

- - -

answer

- - -
```
**Example:**
```
#flashcard #git   

![](https://avatars.githubusercontent.com/u/18133?s=200&v=4)   
What does this command do?   
    
`git clean -nfd`    
   
- - -     
remove current untracked files/directories   
d - directories     
f - files      
n - show result first     
- - -     
```
## Tag Groups

Every card below #tags will have all the tags attached automatically 👍 (#tagA #tagB #tagC)
```
#tags #tagA #tagB #tagC

Question 1 #flashcard 
Answer 1
- - -

Question 2 : Answer 2 #flashcard

```
**Example:**
```
#tags #cats #animal #nature

max speed of a cat : 30 mph #flashcard 
is cat a tiger? : genetically 95.6% #flashcard
```
Credits: 

[Marcin Czech](https://twitter.com/marcin_czech) Regular Cards, Two-Sided Cards, Tag Groups, Spaced Repetition Cards

[Reto Stamm](https://github.com/retospect) Initial concept of One-Line and Micro Cards

Full documentation with examples: 

https://wiki.neuracache.com/markdown-flashcards
