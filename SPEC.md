# Markdown Flashcards: the specification

Version 2.0

This specification aims to standardize the creation of flashcards and cards for spaced repetition in Markdown files. It says exactly how a file is read into cards, so that any app can read the same notes the same way. For a friendlier tour, start with the [README](README.md).

Two principles shape it. A note stays an ordinary Markdown note, and a reader can find the cards in it one line at a time, without parsing the whole document.

[NeuraCache](https://neuracache.com/) is one app that implements it. Where this document describes what NeuraCache does beyond the format, it says so.

**Contents**

1. [Terms](#1-terms)
2. [Markers and tags](#2-markers-and-tags)
3. [Rule lines](#3-rule-lines)
4. [One-line cards](#4-one-line-cards)
5. [Regular cards](#5-regular-cards)
6. [Two-sided flashcards](#6-two-sided-flashcards)
7. [Multiple choice](#7-multiple-choice)
8. [Tag groups](#8-tag-groups)
9. [Outline cards](#9-outline-cards)
10. [Card content](#10-card-content)
11. [Identity and syncing](#11-identity-and-syncing)
12. [Writing portable notes](#12-writing-portable-notes)
13. [History](#13-history)

## 1. Terms

| Term | Meaning |
| --- | --- |
| **Flashcard** | A card with a question and an answer. |
| **Spaced repetition card** | A card with one side: its text. |
| **Multiple-choice card** | A flashcard answered by picking one of several choices. |
| **Marker** | The tag that makes a line a card: `#flashcard` or `#spaced`. |
| **Marker line** | The line that carries a marker. It starts a card. |
| **Deck tag** | Any other tag on a marker line. It names a deck. |
| **Rule line** | A horizontal rule. It ends a side of a card, or the card. |
| **Word** | A run of characters between spaces. |

A file is read from top to bottom, one line at a time. A line that belongs to no card is ordinary text and is ignored.

## 2. Markers and tags

1. A **tag** is a word that starts with `#`, has at least one more character, and is not made of `#` alone. So `##` in a heading is not a tag.
2. The **markers** are `#flashcard` and `#spaced`. Write them in lower case, as words of their own: `answer #flashcard`, not `answer#flashcard`.
3. In a [one-line flashcard](#4-one-line-cards), the emoji ⚡ (U+26A1) or 🧠 (U+1F9E0) may stand in for `#flashcard`. The emoji is a word of its own, with or without the variation selector U+FE0F.
4. Tags are read from the marker line only. A tag inside an answer is text.
5. A **nested tag** such as `#science/physics` gives the card two deck tags: `#science` and `#physics`.
6. Every word that starts with `#` is taken out of the marker line before its text becomes a question or a card. Heading marks go the same way, so `## A question #flashcard` has the question `A question`.

Readers may let people rename the markers. In NeuraCache this is **Sources → Markdown**: the flashcard tag, the spaced repetition tag and the one-line separator can be changed, and the emoji markers turned off.

## 3. Rule lines

A line is a rule line when it contains any of:

```markdown
---
- - -
***
* * *
```

"Contains" is literal. A line with other text around one of these sequences is still a rule line. Two things follow:

- the divider row of a table (`| --- | --- |`) is a rule line;
- so is a line with bold italics written as `***text***`.

A rule line is never part of a card.

## 4. One-line cards

### 4.1 One-line flashcard

```markdown
question :: answer #flashcard #deck-tag
question :: answer ⚡️ #deck-tag
```

A line is a one-line flashcard when it contains the separator `::` and a flashcard marker (`#flashcard`, ⚡ or 🧠) as a word of its own.

- The **question** is the text before the first separator.
- The **answer** is everything after it. Later separators belong to the answer.
- Both are trimmed. The answer must not be empty.
- Tags may stand anywhere on the line. They are removed from the text.

A one-line flashcard written with an emoji is also called a **micro card**.

### 4.2 One-line spaced repetition card

```markdown
something worth remembering #spaced #deck-tag
```

A line is a one-line spaced repetition card when it contains `#spaced` and has text besides its tags. The card's text is the line without its tags.

### 4.3 The separator

The separator is `::`. Put a space on each side of it.

The first version of this format used a single colon (`question : answer`). Readers may offer it as a setting. It is no longer the default, because a colon is common in ordinary sentences.

## 5. Regular cards

### 5.1 Regular flashcard

```markdown
question #flashcard #deck-tag
answer line
answer line
- - -
```

A line that contains `#flashcard`, is not a one-line card and does not begin with `#flashcard` starts a regular flashcard.

- The **question** is the marker line without its tags.
- If the marker line holds only tags, the question is the nearest line above it that is not empty:

  ```markdown
  What is the powerhouse of the cell?
  #biology #flashcard
  the mitochondrion
  - - -
  ```

- The **answer** is every line after the marker line, up to the [end of the card](#53-where-a-card-ends).

### 5.2 Regular spaced repetition card

```markdown
#spaced #deck-tag
card text
card text
- - -
```

A line that contains `#spaced` and no text besides tags starts a regular spaced repetition card. The card's text is every line after it, up to the end of the card.

With no rule line below it, the card runs to the end of the file. A `#spaced` line at the top of a note turns the whole note into one card.

### 5.3 Where a card ends

A regular card ends at the first of:

1. a rule line;
2. a tag group line ([section 8](#8-tag-groups));
3. a line that starts another card: any line that contains a marker, or is a one-line card;
4. the end of the file.

Because of rule 3, the words `#flashcard` and `#spaced` cannot appear inside a card's text.

## 6. Two-sided flashcards

```markdown
#flashcard #deck-tag
question line
question line
- - -
answer line
answer line
- - -
```

A line that begins with `#flashcard`, and is not a one-line card, starts a two-sided flashcard.

- The **question** is every line after the marker line, up to the first rule line.
- The **answer** is every line after that rule line, up to the [end of the card](#53-where-a-card-ends).

## 7. Multiple choice

```markdown
Which planet is the largest? #flashcard
- [ ] Earth
- [x] Jupiter
- [ ] Saturn
- [ ] Neptune
- - -
```

A flashcard whose answer is a task list with exactly one ticked item is a multiple-choice card. The ticked item is the **right answer**. The unticked items are the **wrong answers**.

This is a reading of an ordinary flashcard, not a new kind of marker. A reader that does not support it shows a flashcard whose answer is the list.

### 7.1 A task item

A task item is one line, made of these parts in order:

1. indentation: spaces or tabs, or none;
2. a bullet: `-`, `*` or `+`;
3. one or more spaces or tabs;
4. a box: `[ ]` for unticked, `[x]` or `[X]` for ticked;
5. one or more spaces or tabs and the choice's text, or nothing at all.

The choice's text is trimmed. It is Markdown, like any other card text.

These are not task items: `1. [x] Paris` (a numbered item), `- [y] Paris` (another letter in the box), `- [x]Paris` (no space after the box). Only ordinary spaces and tabs separate the parts.

### 7.2 When a flashcard is multiple choice

All of these must hold:

1. The card has a question.
2. The answer starts with a task item, and holds nothing but task items and blank lines. Text before, between or after the items keeps the card a regular flashcard.
3. Every item has the same indentation, character for character. Nested items keep the card a regular flashcard. A list indented as a whole is fine.
4. Exactly one item is ticked, and it has text.
5. At least one unticked item is a usable wrong answer: it has text, and its text is not the right answer again (compared without case or surrounding space).

Unticked items without text are skipped. Wrong answers that repeat each other count once.

In every other case the card is a regular flashcard and its answer is the list as written. That includes a list with no item ticked, with two or more ticked, or with a ticked item alone.

### 7.3 Which flashcards

The rule applies wherever a flashcard has a multi-line answer: [regular](#51-regular-flashcard), [two-sided](#6-two-sided-flashcards) and [outline](#9-outline-cards) flashcards, with or without a tag group.

A [one-line flashcard](#41-one-line-flashcard) is never multiple choice.

### 7.4 Reviewing

A card may list any number of wrong answers. A review shows the right answer with up to three of them, drawn at random, in a shuffled order.

### 7.5 Task dates

[Obsidian Tasks](https://publish.obsidian.md/tasks/) writes dates at the end of a task, such as the done date it adds when an item is ticked. Left in, `- [x] Paris ✅ 2026-11-22` would give the right answer away.

A run of date marks at the end of a choice is therefore removed. Each mark is:

- one of ✅ ➕ 📅 📆 🗓 ⏳ ⌛ 🛫 ❌, with or without U+FE0F;
- then one or more spaces or tabs;
- then a date written `YYYY-MM-DD`.

A block link written straight after the dates (a space, `^`, then letters, digits or hyphens, ending the line) is removed with them. Nothing else is removed: other Tasks marks, such as priority and recurrence, stay in the choice.

### 7.6 Changing a card

Whether a flashcard is multiple choice is decided each time the file is read. Tick a second item, untick them all, or add a line of text, and the card is a regular flashcard at the next sync. Restore the list and it is multiple choice again. The card keeps its schedule and history throughout, because its question has not changed ([section 11](#11-identity-and-syncing)).

## 8. Tag groups

```markdown
#tags #cats #animals

Top speed of a cat :: 30 mph #flashcard
Is a cat a tiger? :: 95.6% genetically ⚡️
```

A line that contains `#tags` followed by a space is a tag group line. Its tags, other than `#tags` itself, are added to every card that starts below it.

- A group lasts until the next tag group line, which replaces it, or the end of the file.
- A card has its own tags and its group's tags.
- A tag group line ends the card above it.

## 9. Outline cards

Outliners such as [Logseq](https://logseq.com/) write a note as nested bullets. In an outline, indentation ends a card, so rule lines are not needed.

Indentation is counted in **tabs**.

### 9.1 Outline flashcard

```markdown
- question #flashcard #deck-tag
	- answer
		- more of the answer
	- still the answer
- not part of the card
```

A bullet (`-`) that carries a marker starts an outline card.

- The **question** is the bullet's text without its tags.
- The **answer** is every following line indented deeper than the question's bullet. It keeps its bullets, and its indentation relative to the question.
- The card ends at the first line indented no deeper than its own bullet. A blank line ends it too. A rule line, a tag group line and a new marker line end it as they end a regular card.

### 9.2 Outline spaced repetition card

```markdown
- a heading for the card #spaced
	- first point
	- second point
```

With `#spaced`, the bullet's own text is the first line of the card, and the lines indented under it are the rest.

### 9.3 One-line cards in an outline

```markdown
- question :: answer #flashcard
```

A bullet that is a one-line card is read as one ([section 4](#4-one-line-cards)), without the bullet.

### 9.4 Batches

```markdown
- #flashcard #biology
	- Powerhouse of the cell?
		- the mitochondrion
	- Where is DNA kept?
		- in the nucleus
```

A bullet that begins with a marker is a **batch**. Each bullet one level under it becomes a card of that kind, with the batch's tags. Deeper bullets are that card's answer. The batch ends where the indentation returns to the batch's own level.

### 9.5 Logseq properties

Lines that Logseq adds under a block are left out of a card: those starting with `card-last`, `card-repeats`, `card-next`, `card-ease`, `title::` or `collapsed::`.

## 10. Card content

A card's text is Markdown, and is drawn as Markdown. Two conventions are part of the format.

### 10.1 Images

An image is written in one of two ways:

```markdown
![alt text](path-or-url)
![[image.png]]
```

The second is Obsidian's embed. It is read as `![](image.png)`.

An image may stand anywhere in a card's text: in an answer, in a spaced repetition card, or in the question of a [two-sided flashcard](#6-two-sided-flashcards).

### 10.2 Where an image comes from

- **A web address** (`https://…`) is loaded from that address when the card is shown.
- **Anything else is a file.** It is found among the files that were imported or synced together with the note, so the picture has to come along with the note:
  - when a folder is imported or synced, every image inside it, at any depth, is available to every note in it;
  - when single files are imported, the images have to be selected in the same step as the note.

A file is matched by its name, the last part of its path. That is how an Obsidian embed such as `![[cell.png]]` finds a picture kept in another folder of the vault. So give image files distinct names.

### 10.3 Image size

A size is written after a `|` in the alt text or in the embed, or as the whole alt text.

| Written | Size |
| --- | --- |
| `![[image.png\|300]]` | 300 wide |
| `![300](image.png)` | 300 wide |
| `![alt\|300](image.png)` | 300 wide |
| `![alt\|300x200](image.png)` | 300 wide, 200 high |

## 11. Identity and syncing

A reader that keeps a schedule has to recognise a card when it reads the file again.

- A **flashcard** is identified by its question.
- A **spaced repetition card** is identified by its text.

So:

- editing a flashcard's answer, its tags or its choices keeps the card and its history;
- editing a flashcard's question, or a spaced repetition card's text, makes a new card.

When a folder is synced and a card is gone from its file, NeuraCache removes the card. The setting is **Single Source of Truth** and it is on by default.

## 12. Writing portable notes

Notes that follow these habits read the same everywhere.

- **End cards with `---` or `- - -`.** NeuraCache for Android also ends a card at a line made only of underscores (`___`). The iPhone, iPad and Mac apps do not, so don't rely on it.
- **Keep tables and `***bold italics***` out of cards.** Both make a rule line ([section 3](#3-rule-lines)).
- **Use `::` with a space on each side**, and keep `::` out of the question line of a regular flashcard: a marker line that contains the separator is a one-line card.
- **Keep words that start with `#` off marker lines** unless they are tags. `Issue #42` on a one-line card loses its `#42`.
- **Indent outlines with tabs.**
- **Write `[x]`, a space, then the choice.**

## 13. History

| Version | Changes |
| --- | --- |
| **2.0** | Multiple choice. `::` is the default one-line separator. Outline cards, batches, nested tags, image sizes, card identity and the exact end-of-card rules are written down. |
| **1.0** | One-line cards, micro cards, regular cards, two-sided flashcards, tag groups. |

Multiple choice is read by NeuraCache 3.8 for iPhone and iPad, 1.6 for Mac and 3.3 for Android.
