---
title: "Thinking Long Term"
date: 2022-10-21T10:00:46+00:00
draft: false
image: "/images/posts/BEF3112D-1F70-4717-94BC-38F3A167BE85.jpeg"
tags: ["career", "strategy"]
---

Businesses operate on a long time horizon. Plans are made for the next 1-5 years. For tech companies, this means software written will live for at least 1-5 years. Take AWS for example, it launched in 2006 and EC2 is still its core offering. Google launched search in 1998, about 24 years, and using the [Lindy Law](https://en.wikipedia.org/wiki/Lindy_effect), it will be here for another 24 years. Facebook launched in 2006 and its main product, after nearly two decades, is still the social media app.

Software has become more about maintenance than writing new services. Services need to "live" longer. The best way to ensure longevity is by programming strategically as opposed to tactically, as the author of the book [A Philosophy of Software Design](https://www.amazon.com/Philosophy-Software-Design-John-Ousterhout/dp/1732102201) urges us.

Tactical programming is feature focused. This approach is concerned with getting a feature out. Working code is where the process ends. You write just enough code to make it work, then ship it. You do this for every single change. Code quality is an afterthought if a thought at all.

Tactical programming is often the default mode of operation because it offers the illusion of speed. The first iteration of your product might be shipped faster, and maybe the second as well. But after a few iterations of change, technical debt starts to become apparent. It starts slowing you down. 5 percent at first, 10 percent the next time, and finally to a point where a small change makes you groan. It's like the boiling frog syndrome: a frog put in water that is gradually heated to boiling point will eventually die because it is unable to realize the bad situation it is in.

Strategic programming is a long-term approach, where the goal is to produce a great design. The fact that it works is a side effect of achieving a good design. It involves writing documentation for your REST API and ensuring it is kept up to date. It involves making sure the codebase is documented and updated as the system evolves. It is ensuring your system has a solid test suite; unit tests, smoke tests, and integration tests (and whatever your system requires).

It’s easy to confuse design with fancy sequence or architecture diagrams, but that’s just a part of it. I believe design means the entire system at hand, including the code, tests, documentation, and CI/CD pipelines.

Strategic programming is an investment that pays dividends but just like any investment it requires capital upfront (in this case time). You will have to spend extra time to flesh out parts of the design. Write documentation so new team members can get it running in a few minutes. Ensure a CI/CD system is in place. It will slow you down in the beginning. Delay the product launch by a few days or weeks. However, the next time you go integrate a feature, it's much faster, because your system is in a good state.

Think long-term, especially if you work on a service that is at the core of your business. Assume you will have to maintain anything you work on for a few years. Make life easy for your future self.

*Thanks for reading the article. If you enjoyed this and would like to receive similar articles, please consider subscribing. It's free, and I won't ever spam your inbox. Share on [Twitter](https://twitter.com/intent/tweet?url=loststoic.com/thinking-long-term).*