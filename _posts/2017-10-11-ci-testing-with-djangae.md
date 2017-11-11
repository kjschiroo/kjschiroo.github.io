---
layout: post
title: "CI: Testing with Djangae"
date: 2017-10-11
comments: true
---
The virtues of continuous integration are espoused by many, but actually setting
it up continues to be a pain. Recently I found myself needing to setup a CI
pipeline for a Djangae project. Djangae is a variation on Django except with
additional integrations with Google App Engine. For working with CI I wanted
the test output to be machine readable, so either `xml` or `json`. Under most
circumstances one would be safe to just to run `pytest --junitxml=path` and
move along, but this isn't one of those circumstances.

The GAE SDK is ... fragile. Libraries that help you work with it, like Djangae,
do a lot of configuration behind the scenes in order to make it easy.
Unfortunately in this situation part of that configuration is dependent on
running tests through `manage.py test`. So whenever I'd run `pytest` it would
just break.

I spent hours trying to fiddle with `pytest`, searching around for plug-ins to
fix the issue, stepping through the code to see what was being missed, but to
no avail.

Seeing no success on that path I shifted my focus to `manage.py` seeing if
there was a way to make it write out results in some machine readable format.
That is when I found [unittest-xml-reporting](https://github.com/xmlrunner/unittest-xml-reporting)
by [Damien Nozay](https://github.com/dnozay). This turned what was a multi-hour
struggle into a one line change.

First install the library
```
pip install unittest-xml-reporting
```
then add it as the test runner for Django (or Djangae).
```
# in settings.py
TEST_RUNNER = 'xmlrunner.extra.djangotestrunner.XMLTestRunner'
```
If you want the results to be stored in a specific location their is another
setting for that too.
```
# in settings.py again
TEST_OUTPUT_DIR = './test_results'
```
And now you're done. All your test results will be stored in the desired location
and ready for the machine to read.
