# Python - Design Patterns

Three short Python demonstrations practise separating object creation,
notifications, and optional behavior. The examples implement a registry-based
factory, an observer subject with topic filtering, and beverage decorators.
Each file runs independently and prints its result to the terminal.

## Files and patterns

| File | Pattern | Main parts |
| --- | --- | --- |
| [`0-factory.py`](0-factory.py) | Factory | Vehicle classes, a registry, registration, and object creation by name |
| [`1-observer.py`](1-observer.py) | Observer | A subject, an observer protocol, subscriptions, topic filters, and notifications |
| [`2-decorator.py`](2-decorator.py) | Decorator | A beverage interface, coffee, and composable milk/sugar/caramel wrappers |

## General Python requirements

- Correction environment: Ubuntu 20.04 LTS with Python 3.8.x.
- Every Python file must start exactly with `#!/usr/bin/env python3`.
- Python files must be executable and end with a newline.
- Code must follow PEP8, checked with pycodestyle 2.7.x.
- Output formatting must match the expected results exactly.
- External libraries are not allowed unless explicitly required by the task.

These examples use only the standard library, including `typing` and `abc`.
Annotations are postponed with `from __future__ import annotations`. No package
installation or application server is needed to run them.

## Factory

`VehicleFactory` starts with Bus, Train, and Bike registrations.
`register_kind(name, cls)` adds or replaces an entry. `create(kind)` constructs
a fresh instance by calling the registered class. The demo registers Scooter
before creating all four vehicle types.

| Vehicle | Value returned by `mode()` |
| --- | --- |
| Bus | `road` |
| Train | `rails` |
| Bike | `lane` |
| Scooter | `scooter_lane` |

From the repository root:

```bash
cd design_patterns
python3 -B 0-factory.py
```

Output:

```text
road
rails
lane
scooter_lane
```

An unknown kind raises `ValueError`. Registration adds a vehicle without
adding another conditional branch to `create`. Registered classes must be
callable without arguments; their interfaces are not validated. The remaining
TODO comments describe Scooter steps that the demo already performs.

## Observer

`NewsSubject` stores observers and optional topic sets. Observers implement
`update(topic, data)`, as described by the `Observer` protocol.

- `subscribe(observer, topics=None)` subscribes to every topic by default.
- A supplied topic set restricts notifications to its members.
- Subscribing the same observer again is ignored, including a new topic set.
- `unsubscribe(observer)` removes the subscription and ignores a missing observer.
- `notify(topic, data)` calls matching observers synchronously.

The demo subscribes a log observer to sports/breaking news, an email observer
to every topic, and an SMS observer to breaking news only.

From `design_patterns`:

```bash
python3 -B 1-observer.py
```

Output:

```text
email:weather=rain
log:sports=goal
email:sports=goal
log:breaking=alert
email:breaking=alert
sms:breaking=alert
```

These observers print messages; they do not send real email or SMS. An empty
topic set receives nothing. Observers must be hashable because subscriptions
are stored in a dictionary. Callback exceptions are not caught.

## Decorator

`Beverage` is an abstract base class with `cost()` and `description()` methods.
`Coffee` supplies the base implementation. Each decorator wraps another
beverage, adds to its cost, and extends its description.

| Component | Cost contribution | Description |
| --- | --- | --- |
| Coffee | `50` | `Coffee` |
| MilkDecorator | `10` | Appends ` + milk` |
| SugarDecorator | `5` | Appends ` + sugar` |
| CaramelDecorator | `15` | Appends ` + caramel` |

Costs are integer example values; the code does not specify a currency.
Nesting wrappers combines behavior without requiring a separate class for
every combination.

From `design_patterns`:

```bash
python3 -B 2-decorator.py
```

Output:

```text
Coffee + milk 60
Coffee + sugar + milk 65
Coffee + sugar + milk + caramel 80
```

Descriptions follow the wrapping order from the inner beverage outward.
Wrappers assume the inner object provides the beverage methods; they do not
validate it or prevent repeated ingredients.

## Checks and current status

With the correction tools available, run from this directory:

```bash
python3 --version
pycodestyle --version
pycodestyle *.py
```

All three files have the required shebang and final newline, and their exact
printed output was verified on local Python 3.8.20. They lack the executable
Git mode, so the examples invoke the interpreter explicitly. The installed
pycodestyle 2.12.1 checker passes these files; correction requires 2.7.x.

`-B` prevents bytecode cache writes. The examples create no application data
files and make no network requests. Each has a `main` guard, so importing it
does not run its demonstration.
