## Prefer Model-First Over Code-First for Service Development

> When developing a service, the contract between the client and server is the most important detail there is, and the code that implements the contract is an implementation detail.
> 
> Consider: if you reimplement your Java web service using Kotlin or Go or Rust, none of your clients will care; but if you make a breaking change to your API, the applications your customers built will stop working.
> 
> Model-first requires that we think about services in terms of how our customers use them rather than in terms of how we will implement them. Model-first development often results in a faster time to market due to earlier feedback loops and less time spent implementing a service before it’s adequately designed.

## Designing Data-Intensive Applications (2018) -- Martin Kleppmann

> Data models are perhaps the most important part of developing software, because they have such a profound effect: not only on how the software is written, but also on how we think about the problem that we are solving.