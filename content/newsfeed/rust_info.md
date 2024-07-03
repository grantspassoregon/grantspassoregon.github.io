+++
title = "The Case for Rust at City of Grants Pass"
date = 2023-12-13

[taxonomies]
categories = ["News"]
tags = ["News", "Rust"]

[extra]
author = "Erik Rose"
+++

From the CISA white paper, [The Case for Memory-Safe Roadmaps](https://www.cisa.gov/sites/default/files/2023-12/The-Case-for-Memory-Safe-Roadmaps-508c.pdf):

> Mozilla released Rust in 2015. It is a compiled language and focuses on performance, type safety, and concurrency. It has an ownership model designed to ensure that there is only one owner of a piece of data. It has a feature called a “borrow checker” designed to ensure memory safety and prevent concurrent data races. While not perfect, the borrow checker system goes a long way to addressing memory safety issues at compile time. Rust enforces correctness at compile time to prevent memory safety and concurrency problems at runtime. As an example, a data race is a class of software bug that is notoriously hard to track down.
>
> _“With Rust, you can statically verify that you don’t have data races. This means you avoid tricky-to-debug bugs by just not letting them into your code in the first place. The compiler won’t let you do it.”_ - Lin Clark (Fastly)
>
> Rust has been getting a great deal of attention from several high-profile technologies, including the Linux kernel, Android, and Windows. It is also used in apps like those from Mozilla, and other online services, such as Dropbox, Amazon, and Facebook.

Reasons that Microsoft [provided](https://security.googleblog.com/2023/01/supporting-use-of-rust-in-chromium.html) for bringing Rust into the Chromium project (the Chrome browser):

- Simpler to use
- Safer
- Speeds up development
