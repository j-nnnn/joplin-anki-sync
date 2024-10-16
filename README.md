# joplin-anki-sync
Automated management of Anki flashcards based on Joplin notes for effective spaced repetition learning. 

# Requirements
- Joplin Web clipper service
- Anki AnkiConnect add-on
- [Markdown and KaTex Support](https://ankiweb.net/shared/info/1087328706) Plugin for Anki

# Configuration
- Clone `https://github.com/abletsoff/joplin-anki-sync`
- Create and copy Joplin Web Clipper authorization token

![clipper](https://github.com/abletsoff/joplin-anki-sync/blob/main/images/clipper.png?raw=true)
- Create `token.json` file in the `joplin-anki-sync` directory with the following content:
``` json
{
        "token":"paste_your_authorization_token_here"
}
```
- Adjust `config.json` file for your personal setup

# Demo
## Script execution
![terminal](https://github.com/abletsoff/joplin-anki-sync/blob/main/images/terminal.png?raw=true)

## Anki card browse
![anki](https://github.com/abletsoff/joplin-anki-sync/blob/main/images/anki.png?raw=true)

## Joplin note
![joplin](https://github.com/abletsoff/joplin-anki-sync/blob/main/images/joplin.png?raw=true)

# joplin-anki-sync algorithm 
- Goes through Joplin folders (specified in `config.json`)
- Separate each Joplin topic at markdown Heading Level 1 (e.g. `# Topic 1`) 
- Generate Anki flashcard based on the Joplin topic. Flashcard front: Joplin note name + `# Topic 1`; flashcard back: Joplin topic content. In the joplin_anki-sync_mathjax.py script, the KaTeX syntax from Joplin is replaced with the MathJaX syntax from Anki ( e.g., \$\$ math \$\$  -> \\[ math \\] )
- Check if there is an Anki flashcard with the same front
  - There is no flashcard with the same front: create new flashcard in Anki deck
  - There is flashcard with the same front, back hash is the same: do nothing
  - There is flashcard with the same front, back hash is not the same: remove old flashcard & create new one
