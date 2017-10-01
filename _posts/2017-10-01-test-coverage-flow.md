---
layout: post
title: "The test coverage flow"
date: 2017-10-01
comments: true
---
I recently found myself needing to write up a
test suite for some preexisting code. Tools like `coverage` are helpful in
identifying untested code paths, but can be annoyingly multi-step when you are
trying to confirm that you hit the paths you were expecting. Fortunately I found
a combination of tools that make this a breeze.

The first step is configure `coverage` to put its html report into the
directory you want. This is done by adding a `.coveragerc` file to the
directory that `coverage` will run in. Since I wanted my report a bit outside
of my main project directory for me the file looked like this.
```
[html]
directory = ../coverage/
```
To get a report you just run
```
coverage run --source='.' manage.py test
coverage html
```

But this is taking two steps, when I'd really prefer zero. Enter `rerun`.
It is a handy little script made by
[Jonathan Hartley](https://github.com/tartley) that polls the files in a given
directory and reruns a command if anything changes. This is especially useful
for running tests, since you can have them run instantly on save.
```
rerun --ignore=.coverage "coverage run --source='.' manage.py test; coverage html"
```
Note the `--ignore=.coverage`. This is the file `coverage` generates and we
don't want it to get stuck in a loop rerunning because this file changes.

Great! Now the coverage html is getting generated automatically, but I still
need to hit refresh on my browser to see it. Now it's `livereload`'s time to
shine. This tool by [Hsiaoming Yang](https://github.com/lepture) does exactly
what it sounds like. Open up a new terminal and navigate to the html directory
then just run
```
livereload .
```
and you're good to go. Connect to the server with your browser and enjoy hands
free code coverage updates.
