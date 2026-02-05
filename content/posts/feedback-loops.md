---
title: "Feedback Loops"
date: 2022-10-28T10:00:58+00:00
draft: false
image: "/images/posts/514E4BCB-8D47-4C38-B00D-17AF95C14A77.jpeg"
tags: ["devops", "engineering"]
---

The fictitious company Parts Unlimited in the book [Unicorn Project](https://www.amazon.com/Unicorn-Project-Developers-Disruption-Thriving/dp/1942788762/) is on the verge of insolvency. It is unable to satisfy customer needs because of archaic technology practices.

As a last-ditch effort, the leadership team invests all their efforts towards the Phoenix Project. A project that is supposed to transform their services for the digital era. A project that will provide customers what they want while increasing profit margins.

The release was scheduled by leadership with no exceptions. Teams had to pull all-nighters to sort out dependencies issues and ensure there was enough server capacity. Devs made last minute fixes without verifying the changes.

To no one's surprise, the release was a massive failure. The application was unable to keep up with customer traffic, crashing the site immediately. It corrupted multiple databases resulting in the loss of customer data. To make things worse, the application started to display customer credit card information on the website.

Failure was a premonition if one looked at the way teams operated. Developers got a feature from the product team and wrote code to develop the feature. They didn’t build their code, because it was impossible. No one knew how. There wasn’t a CI system in place to do it. Imagine not being able to build the code you write let alone test it. It’s delusional to think that what you write will always work or even compile.

As if that wasn’t bad enough, developers handed the testing to the QA team. The QA team took a month to test new changes and let the developers know if their code worked as expected or not.

Developers were restricted to deploy their code to production robbing them of ownership. They had to be available when Ops deployed to production in case something went wrong.

The issue with all of this is that the feedback cycle is in the order of weeks or months. You don’t know if your changes worked as a developer, but you don’t want to sit around and do nothing so you build on top of the buggy code.

In information theory, entropy is used to measure the degree of uncertainty in the outcome of a process.  Feedback loops reduce entropy. They help reduce risk when performing major changes because you have already seen all the surprises. Deploying to production is no different than deploying it on your laptop.

At the end of the book, we see effective feedback loops in place. Developers are writing code and receiving feedback within minutes. They know if their code works without breaking existing functionality. It is achieved through automated tests and a build pipeline. When tests fail, developers push a fix within a few hours. This is far better than getting paged at 1 am to know that your code breaks a critical workflow.

Have feedback loops where possible to catch issues early. That's what it means to shift left, you shift issues to the left. The alternative is to wait until things go wrong in production.

*Thanks for reading the article. If you enjoyed this and would like to receive similar articles, please consider subscribing. It's free, and I won't ever spam your inbox. Share on [Twitter](https://twitter.com/intent/tweet?url=loststoic.com/feedback-loops).*