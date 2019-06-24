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
git clone https://github.com/HalalChain/docs.git
cd docs/Document/themes/
git clone https://github.com/matcornic/hugo-theme-learn.git
cd ..
hugo sersve

open http://localhost:1313
```

# How To Add Document

#### creat a document item

```bash
hugo new content/example/_index.en.md
vim content/example/_index.en.md
```

> Note that all document files are placed under the content folder

Detailed tutorials are available [hugo_example](https://zhangyi999.github.io/hugo_example/)