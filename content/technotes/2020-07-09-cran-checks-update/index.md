---
slug: "cran-checks-docs-notifications"
title: "cran checks API: Documentation, Notifications, and more"
date: 2020-07-09
author:
  - Scott Chamberlain
  - Maëlle Salmon
description: cran checks api update - notifications and documentation.
tags:
  - API
  - software development
  - R
output: 
  html_document:
    keep_md: true
---



In October last year [we wrote][ccblog] about the CRAN Checks API (<https://cranchecks.info>). Since then there have been four new major items introduced: documentation, notifications, search, and a new version of the cchecks R package. First, an introduction to the API for those not familiar.

<br>

### CRAN Checks API

The CRAN checks API was born out of a few things:

- the pain of CRAN checks data not being easily machine readable
- the importance of CRAN checks vs. other checks (the maintainer's Travis-CI, Appveyor, etc.) for determining whether your package stays on CRAN or not

CRAN checks are presented for packages in html meant for browser interaction, in a combination of tables, lists and text. On our server we scrape checks data for each package, and manipulate the data into a format that can be easily stored and searched, and then made machine readable.

The main thing this API is used for is badges like the one below that indicate status of the CRAN checks for a package. Many package maintainers have these in the README of their code repository.

<!-- <img src="/img/blog-images/2019-10-09-cran-checks-api-update/svgs/ok.svg"> -->

<br>

### Documentation

APIs are not very useful without good documentation.  Maëlle has single-handedly produced very nice documentation for the API: https://docs.cranchecks.info/

The documentation includes explanation of all the API routes, and includes examples in Shell/command line and for use in R. 

There's also detailed explanation of notifications, see below.

> Maëlle, what do you want to discuss here?


<br>

### Notifications

Good technical solutions are often born from scratching one's own itch. The first author has many packages on CRAN and would like to avoid getting emails from the CRAN maintainers with a deadline to fix a problem. If I could only know about a problem with a CRAN check and fix it quickly, we're all better off as users get fixes quickly, and CRAN maintainers email burden is that much less. 

We're announcing here the availability of cran checks notifications. These notificaitons are emails; there could be other forms (e.g., twitter, etc.), but emails probably meet most people's needs. To get started see the docs at <https://docs.cranchecks.info/#notifications>.

Notifications work via a rule that you set. A rule is made up of one or more of four categories:

- status: match against check status. one of: ok, note, warn, error, or fail
- time: days in a row the match occurs. an integer. can only go 30 days back (history cleaned up after 30 days)
- platforms: platform the status occurs on, including negation (e.g., “-solaris”). options: solaris, osx, linux, windows, devel, release, patched, oldrel
- regex: a regex to match against the text of an error in `check_details.output`

A user can set as many rules as they like. A package can have more than one rule. Users can delete only their own rules (as one would expect). Rules are used indefinitely, until deleted by the user. 

Once a rule is triggered an email is sent to the user. We won't send the same email for 5 days. After 5 days has past, if the rule is matched, we'll send the same email; and repeat. 

Feel free to ignore these emails, or act them as you see fit. 

The email is structured as follows:

{{<figure src="email.png" alt="example cran checks email" width="450">}}

- Triggered rule: with a list of each of the four categories and their values.
- Date of the check result (matches closely the date on the CRAN check results that CRAN maintainers created)
- Your check results: link to the CRAN checks API JSON output for your package
- The rest is information, report bugs, ask for help, etc. Note the "Unsubscribe" link doesn't actually work yet!

#### Managing notifications

There is no web interface to notifications at this time. The only interface is the cchecks R package.

First, you'll need to register for a token (aka key). Using [cchn_register()](https://docs.ropensci.org/cchecks/reference/cchn_register), you run the function with or without an email address. If no email address is given we look for an email address in various places.

```r
cchn_register()
```

Running `cchn_register()` caches the token in a file locally on your computer. 

After registering, you can manage rules for your packges. There's two ways to manage rules: a) across packages, or b) in a single package context.

Functions prefixed with `cchn_pkg_` operate within a package directory. That is, your current working directory is an R package, and is the package for which you want to handle CRAN checks notifications. These functions make sure that you are inside of an R package, and use the email address and package name based on the directory you're in.

Functions prefixed with just `cchn_` do not operate within a package. These functions do not guess package name at all, but require the user to supply a package name (for those functions that require a package name); and instead of guessing an email address from your package, we guess email from the cached email/token file.

If you don't use the package specific functions, you can add a rule like:

```r
cchn_rule_add(package = "foobar", status = "warn", platform = 2)
```

Using package specific functions, you can add a rule like:

```r
cchn_pkg_rule_add(status = "warn", platform = 2)
```

See `cchn_rules_add()` for adding many rules at once.

<br>

### Search

A benefit of having a proper database (aka SQL) of anything is that you can search it. We did not have search until May 2020, so it's relatively new. [Search](https://docs.cranchecks.info/#search) allows users to do full-text search the `check_details` field of the 30-day historical data across all packages. There's a few parameters users can toggle, including `one_each` (boolean) to only return a single result per matching package (rather than results for all days matching). The equivalent function in the R package is `cchecks::cch_pkgs_search()`. 

<br>

### cchecks R package

The [cchecks package][cchecks] has been around for a while, but has received a lot of work recently, and is up to date with the current CRAN checks API. It is not on CRAN right now. To get started see the docs for the package at <https://docs.ropensci.org/cchecks>, as well as the API docs at <https://docs.cranchecks.info/>. You can install it like:

```r
remotes::install_github("ropenscilabs/cchecks")
```

> What else to say here? Maybe go through some examples?



[ccblog]: https://ropensci.org/technotes/2019/10/09/cran-checks-api-update/
[cchecks]: https://github.com/ropenscilabs/cchecks