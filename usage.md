---
title: "Usage"
layout: page
permalink: "/usage"
---

**If you need help**, please
[open an issue](https://github.com/duckinator/inq), or [join the Bundler
slack](https://slack.bundler.io) and then join in the #how\_is channel.


## Basic Usage

The quickest way to use Inq is to provide all of the information
directly on the command line.

For example,

    $ inq --repository rubygems/rubygems --date 2019-03-01
    Saved report to report.html.

Or, if you want the report to be in `example.html`:

    $ inq --repository rubygems/rubygems --date 2019-03-01 --output example.html
    Saved report to example.html.

## Project Config Files

(TODO: Improve this section.)

You can also specify a project config file, which will generate all of the
reports specified in said file.

For example,

    $ inq --date 2019-03-01 --config rubygems.yml
    Saved reports to:
    - rubygems/_posts/2019-03-01T00:00:00+00:00-report.html
    - json/rubygems/2019-03-01T00:00:00+00:00.json 

Below is an example config file:

```yaml
default_reports:
  html:
    directory: output
    frontmatter:
      title: "%{date} Report"
      layout: default
    filename: "%{date}-report.html"
  json:
    directory: output
    filename: "%{date}.json"

repositories:
  - repository: rubygems/rubygems
    reports:
      html:
        directory: rubygems/_posts
      json:
        directory: json/rubygems
  - repository: duckinator/inq
    reports:
      html:
        directory: inq/_posts
      json:
        directory: json/inq
```

The config file is a YAML file, and the two root keys are
`default_reports` and `repositories`. The value of `default_reports` is
a hash of default options used for reports.

Under `repositories`, there are two keys:  `repository` and `reports`.

`repository` is the name of the repository that collection of reports is for.

`reports` is a hash of key/value pairs, with the keys
being the type of report ("html" or "json") and the values being another hash.

That hash can have the following keys: `directory` (the directory to place the
report in), `filename` (the format string for filenames), and (optionally)
`frontmatter`.

`frontmatter` is a set of key/value pairs specifying frontmatter as used by
various blog engines (e.g. Jekyll), so you can set the title, layout, etc of
the page.

Every value under `reports` is a format string, so you can do e.g.
`filename: "%{date}-report.html"` or (under `frontmatter`)
`title: "%{date} Report"`.
