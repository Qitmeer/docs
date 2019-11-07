# docs
The Qitmeer documentation &amp; guides and tutorials.

# How To Run

### Mac

#### download and install hugo

#### Prerequisite Tools

* [Git](https://git-scm.com/)
* [Go (at least Go 1.11)](https://golang.org/dl/)

#### Fetch from GitHub

Since Hugo 0.48, Hugo uses the Go Modules support built into Go 1.11 to build. The easiest is to clone Hugo in a directory outside of `GOPATH`, as in the following example:

```bash
mkdir $HOME/src
cd $HOME/src
git clone https://github.com/gohugoio/hugo.git
cd hugo
go install

hugo version

Hugo Static Site Generator v0.55.6/extended darwin/amd64 BuildDate: unknown
```

#### Run

```bash
git clone https://github.com/qitmeer/docs.git
cd docs/Document/

hugo serve

open http://localhost:1313/docs/
```

# How To Add Document

#### create a document item

```bash
hugo new content/example/_index.en.md
vim content/example/_index.en.md
```

> Note that all document files are placed under the content folder

#### Configuration page

```bash
hugo new content/nxtools/_index.en.md
vim content/nxtools/_index.en.md
```

Edit page parameters `content/nxtools/_index.en.md`

```bash
---
title: NxTools

# Represents the sorting position of the sidebar
weight: 1

# According to the serial number
pre: "<b>1. </b>"

# When true, the page paragraph is displayed in the center
chapter: true

# This option needs to be set if the page has formula content
mathjax: true
---

### content
```

# Deploy

```bash
cd Document
hugo

```