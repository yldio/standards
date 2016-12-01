## Use the body to explain what and why vs. how

[Back](../gitiquette.md)

This commit from Bitcoin Core is a great example of explaining what changed and
why:

```
commit eb0b56b19017ab5c16c745e6da39c53126924ed6 Author: Pieter Wuille
<pieter.wuille@gmail.com> Date:   Fri Aug 1 22:57:55 2014 +0200

   Simplify serialize.h's exception handling

   Remove the 'state' and 'exceptmask' from serialize.h's stream
   implementations, as well as related methods.

   As exceptmask always included 'failbit', and setstate was always called with
   bits = failbit, all it did was immediately raise an exception. Get rid of
   those variables, and replace the setstate with direct exception throwing
   (which also removes some dead code).

   As a result, good() is never reached after a failure (there are only 2 calls,
   one of which is in tests), and can just be replaced by !eof().

   fail(), clear(n) and exceptions() are just never called. Delete them.
```

Take a look at the full diff and just think how much time the author is saving
fellow and future committers by taking the time to provide this context here
and now. If he didn't, it would probably be lost forever.

In most cases, you can leave out details about how a change has been made. Code
is generally self-explanatory in this regard (and if the code is so complex that
it needs to be explained in prose, that's what source comments are for). Just
focus on making clear the reasons why you made the change in the first place—the
way things worked before the change (and what was wrong with that), the way they
work now, and why you decided to solve it the way you did.

The future maintainer that thanks you may be yourself!

[Back](../gitiquette.md)
