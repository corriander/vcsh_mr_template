vcsh_mr_template
================

This is a [fork](https://github.com/RichiH/vcsh_mr_template) and isn't
intended to be directly used like the upstream. `git clone` to a
$HOME` subdir is fine but dropping it directly into `$HOME` is not
intended currently.

Note to future me: If it looks like it's just this file in here show
dotfiles ;)

Branch Info
-----------

This branch (`alt_2`) implements the following changes to branch:
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

	.
	|-- .config/
	|   `-- mr/
	|       |-- repos-available/
	|       |   |-- mr.vcsh.mrconfig
	|       |   `-- zsh.vcsh.mrconfig
	|       `-- repos-enabled/
	|           `-- mr.vcsh.mrconfig -> ../repos-available/mr.vcsh.mrconfig
	`-- .mrconfig

Directory and `mrconfig` snippet nomenclature has been altered to
shift the clue to the nature of the snippets as files to the
file-names themselves. This drops the `*.d/` directory suffix
convention in favour of a style employed in `/etc/apache2/sites-*` and
`/etc/apache2/mods-*`: 

	/etc/apache2
	|-- mods-available/
	|   |-- ...
	|   |-- env.load
	|   |-- ...
	|   |-- mime.conf
	|   |-- mime.load
	|	`-- ...
	|-- mods-enabled/
	|   |-- mime.conf -> ../mods-available/mime.conf
	|   `-- mime.load -> ../mods-available/mime.load
	|-- sites-available/
	|   |-- default
	|   |-- mydomain.local
	|	`-- mydomain.com
	`-- sites-enabled/
	    |-- 000-default -> ../sites-available/default
	    `-- mydomain.local -> ../sites-available/mydomain.local

The snippet suffix is a bit of a mouthful, but it makes it obvious
what they really are.
