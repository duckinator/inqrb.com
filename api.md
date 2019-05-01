---
title: "API"
layout: page
permalink: "/api"
---

The API documentation is in-progress.

**If you need help**, please
[open an issue](https://github.com/duckinator/inq), or [join the Bundler
slack](https://slack.bundler.io) and then join in the #how\_is channel.

## TODO

There's still a lot of work to be done on documenting the API.

Here are some features that are currently undocumented:

- when `~/.config/inq/config.yml` is used.
- how to use an alternative config file.
- how to use multiple config files instead of the default.
- how to use the default config file + additional ones.
- new functionality in v25+.

## Basic API

If you only need to generate a single report, the basic API will often
suffice:

```ruby
# Generate an HTML report for rubygems/rubygems, for the date range of
# 2019-02-01 to 2019-03-01, and save it as rubygems-report.html:
report = Inq.new("rubygems/rubygems", "2019-03-01")
report.save_as("rubygems-report.html")
```

## Project Config API

If you need more complicated functionality, you may want to to use the
Project Config API. This is the equivalent to using the `--config` flag on
the command line.

```
# Generate a report from a config Hash.
reports = Inq.from_config({
  repository: 'rubygems/rubygems',
  reports: {
    html: {
      directory: '_posts',
      frontmatter: {
        title: '%{date} Report',
        layout: 'default'
      },
      filename: "%{date}-report.html"
    },
    json: {
      directory: 'json',
      filename: '%{date}.json'
    }
  }
}, "2017-12-01")

# Save all of the reports.
# This assumes all of the directories the files go in already exist!
reports.map {|file, report| File.write(file, report) }
```
