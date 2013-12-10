---   
name: 2013-11-27-sharing-and-extending-research-protocols
layout: post
title: sharing-and-extending-research-protocols
date: 2013-11-27
categories:
- research methods
---

- Last week I started a new discussion about sharing and extending research protocols.

#### My Colleague sent me a link to the [Prometheus Wiki](http://prometheuswiki.publish.csiro.au/tiki-custom_home.php)​
    a site for sharing research protocols. The idea is to give people
    a place to post research protocols since everyone develops them
    and then mentions them in papers but they rarely make it online in
    a usable format. We see this as a big bottleneck in the rate of
    knowledge discovery. Since users will always want to change and
    adapt a given protocol for changing applications or new technology
    or just to improve it. This sort of thing is done with open source
    all the time (i.e. git) but how you'd do it with an online
    protocol based out of a wiki is unknown. The current version of
    the website is not very flexible and doesn't really enable the
    sort of dynamic collaboration that I envision would make this a
    really useful tool. Git seems like an obvious conceptual starting
    point but there'd need to be a front end markup system in place
    that was integrated with that git-type backend. Since you've
    mentioned git a few times and the open science project, I thought
    you might find this interesting to think about. any suggestions or
    inspirations would be welcomed
<p></p>
#### My past experience

- I have previously tried to use a wiki for the development of new sections in an existing study protocol on estimating the effects of bushfire smoke air pollution and human health.
- We combined elements of two major air pollution/health study protocols (one from Europe, one from America) with local considerations and decisions made within our team.
- On reflection all this was mostly useful for me, to a lesser extent the other programmer and I don't think the project manager or statistician ever even looked at any of this.

#### Jeff Leek's current approach using GitHub

I have been keeping an eye on the work by Jeff Leek on putting protocols onto Github and inviting collaboration to edit and extend them [as he says](http://simplystatistics.org/2013/10/07/the-leek-group-policy-for-developing-sustainable-r-packages/):

    I put it on Github because I'm still not 100% sure I got it
    right... I would welcome feedback/pull requests on how we can
    improve the policy to make it better

<p></p>
#### Leek Group policies and protocols on github so far

- [https://github.com/jtleek/rpackages](https://github.com/jtleek/rpackages) accompanied by [this post](http://simplystatistics.org/2013/10/07/the-leek-group-policy-for-developing-sustainable-r-packages/)
- [https://github.com/jtleek/reviews](https://github.com/jtleek/reviews) accompanied by [this post](http://simplystatistics.org/2013/10/23/the-leek-group-guide-to-reviewing-scientific-papers/)
- [https://github.com/jtleek/datasharing](https://github.com/jtleek/datasharing) accompanied by [this post](http://simplystatistics.org/2013/11/14/the-leek-group-guide-to-sharing-data-with-a-statistician-to-speed-collaboration/)

#### I forked "datasharing" for my own. Renamed: "How to share data to avoid misunderstanding"

- I liked the datasharing policy so much [I forked it for my own collaborations](http://ivanhanigan.github.io/datasharing/).
- I initially just made a minor recommendation to one of the lines in the original using the great Github feature that if you edit a repo you don't have access to, it forks the repo and creates a feature branch behind the scenes. After you submit the changes (which is a commit) it puts you right into the pull request form.
- Therefore it can all be done on the GitHub site. I submitted [the pull request without leaving my web browser](https://github.com/jtleek/datasharing/pull/11).
- But then I thought I would have done things a bit differently.  In particular I'd like a webpage with a table of contents, and a nicer looking landing page.
- so I cloned my fork of the repo, then created a new branch called gh-pages, then copied the original to a new file called index.org, added some Emacs Orgmode HTML export magic and then "C-c C-e h" and WHAMM-O I've got my own version for extending with at [http://ivanhanigan.github.io/datasharing/](http://ivanhanigan.github.io/datasharing/).

#### The code version:
    git clone git@github.com:ivanhanigan/datasharing.git ~/tools/datasharing
    cd ~/tools/datasharing
    git checkout -b gh-pages
    mv README.md index.org
    touch README.md
    # edits to index.org, "C-c C-e h" and WHAMM-O
    git add index.org index.html README.md
    git push origin gh-pages

<p></p>

- In this way I think people can share and collaborate easily [(if they know git)](http://yihui.name/en/2013/06/fix-typo-in-documentation/)
- as well as easily take work started by someone else and extend it for their own work.
- I wonder a little bit about how much of my extensions I should offer back to Jeff Leek as the original author.
- I guess he can always track what I do to it via the link back to his original shown in [https://github.com/jtleek/datasharing/network](https://github.com/jtleek/datasharing/network)

#### PS Jeff Leek uses github a lot!
As he says in [this post from the future-of-statistics unconference](http://simplystatistics.org/2013/11/21/future-of-statistics-take-home-messages-futureofstats/):

    You can read it on Github here (https://github.com/jtleek/futureofstats).
    I put it on Github for two reasons:
     
    - I agree with Hadley's statement that the future of statistics is on Github.
    - I summarized them based on my interpretation and would love
      collaboration on the document. If you want to add your new
      thoughts/summaries, add a new section with your bullet pointed
      ideas and send me a pull request!
<p></p>
#### Conclusions

- Jeff Leek is on to something really interesting with these github policies and protocols
- I find the look of his plain markdown README.md pages a bit un-inspiring
- but then I spend too much of my time tweaking my html by far (while Jeff is getting on with the real work of publishing papers)
