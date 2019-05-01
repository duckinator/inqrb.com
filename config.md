---
title: Configuration
layout: page
permalink: "/config"
---
<style>h2 { margin: 1em 0 0.25em 0; } /* sigh */</style>

NOTE:

- As of v25, Inq defaults to using a configuration file.
- As of v26, HowIs became Inq.

If you are using Inq on a build server or similar, you may want to see
the section on
[Using Environment Variables](#using-environment-variables).

**If you need help**, please
[open an issue](https://github.com/duckinator/inq/issues), or [join the Bundler
slack](https://slack.bundler.io) and then join in the #how\_is channel.


## GitHub Access Tokens

To acquire a personal access token:

1. Go to https://github.com/settings/tokens/new
2. For `Token description`, enter a description (e.g. "Inq CLI client").
3. Scroll to the bottom of the page.
4. Click "Generate token".
5. Save the token somewhere. **You can't access it again.**

**NOTE**: Inq _only_ needs read access.

## Setting Up Inq

The config file is located at `~/.config/inq/config.yml`.

(FIXME: What about Windows, macOS, etc?)

The format for a configuration file is:

```yaml
sources/github:
  username: <github-username>
  token:    <github-token>
```

Where:
- `<github-token>` is your personal access token (see previous section).
- `<github-username>` is your GitHub username.


## Using Environment Variables

To use environment variables for config, set them as appropriate and
pass `--no-user-config --env-config`.

Supported environment variables:

```
INQ_GITHUB_TOKEN=<github-token>
INQ_GITHUB_USERNAME=<github-username>
```

Where the values (represented with `<value-name>`) are the same as above.

## Why two systems?

Credentials stored as environment variables can be exposed if you e.g.
share the output of `env`.

Given that using environment variables for this tends to be cumbersome
at best anyway, we switched to config files.

However, using environment variables instead of a file is often more
practical for continuous integration, so we kept that as an option 
