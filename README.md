# vim-better-sml

> Some improvements to the default SML filetype plugins for Vim.

## Install

Install using your favorite plugin manager. For example, to install using
Vundle, add this line to your ~/.vimrc:

```
Plugin 'jez/vim-better-sml'
```

If you're unfamiliar using Vim plugins, check out [Vim as an IDE][vim-ide] which
will get you up to speed.

## Summary of Modifications

### Indentation

- [x] `let` statements are indented under `fun` statements
- [ ] Indent level is properly adjusted when using nested case statements.
  Consider the following snippet of SML:

      datatype ord = Z | S of ord | Sup of (int -> ord)

      fun toString n =
        case n
          of Z => "0"
           | S n' =>
               (case n'
                  of Z => "1"
                   | S _ => "1 < n < aleph"
                   | _ => "malformed")
           | Sup f => ">= aleph"

  Try transcribing this into Vim right now; the last line isn't indented
  properly. Right now, the indent file indents lines like the last line under
  the most recent `case` keyword, ignoring any nesting structure. See [this
  issue][issue-1] for some of my thoughts on the matter.

### Filetype

- [x] Detects signature files (`*.sig`) properly
- [x] Treats apostrophes (`'`) as keyword characters (i.e., we can use "primes"
  in variable names)
- [x] Sets up the comment string properly. This is useful...
  - in conjunction with [tpope/vim-commentary], a plugin that sets up bindings
    for commenting/uncommenting regions in a file
  - when using `foldmethod=marker`, which inserts fold markers into the text
    wrapped in comments

### External Plugins

- __delimitMate__
  - [x] Sets up the appropriate quote characters
- __Syntastic__
  - [x] For the SML/NJ syntax checker, tries to check if you're using a CM file
    to build the project, and loads it appropriately.
- __a.vim__:
  - [x] Set up `*.sig` and `*.sml` as alternate extensions (similar to `*.h` and
    `*.cpp`)


## License

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](https://jez.io/MIT-LICENSE.txt)


<!-- References -->

[vim-ide]: https://github.com/jez/vim-as-an-ide
[issue-1]: https://github.com/jez/vim-sml/issues/1
[tpope/vim-commentary]: https://github.com/tpope/vim-commentary
