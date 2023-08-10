**DRY** is an acronym for **"Don't Repeat Yourself"**.

Popularized by the book, The Pragmatic Programmer, the DRY principle states that, “every piece of knowledge must have a single, unambiguous, authoritative representation within a system.” Using the principle, logic or algorithms that have certain functionality should only appear once in an application.

It begs the question: what’s a _piece of knowledge_? I would define it either as:

- A precise functionality in the business domain of your application.
- An [[Algorithm]].

To take an overly used e-commerce examples, a `shipment` class and its behavior would be part of the _business domain_ of your application. A shipment is something real your company uses to send products to their customers.

Code repetition that is not necessary should be avoided as recommended by the DRY philosophy. It highlights the value of code reuse and encourages developers to use pre-existing code rather than duplicating it throughout various software system components. Following this rule reduces the possibility of mistakes and defects while also making the maintenance and update processes easier.

- Why

	- Duplication (inadvertent or purposeful duplication) can lead to maintenance nightmares, poor factoring, and logical contradictions.
	- A modification of any single element of a system does not require a change in other logically unrelated elements.
	- Additionally, elements that are logically related all change predictably and uniformly, and are thus kept in sync.

- How

	- Put business rules, long expressions, if statements, math formulas, metadata, etc. in only one place.
	- Identify the single, definitive source of every piece of knowledge used in your system, and then use that source to generate applicable instances of that knowledge (code, documentation, tests, etc).
	- Apply the [Rule of three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)).