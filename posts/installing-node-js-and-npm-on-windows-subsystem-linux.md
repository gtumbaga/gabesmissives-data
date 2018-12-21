# Installing Node.js and NPM on Windows Subsystem Linux
---

### UPDATE
<aside class="alert alert-primary">
I found a program called [https://conemu.github.io/](conEmu) that acts as a front-end terminal that sits on top of what ever shells you want to use.  It let me use it as a front-end for WSL, giving me the ability to fix a few problems, like using my custom color theme, giving me tabs for multiple ubuntu windows, and TMUX's borders being drawn incorrectly.
 
 I am now currently using an XPS 13 as my main dev machine, and am currently very happy with the workflow of being able to use WSL Ubuntu, along with the extended functionality that ConEmu is providing me!
</aside>

### Original Post
Today I ran through quite a bit of trouble getting the most current versiosn of nodejs and npm installed in my Ubuntu 18 (on windows 10).

It turns out, the normal way of using apt-get to install it, installs a pretty old version.  The workaround, I found on a [github gist here](https://gist.github.com/micahgodbolt/8b9a338c8bab7bc147975646ea20826c).

```
$ touch ~/.bashrc
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
// restart bash
$ nvm install node
```
(note, for the 1st line to create a `.bashrc` file, mine already existed, so I skipped that line).

These are the lines that it adds into your .bashrc file:
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

(another note, on a ubuntu 18 machine, for some reason the lines that were inserted into the .bashrc file weren't working, so I copy/pasted them out of `.bashrc` into `.bash_profile` and things worked correctly from there.

It's a simple curl command that will download and run a bash script that will install NVM (Node Version Manager), and then you use NVM to install the latest and greatest node and npm.

Here is the actual github page for nvm itself, if you're curious:
[https://github.com/creationix/nvm/blob/master/README.md](https://github.com/creationix/nvm/blob/master/README.md)

As of writing this article, this worked for me, and I was able to proceed working on my angular project originally started on my Macbook Pro.
