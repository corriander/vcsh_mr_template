vcsh_mr_template
================

This is a [fork](https://github.com/RichiH/vcsh_mr_template) and isn't
intended to be directly used like the upstream. `git clone` to a
`$HOME` subdir is fine but dropping it directly into `$HOME` is not
intended currently.

Note to future me: If it looks like it's just this file in here show
dotfiles ;)

Branch Info
-----------

This branch (`alt_1`) implements the following changes to branch:
`master`. See `master` README for full information.

### Master Template

	.
	|-- .config/
	|   `-- mr/
	|       |-- available.d/
	|       |   |-- mr.vcsh
	|       |   `-- zsh.vcsh
	|       `-- config.d/
	|           `-- mr.vcsh -> ../available.d/mr.vcsh
	`-- .mrconfig

### Changes

This is a trivial alteration:

	.
	|-- .config/
	|   `-- mr/
	|       |-- available.d/
	|       |   |-- mr.vcsh
	|       |   `-- zsh.vcsh
	|       `-- enabled.d/
	|           `-- mr.vcsh -> ../available.d/mr.vcsh
	`-- .mrconfig

Directory and nomenclature has been altered to emphasise the nature of
the symlinks as "enablers" rather than just the ambiguous (in context
of a config management system!) "config". 
