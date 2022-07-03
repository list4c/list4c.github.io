---
layout: post
title:  "How to access your favourite docs the green way"
date:   2022-07-03 12:59:00 +0100
---

Some time ago I was writing a Cypress test and opening a lot of tabs with Cypress documentation. At some point I became haunted by the idea that opening these doc pages over and over multiple times is a waste of energy and may have some impact on climate change.

Hours later I was becoming acquainted with the reports about the impact of ICT (Informatics and Communication Technology) on our planet. I learned that although many digital services, like AI, help us optimize resources and reduce waste, ICT still contributes to green house gas emissions (GHGE) because of infrastructure needed to run it. The level of GHGE emissions attributed to ICT is increasing with every year, as there are more and more digital services and Internet users in general. Bottom line: some of the most energy-hungry forms of ICT are video streaming, bitcoin mining and AI. Compared to those, my transgressions appeared minute. But I still felt something could be done about my browsing habits. 

So I restated my problem: I was opening and closing the same websites, thereby leading to waste. And I came up with several ideas, specifically for the dev documentation:

### cloning the whole docs repo 

![Cypress docs running on localhost](/assets/images/cypress-docs.png){:class="img-responsive"}


"Great idea" :D, I thought to myself. I could clone the [repo of Cypress docs](docs.cypress.io/) and would then be able to save on network requests. But I soon came to the conclusion that it was only a half-great solution. Cypress documentation is pretty big. As you can imagine, cloning the whole repo and installing all the dependencies was more than a couple hundred megabytes. Not that sustainable I guess... And if you want to have some other documentation repositories  accessible offline in the same manner, you would need to follow the same procedure for all of them. Too time-consuming and resource-exhaustive.

### [devdocs.io](https://devdocs.io/)


![Dev.docs example](/assets/images/devdocs.png){:class="img-responsive"}

So I looked a bit further and found devdocs.io. You could compare it to a wiki with offline capabilities. It has lots of APIs listed, i.e. programming languages, markup languages, frameworks, and you can select chosen documentation packages to your local storage so that browsing the docs requires no internet at all. Yippee! Finally I found something that was a comprehensive answer to my problem.


### [Zeal](https://zealdocs.org/)


![Dev.docs example](/assets/images/zeal-example.png){:class="img-responsive"}

I thought I found the ultimate solution with devdocs.io, but some time a later a developer in my team told us about an app that did the same and could be installed as Linux package. Enter Zeal. Zeal is a pretty powerful tool which allows you to choose from over 200 APIs. It is inspired by [Dash](https://kapeli.com/dash), a similar tool that works on MacOS. Zeal also uses Dash's documentation library, so I guess the two of them have identical resources.  

How to install Zeal in Debian/Ubuntu distributions:

{% highlight bash %}
sudo apt install zeal 
{% endhighlight %}

Installation  worked nicely in Ubuntu 20.10 but then I tried installing it on my Debian machine:


![Example of a search in zeal](/assets/images/zeal-non.png){:class="img-responsive"}

Ouch! Not working in Debian Bullseye?

Indeed. The _zeal_ package is not supported in the stable version of Debian. But you can add one of the Debian packages that contain _zeal_ and after updating your package sources, you're good to go.

The list of packages which support zeal in Debian can be found [here](https://packages.Debian.org/search?suite=all&searchon=names&keywords=zeal). One of the packages is bullseye-backports - a pretty clever way to get updates for a specific package from the Debian testing distribution (at the time of publishing this post, the codename for next release is _bookworm_) to your stable Bullseye system. You get the best of both worlds, i.e. a package that has not arrived in Debian stable yet, or a newer version of a package which is not yet available for users of the stable distribution. 

How to enable a backports repository for my Debian Bullseye? I followed advice from [this article](https://wiki.Debian.org/Backports).If you don't want to read through it and need an easy fix, just type this in your terminal (use `sudo` if needed)

`apt update`

`apt edit-sources`


(here choose a text editor by typing a number)

Now at this point it's pretty possible that you will see a list of repositories for updates to your release.

This is how it looked in my vim editor after enabling the Bullseye-backports:


![Apt sources content in the vim editor](/assets/images/apt-sources.png){:class="img-responsive"}

 As you can seen, there is a list called Bullseye-updates. Below you will see a list of links, some of them commented out. All that needs to be done is to remove the `#` at `deb http://deb.debian.org/debian bullseye-backports main contrib non-free` and save changes to the document. (Note: you don't need the [deb-src package](https://unix.stackexchange.com/questions/20504/the-difference-between-deb-versus-deb-src-in-sources-list) if you're not developing or testing Debian packages).

However, if you do not see such a ready-made list, add `deb http://deb.debian.org/debian bullseye-backports main contrib non-free` at the bottom and save changes.

Then:

`apt update`
`apt install zeal`


And you're there (for Debian Bullseye).



### Conclusions


I must confess that using offline documentation has not become my second nature yet. But when you realise that you can have a tool which contains many documentations in one place, such as Zeal or devdocs.io, you start to appreciate it. 

Have I found all the libraries I was interested in? Yes, pretty much all of them, except [_detox_](https://github.com/wix/detox). Some libraries were present in devdocs.io, but no in Zeal and I have a feeling that devdocs.io might have a bit more of them than Zeal, e.g. I found Jest and Cypress in devdocs.io, but not in Zeal. So I'm not sure yet which of these two I will be using most, but definitely plan to use them and:
- save precious energy
- save time

Hope it helps you as well. Till next time!


### Links:

[Digital 2022: Global Overview Report](https://datareportal.com/reports/digital-2022-global-overview-report) - Comprehensive report with lots of data on the number of Internet users worldwide, trends, market share and lots of other interesting findings
[Global climate change: Vital Signs of the Planet](https://climate.nasa.gov/facts/) - Website by NASA clearly presented the facts on global warming
[Assessing ICT global emissions footprint: Trends to 2040 & recommendations](https://www.sciencedirect.com/science/article/abs/pii/S095965261733233X) - Scientific article on measuring the carbon footprint of ICT, which may rise up to even 16% of total GHGE emissions in 2040
[Why your internet habits are not as clean as you think](https://www.bbc.com/future/article/20200305-why-your-internet-habits-are-not-as-clean-as-you-think) - a very well written article from BBC which presents most important facts about the carbon footprint of ICT and what we can to reduce it as individual users
[Carbonalyser website](https://theshiftproject.org/en/carbonalyser-browser-extension/) - Carbonalyser is a browser extension published by NGO The Shift Project. It makes you more aware of the green house gas emissions you produce as a user and shows whch websites are most CO2-intensive.
