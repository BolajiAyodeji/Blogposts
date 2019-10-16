## GitHub repository language overview - How?

The files and directories within a repository determine the languages that make up the repository. With GitHub, you can view a repository’s languages to get a quick overview of the repository. But how does this happen? What powers this repository language overview?

----

You might have noticed this section at the top of your GitHub repositories that give you an overview of languages contained in the repository

![](https://cdn-images-1.medium.com/max/800/1*FWBD77YB6yedoMIc04BSOA.png)

Well, GitHub uses the open source [Linguist
library](https://github.com/github/linguist) to determine file languages for
syntax highlighting and repository statistics. Language statistics will update
after you push changes to your default branch (which is usually `master`).

## What is GitHub Linguist?

> GitHub Linguist is a library is used on GitHub.com to detect blob languages, ignore binary or vendored files, suppress generated files in diffs, and generate language breakdown graphs. - GitHub Linguist Docs

Basically, Linguist is a library that runs on every GitHub repository. It checks
every file and directory and detects the programming language used in that file.

## How does Linguist work?

Linguist takes the list of languages it knows from `languages.yml` and uses a number of methods to try and determine the language used by each file, and the overall repository breakdown.

Linguist starts by going through all the files in a repository and excludes all
files that it determines to be binary data, vendored code, generated code,
documentation, or are defined as `data` (e.g. SQL) or `prose` (e.g. Markdown) languages, whilst taking into account any overrides.

The result of this analysis is used to produce the language stats bar which
displays the languages percentages for the files in the repository. The
percentages are calculated based on the bytes of code for each language as
reported by the [List Languages](https://developer.github.com/v3/repos/#list-languages) API.

## How to fix common Linguist issues

Some files are hard to identify, and sometimes projects contain more library and vendor files than their primary code. If you’re receiving incorrect language analysis, then read below for common Linguist issues and how to fix them.

Linguist does not consider [vendored code](https://github.com/github/linguist#vendored-code), [generated code](https://github.com/github/linguist#generated-code),
[documentation](https://github.com/github/linguist#documentation), or data (e.g. SQL) or prose (e.g. Markdown) languages (as defined by the `type` attribute in `languages.yml`) when calculating the repository language statistics.

If the language statistics bar is not showing your language at all, it could be
for a few reasons:

-  Linguist doesn’t know about your language.
-  The extension you have chosen is not associated with your language in
`languages.yml` e.g saving a JavaScript file as `app.jss`
- All the files in your repository are either [vendored code](https://github.com/github/linguist#vendored-code), [generated code](https://github.com/github/linguist#generated-code) or
[documentation](https://github.com/github/linguist#documentation) (e.g. SQL, prose, Markdown…) Linguist excludes these files by default.

> If Linguist doesn’t know about the language or the extension you’re using, consider [contributing](https://github.com/github/linguist/blob/master/CONTRIBUTING.md)
to Linguist by opening a pull request to add support for your language or
extension.

> You can also to tell Linguist to include your files in the language statistics
> by overridding it.

## How to use gitattributes to override Linguist

Just as you can customize and override the default configurations of a gaming control pad, you can also use custom override strategies for language definitions and file paths in Linguist.

Basically, `gitattributes` is just a file used to command or tell Git to perform
some specific tasks, sort of a way to tweaking it.

* Add a `.gitattributes` file to the root of your project

```bash
touch .gitattributes
```

* Use the standard git-style path matchers for the files you want to override
using the **linguist-documentation**, **linguist-language**, **linguist-vendored**, **linguist-generated** and **linguist-detectable** attributes.

> When testing with a local installation of Linguist, take note that the added
> attributes will not take effect until the `.gitattributes` file is committed to
your GitHub repository.

- Using  **linguist-language** attribute to override language extensions

```
    # .gitattributes file which reclassifies `.js` files as Java:

     *.js linguist-language=Java
```

- Using the **linguist-vendored** attribute to vendor or un-vendor paths

> By default, Linguist treats all of the paths defined in `vendor.yml` as vendored and therefore doesn't include them in the language statistics for a repository.

```
    special-vendored-path/* linguist-vendored
     jquery.js linguist-vendored=false
```

- Using the **linguist-documentation** attribute to mark or unmark paths as documentation

```
    project-docs/* linguist-documentation
     docs/formatter.rb linguist-documentation=false
```

### Using the **linguist-generated** attribute to mark or unmark paths as generated.

> Not all plain text files are true source files. Generated files like minified JavaScript and compiled CoffeeScript can be detected and excluded from language stats.

```
    Api.elm linguist-generated=true
```

- Using the **linguist-detectable** attribute to mark or unmark paths as
detectable

> Only programming languages are included in the language statistics. Languages of a different type (as defined in `languages.yml`) are not "detectable" causing them not to be included in the language statistics.

```
    *.kicad_pcb linguist-detectable=true
     *.sch linguist-detectable=true
     tools/export_bom.py linguist-detectable=false
```

## Conclusion

Linguist defines the list of all languages known to GitHub in a [yaml file](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml).
In order for a file to be highlighted, a language and lexer must be defined
there.

Most languages are detected by their file extension. This is the fastest and
most common situation.

If you experience any issue with Linguist, a quick way to get help is by
contributing via [Pull Requests](https://github.com/github/linguist/pulls) or submitting an [Issue](https://github.com/github/linguist/issues).

## Reference

[GitHub Linguist docs](https://github.com/github/linguist)