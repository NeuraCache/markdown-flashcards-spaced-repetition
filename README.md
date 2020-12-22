
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
| Batch import of One-Line Flashcards | - |
| One-Line Spaced Repetition  | ✅ |
| Batch import of One-Line Spaced Repetition | - |
| Micro-Cards | ✅ |
| Regular Flashcards | ✅ |
| Regular Spaced Repetition | ✅ |

## Full Example

See this .md file, which is ready to use with NeuraCache.

[example_note.md](example_note.md)

It contains all types of supported cards.

# Specification

## One-Line Cards

### One-Line Flashcards

question : answer #flashcard #optionaltag1 #optionaltag2

**Example:**

⌥⏎ : follow link #flashcard #intellij #shortkeys

### Batch import of One-Line Flashcards

#flashcard #optionaltag1 #optionaltag2 
- question 1 : answer 1
- question 2 : answer 2

**Example:**

#flashcard #intellij #shortkeys
- **⌥⏎**: follow link
- **⌥o**: quick switcher
- **⌥⌘⏎**: open in new pane

### One-Line Spaced Repetition

content #spaced #optionaltag1 #optionaltag2

**Example:**

"We are what we repeadetly do" #spaced

### Batch import of One-Line Spaced Repetition

#spaced #optionaltag1 #optionaltag2 
- content 1
- content 2

**Example:**

#spaced #quotes
- "We are what we repeadetly do" Will Durant
- “Be yourself; everyone else is already taken.” Oscar Wilde

## Micro Cards

Same as "One-Line Flashcards" but instead of a #flashcard you can use ⚡️ or 🧠
This is great for Github README.md files where a #flashcard could look strange.

**Example:**

**⌥⏎**: follow link ⚡️

## Regular Cards

Regular cards allow creating cards with images, latex, lists, etc.

A horizontal rule is used to mark the end of the card.

You can use: 

\-\-\-, \- \- \-, \*\*\*, \* \* \*

### Regular Flashcards
question #flashcard #optionaltag1 #optionaltag2 

answer

\-\-\-

**Example:**

Radii of stable orbits in the Bohr model #flashcard 

$a_0  = \frac{{ \hbar ^2}}{{m_e ke^2}}$

$\Delta E = h\nu$

$c = \lambda \nu$

\-\-\-

### Regular Spaced Repetition

#spaced #optionaltag1 #optionaltag2 

content

\-\-\-

**Example:**

#spaced #quotes

"We are what we repeatedly do. Excellence, then, is not an act, but a habit."

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/The_collection_of_11_volumes_of_the_Story_of_Civilization_by_Will_and_Ariel_Durant.jpg/220px-The_collection_of_11_volumes_of_the_Story_of_Civilization_by_Will_and_Ariel_Durant.jpg)

\-\-\-

Credits: 
[Reto Stamm](https://github.com/retospect) for starting the conversation and initial concept 👍

