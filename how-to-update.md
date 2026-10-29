# How to update this site

Written for you, not for a developer. No coding knowledge assumed.

---

## What the files are

| File or folder | What it is |
|---|---|
| `index.html` | Home page |
| `work.html`, `lab.html`, `field-notes.html`, `speaking.html`, `about.html`, `contact.html` | The other pages |
| `assets/styles.css` | All the colours, fonts and spacing for the whole site. Change a colour once here and it changes everywhere. |
| `projects/` | One folder per project. Case study pages and Rise/Storyline exports live here. |
| `how-to-update.md` | This file. It is not part of the website; visitors never see it. |

---

## Put it online for the first time

1. Go to **app.netlify.com/drop**
2. Drag the whole `mel-lizardo` folder onto the page.
3. Wait about thirty seconds. You now have a live URL.
4. In Netlify's site settings you can rename it, e.g. `mellizardo.netlify.app`.

To update later, drag the folder on again. When that gets tedious, move to GitHub (bottom of this file).

---

## Add a case study

1. Copy the folder `projects/sample-case-study`.
2. Rename the copy — lowercase, hyphens, no spaces. Example: `projects/safety-induction`.
3. Open `index.html` inside it and edit the text. The HTML tags stay; only the words between them change.
4. Open `work.html`, find a block that starts with `<a class="row"`, copy it, and change the title, the sentence, the tags and the link.

The link needs to match your folder name exactly:

```html
<a class="row" href="projects/safety-induction/index.html">
```

---

## Add a Rise course

1. In Rise: **Export → Web** (not SCORM, not LMS).
2. Unzip it. You get a folder with an `index.html` inside.
3. Put that folder inside your project folder and name it `rise`:
   `projects/safety-induction/rise/`
4. In your case study page, find the `<iframe src="about:blank"` line and change it to:

```html
<iframe src="rise/index.html" title="Safety induction course" loading="lazy"></iframe>
```

---

## Add a Storyline course

Same as Rise, but publish to **Web** and the entry file is `story.html`:

```html
<iframe src="storyline/story.html" title="Decision scenario" loading="lazy"></iframe>
```

---

## Add a 3D model

Easiest route: upload it to Sketchfab (free account), press Embed, copy what they give you, and paste it in place of the `<figure class="embed">` block.

---

## Add a video

Upload to YouTube or Vimeo, then use their embed URL:

```html
<iframe src="https://www.youtube.com/embed/VIDEO_ID" title="Short description" loading="lazy" allowfullscreen></iframe>
```

Never put video files in the site folder. They are too big and they will break your deploy.

---

## Change the colours

Open `assets/styles.css`. The first block looks like this:

```css
--blue:  #1B3FA0;
--red:   #D62839;
--sun:   #F5C518;
```

Change a hex code, save, reload. That is the whole process.

One warning: the yellow is a signal colour. It works as a thin rule or a small block with dark text on it. Large areas of yellow with white text fail accessibility contrast badly.

---

## Delete the placeholder boxes

Anything in a yellow-edged box on the site is a note from me to you. In the code it looks like:

```html
<div class="todo">
  <p>...</p>
</div>
```

Delete the whole block, opening tag to closing tag, once you have replaced that section.

---

## Rules that prevent most problems

- Folder and file names: lowercase, hyphens, no spaces, no accents. `my project` breaks; `my-project` works.
- Always keep a file called `index.html` at the top level.
- Check your phone after every update.
- Keep single files under 100 MB. Rise exports with embedded video blow past this fast — host the video on YouTube and link it instead.

---

## When you are ready for GitHub

Once you have three or more projects, re-dragging the whole folder gets slow.

1. Install **GitHub Desktop**. No command line involved.
2. File → Add Local Repository → choose your `mel-lizardo` folder → Publish.
3. In Netlify: **Add new site → Import an existing project → GitHub** → pick the repo.

From then on, updating is: edit files, open GitHub Desktop, write one line about what changed, press **Commit** then **Push**. Netlify rebuilds by itself in about a minute.

---

## When something breaks

Nine times out of ten it is one of these:

| Symptom | Cause |
|---|---|
| Page loads with no colours or fonts | The path to `styles.css` is wrong. Pages in `projects/` need `../../assets/styles.css`. |
| Link goes to a "Page not found" | Folder name and link do not match exactly. Check capitals and spaces. |
| Embed is blank | Wrong entry file. Rise uses `index.html`, Storyline uses `story.html`. |
| Embed shows "refused to connect" | That site blocks embedding. Link to it instead of framing it. Articulate Review 360 does this. |
