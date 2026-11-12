# UML - Introduction

This project uses Mermaid source files to practise two views of a small library
system: a class diagram for the model's structure and a sequence diagram for
interactions during a loan request.

These are design exercises. The repository does not include a running library
application that implements the classes or workflow shown here.

## Files

| File | Purpose |
| --- | --- |
| [`0-class_diagram.mmd`](0-class_diagram.mmd) | Classes, attributes, public operations, and association multiplicities |
| [`1-sequence_diagram.mmd`](1-sequence_diagram.mmd) | A short interaction sketch involving User, Library, Book, and Loan |

## Class diagram

The diagram defines four classes:

| Class | Attributes shown | Public operations shown |
| --- | --- | --- |
| Library | None listed | `add_book()`, `register_user()`, `create_loan()` |
| Book | `title: str`, `author: str`, `state: bool` | `mark_as_unavailable()`, `mark_as_available()` |
| User | `name: str`, `email: str` | None listed |
| Loan | `start_date: int`, `end_date: int` | `close_loan()` |

The `+` prefix marks public members. The date fields are typed as integers in
the current source; no timestamp format or date representation is defined.
The meaning of the Book `state` flag is not explicitly documented.

### Relationships

| Association | Multiplicity expressed by the diagram |
| --- | --- |
| Library to Book | One library can be associated with zero or more books; each book is associated with one library |
| Library to User | One library can be associated with zero or more users; each user is associated with one library |
| Library to Loan | One library can be associated with zero or more loans; each loan is associated with one library |
| Book to Loan | One book can be associated with zero or more loans; each loan is associated with one book |
| User to Loan | One user can be associated with zero or more loans; each loan is associated with one user |

The connectors are associations. They do not specify inheritance, aggregation,
or composition. The multiplicities alone do not define rules such as allowing
only one active loan for a book.

## Sequence diagram

The current source shows four messages in order:

| Step | From | To | Label |
| --- | --- | --- | --- |
| 1 | User | Library | No descriptive label |
| 2 | Library | Book | No descriptive label |
| 3 | Library | Loan | `create participant Loan` |
| 4 | Library | User | `loan created` |

This sketches a user request, a book interaction, a loan interaction, and a
response. The first two messages do not yet identify an operation or its
arguments. `create participant Loan` appears after the message's colon, so it
is message text rather than a separate participant-creation directive.

The class diagram describes available operations, but the sequence does not
yet explicitly call them or show availability checks, rejected requests,
returns, or closing a loan. It represents an initial success-path sketch,
not a complete specification.

## Viewing the diagrams

The files are plain-text Mermaid source. Open them in an editor to inspect
the notation. For a rendered view, open the source in a Mermaid-capable viewer
that supports class and sequence diagrams.

To read the files from the repository root:

```bash
cd uml_intro
cat 0-class_diagram.mmd
cat 1-sequence_diagram.mmd
```

Printing a `.mmd` file displays its source, not an image. This repository has
no pinned renderer, rendering configuration, or generated diagram images.
There is no compilation step for these design documents.

## What the exercise practises

- Distinguishing a system's static class structure from its interactions.
- Recording attributes, method names, and visibility.
- Expressing one-to-many associations with multiplicities.
- Identifying participants, message order, and a response.
- Checking whether a sequence names the operations and rules implied by a model.

## Verification and current limits

The classes, members, relationships, and message labels above were checked
against the Mermaid source. Rendering and Mermaid syntax acceptance were not
verified because a renderer is not installed in the local environment.

The diagrams leave method signatures, validation rules, storage details, and
failure paths unspecified. Those details should be decided before treating
the model as an implementation contract.
