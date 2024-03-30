# Project "Cobalt"

This is a Git repository for all data files and artifacts needed to build a static website with the Hugo site generator.

## 1. Structure

The repository is structured as a Hugo site, having the content files in the `content` directory, themes in the `themes`
directory etc. In the future, I may add new directories, unrelated to Hugo, containing source code for programs that
will do validation and backup of data files.

## 2. Instructions

### 2.1. Hugo

To install Hugo, configure and build the site, follow the [Hugo documentation](https://gohugo.io/documentation/).

#### 2.1.1. Hugo Theme: [hugo-xmin-fork](https://github.com/cicovic-andrija/hugo-xmin-fork)

1. Since the theme is included in the repository as a Git submodule, it requires re-init after every new repo clone:
   `git submodule update --init --recursive`.
2. If the theme gets updated, execute: `git submodule update --remote --merge`.

### 2.2. Deployment

Currently, the site is hosted on [GitHub Pages](https://pages.github.com/). The setup was done by following the
[Hugo Deploy documentation](https://gohugo.io/hosting-and-deployment/hugo-deploy/) and the
[GitHub Pages documentation](https://docs.github.com/en/pages).

Site build and deployment is performed by a GitHub Action which is automatically triggered by a `git push` operation
on the `master` branch in the GitHub repository. The same Action can be invoked manually.

## 3. Content Standard

This section describes the additional markdown formatting rules followed in the textual content files:

1. No line can exceed 120 characters (aka. columns of monospaced text, assuming all characters are 1 column wide).
2. Paragraphs, headings, tables, code and other markdown elements must be separated by blank lines.
3. There cannot be two or more consecutive blank lines.
