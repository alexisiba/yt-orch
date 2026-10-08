# yt-orch-new-project

Start a new YouTube video project in seconds. The skill creates a folder named after your video with a set of markdown documents to help you take it from idea to publishing.

The documents are a starting point, not a workflow. Rename, delete, reorganize or extend them however you like.

## Usage

Ask your agent to start a new video project. For example:

- "New YouTube project called How I organize my week"
- "Let's make a video about home coffee brewing" (the agent suggests a name and waits for you to confirm it)
- "Set up a project for my next video in ~/Videos/YouTube"

## What it creates

```
How I organize my week/
├── Overview.md
├── Idea.md
├── Research.md
├── Sources.md
├── Outline.md
├── Script.md
├── Production.md
└── Publishing.md
```

| Document | Purpose |
|---|---|
| `Overview.md` | Project hub: one-line pitch, metadata and links to every document |
| `Idea.md` | Premise, packaging (working title and thumbnail concept), audience, angle, what the viewer takes away, and reference videos |
| `Research.md` | Findings, facts to verify, open questions |
| `Sources.md` | References and what each one supports |
| `Outline.md` | Hook that delivers on the packaging, sections and ending |
| `Script.md` | What will be said in the video: hook, body and ending |
| `Production.md` | Shot list, b-roll, and references to where media lives |
| `Publishing.md` | Final title and thumbnail variations, description, tags, shorts |

`Overview.md` has frontmatter (`status`, `created`, `language` and the `youtube` tag) and relative links to the other documents, so the project works well in Obsidian or any markdown editor.

`Script.md` only has a few headings and guidance comments, ready for you to write in your own format. The agent never writes the script while creating the project; you write it yourself or with the help of a script skill.

## How it works

### Name

The folder name is the video's working name, kept as you wrote it: spaces, capitalization and accents included. Only characters the filesystem cannot store are removed, and the agent tells you if it had to change anything.

### Location

The agent picks where to create the project in this order:

1. The location you gave.
2. The current folder, if its name already matches the project name.
3. The current folder, if it clearly holds video projects (it already contains some, or its name refers to YouTube).
4. If a folder nearby looks like it could hold your video projects, the agent asks you where to create it.
5. Otherwise, a new folder inside the current one.

### Existing content

Nothing is ever deleted, moved, renamed or overwritten. If the project folder already exists and has content, the agent asks you to choose:

- **Cancel** — do nothing.
- **Use a different name** — create the project under another name.
- **Add missing files only** — create only the documents that are not there yet.

Folders with a similar but different name are left alone. The agent mentions them so you can check whether they are the same project.

### Language

The documents are created in the language you are writing in, unless you ask for another one. File names, headings and guidance comments are translated; frontmatter keys stay in English. The language is recorded in `Overview.md` so later work on the project keeps using it.

## What it does not do

- Write the script.
- Edit, fill in or review an existing project.
- Create media folders. Documents reference media by path when you have it.
