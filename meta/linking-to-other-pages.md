# Linking to Other Pages

Linking to another page in [GitHub Pages](https://help.github.com/en/github/working-with-github-pages) can be rather tricky. GitHub supports a number of conventions which novice and experienced users alike might find unintuitive. Please review the information below for the preferred conventions to use in this wiki.

- [Internal Links](#internal-links)
- [External Links](#external-links)

---

### Internal Links

When linking to pages contained within a local repository, GitHub supports using both [absolute](#absolute-paths) and [relative](#relative-paths) paths. With [one notable exception](#the-root-index.md), these links don't require the domain name or an http(s) in front of them, and they don't need a a file extension.

#### Absolute Paths

Links to pages which might be moved or renamed should be linked to with absolute paths to make _Find and Replace_ operations easier for the individual who is performing the move.
> Absolute paths begin at the top level of the repository `/lab-wiki/` and continue through the directory tree from there. For example, the page you are currently reading is located at `/lab-wiki/meta/linking-to-other-pages`.

#### Relative Paths

Links to or from pages which will always be moved together, or links from _Index Pages_ ([example](/lab-wiki/meta/index)) may use relative pathing.
> Relative paths begin at the parent directory of the current file and continue from there. This allows files which are located in the same directory to be linked with just the file name and no other prefix.

#### Markdown
For internal links, always use the `[]()` syntax:
```markdown
[text](/lab-wiki/absolute/link/path)
```
or
```markdown
[text](relative/link/path)
```

#### The Root `index.md`
GitHub Pages has a fairly arcane way of choosing which Markdown documents to generate into html pages. Documents which are not linked to within a project are not generated, but not all files seem to be checked for links. To remedy this, the Lab Wiki maintains an [Index Page](/lab-wiki/index) which contains a complete enumeration of all of the pages in the wiki. These links **must** be absolute paths which end in `.html`. Other link styles do not seem to work and will cause the target page to become a _dead link_.

---

### External Links

Links to pages on sites other than the Lab Wiki require slightly more strict syntax than internal links. These paths are always absolute and require a full protocol and domain name `http://example.com/` as a part of the destination URL. The following conventions should be followed for external links.

#### Markdown
For external links, always use the `()[]` syntax, even when the link text is a bare URL:
```markdown
[Example Website](http://example.com/)
```
or
```markdown
[http://example.com](http://example.com)
```