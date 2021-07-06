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
