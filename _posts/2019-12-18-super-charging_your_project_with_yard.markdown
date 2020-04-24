---
layout: post
title:      "Super-charging your project with Yard"
date:       2019-12-18 19:11:24 -0500
permalink:  super-charging_your_project_with_yard
---


When looking at many major open-source projects, we see extensive documentation on almost all methods or API calls ([e.g](https://rubydoc.info/gems/yard/file/docs/GettingStarted.md)). As a small team or one person, it would be nice to have similar output, without a large amount of work required.  Luckily, most of the documentation used by those projects is auto-generating. There are [tools](https://en.wikipedia.org/wiki/Documentation_generator) that scans your code and comments to generate documentation that can be exported in different formats such as HTML.  I used the tool to add this document to my [CLI project](https://anthonyntilelli.github.io/MealSelector/).

When using ruby, there are two major choices [yard](https://yardoc.org/) and [rdoc](https://github.com/ruby/rdoc). While both are great choices, I decided to use Yard, as it seemed a bit more feature complete, supported extensions (if needed in future) and it’s preferred commenting syntax was similar to document generators on other languages. While Yard will scan source code and generate documents for you, adding special comments in the code will allow it to create more detailed documentation. These special comments provide Yard with information on the program that is not easy to derive by looking at the code alone, such as the desired data type for method parameters and method return type.  Yard uses a meta-tagging system to determine which comment it should pay attention to. Additionally, the special comments improve the general quality of your code's documentation. I found Yard particularly helpful in keeping track of methods return and parameters expected data types

``` ruby
# Compares if two meal objects are equal
# @param other [Meal]
# @return [Boolean]
 def ==(other)
 # <code>
 end
```

Yard will tell the end-user, which documents are missing their values and what is missing when generating the document.

- Partial

```bash
$ yard
Files:           5
Modules:         1 (    0 undocumented)
Classes:         5 (    2 undocumented)
Constants:       4 (    0 undocumented)
Attributes:     10 (    0 undocumented)
Methods:        39 (    2 undocumented)
 93.22% documented
```

- Fully documented

```bash
$: yard
Files:                5
Modules:        1 (    0 undocumented)
Classes:         5 (    0 undocumented)
Constants:    4 (    0 undocumented)
Attributes:     10 (    0 undocumented)
Methods:        39 (    0 undocumented)
100.00% documented
```

When using any documentation generator, it is important to ensure that neither your docs or comments go stale, such that the documentation/comments no longer reflect the actual state of the written code.  For example, your add two new methods but your documentation does not mention them,  Most documentation generators, including yard, produce static documentation and are not regenerated when being viewed. You will need to call the generator every time you need to update the docs.  Many teams integrate documentation generation into their CI/CD solution. While Yard does support a server, via `yard server --reload` this is designed for development and will not work with Github pages. The other issue of incorrect comments can cause you documentation to output bad information. Whenever updating your code, be sure to update any related comments. Sadly, I have not found a good way to ensure that code comment is in sync with the code of a project.

Learn more about Yard Doc
- https://rubydoc.info/gems/yard/file/docs/GettingStarted.md
- https://medium.com/make-school/a-cheatsheet-to-generate-documentation-for-your-rails-project-on-gh-pages-e28f6acfb9b9
