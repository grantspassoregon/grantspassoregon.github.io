+++
title = "The Case for Rust at City of Grants Pass"
date = 2023-12-13

[taxonomies]
categories = ["News"]
tags = ["News", "Rust"]

[extra]
author = "Erik Rose"
+++

# Why Rust?

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

## Memory Safety

_The Case for Memory Safe Roadmaps_ published by the Cybersecurity and Infrastructure Security Agency (CISA) in December 2023 describes a memory safety vulnerability as a vulnerability affecting how memory can be accessed, written, allocated or deallocated in unintended ways. Memory-related coding errors include "buffer overflow" ([CWE-120](https://cwe.mitre.org/data/definitions/120.html)), "use after free" ([CWE-416](https://cwe.mitre.org/data/definitions/416.html)), "use of uninitialized memory" ([CWE-908](https://cwe.mitre.org/data/definitions/908.html)) and "double free" ([CWE-415](https://cwe.mitre.org/data/definitions/415.html)).

Memory safety vulnerabilities account for a large class of common vulnerabilities and exposures (CVEs). About 70% of Microsoft CVEs from [2006-2018](https://msrc.microsoft.com/blog/2019/07/a-proactive-approach-to-more-secure-code/) were memory safety vulnerabilities, as well as 70% of vulnerabilities identified in Google's [Chromium](https://www.chromium.org/Home/chromium-security/memory-safety/) project. One [analysis](https://hacks.mozilla.org/2019/02/rewriting-a-browser-component-in-rust/) found 32 of 34 critical/high bugs were memory safety vulnerabilities, and Google's [Project Zero](https://googleprojectzero.blogspot.com/2022/04/the-more-you-know-more-you-know-you.html) team found 67% of zero-day vulnerabilities in 2021 were memory safety vulnerabilities.

## Adoption

[Rust Daily Downloads](./images/rust_daily_downloads.png)

This [article](https://maticrobots.com/blog/why-rust-its-the-safe-choice/) from Matic:

> Using Rust for critical tasks prevents many common security bugs, and encourages robust error handling. This helps us harden our software and protect private data.

> We don't spend time chasing memory safety bugs or concurrency errors, because the compiler has guard rails that push back when code tries to do something dangerous. It's easy to make changes quickly, because the compiler will prevent entire categories of errors. In other languages, this "push back" can be delayed a long time (until static analysis runs, or runtime safety checks fire, or customers report bugs). With Rust we can catch most of these bugs almost instantly.

> There are long-term benefits, too. Rust's type-focused style and firm boundaries improve the long-term manageability of code. Refactoring can be done fearlessly, and the compiler safety checks are robust enough that the refactoring is often done the moment the code compiles.

> Did we take a risk by using Rust? Are we spending our "innovation tokens" recklessly? In our experience, Rust is the safe choice, and it's hard to imagine using anything else. We are able to build things in less time, with less risk, and have more fun doing it. Developers can be fearlessly productive, because there is a lower risk of bugs that cost months of developer time.

From the Filtra Rust [jobs report](https://filtra.io/rust-feb-24), Matic has five full-time Rust developers on staff.

This [article](https://blog.sdf.com/p/fast-development-in-rust-part-one) from SDF:

> Looking back from this one year mark, we're happy to report that not only did we not die on the proverbial hill of learning Rust, the (much hyped) benefits of the language started materializing into tangible returns far sooner than we anticipated. While there is undeniably an upfront investment to learn Rust, by this point for us it has easily paid for itself many, many times over. Rust makes certain tasks easy that would have been exceedingly challenging in other languages.

> An often under appreciated benefit of using a strongly-typed language like Rust in a fast-paced startup environment, is how much it helps with the task of refactoring. ... Because we know that better abstractions an be easily added later, it frees us to be much more bold in experimenting with new features! In Rust we are actually far more comfortable doing the 'quick and dirty' thing to rapidly implement some new feature, knowing that it can all be easily cleaned up into better abstractions later when the requirements become better understood.

Quoting Lars Bergstrom from [The Register](https://www.theregister.com/2024/03/31/rust_google_c/):

> There's no loss in productivity when moving from Go to Rust. And the interesting thing is we do see some benefits from it. So we see reduced memory usage in the services that we've moved from Go ... and we see a decreased defect rate over time in those services that have been rewritten in Rust – so increasing correctness.

> We've seen a decrease by more than 2x in the amount of effort required to build the services in Rust [compared to C++] as well as maintain and update those services written in Rust, and so that's a really huge thing for us because C++ code is very expensive.

> Eight-five percent of [our developers] believe that their Rust code is more likely to be correct than the other code within their system. … I've been through more than one language survey in my life and I've never seen those kinds of numbers before.

---

From [The New Stack](https://thenewstack.io/meet-grain-the-high-level-language-optimized-for-webassembly/):

> “OCaml [was] this fantastic language from the ’90s, with all these amazing different language features … one of the huge features was pattern matching,” he said. “Pattern matching is this incredible, powerful programming language feature that most languages have not had at all.”
>
> Pattern matching in languages like OCaml, Grain and Rust means the compiler will alert the developer if an edge case is missed and a piece of data might break the program, he explained.
>
> “That is such a powerful concept; just because of that you eliminate so many different possible bugs in your programs,” Spencer said. “One of the funny things they say about OCaml is [that] if your code compiles, it’s correct. It might not do what you wanted it to do, but it’s definitely doing what it’s supposed to do based on the code.”
>
> That’s not something you have with JavaScript or Python, he added.
>
> “You write those programs, and it’s broken, you’ve got to go figure out why is the thing broken. And you put in a bunch of log statements and try to debug it and it’s a pain in the butt when you have these other languages that are able to just tell you, ‘Hey, here’s exactly how your code is broken,’” he said.

This is from an interview of Oscar Spencer about the Grain language for web assembly. Even though the author is not promoting Rust, this statement on the virtues of pattern matching in Rust closely matches my own experience.

From [Leonardo Santiago](https://o-santi.github.io/blog/rust-is-not-about-memory-safety/):

> The main strength of Rust, and where it differs from all mainstream languages, is that it has a very clear focus on program correctness. The _raison d’être_ of the borrow checker is statically assuring that all references are pointing to valid memory, such that it is literally impossible for any borrow be null or to point to some freed memory (modulus implementation errors of course).

...

> Not only that, but Rust language's features makes it so, so much easier to write correct software: sum types (tagged unions), `Option` instead of `NULL` (which in and of itself is amazing), `Result` for errors (making obligatory to handle all possible branches your program can take), a strong and powerful static type system, and ditching inheritance and classes in favor of traits.

> Note that I never ever talked about memory safety. Even in a world where C wasn’t in fact full of memory vulnerabilities, Rust would still be miles better, because it statically assures you that the meaning of your program is tightly reproduced by the code you’ve written.
