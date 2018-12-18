# Installing Node.js and NPM on Windows Subsystem Linux
---

### UPDATE
<aside class="alert alert-danger" style="font-size: 14px">
After having installed everything in this article, WSL Ubuntu was running mad slow.  A quick google will show a bunch of people complaining about slow I/O problems with WSL. I have currently switched back to using Cygwin, which has been the best linux-style experience for me in windows for years.  I wanted to give WSL a chance, but it sucks to much...

 - Also, WSL uses the windows CMD style color chooser, which lets you choose the 16 basic linux colors, without letting you choose a seperate BG color and FG color separate from the 16 ansi colors. Cygwin lets you customize the colors using a config file ".minttyrc".

 - Also #2, WSL Ubuntu was getting VIM's colors wrong unless I used TMUX, which I am assuming forces xterm-16 or something.

 - Also #3, Tmux's border that it draws between panes was being dispaled as a bunch of squares (the rectangle character that shows up if a character isn't supported).

This was just way too many problems to deal with, that don't exist in Cygwin.
</aside>

### Original Post
Today I ran through quite a bit of trouble getting the most current versiosn of nodejs and npm installed in my Ubuntu 16 (on windows 10).

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
