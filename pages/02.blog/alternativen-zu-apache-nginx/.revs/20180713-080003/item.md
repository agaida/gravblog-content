---
title: 'Alternativen zu Apache: Nginx'
published: false
date: '18-06-2016 02:10'
taxonomy:
    category:
        - blog
    tag:
        - test
        - journal
external_links:
    process: true
    mode: active
twitterenable: false
twittercardoptions: summary
articleenabled: false
facebookenable: false
content:
    items: '@self.children'
    limit: '5'
    order:
        by: date
        dir: desc
    pagination: '1'
---

Every year I am reactive about the processing speed of my private websites. So again a few days ago. I admit that there are more potent webservers than my atom 510 with 4G, but as a desktop server the thing has its permission: The low cost at 24x7. Of course, one can remedy this: I could pack my blog, the wiki, the bug tracker on the big machine at Strato, but that's not what I want, because I feel it is very pleasant to have a server where I can try all the updates, next to the desk.

===

If this thing is going to tear up the hooves, then only a portion of my private pages will be unreachable. A condition that I feel is very reassuring. Upgrading the atom is difficult, which is fully expanded, an AMD e 450 would have its advantages but cost money. An energy-saving i3 ditto, that would be shot with cannons on sparrows. The only chance to change what is in the software used. Since I came with lighttpd not really good which, the plan matured to redeploy to nginx.

Said, done, a virtual machine set up and the first nginx put on. At least at this point, the Debian packages were useful. A few hours later, the first test pages were set up and reproducibly put into operation. The only sticking point was chili project. A short test with a standalone combi passenger and Nginx also came quite well and thus began the doom.

Unlike Apache, the modules for Nginx are not available separately, which are configured and compiled. "Of course" this also applies to all settings, paths etc. This doesn't even sound so tragic, but it will be on closer inspection:

* What if one of the most important modules for daily operation does not appear in any Debian package?
* If the module is called a passenger-for this there is a Debian package, which in the installation also pushes a new nginx-of course without the other modules that you have installed with the regular nginx.
* It is only logical that any configuration will be hacked mercilessly.

One possible solution is to uninstall the actually pre-configured Debian package, use it passenger package or simply abandon Debian packages without any if and however. This has its advantages and disadvantages.

Benefits:
* It works, if not, then the responsible idiot sits right in front of the screen
* One is independent of the sometimes somewhat disskussionwürdigen package maintenance in Debian in the area of web.

Disadvantages:
* You are working on the parcel system, you have to rely on local construction of the packages. Depending on personal can not necessarily be a dream state, rather one for nightmares
* Apt-Get dist-upgrade does not attack, I have to keep the stuff manually up to date. Compiling on an atom also doesn't really make fun
* You have to keep a build system on the server. Not really a nice condition. But that's about Ruby, you need that in doubt either way, since the required gems will not be available in the version you need in Debian repo.
* There is no package down, you can rebuild on any installation.

All in all, not a particularly satisfying condition, which I should actually solve by a separate package. Even nicer would be a separate package on this subject. However, since I have no plan how to implement the most cleverly it will remain at the Scriptanpassung, ideally would be the change directly in Debian.