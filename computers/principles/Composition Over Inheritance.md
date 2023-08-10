It is better to compose what an object can do than extend what it is. Compose when there is a "has a" (or "uses a") relationship, inherit when "is a".

- Why
	- Less coupling between classes.
	- Using inheritance, subclasses easily make assumptions, and break [LSP](https://github.com/webpro/programming-principles#lsp).
	- Increase flexibility: accommodate future requirements changes, otherwise requiring restructuring of business-domain classes in the inheritance model.
	- Avoid problems often associated with relatively minor changes to an inheritance-based model including several generations of classes.
- How
	- Identify system object behaviors in separate interfaces, instead of creating a hierarchical relationship to distribute behaviors among business-domain classes via inheritance.
	- Test for [LSP](https://github.com/webpro/programming-principles#lsp) to decide when to inherit.