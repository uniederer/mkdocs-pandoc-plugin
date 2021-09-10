# MkDocs Pandoc Plugin

The pandoc plugin will export all markdown pages in your MkDocs repository to any format suppoorted by Pandoc.

This package requires:

1. Python 3.6 or higher
2. pandoc, xelatex(to support Chinese)

    ```bash
    sudo apt install pandoc
    sudo apt install \
        texlive \
        texlive-latex-extra \
        texlive-latex-recommended \
        texlive-xetex
    ```
    
3. MkDocs version 1.0 or higher (0.17 works as well)

## Installation

Install the package with pip:

```bash
pip install mkdocs-pandoc-plugin
```

Enable the plugin in your `mkdocs.yml`:

```yaml
plugins:
    - search
    - pandoc
```

> **Note:** If you have no `plugins` entry in your config file yet, you'll likely also want to add the `search` plugin. MkDocs enables it by default if there is no `plugins` entry set, but now you have to enable it explicitly.

More information about plugins in the [MkDocs documentation](http://www.mkdocs.org/user-guide/plugins/).

## Contributing

From reporting a bug to submitting a pull request: every contribution is appreciated and welcome. Report bugs, ask questions and request features using [Github issues][github-issues].

If you want to contribute to the code of this project, please read the [Contribution Guidelines][contributing].

#### **Special thanks**

Special thanks to [Stephan Hauser][shauser] for the development of [mkdocs-pdf-export-plugin][mkdocs-pdf-export-plugin] from which this plugin was forked.

[github-issues]: https://github.com/alexandre-perrin/mkdocs-pandoc-plugin/issues
[contributing]: https://github.com/alexandre-perrin/mkdocs-pandoc-plugin/blob/master/CONTRIBUTING.md
[shauser]: https://github.com/shauser
[mkdocs-pdf-export-plugin]: https://github.com/shauser/mkdocs-pdf-export-plugin

# Options

Pass in options through `mkdocs.yml`:

```yaml
plugins:
  - pandoc:
      combined: yes
      enabled_if_env: CI_ENABLE_PANDOC_EXPORT
      pandoc_args:
        pdf_engine: xelatex
        to: pdf
        
```

### `enabled_if_env`

<small>*default: not set*</small>

Setting this option will enable the build only if there is an environment variable set to 1. This is useful to disable building the PDF files during development, since it can take a long time to export all files.

### `combined` 

<small>*default: false*</small>

Setting this to `true` will combine all pages into a single document. All download links will point to this file.

### `combined_output_path` 

<small>*default: pdf/combined.pdf*</small>

This option allows you to use a different destination for the combined document file. Has no effect when `combined` is set to `false`.

### `pandoc_args`

<small>*default: empty dict*</small>

This allow to pass options to the pandoc export commands. 
`pandoc_args` must be a dict of full pandoc option name / value:

```yaml
plugins:
  - pandoc:
      pandoc_args:
        template: template.latex
        pdf_engine: xelatex
```

Which will be translated to `pandoc --template=template.latex --pdf-engine=xelatex -o <file>.pdf <file>.md`

### `pandoc_extra_args`

<small>*default: empty string*</small>

This allow to pass a string as raw options to the pandoc export commands.

> **Note**: Be mindful not to duplicate arguments from `pandoc_args`.

```yaml
plugins:
  - pandoc:
      pandoc_extra_args: "--template template.latex --pdf-engine xelatex"
```

