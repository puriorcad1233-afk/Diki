# Architecture Overview

This repository is a small, self-contained Python terminal animation for a birthday greeting. The architecture is intentionally simple: one script generates the output directly in the terminal with no external dependencies or services.

```mermaid
flowchart LR
    User[User / Birthday Occasion] --> Script[happy_birthday_diki.py]

    subgraph PythonApp[Python Terminal App]
        Script --> Clear[clear()]
        Script --> Render[render(name, visible)]
        Script --> TypeText[type_text()]
        Script --> Animate[animate_name()]
        Script --> Cake[ASCII Cake Artwork]
        Script --> Message[Birthday Message]
        Render --> Font[FONT Letter Map]
        Animate --> Terminal[Terminal Screen]
        TypeText --> Terminal
        Cake --> Terminal
        Message --> Terminal
    end

    Terminal --> Output[Console Display]
    Output --> Viewer[User Viewing Greeting]
```

## Component Notes

- `happy_birthday_diki.py`: entry point; manages the animation flow.
- `clear()`: refreshes the terminal screen between frames.
- `render()`: builds large ASCII text by drawing each character from a predefined font map.
- `type_text()`: prints text gradually to simulate a typing effect.
- `animate_name()`: reveals the name one character at a time.
- `FONT`: stores the multi-line ASCII layout for letters.
- Terminal output: the final experience is displayed directly in the console without a database, API, or frontend.
