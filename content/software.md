---
title: Software
weight: 2
---

Some interesting and hopefully helpful tools for others.

### conbench

I'm a core maintainer of [conbench](https://github.com/conbench/conbench). I've been with the project since the early days and have helped it grow and built a team of maintainers around it from one internal use to multiple use cases, including external and unrelated users.

The conbench project is a Language-independent Continuous Benchmarking Framework. The conbench family consists of a (Python) backend and {{< smallcaps api >}} for storing + serving benchmark results over time as well as benchmarking packages for taking benchmarks from various languages (Python, {{< smallcaps r >}}, JavaScript, {{< smallcaps "c++" >}}, Go, Rust) and sending them to conbench for monitoring.


### Arrow

I've been a committer to Arrow since 2021. 

Arrow is a software development platform for building high performance applications that process and transport large data sets. It is designed to both improve the performance of analytical algorithms and the efficiency of moving data from one system (or programming language to another). My specific contributions are in the {{< smallcaps r >}} and Python implementations (including some {{< smallcaps "c++" >}} binding work used by both) along with systems for macro and micro benchmarking of the broader project, improvements to CI and user experience.


### dittodb

I'm the creator and maintainer of [dittodb](https://github.com/jonkeane/dittodb).

[dittodb](https://github.com/jonkeane/dittodb) is a package that makes testing against databases easy. When writing code that relies on interactions with databases, testing has been difficult without recreating test databases in your {{< smallcaps ci >}} environment, or resorting to using sqlite databases instead of the database engines you have in production. Both have their downsides: recreating database infrastructure is slow, error prone, and hard to iterate with. Using sqlite works well, right up until you use a feature (like [a full outer join](https://www.sqlite.org/omitted.html)) or has [quirks](https://www.sqlite.org/quirks.html) that might differ from your production database. dittodb solves this by recording database interactions, saving them as mocks, and then replaying them seamlessly during testing. This means that if you can get a query from your database, you can record the response and reliably reproduce that response in tests.
