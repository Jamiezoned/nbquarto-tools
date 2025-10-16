## Key Terms

- `Cell`: A code or Markdown unit inside a Jupyter Notebook.
- `Directive`: A pipe-delineated (`|`) comment block recognized by Quarto and `nbquarto-lite`.
- `Processor`: A Python class that modifies or extends notebook cell behavior based on its directives.

---

## Introducing `nbquarto-lite`: Python-Powered Notebook Automation

`nbquarto-lite` is a Python framework I built to simplify how Jupyter and Quarto notebooks are processed and exported.  
It provides a fast, scriptable interface for automatically transforming cells, cleaning markdown, and generating `.qmd` files — without ever touching Lua.

Originally designed for internal documentation workflows, it’s now a lightweight open-source tool that integrates perfectly into any notebook-based Python project.

---

## Why I Built It

Working across infrastructure and automation projects, I constantly needed a way to preprocess large notebooks for documentation.  
Existing solutions (like `nbdev`) were powerful but bloated — so I wrote `nbquarto-lite`, a simpler, more Pythonic alternative.  
No hidden magic, no complex dependencies — just fast, transparent notebook transformation.

---

## How It Works

At the core of `nbquarto-lite` is the **Processor** — a modular class that lets you define exactly how your notebook cells should be modified.

Example:

```python
from nbquarto import Processor

class BasicProcessor(Processor):
    "Adds a comment to the top of each cell that uses a directive."
    directives = ["process"]

    def process(self, cell):
        if any(d in cell.directives_ for d in self.directives):
            cell.source = f"# Processed by nbquarto-lite\n{cell.source}"
