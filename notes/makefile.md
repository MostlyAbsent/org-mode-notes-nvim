# Introduction

The makefile generally calls out to other files in the `mk` dir.

# Dependencies

- mk/default.mk
- local.mk
- mk/target.mk

# targets.mk

It's mostly compiling the lisp files, and a little git for updates. No need to consider this for the
re-implementation. This is for dev use, it has hooks to upload documentation and fun things like that.

# default.mk

A set of default make configurations.

It sets up tests against vanilla emacs, this is probably a good idea.
