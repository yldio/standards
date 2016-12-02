# Writing Bash Scripts

## When to use bash

If you are coordinating a bunch of other utilities and it is not a complex
process bash is a good choice.  It can also be helpful for prototyping quickly
before reaching for a more powerful language.  As a rule of thumb bash scripts
should never grow larger than a few hundred lines.  At this stage you might want
to re-evaluate choosing bash

## Bash code style

In general follow [Google's excellent recommendations](https://google.github.io/styleguide/shell.xml)
for writing Bash.

## Linting

Use shellcheck to point out obvious mistakes https://www.shellcheck.net/.  If
you are a vim user [syntastic](https://github.com/vim-syntastic/syntastic)
will flag errors when you have shellcheck installed.

## Highlights and exceptions from the google style guide

* Bash and in particular pipelines can be very difficult to digest at a glance:
apply functional decomposition liberally and don't be afraid of long descriptive
function names.  This will help readers understand your intent and identify bugs
(the terseness and quirks of bash ensures there will be bugs!)
* Create a main function at the top of your file with the flow of small functions
so it's easy to read at a glance what the script does.  Like [this for example](https://github.com/raoulmillais/history-check/blob/master/bin/history-check).
* Favour builtins over shelling out to utilities where possible.  It's easy to
trip up on portability issues between OSX and linux when using unix utilities
and builtins are faster.
* Avoid global variables as much as possible.
* Be **even more conservative** in what you export to the environment
* Make everything readonly including your functions, unless you really want it
to be mutable. This can avoid obvious foot gun moments when you're sourcing
utility scripts.
* Favour `[[ ... ]]` over `if` for tests, but watch out if the check is expected
to fail in the tail position of a function.  You need to add an explicit return
or the script will silently stop at that point leaving you scratching your head!
See [here](https://github.com/raoulmillais/history-check/blob/master/bin/history-check#L139)
for an example.

## Unofficial bash strict mode

Follow the advice in [this excellent article](http://redsymbol.net/articles/unofficial-bash-strict-mode/).
Go read it for more detailed advice, I've included the highlights below.

Your bash scripts will be more robust, reliable and maintainable if you start
them like this:

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'
```

### set -e
The set -e option instructs bash to immediately exit if any command has a
non-zero exit status. You wouldn't want to set this for your command-line shell,
but in a script it's massively helpful. In all widely used general-purpose
programming languages, an unhandled runtime error - whether that's a thrown
exception in Java, or a segmentation fault in C, or a syntax error in Python -
immediately halts execution of the program; subsequent lines are not executed.

### set -u

The set -u option affects variables. When set, a reference to any variable you
haven't previously defined - with the exceptions of `$*` and `$@` - is an error, and
causes the program to immediately exit. Languages like Python, C, Java and more
all behave the same way, for all sorts of good reasons. One is so typos don't
create new variables without you realizing it.

### set -o pipefail

This setting prevents errors in a pipeline from being masked. If any command in
a pipeline fails, that return code will be used as the return code of the whole
pipeline. By default, the pipeline's return code is that of the last command -
even if it succeeds.

### Setting IFS

The next question is, why are we setting IFS to a string consisting of a tab
character and a newline? Because it gives us better behavior when iterating over
a loop. By "better", I mean "much less likely to cause surprising and confusing
bugs". This is apparent in working with bash arrays:

```bash
#!/usr/bin/env bash
names=(
  "Aaron Maxwell"
  "Wayne Gretzky"
  "David Beckham"
  "Anderson da Silva"
)

echo "With default IFS value..."
for name in ${names[@]}; do
  echo "$name"
done

echo ""
echo "With strict-mode IFS value..."
IFS=$'\n\t'
for name in ${names[@]}; do
  echo "$name"
done
```

With default IFS value, the output is:
```
Aaron
Maxwell
Wayne
Gretzky
David
Beckham
Anderson
da
Silva
```
With strict-mode IFS value, the output is:
```
Aaron Maxwell
Wayne Gretzky
David Beckham
Anderson da Silva
```

Or consider a script that takes filenames as command line arguments:

```bash
for arg in $@; do
    echo "doing something with file: $arg"
done
```

If you invoke this as myscript.sh notes todo-list 'My Resume.doc', then with the
default IFS value, the third argument will be mis-parsed as two separate files -
named "My" and "Resume.doc". When actually it's a file that has a space in it,
named "My Resume.doc".

Which behavior is more generally useful? The second, of course - where we have
the ability to not split on spaces. If we have an array of strings that in
general contain spaces, we normally want to iterate through them item by item,
and not split an individual item into several.

Setting IFS to $'\n\t' means that word splitting will happen only on newlines
and tab characters. This very often produces useful splitting behavior. By
default, bash sets this to $' \n\t' - space, newline, tab - which is too eager.

### Beware of CDPATH

Beware of CDPATH gotchas causing cd not to work correctly when a user has
set this in their environment, always unset it at the top of scripts:

```bash
unset CDPATH
```

You can read more about how this can cause problems [here](https://bosker.wordpress.com/2012/02/12/bash-scripters-beware-of-the-cdpath/)
