---
title: "Python: On typing.Protocol and Duck Typing"
date: 2024-01-08T17:22:02Z
tags: [Python, types, typing.Protocol]
---

Python like other dynamically typed programming languages uses duck typing. Duck typing is typically explained as a type system that does not necessarily care if an object/type is labelled as a duck, but just that if it can quack then it is a duck (see another [example](https://en.wikipedia.org/wiki/Duck_typing#Example)). On the other hand, Rust, C and C++ have a nominal type system, in which types are explicitly declared. Furthermore, Python's classical type hints introduced in [PEP 484](https://peps.python.org/pep-0484/) are evaluated as a nominal type system.

Duck typing is dynamic, and the compatibility of types is checked during runtime. Since the implementation of [PEP 484](https://peps.python.org/pep-0484/) in Python 3.5, many engineers have slowly been adding type hints to their code. However, nominal types are in my opinion not natural to use in Python, given the duck typing behaviour during runtime. 

But lucky for us, duck typing's static sibling [structural subtyping](https://en.wikipedia.org/wiki/Structural_type_system) was introduced in [PEP 544](https://peps.python.org/pep-0544/) in Python 3.8. A structural type system determines type compatibility and equivalences by the structure of a type. That is to mean that A is a subtype of B if and only if all information such as methods, properties and so on of B are also contained in A [0]. Structural subtyping in my opinion is the perfect way to deal with types in Python, as it embodies the idea of duck typing but statically. That allows one to have a more precise one-to-one mapping from the static type system to the runtime type system. 

Now one could resolve the classical duck typing example/question statically using the `Duck` Protocol in Python as follows:

```python
from typing import Protocol
from abc import abstractmethod

class Duck(Protocol):
    @abstractmethod
    def quack(self) -> str:
        raise NotImplementedError
```

As great as theoretically `typing.Protocol` is, I have come across many good Python engineers unaware of `typing.Protocol`'s existence. I think one reason could be that it is often hidden, in other languages you could learn this concept from reading the language's source code. However, Python's source code does not use type hints. Python does have the type information in [typeshed](https://github.com/python/typeshed), this is for historical reasons, but works well. Luckily, your IDE (or Python-related extension to the IDE) likely includes type information from [typeshed](https://github.com/python/typeshed) to help with development (which after all has been one of the main drivers for adding type hints in Python code). 

In the `typing` module, there are already several ready-to-use protocols for common types/methods, and can be found [here](https://docs.python.org/3/library/typing.html#protocols). I have a fond memory of an interview in which they wanted me to add type hint annotations to a function, and I used `typing.SupportsFloat` which exceeded their expectations :).

Python protocol analogues in other languages are often known as interfaces or abstract classes. In my beloved rust, they are known as [traits](https://doc.rust-lang.org/book/ch10-02-traits.html).

On a semi-related note, now in 3.12, one can expose a buffer interface via the [buffer protocol](https://docs.python.org/3/c-api/buffer.html) (note this is different from the typing protocols) directly from Python per [PEP 688](https://peps.python.org/pep-0688/). I can say from personal experience that it is easy to mess up writing a buffer protocol in C, so it is a welcome introduction, especially if you are just wrapping an object that exposes a buffer interface.

[0] https://wiki.c2.com/?StructuralSubtyping
