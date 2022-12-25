---
layout: post
title:  "Use Bash aliases to speed up your work"
date:   2022-12-25 13:31:00 +0100
---


### What is detox?

Detox is an open-source framework for testing mobile applications, especially those written in React Native. It is highly configurable and easy to install using `yarn` or `npm`. It was created by developers of [Wix](https://www.wix.com) company to aid in their release process.

### Where can you get detox?

The docs for detox are available [here](https://wix.github.io/Detox/docs/introduction/getting-started/). You might also be interested in [this](https://hackernoon.com/detox-gray-box-end-to-end-testing-framework-for-mobile-apps-196ccd9564ce) article from the authors of Detox, where they explain the road towards creating a testing framework and how they tried Appium but were not satisfied with the flakiness.

### Flakiness - serious problem

I'll bring one interesting fact from that second article: In a test suite with 100 tests, a 0.5% chance of any test failing due to flakiness means that there is almost 40% chance of a failed test run (!). Think about larger suites... this calculation really stuck in my mind. Fortunately, detox comes to the rescue. It does not require sleeps and waits. What is more, it automatically detects when application is in idle state.

### Conclusions

This short article was meant to provide a concise picture of detox as a testing framework. I hope it helps you to ensure a stable release process without flake.