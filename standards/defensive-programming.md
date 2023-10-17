---
title: Defensive programming techniques for OutSystems
---
# {{page.title}}

* TOC
{:toc}

> How do you become a good programmer? Accept that you have bad programming habits. The authors of 'The Pragmatic Programmer' share tips for defensive code creation.

## 1. Design by Contract

With design by contract (DBC) organizations should define agreements for how software modules interact: Just as people agree on contracts, so too should systems. DBC aims to ensure the program works in all cases, and everyone validates data in that approach

* [ ] TODO OutSystems how-to

## 2. Dead programs tell no lies

Dead programs tell no lies is a way to say: Detect problems as soon as possible in the program, then have it crash rather than continue to run with issues. As the authors point out in The Pragmatic Programmer, errors result in compromised applications:

"When your code discovers that something that was supposed to be impossible just happened, your program is no longer viable. Anything it does from this point forward becomes suspect, so terminate it as soon as possible. A dead program normally does a lot less damage than a crippled one."

* [ ] TODO OutSystems how-to

## 3. Assertive Programming

> Developers can use assertive programming to verify assumptions as they write code. The authors recommend that programmers leave assertions in place when they deliver a program, rather than follow the common practice of removing them upon delivery. Assertions aim to prevent seemingly impossible things from happening -- though they can't replace error handling. Assertions, while useful, can cause side effects, such as Heisenbugs -- bugs that disappear or alter behavior when a developer or tester tries to study them.

* [ ] TODO OutSystems how-to

## 4. How to Balance Resources

> Thomas and Hunt explain another defensive programming practice is to accept responsibility for resources such as files, memory and devices. The person who allocates a resource should be the one to deallocate it. For example, if a developer accesses a file within code, she should close it within the same routine. Object-oriented programming languages enable developers to encapsulate resources and classes, or they can use code wrappers to check for details like resource state. When in doubt, a defensive programmer should build code to check that the software handles resources appropriately.

* [ ] TODO OutSystems how-to

## 5. Don't Outrun Your Headlights

> Finally, the authors recommend that good programmers take small, deliberate steps rather than risk exceeding the rate of feedback via unit tests and user feedback. Thomas and Hunt recommend that programmers avoid project completion and maintenance timetables that extend months into the future, and eschew guessing at users' future needs, or technology availability.
>
> While a programmer can reasonably predict some things, it's all too easy to fall into the trap of an assumption.
>
> "Much of the time, tomorrow looks a lot like today. But don't count on it."

N

## Reference

* [Learn 5 defensive programming techniques from experts]
* [The Pragmatic Programmer: your journey to mastery, 20th Anniversary Edition, 2nd Edition]
*[Defensive Programming Techniques Explained with Examples]

[Learn 5 defensive programming techniques from experts]: https://www.techtarget.com/searchsoftwarequality/feature/Learn-5-defensive-programming-techniques-from-experts
[The Pragmatic Programmer: your journey to mastery, 20th Anniversary Edition, 2nd Edition]: https://www.informit.com/store/pragmatic-programmer-your-journey-to-mastery-20th-anniversary-9780135957059
[Defensive Programming Techniques Explained with Examples]: https://www.golinuxcloud.com/defensive-programming/
