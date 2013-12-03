vcsh_mr_template
================

This is a [fork](https://github.com/RichiH/vcsh_mr_template) and isn't
intended to be directly used like the upstream. `git clone` to a
$HOME` subdir is fine but dropping it directly into `$HOME` is not
intended currently.

This README might be better as a gist, but it attempts to provide some
rationale for the branches.

Note to future self: If it looks like it's just this file in here show
dotfiles ;)

About
-----

I feel that vcsh in conjunction with mr is a powerful combination
yet also has the potential for simple user interaction. I'm not
stupid and I'm pretty comfortable on the command line but I had some
not-insignificant issues grokking how this all fits together to a
level my perfectionist self was happy to proceed with. *One* source of
my confusion was the template (there were many others, including
relative inexperience with Git), so here's my attempt to unravel why
and suggest some alternatives/improvements to aid understanding.

The original template is a directory structure with a couple of
example config files to get one started with an integrated vcsh and
mr setup. The original structure looks like this:

	.
	|-- .config/
	|   `-- mr/
	|       |-- available.d/
	|       |   |-- mr.vcsh
	|       |   `-- zsh.vcsh
	|       `-- config.d/
	|           `-- mr.vcsh -> ../available.d/mr.vcsh
	`-- .mrconfig

I believe this presents some barriers to understanding which might be
mitigated with some simple nomenclature alterations. It's internally
consistent and makes sense as it is, but it assumes some prior
knowledge on the user's part. I'll extend this structure slightly to
incorporate some of the other recommendations in the vcsh
documentation and in turn emphasise some of the issues I percieve.

Explanation & Issues
--------------------
	.
	|-- .config/
	|   `-- mr/
	|       |-- available.d/
	|       |   |-- mr.vcsh
	|		|	|-- zsh.vcsh
	|       |   `-- mr.git
	|       `-- config.d/
	|           `-- mr.vcsh -> ../available.d/mr.vcsh
	|			`-- mr.git -> ..available.d/mr.git
	`-- .mrconfig

I extended this to include `mr.git` to emphasise a point of confusion
which will become apparent.

The contents of `available.d/` (`mr.vcsh`, `zsh.vcsh` and `mr.git`)
are `mrconfig` snippets. The `vcsh` suffix is just a convention to
imply that the config is referring to a  vcsh-managed repo. Similarly,
the `git` extension is merely convention to indicate it's pointing to
a "regular" Git repository (in this case, a local copy of [mr](https://github.com/joeyh/myrepos)). 

The contents of `config.d/` are symlinks to the snippets allowing one
to selectively expose them to `mr`. The `include` stanza in
`.mrconfig` concatenates the snippets these symlinks point to. As an
aside, I highly approve of the XDG compliant `.config/mr/` structure
and this modular approach is great.

So what's the problem?

#### Config file nomenclature

The snippet nomenclature is ...confusing. `vcsh` employs "fake-bare"
git repos (i.e. there's a repo pretending to be one without a work
tree, `zsh.git`, in the vcsh data directory that the `zsh.vcsh`
snippet points at). There's no such thing as a `vcsh` repo so as long
as you're aware of this, this by itself is perhaps not that confusing.

I specifically added the `vcsh.git` snippet to illustrate how this can
become a source of confusion. I've included it in line with the
recommendations in the vcsh README to use the `.git` extension to
indicate it's a "regular" Git repo (the README does also point out the
nomenclature is arbitrary, addressing this somewhat).

Why is this potentially confusing? Simply because it looks a lot like
a bare Git repo, fake or not. If you don't assume the user will infer
this from knowing `*.vcsh` can't be repos, it might not be apparent
these are config files at all until they look closer. Obviously you
don't have to look much closer to figure this out, but on scanning the
README?

*However*, this is mitigated by...

#### Directory nomenclature

The `*.d` nomenclature implies that the contents are config
snippets. Fair enough, but this relies on the user being familiar with
this convention. Aside from convention, is there any real reason why
the suffix is required? It's not like it makes sense for there to be a
`.../mr/config` or `.../mr/available`. 

One slightly larger issue I have with the default nomenclature is the
use of `.../mr/config.d/`. I get that the contents imply a mr-managed
configuration so it makes sense on that level, but it's all config on
some level in the end...

#### Summary

Ultimately, the nomenclature here is arbitrary. The nature of the
beast allows users to bypass this template entirely and configure as
they see fit. The point of the template, however, is to get users
started and, I would argue, provide some assistance in understanding
the back-end concepts (which is actually currently a pre-requisite to
using vcsh confidently, IMO). 

I've created a number of branches illustrating iterative changes to
the original template which aim to improve conceptual clarity, each
building on the previous.
