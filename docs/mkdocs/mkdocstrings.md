# Referencing python source code

## If you want to add source code description to your page, you can use the following syntax.

```md
::: my_project.two_numbers.TwoNumbers
    options:
        show_root_heading: true
```

::: my_project.two_numbers.TwoNumbers
    options:
        show_root_heading: true


---
## If you want to include all submodules, you can use the following syntax.

```md
::: my_project
    options:
        show_root_heading: true
        show_submodules: true
```

::: my_project
    options:
        show_submodules: true


---
## If you want to show only the source code, you can use the following syntax.

```md
::: my_project.two_numbers.TwoNumbers
    options:
        show_docstring_attributes: false
        show_docstring_functions: false
        show_docstring_classes: false
        show_docstring_modules: false
        show_docstring_description: false
        show_docstring_examples: false
        show_docstring_other_parameters: false
        show_docstring_parameters: false
        show_docstring_raises: false
        show_docstring_receives: false
        show_docstring_returns: false
        show_docstring_warns: false
        show_docstring_yields: false
        members: false
        show_bases: false
        show_source: true
```

::: my_project.two_numbers.TwoNumbers
    options:
        show_docstring_attributes: false
        show_docstring_functions: false
        show_docstring_classes: false
        show_docstring_modules: false
        show_docstring_description: false
        show_docstring_examples: false
        show_docstring_other_parameters: false
        show_docstring_parameters: false
        show_docstring_raises: false
        show_docstring_receives: false
        show_docstring_returns: false
        show_docstring_warns: false
        show_docstring_yields: false
        members: false
        show_bases: false
        show_source: true


See [mkdocstrings](https://mkdocstrings.github.io/usage/) for more about the options.

---

## If you want to change the heading level in the table of contents, you can use the # as in markdown.

```md
### ::: my_project.two_numbers.TwoNumbers
    options:
        show_docstring_description: false
        show_docstring_examples: false
        members: false
        show_bases: false
        show_source: true
```

### ::: my_project.two_numbers.TwoNumbers
    options:
        show_docstring_description: false
        show_docstring_examples: false
        members: false
        show_bases: false
        show_source: true

---

