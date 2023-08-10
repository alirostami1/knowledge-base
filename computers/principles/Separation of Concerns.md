The term 'separation of concerns' (SoC) was coined in Edsger W. Dijkstra's article On the role of scientific thought from 1974:
"... But nothing is gained --on the contrary!-- by tackling these various aspects simultaneously. It is what I sometimes have called 'the separation of concerns', which, even if not perfectly possible, is yet the only available technique for effective ordering of one's thoughts, that I know of. This is what I mean by 'focusing one's attention upon some aspect': it does not mean ignoring the other aspects, it is just doing justice to the fact that from this aspect's point of view, the other is irrelevant." (Springer-Verlag, 1982)

Separation of concerns is a principle used in programming to separate an application into units, with minimal overlapping between the functions of the individual units. The separation of concerns is achieved using modularization, encapsulation and arrangement in software layers.

Although the classic three-layer architecture of Application Server ABAP (AS ABAP) is ideal for ABAP programming based on the SoC principle, this possibility was never explored. Application programs (in other words, dialog programs in module pools or reports in executable programs) were usually displayed as monolithic blocks, in which the system simultaneously reacted to user actions of the presentation layer, completed the application logic and executed accesses to data on the persistency layer. This type of programming is no longer relevant in today's programming world, where concepts like service-oriented architecture (SOA) set the trend.

- Why

	- Simplify development and maintenance of software applications.
	- When concerns are well-separated, individual sections can be reused, as well as developed and updated independently.

- How

	- Break program functionality into separate modules that overlap as little as possible.