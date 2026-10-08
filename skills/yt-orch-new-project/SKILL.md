---
name: yt-orch-new-project
description: Creates the scaffolding for a new YouTube video project — a folder named after the video containing markdown documents for the idea, research, sources, outline, script, production and publishing. Use when the user wants to start, create or set up a new video project, or add the starter documents to an existing project folder, e.g. "let's make a video about Godot", "new YouTube project called X", "set up a project for my next video". Do not use to edit, write content in or review an existing project.
metadata:
  version: "0.3.0"
---

# yt-orch-new-project

Create a new YouTube video project: one folder, named after the video, containing a set of markdown documents that help the user document the video from idea to publishing.

The project is only a place to think and work. The documents are scaffolding: the user can rename, delete, reorganize or extend them at any time, and nothing else should depend on them keeping their original shape.

## Principles

- **Never destroy.** Do not delete, move, rename or overwrite anything that already exists. When something is in the way, ask; never resolve it by removing content.
- **Project structure is user-owned.** Create the scaffolding only for the new project. Never reorganize existing folders to match it.
- **Use the tools you have.** This skill describes outcomes, not tools. Inspect, create and write files with whatever the environment provides.
- **Speak the user's language.** See [Language](#language).
- **Do not prescribe a workflow.** The documents support the user's process; they do not impose an order or tell the user what to do.

## Workflow

### 1. Get the project name

The project name is the working name of the video, written in natural language (e.g. `Exploring Godot for the first time`). It is not necessarily the final YouTube title.

- If the user gave an explicit name, use it exactly as given. Respect their creative choice.
- If the user described the video but did not give an exact name, suggest one and ask whether it works or whether they want to choose their own. Do not create anything until the name is confirmed.

The folder name is the project name. Keep spaces, capitalization and accents. Only remove characters the filesystem cannot store (`/ \ : * ? " < > |` and control characters) and any trailing dots or spaces. If you had to change the name, tell the user.

Two folder names **match** when they are equal ignoring case, spaces, hyphens and underscores (`Exploring Godot` matches `exploring-godot`). Use this comparison everywhere this skill checks whether a folder has the project name.

### 2. Choose the location

Resolve the **project folder**: the folder that will contain the project's documents. In most cases it is a new folder with the project name inside a parent location; in rule 2 it is the current directory itself. Apply the first rule that fits:

1. **The user named a location** → create the project folder there. If that location does not exist, confirm it with the user before creating it, since it may be a typo.
2. **The current directory is the project folder** — its name matches the project name → use the current directory itself, whether or not it has content. Step 3 handles any existing content.
3. **The current directory is clearly a video-projects container** → create the project folder inside it, without asking.
4. **A possible video-projects container is nearby** → look at the immediate subdirectories of the current directory, and at the current directory itself if it only weakly looks like a container. If you find candidates, ask the user where to create the project: the current directory or one of the candidates. Keep the search shallow; do not crawl the whole disk.
5. **Otherwise** → create the project folder inside the current directory.

A video-projects container is a folder that holds video projects. Treat it as **clearly** a container when it already contains video projects or its name clearly refers to YouTube. A generic name such as `Videos`, `Content` or `Media` is only a weak signal: system folders with those names often hold plain media files, so ask instead of assuming.

A folder is likely a video project if it has a hub document whose frontmatter is tagged `youtube`, or several documents like the ones in the templates. These are hints, not requirements; user-made projects can look like anything.

### 3. Check for conflicts

If the user asked for their own templates, resolve them first (see [User templates](#user-templates)); create nothing until they resolve.

Before creating anything, check the project folder. When it is a new folder inside a parent location, an existing folder in that location whose name matches the project name counts as the project folder.

- **It does not exist** → create it.
- **It exists and is empty** → use it.
- **It exists and has content** → stop and ask the user to choose one of:
  - **Cancel** — do nothing.
  - **Use a different name** — suggest a name that no existing folder in the parent location matches, or let the user give one, then repeat these checks with the new name. Do not offer this option when the project folder is the current directory itself (location rule 2): a new project created from there would end up nested inside this one.
  - **Add missing files only** — create only the documents that do not already exist in the folder. Leave every existing file untouched.

Folders next to the project folder whose name is similar but does not match (e.g. `godot-first-look` vs `Exploring Godot for the first time`) are not conflicts. Do not ask about them and do not touch them; continue normally and mention them in the report.

Never offer to replace or overwrite existing content.

### 4. Create the documents

If the user asked for their own templates, follow [User templates](#user-templates); it says when to also use the bundled templates below.

Read the templates in [assets/templates/](assets/templates/) only now, when you are about to create the files:

| Template | Purpose |
|---|---|
| `Overview.md` | Project hub: one-line pitch, metadata and links to every document |
| `Idea.md` | Premise, packaging (working title and thumbnail concept), audience, angle, what the viewer takes away, and reference videos |
| `Research.md` | Findings, facts to verify, open questions |
| `Sources.md` | References and what each one supports |
| `Outline.md` | Hook that delivers on the packaging, sections and ending |
| `Script.md` | What will be said in the video: hook, body and ending |
| `Production.md` | Shot list, b-roll, and references to where media lives |
| `Publishing.md` | Final title and thumbnail variations, description, tags, shorts |

`Script.md` is only a place for the script. Do not write any script content: the user writes it when they are ready, either on their own or with a dedicated skill.

For each template:

- Translate file names, headings and guidance comments into the project language (see [Language](#language)). When a comment mentions another document, use that document's translated name. Do not translate frontmatter: keep every key, and the values of `status` and `tags`, exactly as in the template.
- Replace placeholders: `{{project_name}}` with the project name, `{{date}}` with today's date as `YYYY-MM-DD` (take it from the environment; if you cannot determine it, leave the value empty rather than guess), `{{language}}` with the project language as a language code (e.g. `en`, `es`).
- Keep the links in `Overview.md` as relative markdown links pointing to the actual (translated) file names. Do not convert them to wiki-links (`[[Note]]`): every project has documents with the same names, so a wiki-link can resolve to another project's document. If a file name contains spaces, wrap the target in angle brackets: `[Production notes](<Production notes.md>)`.
- When adding missing files only, skip any document whose file name already exists in the folder.

Besides the project folder, create only files. Do not create empty folders (for media or anything else); documents reference media by path when the user has it.

#### User templates

Use the user's own templates only when they explicitly name the templates and where to take them from (e.g. "use idea, research and script from ~/templates"). Never look for user templates otherwise.

- **Find them.** A file matches a named template when its name, without extension, is equal to the name ignoring case, accents, spaces, hyphens and underscores. Look only in the location the user gave.
- **Ask before creating anything** when the location does not exist, or when none of the named templates is found in it. Offer to use a different location, use the bundled templates instead, or cancel.
- **Skip what does not resolve.** When a named template is not found, or matches more than one file, skip it and mention it in the report. Do not replace it with a bundled template or pick a candidate.
- **Copy, do not adapt.** Do not judge, interpret or restructure the templates. Keep each file's name and content as they are, without translating them. Only replace `{{project_name}}`, `{{date}}` and `{{language}}` if they appear, as described above; leave any other placeholder or template syntax untouched.
- **Mix only on request.** Add bundled templates only when the user explicitly asks (e.g. "use my idea and the rest of the defaults"). Then create the bundled templates they asked for, following the rules above, except those the user says their own templates replace. If both would have the same file name, keep the user's. If the bundled `Overview.md` is created, link only the documents that exist in the project folder.
- When adding missing files only, skip any template whose file name already exists in the folder.

### 5. Report

Tell the user, in their language (see [Language](#language)):

- the full path of the project;
- which documents were created, and from which location when they come from the user's templates;
- which user templates were skipped because they were not found or matched more than one file (list the candidates);
- which were skipped because they already existed, and any existing files that look like they serve the same purpose as a bundled template (mention them; do not touch them);
- any folder next to the project folder with a similar name: say it was not touched and suggest the user check whether it is the same project;
- any change made to the requested name.

If something fails partway through, report exactly what was and was not created. Do not try to undo by deleting.

## Language

This skill and its templates are written in English as a reference, not as literal text.

- Determine the **project language**, in this order:
  1. The language the user explicitly asks for.
  2. When adding missing files to a folder whose hub document already records a `language`, that language, so the new documents match the existing ones.
  3. The language the user is writing in. If the request is too short to tell (e.g. only a project name), use the language of the rest of the conversation, then the language of the project name.
- Ask every question and write every report in the language the user is writing in, or the one they asked for. This can differ from the project language only when the new documents follow the language already recorded in the folder.
- Create file names, headings and guidance comments of the bundled templates in the project language. User templates are never translated.
- Record the project language in the `language` field of `Overview.md`, when it is created, so later work on the project can keep using it.
