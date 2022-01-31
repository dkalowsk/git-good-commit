# git-good-commit

This is a fork of [Tom
Marshall's](https://github.com/tommarshall/git-good-commit) excellent bash
script to help enforce git commit messages best practices.

## Why A Fork?

The original version has some hard set rules that I don't completely agree with
and thus the fork.  It's possible the two can be reconciled later on, but right
now with the needs I have I don't have the time to do so.  Yet, I want to make
sure anyone else can use them (if needed).

## What Changed?

The original README cites:

Validates commit messages conform to six of [the seven rules of a great git
commit message](http://chris.beams.io/posts/git-commit/), plus a couple of
extras:

1. [Separate subject from body with a blank line](http://chris.beams.io/posts/git-commit/#separate)
1. [Limit the subject line to 50 characters](http://chris.beams.io/posts/git-commit/#limit-50)
1. [Capitalize the subject line](http://chris.beams.io/posts/git-commit/#capitalize)
1. [Do not end the subject line with a period](http://chris.beams.io/posts/git-commit/#end)
1. [Use the imperative mood in the subject line](http://chris.beams.io/posts/git-commit/#imperative)
1. [Wrap the body at 72 characters](http://chris.beams.io/posts/git-commit/#wrap-72)
1. ~~[Use the body to explain what and why vs.
   how](http://chris.beams.io/posts/git-commit/#why-not-how)~~ _- you're on your
   own with this one_
1. Do no write single worded commits
1. Do not start the subject line with whitespace

The updated rules for this version:

1. [Separate subject from body with a blank line](http://chris.beams.io/posts/git-commit/#separate)
1. Limit the subject line to 72 characters
1. Prefix the subject line with the area of work
1. [Do not end the subject line with a period](http://chris.beams.io/posts/git-commit/#end)
1. [Use the imperative mood in the subject line](http://chris.beams.io/posts/git-commit/#imperative)
1. [Wrap the body at 72 characters](http://chris.beams.io/posts/git-commit/#wrap-72)
1. ~~[Use the body to explain what and why vs.
   how](http://chris.beams.io/posts/git-commit/#why-not-how)~~ _- you're on your
   own with this one_
1. Do no write single worded commits
1. Do not start the subject line with whitespace

I don't believe in the 50 character limit for the subject line.  The value has
been average discovered over time, but is not the maximum line length.  The
subject should be short, as short as possible, but not obscure and sometimes
that goes beyond 50 characters.

Adding the section on prefix'ing the subject line with the area of work.  This
makes it easier to examine the git log and see what is going on where.  For
example `drivers/i2c: add support for DesignWare`.

## Installation

### Single repository

At the root of the repository, run:

```sh
curl https://cdn.rawgit.com/tommarshall/git-good-commit/v0.6.1/hook.sh > .git/hooks/commit-msg && chmod +x .git/hooks/commit-msg
```

### Globally

To use the hook globally, you can use `git-init`'s template directory:

```sh
mkdir -p ~/.git-template/hooks
git config --global init.templatedir '~/.git-template'
curl https://cdn.rawgit.com/tommarshall/git-good-commit/v0.6.1/hook.sh > ~/.git-template/hooks/commit-msg && chmod +x ~/.git-template/hooks/commit-msg
```

The hook will now be present after any `git init` or `git clone`. You can
[safely re-run `git init`](http://stackoverflow.com/a/5149861/885540) on any
existing repositories to add the hook there.

---

_If you're security conscious, you may be reasonably suspicious of [curling
executable files](https://www.seancassidy.me/dont-pipe-to-your-shell.html). In
this case you're on HTTPS throughout, and not piping directly to execution, so
you can check contents and the hash against MD5
`12fd3b8829eead2eff9a72598cbc9f4b` for v0.6.1._

## Usage

```sh
echo "apple" > ./bar.txt
git add fruits.txt

# should warn you that the subject line is not capitalised, and offer an interactive prompt.
git commit -m 'add fruits.txt'
```

### Options

```
e - edit commit message
y - proceed with commit
n - abort commit
? - print help
```

## Configuration

The default colour setting is `auto`, but the hook will use `git`'s `color.ui`
config setting if defined. You override the colour setting for the hook with:

```
git config --global hooks.goodcommit.color "never"
```

Supported values are `always`, `auto`, `never` and `false`.

## Dependencies

None, other than Bash.

## Credits

* http://chris.beams.io/posts/git-commit
* http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
* https://www.git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#Commit-Guidelines
* Tim Perry's excellent [git-confirm](https://github.com/pimterry/git-confirm)
  hook, which provided the inspiration and much of the scaffolding for this
  hook.

