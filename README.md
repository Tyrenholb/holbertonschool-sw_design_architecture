# Software Design and Architecture

This repository contains my Holberton School exercises in software design.
The projects combine small Python implementations of design patterns with UML
models written in Mermaid.

The Python examples show how object creation, notifications, and composable
behavior can be separated. The diagrams explore a library system's classes,
relationships, and the order of interactions during a loan request.

## Project folders

| Folder | Contents | What it covers |
| --- | --- | --- |
| [`design_patterns`](design_patterns/README.md) | Three Python demonstrations | A vehicle factory, topic-filtered observers, and beverage decorators |
| [`uml_intro`](uml_intro/README.md) | Two Mermaid source diagrams | A library class model and a loan-request sequence sketch |

These are independent exercises, not components of a single application.
The vehicle, news, and beverage examples do not implement the library model.

## Design patterns

| Example | Design idea |
| --- | --- |
| [`0-factory.py`](design_patterns/0-factory.py) | A registry maps names to vehicle classes so callers can request instances and register additional kinds |
| [`1-observer.py`](design_patterns/1-observer.py) | A subject delivers topic notifications to subscribed observers without hard-coding each observer type |
| [`2-decorator.py`](design_patterns/2-decorator.py) | Wrappers add ingredients, cost, and description around a shared beverage interface |

Each file includes its own demonstration guarded by
`if __name__ == "__main__"`. There are no external runtime packages, network
requests, or application data files needed for these examples.

## UML diagrams

| Diagram | What it shows |
| --- | --- |
| [`0-class_diagram.mmd`](uml_intro/0-class_diagram.mmd) | Library, Book, User, and Loan classes, their public members, and one-to-many associations |
| [`1-sequence_diagram.mmd`](uml_intro/1-sequence_diagram.mmd) | Messages between User, Library, Book, and Loan, ending with a loan-created response |

The class diagram describes structure; the sequence sketch describes message
order. The sequence has unlabeled messages and does not yet fully specify the
operations or error paths. See its folder README for the exact source details.

## General Python requirements

- Correction environment: Ubuntu 20.04 LTS with Python 3.8.x.
- Every Python file must start exactly with `#!/usr/bin/env python3`.
- Python files must be executable and end with a newline.
- Code must follow PEP8, checked with pycodestyle 2.7.x.
- Output formatting must match the expected results exactly.
- External libraries are not allowed unless explicitly required by the task.

The Python examples use standard-library features, including `typing.Protocol`
and abstract base classes from `abc`. They postpone type annotations with
`from __future__ import annotations`.

Mermaid diagrams require a compatible viewer for rendering. They are plain
text and do not use the Python execution or style-checking workflow. No
Mermaid renderer or version is configured in this repository.

## Run an example

From the repository root:

```bash
python3 -B design_patterns/0-factory.py
```

Output:

```text
road
rails
lane
scooter_lane
```

Run the other two demonstrations separately:

```bash
python3 -B design_patterns/1-observer.py
python3 -B design_patterns/2-decorator.py
```

Their folder README explains every output line and how the classes interact.
`-B` prevents bytecode cache writes. To inspect the diagram source, open the
`.mmd` files in an editor; rendering them requires a Mermaid-capable viewer.

## Checks and current status

Check the interpreter and style-checker versions in your selected environment:

```bash
python3 --version
pycodestyle --version
pycodestyle design_patterns/*.py
```

All three demonstrations produced their documented output on local Python
3.8.20. Their shebangs and final newlines match the requirements, but their
tracked file modes are not executable. Invoking them with `python3` works
without that mode and does not prove direct-execution compliance.

The installed pycodestyle 2.12.1 checker passes the Python files; correction
requires 2.7.x. Local checks are separate from an Ubuntu 20.04 correction run.

UML descriptions were checked against the source. Diagram rendering and
Mermaid parser acceptance were not verified locally. The model is a design
sketch rather than a complete library application or implementation contract.
