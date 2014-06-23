Lisp In Small Pieces for Modern Schemes
=======================================

This repository contains source code from the book [Lisp In Small Pieces][LiSP]
by Christian Queinnec, updated to work with modern versions of Bigloo, Gambit,
and Mit-scheme. Specifically, the following versions are known to pass the
included test suite, with a [few exceptions][failing-tests] noted below.

- [bigloo][] 4.1a
- [gambit][] 4.7.2
- [mit-scheme][] 9.2

Running the code
----------------

1. Install one of the above mentioned schemes

2. Clone this repo.
    `git clone https://github.com/appleby/LiSP-2ndEdition.git`

3. Build the interpreter for the book. Edit the Makefile and set the `SCHEME`
   variable to the version of scheme you want. The supported values for
   `SCHEME` are `o/${HOSTTYPE}/book.{bigloo,gsi,mit}`. So, e.g., to build the
   Gambit interpreter, set `SCHEME = o/${HOSTTYPE}/book.gsi`. Then run `make` to
   build the interpreter. If everything goes well, you should have an
   executable in `o/${HOSTTYPE}/book.gsi`.

4. Run `make grand.test` to run the test suite. This will take several minutes,
   but at the end you should see a message that says "All tests passed."

Failing GRAND_TESTS
-------------------

The following tests from the `grand.test` target are know to fail.

| Scheme | Failing Tests             |
| ------ | ------------------------- |
| bigloo | test.reflisp, test.chap8j |
| gambit | test.reflisp              |
| mit    | test.reflisp              |

Note that `test.reflisp` was not supported for gambit and mit-scheme even in
the original sources. Attempting to compile the `monitor` macro in
`src/chap8k.scm` would intentionally generate a divide-by-zero error if the
scheme version was anything other than bigloo, scheme2c, or scm.

The reflective interpreter is doing some interesting things, and I suspect that
it will take some digging to find the correct fix. I plan to revisit these
failing tests when I get to the corresponding chapter in the book.

Other Failing Tests
-------------------

- test.chap10i
- test.chap10e.c

Note that for test.chap10i, a comment in the Makefile warns that it's an
untested variant. Not sure if it's worth trying to get it working...

```
# # chap10i.scm : *Untested* variants for function invokation since
# # it requires a change in SCM_invoke (in scheme.c).
```

Other Schemes
-------------

In addition to [bigloo][], [gambit][], and [mit-scheme][] the [original
sources][LiSP-2ndEdition] also supported [elk][], [scheme2c][], and [scm][].
I'm not planning to get those working myself, but pull requests are welcome.

More Info
---------

For more info, see the [original README][README] file.

TODO
----

* Handle easy-to-fix compiler warnings, like return type of `main` being void.
* Fix issues where make complains about not finding `time` for benchmarks.
* Maybe: Remove unused code, like the included syntax-case files.
* Maybe: Remove unused/unsupported/deprecated targets from the Makefile. 
* Maybe: Get C files to compile without warnings
* Maybe: Clean up formatting of the Makefile
* Maybe: Move common code out of `<interpreter>/book.scm`.


[README]: https://raw.githubusercontent.com/appleby/LiSP-2ndEdition/master/README.orig
[failing-tests]: https://github.com/appleby/LiSP-2ndEdition#failing-grand_tests

[LiSP]: http://pagesperso-systeme.lip6.fr/Christian.Queinnec/WWW/LiSP.html
[LiSP-2ndEdition]: http://pagesperso-systeme.lip6.fr/Christian.Queinnec/Books/LiSP-2ndEdition-2006Dec11.tgz

[bigloo]: http://www-sop.inria.fr/indes/fp/Bigloo
[elk]: http://sam.zoy.org/elk/
[gambit]: http://dynamo.iro.umontreal.ca/wiki/index.php/Main_Page
[mit-scheme]: http://www.gnu.org/software/mit-scheme/
[scheme2c]: https://github.com/barak/scheme2c
[scm]: http://people.csail.mit.edu/jaffer/SCM
