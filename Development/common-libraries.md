- [TL;DR](#tldr)
- [Why Common Libraries](#why-common-libraries)
	- [Convenience](#convenience)
	- [Dependency Management](#dependency-management)
	- [Laziness](#laziness)
- [The Trash Bin](#the-trash-bin)
- [In Conclusion](#in-conclusion)


2023-06-21

As software engineers, we've all seen many large, well-architected projects that split their logic into multiple libraries. As our codebases grow larger and more complex, it's necessary to partition our code into a hierarchy of responsibility. If we didn't do this, we'd have a disorganized mess on our hands, taking the form of antipatterns such as spaghetti code or [The Blob](https://sourcemaking.com/antipatterns/the-blob).

In the process of this organization, nearly all projects develop a _shared_ or _common_ library. As these names suggest, this is where code goes when it has multiple dependents. These libraries are ubiquitous, and serve as a convenient catch-all for logic, configuration, or dependencies that either need to be reused or don't fit in an existing library.

Unfortunatly, common libraries are themselves an antipattern, in my not-so-humble opinion. Here's why.

# TL;DR

Common libraries are bad because they inherently lack specificity. As a project grows, they're also highly susceptible to bloating. Instead of implementing a common library, take the time to think of more specific categories for shared code. Then, build libraries for each category with accurate and descriptive names.

# Why Common Libraries

We've already discussed how "common" it is to find these code caches. Even world-class projects like Chromium are guilty of this. Why? There may be any number of reasons, and even some good ones; but a few seem to stand out.

## Convenience

There's no denying that having a single location from which to access all shared project code is very convenient. It's a simple way to create a kind of generic hierarchy, in which all the specific modules of your project are built on the "foundation" of your common library. It also helps you to avoid pitfalls like circular references.

## Dependency Management

If you've ever worked on a project with third-party dependencies, you know just how quickly managing those dependencies can devolve into chaos. Trying to juggle versions and vendors among all the separate parts of your project is an engineer's worst nightmare, and takes significant time away from the productive side of our jobs.

With a common library, you simply dump all your dependencies into one place, and manage them all together. The pieces of your project that depend on the common library will inherit those dependencies. The same is true for external configuration.

## Laziness

This is the real elephant in the room. The truth is that common libraries are an attractive means to sweep the hard task of naming under the rug. As a bonus, they do so in a way that's become an industry standard. It's a seemingly free way to cut corners and save some time over the life of the project.

# The Trash Bin

Common libraries have a tendency to devolve into technical debt of one form or another. They are ambiguous by their nature: the word _common_ is a direct antonym of _specific_.

Likely the most prevalent issue with common libraries is their susceptibility to bloat. As previously stated, they're a catch-all; an excuse to dump code that doesn't immediately fit in a more specific part of the project. 

In the worst cases, large swaths of the common library actually aren't "common" at all. Instead, they contain code that is referenced in one or fewer places. This code seemed likely to become widely used, but was later abandoned for a different solution. 

Rather than discard unused code, the engineer may be tempted to drop it into the common library, "just in case" they need it later. A slap in the face to version control.

# In Conclusion

Common libraries have a lot in common with variables named `x` and `y`: They're vague and they're generally a result of laziness. Most importantly, they make the codebase more difficult to understand.

Take the time to organize _all_ of your code. Name it. Categorize it. Every line has its proper place. Conversely, no code is so generic that it warrants being placed in a universal category. If you think yours is, then you've made it too abstract, and it's a waste of the bytes needed to store it. Get rid of it and make something specific and useful.