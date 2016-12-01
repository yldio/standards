## Use the imperative mood in the subject line

[Back](../gitiquette.md)

Imperative mood just means "spoken or written as if giving a command or
instruction". A few examples:

* Clean your room
* Close the door
* Take out the trash

Each of the seven rules you're reading about right now are written in the
imperative ("Wrap the body at 72 characters", etc.).

The imperative can sound a little rude; that's why we don't often use it. But
it's perfect for git commit subject lines. One reason for this is that git
itself uses the imperative whenever it creates a commit on your behalf.

For example, the default message created when using git merge reads:

```
Merge branch 'myfeature'
```

And when using `git revert`:

```
Revert "Add the thing with the stuff"

This reverts commit cc87791524aedd593cff5a74532befe7ab69ce9d.
```
Or when clicking the "Merge" button on a GitHub pull request:

```
Merge pull request #123 from someuser/somebranch
```
So when you write your commit messages in the imperative, you're following
git's own built-in conventions. For example:

* Refactor subsystem X for readability
* Update getting started documentation
* Remove deprecated methods Release version 1.0.0

Writing this way can be a little awkward at first. We're more used to speaking
in the indicative mood, which is all about reporting facts. That's why commit
messages often end up reading like this:

* Fixed bug with Y
* Changing behavior of X

And sometimes commit messages get written as a description of their contents:

* More fixes for broken stuff
* Sweet new API methods

To remove any confusion, here's a simple rule to get it right every time.

A properly formed git commit subject line should always be able to complete the
following sentence:

If applied, this commit will <your subject line here>

 For example:

* If applied, this commit will *refactor subsystem X for readability*
* If applied, this commit will *update getting started documentation*
* If applied, this commit will *remove deprecated methods*
* If applied, this commit will *release version 1.0.0*
* If applied, this commit will merge pull request #123 from user/branch

Notice how this doesn't work for the other non-imperative forms:

If applied, this commit will *fixed bug with Y*
If applied, this commit will *changing behavior of X*
If applied, this commit will *more fixes for broken stuff*
If applied, this commit will *sweet new API method*

Remember: Use of the imperative is important only in the subject line. You can
relax this restriction when you're writing the body.

[Back](../gitiquette.md)
