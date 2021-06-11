---
layout: post
title: Bare Minimum
---

This is a late post indeed. I am writing this post in the bare minimum setup which I had been trying to perfect.
There is indeed nothing that is perfect, but in my opinion, one can really settle down with certain things which
will just work out.

The one thing that this pandemic helped me with was sit down on this 6 year old system running Ubuntu 20.04 and
figure out the right configurations and the tools that I should be concentrating on in the near future. My choice
of tools have always been those which required more use of the keyboard and less use of the mouse. This has led
me to search for those programs which will allow me to survive in the terminal. Ofcourse there are those which
have now become so much embedded into the workflow that I will not be able to replace them, the web browser being
one of them. However, I am mostly referring to the tools that I use majority of the time, those can be something
that uses the least amount of system resources. So, here is the detailed thought process, listing of tools and
the configurations that I have as of now put into bare minimum.

#### state of the system
The state of the current system that I am using can be described with one word - SLOW! The processor is a low
power processor(i5 4210u) with a base frequency of 1.7GHz. Given the current set of processors out there in the
market, it is a slow processor. I had mainly bought this system for programming and had opted out of having a
discreet GFX option, I had a 3 year old system already before that with Nvidia GT-630M chip which gave me enough
issue with the Optimus Technology. The system also came with a 4GB RAM, which I had upgraded to 8GB, which is the
only nice thing about this system as of now, it responds fast enough as compared to systems of the same age.

#### Tools choice
Given the state of the system, I needed something that would be fast enough to respond to my touches and uses
less RAM. So, I would have to ditch GUI from the very start. I like to write code and while coding what one
does the most is edit text. Naturally my first choice would have to be the text editor that I use. I had been
using `vim` for quite some time, so that made it easier to stick to my choice of text editor.

I know that people are moving to `neovim` as of now, but I like `vim` just the way it is available. Of course,
I add my own set of plugins, but I am okay with `vim`. Apart from the text editor, the other tool that I was
using was `tmux` for multiplexing the windows while working on/with multiple programs. The new `tmux` version
available for Ubuntu 20.04 gave me a few issues since the earlier configuration did not just work out of the
box on this updated one. Here I had to make certain changes. The next set of tools that I was also already
using were `valgrind`, `gdb` and `irssi`. The only 2 more things that I would require were a web browser amd a
mail client. I replaced the mail client with `alpine`, easy enough to set up and good enough to send out mails. It
needs a little getting used to, but once you get the hang of it, becomes muscle memory again.

One other utility which I was looking for was a terminal based file explorer. I had used `ranger` before, but for
some reason, `ranger` was not fitting well with the workflow that I had. The keys were not consistent with my
workflow. I also came across `vifm`, `fff` and `nnn`, but none of them caught my eye for long. So, I went to look
for an old program, one which does the work for me and fits right into my workflow - `Midnight Commander`.
Double paned, it had the same controls as that of top/htop, copying and making directories also seemed like a breeze,
one can switch to the terminal, run a command and while running the command still switch back to `mc` and perform
other operations - something that piqued my interest.

Now the in the next set, the ricing that I had done in `vim`, `tmux` and the terminal emulator would have to go.

#### Ricing, terminal emulator and the switch to urxvt
