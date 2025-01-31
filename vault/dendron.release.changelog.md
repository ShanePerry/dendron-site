---
id: 9bc92432-a24c-492b-b831-4d5378c1692b
title: Changelog
desc: ''
updated: 1610407009552
created: 1601508213606
date: 2021-01-07
---

## 0.23.2

### Features

### Enhancements
- better 403 page ([[docs|dendron.topic.publishingv2.selective-publication#403-page]])
- spurious error message if user doesn't create note from not selecting a vault
- better default journal note titles

### Bug Fixes
- issue publishing with subdomain
- some queries not being returned in multi-vault settings
- issue with noteRef mangling when using doctor

### House Cleaning
- update on date format for journal and scratch notes to use [Luxon style formatting](https://moment.github.io/luxon/docs/manual/formatting.html)

## 0.23.1
- Dendron Markdown Preview: 0.10.18
- Dendron 11ty: 1.23.6

### Features

#### Updated Note Ref Syntax

You can now do references to notes using `![[note]]` instead of `((ref: [[note]]))` syntax. To reference a header, use `![[note#foo]]`. This changes makes our note ref syntax more consistent with our wiki link syntax. 

Note that the new ref syntax expects a [[sluggified|dendron.ref.terms#slug]] header. This is done automatically when you use the updated [[copy note ref|dendron.topic.commands#copy-note-ref]] command. 

This change makes it possible to create a ref to a header with special characters.

The old syntax ref syntax will still work but should now be considered deprecated. We will release a `doctor` command to help you auto-upgrade from the old syntax to the new syntax in the coming week.

#### Frontmatter Variable Substitution

It is now possible to use variables defined in your note frontmatter inside your note. The syntax is `{{fm.VAR_NAME}}` where `VAR_NAME` is the name of your variable. The `fm` designates that you want to use a frontmatter variable. 

<!-- 
#### Publishing V2 Integration with Plugin

You can now both build your notes for publication and preview it from inside vscode. 

![[dendron.topic.commands#site-build:#dev]]
-->

### Enhancements
- `nav_exclude` property excludes from nav sider and table of contents ([[docs|dendron.topic.publishingv2.navigation#nav-exclude]])
- [[copy note ref|dendron.topic.commands#copy-note-ref]] command will use the new note ref syntax
- footnote support in preview and when publishing ([[docs|dendron.topic.markdown#footnotes]])

### Bug Fixes
- spaces in wiki link not rendering in preview

## 0.22.2

### Enhancements

- better fuzzy search for lookup
- publishing v2 enhancements
  - abbreviation support for 11ty publishing ([[docs|dendron.topic.markdown#abbreviation]])
  - better note titles ([[docs|dendron.ref.titles]])
  - shrink size of published page 10x
  - fix left nav position of current active page
  - ability to override output folder from CLI when building site
  - don't throw error on code blocks that are unsupported by prismjs

### Bug Fixes

- markdown preview delay in showing newly created notes
- `buildSiteV2` not connect to running workspace

## 0.22.1

### Features

- [[Collections|dendron.topic.publishingv2.collections]] support for 11ty
  - publish blog like archives using Dendron
- CLI Based Doctor ([[docs|dendron.pro.dendron-cli#doctor]])
  - run various tests to make your notes are healthy for the new year
- use frontmatter as title when publishing and in the preview ([[docs|dendron.topic.config#usefmtitle]])

### Enhancements

- additional metadata tags for published pages
- support `noindex` option ([[docs|dendron.topic.publishingv2.configuration#noindex]])
- add anchor links to headers
- use note title for page title
- support [[nav_exclude|dendron.topic.publishingv2.configuration#nav_exclude]] option
- support overriding [[output|dendron.pro.dendron-cli#buildsitev2]] in `buildSiteV2` command
- don't throw error if no syntax highlighter available for code block

### Bug Fixes

- issue connecting to open workspace using CLI
- nav bar when publishing multiple hierarchies will show wrong expansion options

## 0.21.2

### Enhancements

- build-site command can connect to current running workspace ([[docs|dendron.pro.dendron-cli#connect-to-open-workspace]])
- support inline math when publishing
- support block math when publishing 
- support rendering gfm inside note reference when publishing
- support anchor headings when publishing
- support relative links when publishing

### Bug Fixes

- issue with displaying math in preview

### House Cleaning

- the code highlighter has been changed from `prismjs` to `highligher.js`

## 0.21.1

### Enhancements

- add seo tags ([[docs|dendron.topic.publishingv2.configuration#seo-options]])
- enable edit on github link ([[docs|dendron.topic.publishingv2.configuration#github-options]])
- migrate all jekyll `_config.yml` settings to `dendron.yml`

### Bug Fixes

- build-site errors when building from vaults without `asset folder`
- build-site error on certain operating systems
- build-site error on node version != 12

### Docs

- [dendron.so](https://dendron.so) is now published using the new 11ty framework
- add [[publishing to github guide|dendron.topic.publishingv2.github]] using github actions

## 0.20.2

### Features

#### Publishing For Multi Vault

![[dendron.topic.multi-vault#publishing:#*]]

### Enhancements

- creating engine via cli also initializes meta files ([d72f097](https://github.com/dendronhq/dendron/commit/d72f097e63d1fda065ac7ad50f85bebe99d6da66))([[docs|dendron.pro.dendron-cli#launchengineserver]])
- remove github light theme from dendron bundle ([33d5708](https://github.com/dendronhq/dendron/commit/33d57086510cdaefbb8af8f72c945d6f5e02be5c))
- support [[note refs for multi-vault|dendron.topic.multi-vault#note-references]] 
- support relative links in dendron preview ([[docs|dendron.topic.links#wiki-links]])
- further speed enhancements to publishing using 11ty resulting in another 5x improvement  
- configure [[writeStubs|dendron.topic.publishingv2.configuration#writestubs-optional]] from `dendron.yml`

### Bug Fixes

- refactor hierarchy miss self referential links ([00b385d](https://github.com/dendronhq/dendron/commit/00b385dd0d13e5809da012bbc88388886012b837))
- reduce frequency of `engine not connecting` error when launching dendron preview

### House Cleaning

- [[writeStubs|dendron.topic.publishingv2.configuration#writestubs-optional]] is set to `true` by default (or when not set) when publishing using 11ty

## 0.20.1

### Publishing V2 (preview)

We've re-build publishing for Dendron from the ground up to be faster, better, and easier to use.

Besides for schemas, publishing has consistently been one of the hardest to use features in Dendron. Dendron currently publishes using [jekyll](https://jekyllrb.com/) using our own [template](https://github.com/dendronhq/dendron-jekyll). While this has served as well initially, slow compile times for large sites and difficulty of getting started has made it a growing pain point.

To address this, we've migrated our publishing stack to [11ty](https://www.11ty.dev/), a super fast javascript based static generator. This means much faster, and perhaps more importantly, easier publishing. 

There's still some work left to integrate publishing into the Dendron plugin - meanwhile, you can take the new publishing workflow for a spin using the [[dendron cli|dendron.pro.dendron-cli]]

In order to to use the 11ty based publishing, initialize your workspace with the following commands.

```bash
npm init -y
npm install @dendronhq/dendron-cli@latest
npm install @dendronhq/dendron-11ty@latest
```

After you have your dependencies installed, build your your site using the following command.

```bash
npx dendron-cli buildSiteV2 --wsRoot .  --stage dev --serve
```

This will both compile your site locally and make it available at `localhost:8080` for instant preview. When building your site locally, the pages will be build to `{wsRoot}/build/site`. 

When you are ready to publish to github, make sure to change the stage to `prod`.

```bash
npx dendron-cli buildSiteV2 --wsRoot .  --stage prod 
```

This will build your site to the path specified by [[siteRootDir|dendron.topic.publishing.configuration#siterootdir]] in `dendron.yml`. 

#### Benchmarks

Publishing V2 is ~10x faster than jekyll based publishing for sites with +100 pages. For comparison, below is the compilation difference between building the dendron site using 11ty vs jekyll. 

- 11ty: 24.45s
- jekyll: 220.33s

There are additional optimizations still on the table that will further drive down he compilation time by another order of magnitude for future releases. 

#### Gaps

11ty publishing is currently not at full feature parity with Jekyll publishing. Notably, the following features are missing:

- setting a custom color theme
- `edit on github` links
- `jekyll-seo` functionality
- mathjax

#### Migration

All values that used to be written into `_config.yml` will now be moved into `dendron.yml`. You can see the currently supported configuration values here: `https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/types.ts#L71:L71`

If you currently have a Jekyll based Dendron page, note that the following settings have changed:

- the `url` property from `_config.yml` is now `siteUrl` in `dendron.yml`
- favicon is now controlled by `siteFaviconPath` in `dendron.yml` and is a path relative to your workspace root
- `CNAME` is now controlled by `githubCname` property in `dendron.yml`

#### Sample dendron.yml config

- publishing without a cname

```yml
version: 1
vaults:
    - fsPath: vault
site:
    copyAssets: true
    siteHierarchies:
        - dendron
    siteRootDir: docs
    siteUrl: "kevinslin.github.io/dendron-11ty-test"
    usePrettyRefs: true
```

- using custom cname

```yml
version: 1
vaults:
    - fsPath: vault
site:
    copyAssets: true
    siteHierarchies:
        - dendron
    siteRootDir: docs
    usePrettyRefs: true
    siteUrl: "11ty.dendron.so"
    githubCname: "11ty.dendron.so"
```

#### Sample repo

- [github repo](https://github.com/kevinslin/dendron-11ty-test/deployments/activity_log?environment=github-pages)
- [github page](https://kevinslin.github.io/dendron-11ty-test/)

#### CLI Command Reference

```bash
dendron-cli buildSiteV2

build notes for publication using 11ty

Options:
  --version  Show version number                                       [boolean]
  --help     Show help                                                 [boolean]
  --wsRoot   location of workspace                                    [required]
  --vaults   location of vault                                           [array]
  --serve    serve over local http server             [boolean] [default: false]
  --stage    serve over local http server
```

<!-- https://hacks.mozilla.org/2020/10/to-eleventy-and-beyond/ -->


## Past Releases
- [[0.1.X|dendron.release.changelog.0-1-x]]