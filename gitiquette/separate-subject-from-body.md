## Separate subject from body with a blank line

[Back](../gitiquette.md)

From the `git commit` manpage:

> Though not required, it's a good idea to begin the commit message with a single
short (less than 50 character) line summarizing the change, followed by a blank
line and then a more thorough description. The text up to the first blank line
in a commit message is treated as the commit title, and that title is used
throughout Git. For example, git-format-patch(1) turns a commit into email, and
it uses the title on the Subject line and the rest of the commit in the body.

Firstly, not every commit requires both a subject and a body. Sometimes a single
line is fine, especially when the change is so simple that no further context is
necessary. For example:

```
Fix typo in introduction to user guide
```

Nothing more need be said; if the reader wonders what the typo was, she can
simply take a look at the change itself, i.e. use `git show` or `git diff` or
`git log -p`.

If you're committing something like this at the command line, it's easy to use
the -m switch to git commit:

```
$ git commit -m"Fix typo in introduction to user guide"
```

However, when a commit merits a bit of explanation and context, you need to
write a body. For example:

```
Derezz the master control program

MCP turned out to be evil and had become intent on world domination. This commit
throws Tron's disc into MCP (causing its deresolution) and turns it back into a
chess game.
```

This is not so easy to commit this with the -m switch. You really
need a proper editor. If you do not already have an editor set up for use with
git at the command line, read this section of Pro Git.

In any case, the separation of subject from body pays off when browsing the log.
Here's the full log entry:

```
$ git log
commit 42e769bdf4894310333942ffc5a15151222a87be
Author: Kevin Flynn <kevin@flynnsarcade.com>
Date:   Fri Jan 01 00:00:00 1982 -0200

 Derezz the master control program

 MCP turned out to be evil and had become intent on world domination. This
 commit throws Tron's disc into MCP (causing its deresolution) and turns it back
 into a chess game.
```

And now `git log --oneline`, which prints out just the subject line:

```
$ git log --oneline
42e769 Derezz the master control program
```

Or, `git shortlog`, which groups commits by user, again showing just the
subject line for concision:

```
$ git shortlog

Kevin Flynn (1):
  Derezz the master control program

Alan Bradley (1):
  Introduce security program "Tron"

Ed Dillinger (3):
  Rename chess program to "MCP"
  Modify chess program
  Upgrade chess program

Walter Gibbs (1):
Introduce prototype chess program
```

There are a number of other contexts in git where the distinction between
subject line and body kicks in—but none of them work properly without the blank
line in between.

[Back](../gitiquette.md)
