---
layout: post
title:  "Use Bash aliases to speed up your work"
date:   2022-12-25 23:15:00 +0100
---

### Bash aliases?

Bash aliases allow you to run complex instructions to your terminal with a just a few keystrokes. For example, you can have 
an alias for some routine task which takes time to type and is tedious. 

`git add` -> `gad`

`git commit -m` -> `gct`

`git push` -> `gps`

This small example shows how three git commands
that often form part of your everyday workflow
can be executed much faster using aliases.

### How to set up bash aliases (Ubuntu)

The bash aliases can be set up within the bashrc file (`.bashrc`), but it's in my opinion
much more convenient to use a dedicated file `.bash_aliases`, where you define your aliases only.

#### 1. Check if your bashrc file contains an entry like this:
```
# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```
This piece of code checks for the existence of `.bash_aliases` file within the home directory
of current user and will make your aliases available to the terminal. 

To check the `bashrc` file within `vi` text editor, type these commands in your terminal:

`vi ~/.bashrc`

**Note**: if you don't feel comfortable viewing and editing `bashrc` file with vi, you can use the default Linux text editor,
gedit. In Ubuntu, go to the Applications menu, type `Text editor` or `gedit` and then look for the `.bashrc` in the `Home` 
directory of your user. This file can sometimes be hidden by default, so make sure you enable the display of hidden files. 

**Note 2**: I use `vi` to show how I edit files in the terminal, but `vim` is an equally valid option and the same commands can be used with it.

#### 2. Optional: Activate `bash_aliases` in bashrc

_Skip this step if you found an entry like in (1) within your bashrc file._

To add above snippet to your bashrc file with vi:
* with the keyboard arrow keys find a place in the document where you can paste the snippet
  * If you need to make some space, press `i` for insert mode. Exit insert mode using `Escape` key
* select the above snippet with your mouse
* with the middle mouse button paste the snippet
  * You can also use copy the snippet with ctr-C, mouse-right click in vi, select "Paste" option from context menu 
* Save the document using `:wq`
  * If you made a mistake, you can type ':wq!' and this will abort changes

Now it's time to reload the bashrc configuration. Go to the terminal (if you're not there already) and type:   

`source ~/.bashrc`

If you see no output, that's fine. Your changes were saved.

#### 3. Check if you have the .bash_aliases file

Now that the bashrc file is linked yo the `bash_aliases` file,  you can add 
aliases there and make available by reloading the `bashrc` just as we did in the end of step 2.

Check if you have the bash_aliases already in your home directory. Using the terminal:

`ls .bash*`

The output for me was

`.bash_aliases  .bash_history  .bash_logout  .bash_profile  .bashrc`

I already have the `.bash_aliases` file, great. 

##### 4. Create the `.bashrc` file 

_Skip this step if you found the `.bash_aliases` in your home directory_

Here are the steps in vi/vim:

`cd ~`
`touch .bash_aliases`

This will create an empty file that you can use in next step.

#### 5. Add your test alias

Let's add a fun alias - a mock response of the terminal whenever you type `hi`.

`cd ~`  
`vi .bash_aliases`


Now that you're with vi editor, press `i` for insert mode and write (or paste) this alias:

`alias hi='echo "Oh hello, sunshine! You look stunning today!!"'
`


#### Let's remember a few key points:
* There must be not blank spaces between `alias`, the equals sign, and the alias value.
* The alias value must be enclosed within quotes (single or double, your choice).
* The alias has to be saved and then the bashrc file reloaded. Only then will it be available in your temrinal. 


Save changes and activate alias:
* leave insert mode by pressing `Escape` key
* type `:wq`
* `source ~/.bashrc`

#### 6. Check if the test alias works

Now, whenever you type `hi` in the terminal, you will be greeted by:

`Oh hello, sunshine! You look stunning today!!`

So now we know how aliases work in general. To make new aliases, simply make a new line and add
a new alias.


##### 7. Bonous: Access and add aliases faster using... aliases :)

I have two aliases defined that help me quickly access the saved aliases and add new ones:

```
alias aldit='vim /home/list4c/.bash_aliases'
alias reload='source /home/list4c/.bashrc'
```

With these aliases my workflow goes like this:

```
aldit
(add new alias in new line using vim)
(Esc)
:wq
reload
```
This is quick enough for me, especially that the saved aliases save me
a lot of typing in the long run.  
Try having meta-aliases as above, I really like them. 

### Conclusions

Bash aliases can speed up your work immensely. I've been using them for:
* git commands
* running gradle commands
* running the React Native bundler with some flags
* running jekyll commands
* and more... 

Hope this post was beneficial for you in any way. If you have any questions, feel free to contact me.
