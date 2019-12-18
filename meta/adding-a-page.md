# Adding A Page

#### Basics
Adding a new page on the SBEL Wiki is as simple as creating a new file. All you need to do is create a file ending in `.md` and it will be rendered as a Markdown webpage in GitHub. It is highly recommended that you follow the guidelines below when creating a new page; this will help prevent problems when other users wish to link to or edit your page.

---

#### Guidelines

##### Naming Your Page
Wiki pages should have a descriptive title which clearly identifies what the page is about. Long titles can be cumbersome, so please try to be as succinct as possible. Your title will also become the name of the saved markdown file, so it is important to choose it carefully. The title goes on the top of your new Markdown (`.md`) file and looks something like this:

```Markdown
# Dan's Succinct and Descriptive Title

... page contents ...
```

When saving your new page, the name of the file should be the same as the title, with the following caveats:
- It should be entirely _lowercase_ and should end in `.md`
- All spaces should be replaced with dashes (`-`)
- Any punctuation in the title should be replaced with an underscore (`_`)

For the example title above, these guidelines would produce the file `dan_s-succinct-and-descriptive-title.md`.

##### Indexing
To make it easier for other folks to find your page, you should add it to the `index.md` files in the [project root folder](/index.md) and the [parent folder](/meta/index.md) of the page. Files should be added to the list of bullet points as a link in the relevant section on the index page. If you are unclear on how to format the page, use existing entries for guidance.