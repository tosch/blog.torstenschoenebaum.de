---
title:  "Highlights @ CodeMotion Berlin 2018"
date:   2019-01-06 20:00:00 +0100
categories: conferences
header:
  image: /assets/images/posts/2019/01/codemotion.jpg
  teaser: /assets/images/posts/2019/01/codemotion_logo.png
toc: true
---
In November 2018, I attended to the CodeMotion software developer conference in Berlin. The CodeMotion is a multi-track
conference, covering a wide range of topics. Obviously, I was only able to see a small and very personal selection of
all talks given. In this article, I'll try to summarize most of the talks I've seen. I won't cover the keynotes, though.
While they were inspirational, they were also very good presentations and it would destroy too much of their magic when
being put into a few words of mine.

## [Stève Sfartz](https://twitter.com/SteveSfartz): Meeting Rooms are talking. Are you listening?

This talk was Cisco's meeting room technology and its APIs. I did not take away very much from this talk, although it
was interesting to see what's possible with modern online conference tech. The most interesting fact I learned is that
they are offering timeboxed access to their sandbox environment: You book a sandbox for a certain period of time and it
is reset afterwards.

## [Alessandro Confetti](https://twitter.com/zigolab): OOP vs. Functional: Stop the fight and start building message driven serverless apps

> Serverless computing is the most intelligent misuse of a bunch of computers

Confetti's talk was more inspirational than technical: He started talking about the programming paradigms behind
John McCharty's LISP (functional with focus on data processing) and Alan Kay's SmallTalk (object oriented with focus on
message delivery between objects). He argued that it is possible to combine the best of both worlds using serverless
computing environments and showed some examples for message driven architechtures.

## [Sasha Romijn](https://twitter.com/mxsash): Everything I always wanted to know about crypto, but never thought I'd understand

Romijn gave a very brief introduction into crypto algorithms and how they work. It doesn't make much sense too do an
excerpt about that here, there are enough online tutorials covering that. There were some useful hints and DOs and DONTs
for your own project that requires crypto, though:

* Fernet is a great library when it comes to symetric encryption, and it is also available for different programming
  languages.
* For asymetric encryption, Romijn kind of avoided a recommendation. GnuPG might be a choice, but it might not be a good
  one.
* When using crypto:
  - always consider a wide range of threats
  - do not forget about recovery options
  - authenticate your users
  - do not confuse authentication and confidentiality
  - handle your keys properly
  - do not forget about side channel attacks
* [https://cryptopals.com](cryptopals.com) has a very nice set of crypto challenges to practice on.

## [Arman Amcalar](https://twitter.com/dashersw): The human side of microservices

This was one of the talks I liked most, not necessarily because it contained many new experiences, but because of the
many hints Amcalar gave about why microservice oriented architectures are useful and how they can be implemented.

He started with the notion that microservice architectures are not introduced for technical reasons. He reasoned that
microservices are all about decoupling with their auto discovery, zero configuration, high redundancy, fault tolerance
and self-healing capabilities. This decoupling, in his opinion, fits very well to the individualistic attitude of the
Generation Y, which is more prominent in tech nowadays. Generation Y software developers seek responsibility and
ownership of their work's results, but they also want to feel happy about what they are doing.

Amcalar gave some hints how to succeed with microservices:
* Observe your team's psychology and build for that.
* Create space and infrastructure for autonomy.
* Decouple communication from implementation.

In his opinion, those are the aspects you have to keep in mind:
* Team setup
* Ownership: Define and document areas of responsibility
* Documentation of public interfaces
* There should be no room for interpretation, because that is being follwed by frustration

## [Ellen König](https://twitter.com/ellen_koenig): Machine Learning for the curious but confused

While this was an interesting talk, I did not take many notable notes. I liked the definition of learning König gave:

> Learning is being able to deal with new situations based on the past.

Her [list of machine learning resources (slide 12)](https://www.slideshare.net/ellenkoenig/machine-learning-for-the-curious-but-scared)
really seemed to be very useful.

## [Willian Martins](https://twitter.com/wmsbill): Back to the future of JavaScript: The next features and amazing proposals

If I would be more into JavaScript and would have been less tired at the end of a long conference day, I probably would
have enjoyed this talk more. So if my notes here are scarce, it's my fault and doesn't say anything about the talk's
quality. Martins showed some proposals for features that might be included in one of the next JavaScript versions. He
particularly mentioned the Bind Operator, the Pipeline Operator and Partial Application. Have a look [at his slides](https://speakerdeck.com/wmsbill/node-conf-ar-2018)
to learn more.

## [Michelle Garret](https://twitter.com/msmichellegar): Build the API you want to see in the world

This was a talk advocating for GraphQL, showing the advantages of this query language for remote data in an application
Garret had worked on. She first compared REST and GraphQL: Multiple vs. single endpoint, pre-defined data set vs.
definable data set and the availability of a schema to describe the data (although I do not agree on this point: When
REST is done completely, there also is a schema for each available resource).

Garret identified the following issues with the REST API that was later replaced by a GraphQL implementation:
* there is a tight coupling between frontend components and REST endpoint responses
* frontend components needed and used contextual information (not just the bare data)
* not all the data returned by the REST endpoint is actually needed, so that there is quite some overhead
* also, often it requires multiple requests to different REST endpoints to fetch all the data needed
* it is always hard to understand and use 3rd party APIs

Garret showed how GraphQL helped them to overcome these issues in their application. It was a nice use case report, but
I still think that there are valid use cases for RESTful APIs. GraphQL is a valid choice in many cases, but it's not a
tool that fits everything.

## [Bernd Rücker](https://twitter.com/berndruecker): 3 common pitfalls in microservice implementation and how to avoid them

This was definitely the talk I liked most. The pitfalls themselves were not new to me, but Rücker showed some ways to
alleviate them which were new to me. You can find the talk at [Bernd Rücker's website](https://berndruecker.io/3-pitfalls-in-microservice-integration/).

Rücker began his talk by stating that it is impossible to avoid failures in distributed systems. That's why resiliency
is important.

He also argued that it is a bad design to block for external requests. The Circuit Breaker Pattern should be used
instead. While there should be short timeouts and fast failures, errors from external requests should not be transported
back to the end user, because this affects the user experience a lot. Instead, the service should send a response to the
consumer that allows the latter to retry the same request later on. In Rücker's opinion, workflow engines are a very
good tool to help with this kind of feature.

> Make sure your service provider implements idempotency. This alone makes the world a better place.

I had to chuckle when Rücker said those words — idempotency is quite some topic in my day job at the moment. Again, in
his opinion, workflow engines are a good tool to implement this feature. Another quote I liked:

> Synchronous communication is the crystal meth of distributed programming.

As failures are likely, relying on synchronous requests will cause a bad user experience. By using asynchronous
communication as often as possible, this can be avoided. It is also possible to take a hybrid approach: Send a
synchronous response when there is no error or timeout, but send an asynchronous one when there is an error.

Rücker also mentioned "Distributed Transactions" as third pitfall, but unfortunately the talk's time was up, so that he
couldn't say anything about this topic, but there is another talk of him available online: "[Lost in Transaction](https://berndruecker.io/lost-in-transaction/)".

## [Jan Stȩpień](https://twitter.com/janstepien): GraalVM: Fast, polyglot, native.

In this talk, Stȩpień showed some impressive features of the GraalVM, which is a Java Virtual Machine that is using the
Graal compiler for Just In Time compilation (instead of Java's default HotSpot compiler). The performance improvements
Graal can yield are stunning. There also is Truffle, which is a set of APIs to use the GraalVM. TruffleRuby is using
this, as well as Sulong, which runs LLVM bytecode — that way, you can use any programming language with Graal were there
is a LLVM bytecode compiler for (which probably is a very long list).

GraalVM also has a new feature that allows Ahead Of Time Compilation. This allows building native machine code binaries,
which could not only improve the performance of your web application, but also reduce the size of your Docker images
drastically, because they would just need your application binary and nothing more.

There are some drawbacks, though, which make this feature rather unusable together with Ruby. For instance, class
initialization is done at compile time, which will cause issues when accessing dynamic data sources like databases
or environment data.

## [Paolo D'Incau](https://twitter.com/pdincau) & [Pietro Di Bello](https://twitter.com/pierodibello): Surviving a legacy codebase

This was the last talk I heard before the closing keynote and it was very entertaining. D'Incau and Di Bello talked
about their experiences as consultants fighting bugs in legacy codebases. They started with various possible definitions
of the term "legacy codebase" like "code without tests" and "valuable code that we feel afraid to change". Then they
presented their principles when dealing with legacy:

1. Understand the context of the software
   Why are we here? It is important to talk with the business and understand their business case.
2. Maximize safety
   You should write tests firsts, for instance characterization tests that describe the current behaviour. Just make
   sure to ensure sufficient code coverage.
3. After having written tests, you can move on carefully by taking tiny steps — as if you were moving on ice
4. Keep focus on what matters
5. Be a good scout and leave the code better than you found it
6. Reduce the information overload

When applied, those principles should allow you to slowly expand your sphere of control. You should, though, always keep
in mind that any refactoring should be driven by real and emergent needs.

## Summary

Those two days at CodeMotion in Berlin were great. As you can see above, I've learned a lot and met many nice people.
Thanks to my employer [Sage](https://sage.com/) for allowing me to attend to this conference :-)
