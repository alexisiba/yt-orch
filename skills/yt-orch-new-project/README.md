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

The documents are created in the language you are writing in, unless you ask for another one. File names, headings and guidance comments are translated; frontmatter keys stay in English. [Custom templates](#custom-templates) are never translated. The language is recorded in `Overview.md` so later work on the project keeps using it.

## Custom templates

If you already have your own templates, you can use them instead of the bundled ones. Tell the agent which templates to use and where they are, for example:

- "New project called How I organize my week, using idea, research and script from ~/templates"
- "New project called How I organize my week, using my idea from ~/templates and the rest of the defaults"

Be specific: the agent only uses custom templates when you name them and their location. It never searches for them on its own.

- **Matching.** A template matches when its file name, without extension, is the name you gave, ignoring case, accents, spaces, hyphens and underscores. `idea` matches `Idea.md`, but not `idea-v2.md`.
- **Copied as they are.** Your templates are not reviewed, interpreted or translated. Only `{{project_name}}`, `{{date}}` and `{{language}}` are filled in if they appear; any other syntax (for example, Templater's) is left untouched. Make sure your templates are ready before you list them.
- **Only what you ask for.** Only the templates you name are created. Bundled templates are added only if you ask for them, as in the second example.
- **Missing templates are skipped.** If a template is not found, or its name matches more than one file, it is skipped and listed in the final report. It is never replaced with a bundled template. To add it later, ask the agent to add the missing files to the project.
- **Wrong location.** If the location does not exist, or none of the templates you named are in it, the agent asks before creating anything.

## What it does not do

- Write the script.
- Edit, fill in or review an existing project.
- Create media folders. Documents reference media by path when you have it.
