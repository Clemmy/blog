---
title: "You Wrote Too Many Tests!"
tags: [tests, react, productivity]
layout: post
date: 2018-02-06
---

No, I’m not saying that you shouldn’t aim for 100% code coverage. I’m not saying that testing for edge cases is bad. What I’m saying is, you should be thinking about why you are testing. Let me start with a little story during my internship on the React team.

One day, I submitted a pull request to add a basic Fragment export to React. It was a pretty simple addition, something along the lines of

```js
React.Fragment = ({ children }) => children;
```

I also added a ton of tests because I was super scared of `React.Fragment` breaking somehow if a renderer implementation changes (Note that there are several different renderers that interface with the core React package in order to render to different targets). Something along the lines of

```js
it('should render via native renderer', () => {...});
it('should render via shallow renderer', () => {...});
it('should render via test renderer', () => {...});
it('should render via noop renderer', () => {...});
it('should render via ReactDOM', () => {...});
```

When I finally submitted the pull request for review, Andrew Clark did not approve:

![Oh no! I wrote too many tests.]({{ site.baseurl }}/assets/in_post_images/acdlite-review.png)

This baffled me. For a while, I wondered what the problem could possibly be with writing too many tests. Isn’t that supposed to be a good thing?

Let’s fast forward a couple of hours to when I returned home from work to take a shower.

<img src="{{ site.baseurl }}/assets/in_post_images/most-interesting-man-shower-idea.jpg" alt="Credits to an anonymous memer for this picture." style="width: 320px; margin: 0 auto; display: block;"/>

I thought of several reasons behind Andrew’s rationale. Before I jump into a list of reasons on why to shorten tests, let’s think about why we test software and who our audience is, and what was wrong with my tests.

## Why do we test software

Not for just the sake of writing tests. At least, I hope not.

It boils down to us not being perfect. We write tests to point out and detect errors during the development phase. It allows us to make changes to a system with a high degree of confidence; With end-to-end integration tests, we can ensure that a system behaves the way we want it to, and will do so even if change the implementation or add additional features. Generally, the more we can automate, the better.

## Who is the audience

Yes, your tests have an audience. As with all the code you write, other developers are going to be reading the code, and that developer may even be the future you! In fact, a study conducted in 1992 found that new project members spend 60% to 80% of their time understanding code. That’s why there is so much emphasis put into clean code; It enables other developers to understand your code quicker. If your code is convoluted, then naturally, it will degrade the productivity of future developers who work with your code.

## What was wrong with my fragment test suite

The main problem with my fragment test suite is that it was scope creeping. Rewinding a bit, the filename of my test suite was ReactFragment-test.js . This means that the responsibility of my test suite is to test the functionality of React.Fragment. Testing that it works with every single renderer in React is out of the responsibility of this test suite. For example, if another renderer is added to React, then this test suite will need to be updated, which isn’t obvious for someone unfamiliar with the fragment codebase. Instead, testing that a Fragment renders via a ReactDOM renderer should be done inside ReactDOM’s test suite. This way, the responsibilities of each test suite is clear. In the next part of this post, I’ll summarize the benefits that I found for making test suites more concise.

## What are the benefits of focused tests

* **Writing tests takes less time** — arguable, but generally, it takes less time to write less code.
* **Reading tests takes less time** — there is less noise in your tests, so readers can be more focused on the core ideas.
* **Prevents the issue from propagating** — Something really common in the workplace is to blindly follow the existing conventions. If there are irrelevant tests in one place, then they’re going to grow exponentially.
* **Faster test runs** — With fewer tests in your test suite, your tests run faster, so you have faster feedback, which results in faster development!

## Wrapping Up

We live in a world where we are bound by human error and time. We need tests to verify that a system works and to move fast with confidence. Tests can even serve as documentation in some cases, if they test against the public API. The quicker that someone can read your code and reason about it, the more productive they are. So keep your tests focused, for yourself and for your peers!

Did I miss anything? I’d love to hear about it in the comments.

Thanks for reading!

P.S. Here’s a pretty funny meme I came across on Twitter that is somewhat relevant:

<div style="width: 320px; margin: 0 auto; display: block;">
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">but unit tests are passing... <a href="https://t.co/4aSwau4LMW">pic.twitter.com/4aSwau4LMW</a></p>&mdash; Sarah Drasner (@sarah_edo) <a href="https://twitter.com/sarah_edo/status/847237039351152641?ref_src=twsrc%5Etfw">March 30, 2017</a></blockquote>
</div>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Also, from now on, I'll be switching over to [Medium](https://medium.com/@clemmmy/you-wrote-too-many-tests-6695d3a66294) as my main blogging platform, but I'll still mirror the posts over here.
