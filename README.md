<h1> A Life Configuring Emacs </h1>

<p align="center"><img src="emacs-logo.png" width=150 height=150/></p>

<p align="center">
   <a href="<https://www.gnu.org/software/emacs/>">
	<img src="<https://img.shields.io/badge/GNU%20Emacs-26.1-b48ead.svg?style=plastic"/>></a>
   <a href="<https://orgmode.org/>"><img src="<https://img.shields.io/badge/org--mode-9.2.3-489a9f.svg?style=plastic"/>></a>
</p>

<h3> My Literate Setup </h3>

I enjoy reading others' *literate* configuration files and incorporating what I learn
into my own. The result is a sufficiently well-documented and accessible read that yields
a stylish and functional system (•̀ᴗ•́)و

This `README.md` has been automatically generated from my configuration
and its contents below could also be read in blog format, with *colour*, or as colourful PDF,
[here](https://alhassy.github.io/init/). Enjoy :smile:


# Table of Contents

1.  [Why Emacs?](#org0792756)
2.  [Booting Up](#org16d3567)
    1.  [`~/.emacs` vs. `init.org`](#org8100679)
    2.  [`use-package` &#x2013;The start of `init.el`](#org17e4339)
    3.  [`magit` &#x2013;Emacs' porcelain interface to git](#org2454226)
    4.  [Fix spelling as you type &#x2013;thesaurus & dictionary too!](#orgb380eb9)
    5.  [Using a Grammar & Style Checker](#org6fb7f1e)
    6.  [Unicode Input via Agda Input](#orgfec3bea)
    7.  [Locally `toggle` a variable](#org616f99c)
    8.  [Syncing to the System's `$PATH`](#orgd6ff30c)
    9.  [Keeping My System Up to Date](#orge459615)
    10. [Who am I? ─Using Gnus for Gmail](#org3064804)
    11. [Emacs keybindings for my brower](#org5729b97)
    12. [Using Emacs in any text area on my OS](#org50647ce)
3.  [Cosmetics](#org9846282)
    1.  [Themes](#org591d9a4)
    2.  [Startup message: Emacs & Org versions](#org0a8b872)
    3.  [Persistent Scratch Buffer](#orgfbfd3cd)
    4.  [Spaceline: A sleek mode line](#org1cedb22)
    5.  [Flashing when something goes wrong ─no blinking](#orgc5c373e)
    6.  [My to-do list: The initial buffer when Emacs opens up](#org4f64043)
    7.  [Showing date, time, and battery life](#org43f6e65)
    8.  [Hiding Scrollbar, tool bar, and menu](#org67e6b57)
    9.  [Increase/decrease text size](#org90a2894)
    10. [Delete Selection mode](#org54e8f4d)
    11. [Highlight & complete parenthesis pair when cursor is near ;-](#orgb2a72f3)
    12. [Minibuffer should display line and column numbers](#org6707e11)
    13. [Neotree: Directory Tree Listing](#org2b6dcae)
    14. [Window resizing using the golden ratio](#org1f6eeaf):Disabled:
4.  [Life within Org-mode](#org2b8adc2)
    1.  [High Speed Literate Programming](#orge3c039f)
    2.  [Using org-mode as a Day Planner](#org24091ac)
    3.  [Automating Pomodoro &#x2013;Dealing with dreadful tasks](#orgf715be6)
    4.  [Journaling](#orgf4d7519)
    5.  [Workflow States](#WorkflowStates)
    6.  [Show off-screen Heading at the top of the window](#org4be7077)
    7.  [Clocking Work Time](#org7190df8)
    8.  [Reveal.JS &#x2013; The HTML Presentation Framework](#orge0d531d)
    9.  [Coloured LaTeX using Minted](#orga487bbe)
    10. [Executing code from `src` blocks](#org02b92ef)
    11. [Hiding Emphasise Markers & Inlining Images](#org4db7ff7)
    12. [Jumping without hassle](#org8ab89a9)
    13. [Folding within a subtree](#org53c2e53)
    14. [Making then opening html's from org's](#org197f9d3)
    15. [Making then opening pdf's from org's](#org3d5d009)
    16. [Interpret the Haskell source blocks in a file](#org5f1bafd)
5.  [Summary of Utilities Provided](#org47aa639)

<p align="center">
	<a href="https://www.gnu.org/software/emacs/">
	<img src="https://img.shields.io/badge/GNU%20Emacs-26.1-b48ead.svg?style=plastic"/></a>
	<a href="https://orgmode.org/"><img src="https://img.shields.io/badge/org--mode-9.2.3-489a9f.svg?style=plastic"/></a>
</p>

<div class="org-center">
**Abstract**
</div>

Herein I document the configurations I utilise with [Emacs](https://gnu.org/s/emacs).

As a [literate program](https://www.offerzen.com/blog/literate-programming-empower-your-writing-with-emacs-org-mode) file with [Org-mode](http://orgmode.org/), I am ensured optimal navigation
through my ever growing configuration files, ease of usability and reference
for peers, and, most importantly, better maintainability for myself!

Dear reader, when encountering a foregin command `X` I encourage you to execute `(describe-symbol 'X)`, or press `C-h o` with the cursor on `X`.
An elementary Elisp Cheat Sheet can be found [here.](https://github.com/alhassy/ElispCheatSheet)


<a id="org0792756"></a>

# Why Emacs?

*Emacs is a flexible platform for developing end-user applications* &#x2013;unfortunately it is generally perceived as
merely a text editor. Some people use it specifically for one or two applications.

For example, [writers](https://www.youtube.com/watch?v=FtieBc3KptU) use it as an interface for Org-mode and others use it as an interface for version
control with Magit. [Org](https://orgmode.org/index.html#sec-4) is an organisation tool that can be used for typesetting which subsumes LaTeX, generating many different
formats &#x2013;html, latex, pdf, etc&#x2013; from a single source, keeping track of [schedules](https://orgmode.org/worg/org-tutorials/index.html#orgff7b885) & task management, blogging, habit tracking, personal information management tool, and [much more](http://orgmode.org/worg/org-contrib/).
Moreover, its syntax is so [natural](https://karl-voit.at/2017/09/23/orgmode-as-markup-only/) that most people use it without even knowing!
For me, Org allows me to do literate programming: I can program and document at the same time,
with no need to seperate the two tasks and with the ability to generate multiple formats and files from a single file.

> If you are a professional writer…Emacs outshines all other editing software
> in approximately the same way that the noonday sun does the stars.
> It is not just bigger and brighter; it simply makes everything else vanish.
> —[Neal Stephenson](http://project.cyberpunk.ru/lib/in_the_beginning_was_the_command_line/), *In the beginning was the command line*

Of course Emacs comes with the basic features of a text editor, but it is much more;
for example, it comes with a powerful notion of ‘undo’: Basic text editors have a single stream of undo,
yet in Emacs, we have a tree &#x2013;when we undo and make new edits, we branch off in our editing stream
as if our text was being version controlled as we type! &#x2013;We can even switch between such branches!

    ;; Allow tree-semantics for undo operations.
    (package-install 'undo-tree)
    (global-undo-tree-mode)
    (diminish 'undo-tree-mode)

    ;; Execute (undo-tree-visualize) then navigate along the tree to witness
    ;; changes being made to your file live!

    ;; Each node in the undo tree should have a timestamp.
    (setq undo-tree-visualizer-timestamps t)

    ;; Show a diff window displaying changes between undo nodes.
    (setq undo-tree-visualizer-diff t)

*Emacs is an extensible editor: You can make it into the editor of your dreams!*
You can make it suited to your personal needs.
If there's a feature you would like, a behaviour your desire, you can simply code that into Emacs with
a bit of Lisp. As a programming language enthusiast, for me Emacs is my default Lisp interpreter
and a customisable IDE that I use for other programming languages
&#x2013;such as C, Haskell, Agda, Racket, and Prolog.
Moreover, being a Lisp interpreter, we can alter the look and feel of Emacs live, without having
to restart it &#x2013;e.g., press `C-x C-e` after the final parenthesis of `(scroll-bar-mode 0)`
to run the code that removes the scroll-bar.

> *I use Emacs every day. I rarely notice it. But when I do, it usually brings me joy.*
> ─[Norman Walsh](https://so.nwalsh.com/2019/03/01/emacs)

I have used Emacs as an interface for developing cheat sheets, for making my blog, and as an application
for ‘interactively learning C’. If anything Emacs is more like an OS than just a text editor
&#x2013;“living within Emacs” provides an abstraction over whatever operating system my machine has:
[It's so easy to take everything with me.](https://www.fugue.co/blog/2015-11-11-guide-to-emacs.html) Moreover, the desire to mould Emacs to my needs has made me
a better programmer: I am now a more literate programmer and, due to Elisp's documentation-oriented nature, I actually take the time
and effort to make meaningful documentation &#x2013;even when the project is private and will likely only be seen by me.

> *Seeing Emacs as an editor is like seeing a car as a seating-accommodation.* &#x2013; [Karl Voit](https://karl-voit.at/2015/10/23/Emacs-is-not-just-an-editor/)

Some possibly interesting reads:

-   [How to Learn Emacs: A Hand-drawn One-pager for Beginners / A visual tutorial](https://sachachua.com/blog/wp-content/uploads/2013/05/How-to-Learn-Emacs-v2-Large.png)
-   [Emacs Mini-Manual, Part I of III](https://tuhdo.github.io/emacs-tutor.html)
-   [Org and R Programming](https://github.com/erikriverson/org-mode-R-tutorial/blob/master/org-mode-R-tutorial.org) &#x2014;a tutorial on literate programming, e.g., evaluating code within `src` bloc.
-   Reference cards for [GNU Emacs](https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf), [Org-mode](https://www.gnu.org/software/emacs/refcards/pdf/orgcard.pdf), and [Elisp](https://github.com/alhassy/ElispCheatSheet/blob/master/CheatSheet.pdf).
-   [“When did you start using Emacs” discussion on Reddit](https://www.reddit.com/r/emacs/comments/6fytr5/when_did_you_start_using_emacs/)
-   [“How to Learn Emacs”](https://david.rothlis.net/emacs/howtolearn.html)
-   [Video Series on Why Emacs Rocks](http://emacsrocks.com/)
-   [The Org-mode Reference Manual](https://orgmode.org/index.html#sec-4) or [Worg: Community-Written Docs](https://orgmode.org/worg/) which includes a [meta-tutorial](https://orgmode.org/worg/org-tutorials/index.html).
-   [Awesome Emacs](https://github.com/emacs-tw/awesome-emacs): A community driven list of useful Emacs packages, libraries and others.
-   [A list of people's nice emacs config files](https://github.com/caisah/emacs.dz)

Remember: Emacs is a flexible platform for developing end-user applications; e.g., this configuration file
is at its core an Emacs Lisp program that yields the editor of my dreams
&#x2013;it encourages me to grow and to be creative, and I hope the same for all who use it;
moreover, it reflects my personality such as what I value and what I neglect in my workflow.

Finally, as will be shown below, you can literrally use [Emacs anywhere](https://github.com/zachcurry/emacs-anywhere/#usage)
for textually input in your operating system &#x2013;no copy-paste required.


<a id="org16d3567"></a>

# Booting Up


<a id="org8100679"></a>

## `~/.emacs` vs. `init.org`

Why not keep Emac's configurations in the `~/.emacs` file?
This is because the Emacs system may explicitly add, or alter, code
in it.

For example, execute the following

1.  `M-x customize-variable RET line-number-mode RET`
2.  Then press: `toggle`, `state`, then `1`.
3.  Now take a look: `(find-file "~/.emacs")`

Notice how additions to the file have been created by \`custom'.

As such, I've chosen to write my Emacs' initialisation configurations
in a file named `~/.emacs.d/init.org`: I have a literate configuration which
is then loaded using org-mode's tangling feature.
Read more about Emacs' initialisation configurations [here.](http://www.gnu.org/software/emacs/manual/html_node/emacs/Init-File.html#Init-File)

Off topic, I love tiling window managers and had been using [xmonad](https://xmonad.org)
until recently when I obtained a mac machine and now use
[Amethyst](https://ianyh.com/amethyst/) &#x2013; “Tiling window manager for macOS along the lines of xmonad.”

Let the Emacs' gui insert default configurations and customisation
into its own file, not touching or altering my initialisation file.
For example, I tend to have local variables to produce `README.md`'s
and other matters, so Emacs' Custom utility will remember to not prompt
me each time for the safety of such local variables.

    ;; (eshell-command "touch ~/.emacs.d/custom.el")

    (setq custom-file "~/.emacs.d/custom.el")
    (load custom-file)

Rather than manually extracting the Lisp code from this literate document
each time we alter it, let's instead add a ‘hook’ ─a method  that is invoked
on a particular event, in this case when we save the file.

    (defun my/make-init-el-and-README ()
      (interactive)
      ;; Make init.el
      (org-babel-tangle)
      (byte-compile-file "~/.emacs.d/init.el")
      (load-file "~/.emacs.d/init.el")

      ;; Make README.md
      ;; (org-babel-goto-named-src-block "make-readme")
      ;; (org-babel-execute-src-block)

      (message "Tangled, compiled, and loaded init.el; and made README.md")
    )

    (add-hook 'after-save-hook 'my/make-init-el nil 'local-to-this-file-please)

Where the following block has `#+NAME: make-readme` before it.
This source block generates the `README` for the associated github repository.

    (with-temp-buffer
	(insert
	"#+EXPORT_FILE_NAME: README.md
	 #+HTML: <h1> A Life Configuring Emacs </h1>

	 <p align=\"center\"><img src=\"emacs-logo.png\" width=150 height=150/></p>

	 <p align=\"center\">
	<a href=\"https://www.gnu.org/software/emacs/\">
	     <img src=\"https://img.shields.io/badge/GNU%20Emacs-26.1-b48ead.svg?style=plastic\"/></a>
	<a href=\"https://orgmode.org/\"><img src=\"https://img.shields.io/badge/org--mode-9.2.3-489a9f.svg?style=plastic\"/></a>
	 </p>

	 #+HTML: <h3> My Literate Setup </h3>
	 #+OPTIONS: toc:nil d:nil
	 # Toc is displayed below at a strategic position.

	 I enjoy reading others' /literate/ configuration files and incorporating what I learn
	 into my own. The result is a sufficiently well-documented and accessible read that yields
	 a stylish and functional system (•̀ᴗ•́)و

	 This ~README.md~ has been automatically generated from my configuration
	 and its contents below could also be read in blog format, with /colour/, or as colourful PDF,
	 [[https://alhassy.github.io/init/][here]]. Enjoy :smile:

	  #+TOC: headlines 2
	  #+INCLUDE: init.org
	")
	(org-mode)
	(org-md-export-to-markdown)
	;; Coloured html does not work in Github, afaik.
	;; (org-html-export-to-html)
	;; (shell-command "mv README.html README.md")
    )


<a id="org17e4339"></a>

## `use-package` &#x2013;The start of `init.el`

There are a few ways to install packages
&#x2013;run `C-h C-e` for a short overview.
The easiest, for a beginner, is to use the command `package-list-packages`
then find the desired package, press `i` to mark it for installation, then
install all marked packages by pressing `x`.

Alternatively, one uses the declarative configuration tool [use-package](https://github.com/jwiegley/use-package/)
&#x2013;a meta-package that manages other packages and the way they interact.

Background:
Recently I switched to mac &#x2013;first time trying the OS.
I had to do a few `package-install`'s and it was annoying.
I'm looking for the best way to package my Emacs installation
&#x2013;inlcuding my installed pacakages and configuration&#x2013;
so that I can quickly install it anywhere, say if I go to another machine.
It seems `use-package` allows me to configure and auto install packages.
On a new machine, when I clone my `.emacs.d` and start emacs,
on the first start it should automatically install and compile
all of my packages through `use-package` when it detects they're missing.

First we need the basic `package` module which not only allows us to obtain `use-package` but
acts as its kernel.

    ;; Make all commands of the “package” module present.
    (require 'package)

    ;; Speef up start up by not loading any packages at startup.
    ;; (setq package-enable-at-startup nil)
    ;; Look at the *Messages* buffer before setting this to nil, then after.

    ;; Internet repositories for new packages.
    (setq package-archives '(("org"       . "https://orgmode.org/elpa/")
			 ("gnu"       . "https://elpa.gnu.org/packages/")
			 ("melpa"     . "https://melpa.org/packages/")
			 ("melpa-stable" . "https://stable.melpa.org/packages/")
			 ;; Maintainer is AWOL.
			 ;; ("marmalade" . "https://marmalade-repo.org/packages/")
			 ))

    ;; Actually get “package” to work.
    (package-initialize)

We can now:

-   `M-x list-packages` to see all melpa packages that can install
    -   Not in alphabetical order, so maybe search with `C-s`.
-   For example to download the haskell mode: `M-x package-install RET haskell-mode RET`.
    -   Or maybe to install `unicode-fonts` ;-)
-   Read more at <http://ergoemacs.org/emacs/emacs_package_system.html> or
    at <https://github.com/milkypostman/melpa>

We now bootstrap `use-package`,

    ;; Unless it's already installed, update the packages archives,
    ;; then install the most recent version of “use-package”.
    (unless (package-installed-p 'use-package)
      (package-refresh-contents)
      (package-install 'use-package))

    (require 'use-package)

We can now invoke `(use-package XYZ :ensure t)`
which should check for the `XYZ` package and make sure it is accessible.
If not, the `:ensure t` part tells `use-package` to download it
&#x2013;using `package.el`&#x2013;
and place it somewhere accessible, in `~/.emacs.d/elpa/` by default.

By default we would like to download packages, since I do not plan on installing them manually
by download `.el` files and placing them in the correct places on my system.

    (setq use-package-always-ensure t)

Here's an example use of `use-package`.
Below I have my “show recent files pop-up” command set to `C-x C-r`;
but what if I forget? This mode shows me all key completions when I type `C-x`, for example.
Moreover, I will be shown other commands I did not know about! Neato :-)

    ;; Making it easier to discover Emacs key presses.
    (use-package which-key
     :diminish which-key-mode
     :init (which-key-mode)
     :config (which-key-setup-side-window-bottom)
	 (setq which-key-idle-delay 0.05)
    )

The `:diminish` keyword indicates that we do not want the mode's name to be
shown to us in the modeline &#x2013;the area near the bottom of Emacs.
It does so by using the `diminish` package, so let's install that.

    (use-package diminish)

Here are other packages that I want to be installed onto my machine.

    ;; Efficient version control.
    (use-package magit
      :config (global-set-key (kbd "C-x g") 'magit-status)
    )

    (use-package htmlize)
    ;; Main use: Org produced htmls are coloured.
    ;; Can be used to export a file into a coloured html.

    (use-package biblio)     ;; Quick BibTeX references, sometimes.

    ;; Get org-headers to look pretty! E.g., * → ⊙, ** ↦ ◯, *** ↦ ★
    ;; https://github.com/emacsorphanage/org-bullets
    (use-package org-bullets)
    (add-hook 'org-mode-hook 'org-bullets-mode)

    (use-package haskell-mode)

    (use-package dash)    ;; “A modern list library for Emacs”
    (use-package s   )    ;; “The long lost Emacs string manipulation library”.

Note:

-   [dash](https://github.com/magnars/dash.el): “A modern list library for Emacs”
    -   E.g., `(--filter (> it 10) (list 8 9 10 11 12))`
-   [s](https://github.com/magnars/s.el): “The long lost Emacs string manipulation library”.
    -   E.g., `s-trim, s-replace, s-join`.

Finally, since I've symlinked my `.emacs`:

    ;; Don't ask for confirmation when opening symlinked files.
    (setq vc-follow-symlinks t)


<a id="org2454226"></a>

## `magit` &#x2013;Emacs' porcelain interface to git

Why use `magit` as the interface to the git version control system?
In a magit buffer nearly everything can be acted upon:
Press `return,` or `space`, to see details and `tab` to see children items, usually.

Below is my personal quick guide to working with magit.
A quick magit tutorial can be found on [jr0cket's blog](http://jr0cket.co.uk/2012/12/driving-git-with-emacs-pure-magic-with.html.html)

-   **`magit-init`:** Put a project under version control.
    The mini-buffer will prompt you for the top level folder version.
    A `.git` folder will be created there.

-   **`magit-status` , `C-x g`:** See status in another buffer. Press `?` to see options,
    including:

    -   **`q`:** Quit magit, or go to previous magit screen.
    -   **`s`:** Stage, i.e., add, a file to version control.
	Add all untracked files by selecting the *Untracked files* title.
    -   **`k`:** Kill, i.e., delete a file locally.
    -   **`K`:** This' `(magit-file-untrack)` which does `git rm --cached`.
    -   **`i`:** Add a file to the project `.gitignore` file. Nice stuff =)
    -   **`u`:** Unstage a specfif staged change highlighed by cursor.
	`C-u s` stages everything &#x2013;tracked or not.
    -   **`c`:** Commit a change.
	-   A new buffer for the commit message appears, you write it then
	    commit with `C-c C-c` or otherwise cancel with `C-c C-k`.
	    These commands are mentioned to you in the minibuffer when you go to commit.
	-   You can provide a commit to *each* altered chunk of text!
	    This is super neat, you make a series of local such commits rather
	    than one nebulous global commit for the file. The `magit` interface
	    makes this far more accessible than a standard terminal approach!
	-   You can look at the unstaged changes, select a *region*, using `C-SPC` as usual,
	    and commit only that if you want!
	-   When looking over a commit, `M-p/n` to efficiently go to previous or next altered sections.
	-   Amend a commit by pressing `a` on `HEAD`.

    -   **`d`:** Show differences, another `d` or another option.
	-   This is magit! Each hunk can be acted upon; e.g., `s` or `c` or `k` ;-)
	-   [The staging area is akin to a pet store; commiting is taking the pet home.](https://softwareengineering.stackexchange.com/a/119807/185815)
    -   **`v`:** Revert a commit.
    -   **`x`:** Undo last commit. Tantamount to `git reset HEAD~` when cursor is on most recent
	commit; otherwise resets to whatever commit is under the cursor.
    -   **`l`:** Show the log, another `l` for current branch; other options will be displayed.
	-   Here `space` shows details in another buffer while cursour remains in current
	    buffer and, moreover, continuing to press `space` scrolls through the other buffer!
	    Neato.
    -   **`P`:** Push.
    -   **`F`:** Pull.
    -   **`:`:** Execute a raw git command; e.g., enter `whatchanged`.

    The status buffer may be refereshed using `g`, and all magit buffer by `G`.

    Press `tab` to see collapsed items, such as what text has been changed.

Notice that every time you press one of these commands, a ‘pop-up’ of realted git options
appears! Thus not only is there no need to memorize many of them, but this approach makes
discovering other commands easier.

Use `M-x (magit-list-repositories) RET` to list local repositories:

Below are the git repos I'd like to clone.

    ;; Do not ask about this variable when cloning.
    (setq magit-clone-set-remote.pushDefault t)

    (cl-defun maybe-clone (remote &optional (local (concat "~/" (file-name-base remote))))
      "Clone a ‘remote’ repository if the ‘local’ directory does not exist.
	Yields ‘nil’ when no cloning transpires, otherwise yields “cloned-repo”.

	‘local’ is optional and defaults to the base name; e.g.,
	if ‘remote’is ‘https://github.com/X/Y’ then ‘local’ becomes ‘~/Y’.
      "
      (unless (file-directory-p local)
	 (magit-clone remote local)
	 (add-to-list 'magit-repository-directories `(,local   . 0))
	 'cloned-repo)
    )

    ;; Set variable without asking.
    (setq magit-clone-set-remote.pushDefault 't)

    ;; Public repos
    (maybe-clone "https://github.com/alhassy/emacs.d")
    (maybe-clone "https://github.com/alhassy/alhassy.github.io")
    (maybe-clone "https://github.com/alhassy/ElispCheatSheet")
    (maybe-clone "https://github.com/alhassy/org-agda-mode")
    (maybe-clone "https://github.com/JacquesCarette/TheoriesAndDataStructures")
    (maybe-clone "https://github.com/alhassy/islam")

Let's always notify ourselves of a file that has [uncommited changes](https://tpapp.github.io/post/check-uncommitted/)
&#x2013;we might have had to step away from the computer and forgotten to commit.

    (require 'magit-git)

    (defun my/magit-check-file-and-popup ()
      "If the file is version controlled with git
      and has uncommitted changes, open the magit status popup."
      (let ((file (buffer-file-name)))
	(when (and file (magit-anything-modified-p t file))
	  (message "This file has uncommited changes!")
	  (when nil ;; Became annyoying after some time.
	  (split-window-below)
	  (other-window 1)
	  (magit-status)))))

    ;; I usually have local variables, so I want the message to show
    ;; after the locals have been loaded.
    (add-hook 'find-file-hook
      '(lambda ()
	  (add-hook 'hack-local-variables-hook 'my/magit-check-file-and-popup)
       ))

Let's try this out:

    (progn (eshell-command "echo change-here >> ~/dotfiles/.emacs")
	   (find-file "~/dotfiles/.emacs")
    )

In doubt, execute `C-h e` to jump to the `*Messages*` buffer.


<a id="orgb380eb9"></a>

## Fix spelling as you type &#x2013;thesaurus & dictionary too!

I would like to check spelling by default.

-   **`C-;`:** Cycle through corrections for word at point.
-   **`M-$`:** Check and correct spelling of the word at point
-   **`M-x ispell-change-dictionary RET TAB`:** To see what dictionaries are available.

    (use-package flyspell
      :hook (
	   (prog-mode . flyspell-prog-mode)
	   (text-mode . flyspell-mode))
    )

Flyspell needs a spell checking tool, which is not included in Emacs.
We install `aspell` spell checker using, say, homebrew via `brew install aspell`.
Note that Emacs' `ispell` is the interface to such a command line spelling utility.

    (setq ispell-program-name "/usr/local/bin/aspell")
    (setq ispell-dictionary "en_GB") ;; set the default dictionary

    (diminish 'flyspell-mode) ;; Don't show it in the modeline.

Ecnabling fly-spell for text-mode enables it for org and latex modes since they
derive from text-mode.

Let us select a correct spelling merely by clicking on a word.

    (eval-after-load "flyspell"
      ' (progn
	 (define-key flyspell-mouse-map [down-mouse-3] #'flyspell-correct-word)
	 (define-key flyspell-mouse-map [mouse-3] #'undefined)))

Colour incorrect works; default is an underline.

    (global-font-lock-mode t)
    (custom-set-faces '(flyspell-incorrect ((t (:inverse-video t)))))

Finally, save to user dictionary without asking:

    (setq ispell-silently-savep t)

Let's keep track of my personal word set by having it be in my version controlled
.emacs directory. [Note](http://aspell.net/man-html/Format-of-the-Personal-and-Replacement-Dictionaries.html) that the default location is `~/.[i|a]spell.DICT` for
a specified dictionary `DICT`.

    (setq ispell-personal-dictionary "~/.emacs.d/.aspell.en.pws")

Nowadays, I very rarely write non-literate programs, but if I do
I'd like to check spelling only in comments/strings. E.g.,

    (add-hook          'c-mode-hook 'flyspell-prog-mode)
    (add-hook 'emacs-lisp-mode-hook 'flyspell-prog-mode)

Use the thesaurus Emacs frontend [Synosaurus](https://github.com/hpdeifel/synosaurus) to avoid unwarranted repetition.

    (use-package synosaurus
      :diminish synosaurus-mode
      :init    (synosaurus-mode)
      :config  (setq synosaurus-choose-method 'popup) ;; 'ido is default.
	   (global-set-key (kbd "M-#") 'synosaurus-choose-and-replace)
    )

The thesaurus is powered by the Wordnet `wn` tool, which can be invoked without an internet connection!

    ;; (shell-command "brew cask install xquartz &") ;; Dependency
    ;; (shell-command "brew install wordnet &")

Let's use Wordnet as a dictionary via the [wordnut](https://github.com/gromnitsky/wordnut) package.

    (use-package wordnut
     :bind ("M-!" . wordnut-lookup-current-word))

    ;; Use M-& for async shell commands.

Use `M-↑,↓` to navigate dictionary results, and `wordnut-search` for a new search.

Use this game to help you learn to spell words that you're having trouble with;
see `~/Dropbox/spelling.txt`.

    (autoload 'typing-of-emacs "~/.emacs.d/typing.el" "The Typing Of Emacs, a game." t)

Practice touch typing using [speed-type](https://github.com/hagleitn/speed-type).

    (use-package speed-type)

Running `M-x speed-type-region` on a region of text, or `M-x speed-type-buffer` on a
whole buffer, or just `M-x speed-type-text` will produce the selected region, buffer,
or random text for practice. The timer begins when the first key is pressed
and stats are shown when the last letter is entered.

Other typing resources include:

-   [Typing of Emacs](https://www.emacswiki.org/emacs/TypingOfEmacs) &#x2013;an Emacs alternative to speed type, possibly more engaging.
-   [Klavaro](https://alternativeto.net/software/klavaro/) &#x2013;a GUI based yet language-independent typing tutor.
    -   I'm enjoying this tool in getting started with Arabic typing.
    -   The plan is to move to using the online [Making Hijrah](https://makinghijrah.com/arabic-typing/) tutor which
	concludes the basic lesson plan with a few short narrations.
-   [Typing.io](https://typing.io/) is a tutor for coders: Lessons are based on open source code, such
    some XMonad written in Haskell or Linux written in  C.
-   [GNU Typist](https://www.gnu.org/software/gtypist/index.html#downloading) &#x2013;which is interactive in the terminal, so not ideal in Emacs&#x2013;,

To assist in language learning, it may be nice to have an Emacs
[interface](https://github.com/atykhonov/google-translate) to Google translate &#x2014;e.g., invoke `google-translate-at-point`.

    (use-package google-translate
     :config
       (global-set-key "\C-ct" 'google-translate-at-point)
    )

Select the following then `C-c t`,

> Hey buddy, what're you up to?

Then *detect language* then *Arabic* to obtain:

> مرحباً يا صديقي ، ماذا تفعل؟

Neato 😲


<a id="org6fb7f1e"></a>

## Using a Grammar & Style Checker

Let's install [a grammar and style checker](https://github.com/mhayashi1120/Emacs-langtool).
We get the offline tool from the bottom of the [LanguageTool](https://languagetool.org/) website, then relocate it
as follows.

    (use-package langtool
     :config
      (setq langtool-language-tool-jar
	 "~/Applications/LanguageTool-4.5/languagetool-commandline.jar")
    )

Now we can run `langtool-check` on the subsequent grammatically incorrect
text &#x2013;which is from the LanguageTool website&#x2013; which colours errors in red,
when we click on them we get the reason why; then we may invoke
`langtool-correct-buffer` to quickly use the suggestions to fix each correction,
and finally invoke `langtool-check-done` to stop any remaining red colouring.

    LanguageTool offers spell and grammar checking. Just paste your text here
    and click the 'Check Text' button. Click the colored phrases for details
    on potential errors. or use this text too see an few of of the problems
    that LanguageTool can detecd. What do you thinks of grammar checkers?
    Please not that they are not perfect. Style issues get a blue marker:
    It's 5 P.M. in the afternoon. The weather was nice on Thursday, 27 June 2017
    --uh oh, that's the wrong date ;-)

By looking around the source code, I can do all three stages smoothly (•̀ᴗ•́)و

    ;; Quickly check, correct, then clean up /region/ with M-^

    (add-hook 'langtool-error-exists-hook
      (lambda ()
	(langtool-correct-buffer)
	(langtool-check-done)
      ))

    (global-set-key "\M-^" 'langtool-check)


<a id="orgfec3bea"></a>

## Unicode Input via Agda Input

[Agda](https://mazzo.li/posts/AgdaSort.html) is one of my favourite languages, it's like Haskell on steroids.
Let's set it up.

Executing `agda-mode setup` appends the following text to the `.emacs` file.
Let's put it here ourselves.

    (load-file (let ((coding-system-for-read 'utf-8))
		(shell-command-to-string "/usr/local/bin/agda-mode locate")))

I almost always want the `agda-mode` input method.

    (require 'agda-input)
    (add-hook 'text-mode-hook (lambda () (set-input-method "Agda")))
    (add-hook 'org-mode-hook (lambda () (set-input-method "Agda")))

Below are my personal Agda input symbol translations;
e.g., `\set → 𝒮ℯ𝓉`. Note that we could give a symbol new Agda TeX binding
interactively: `M-x customize-variable agda-input-user-translations` then
`INS` then for key sequence type `set` then `INS` and for string paste `𝒮ℯ𝓉`.

    ;; category theory
    (add-to-list 'agda-input-user-translations '("set" "𝒮ℯ𝓉"))
    (add-to-list 'agda-input-user-translations '("alg" "𝒜𝓁ℊ"))
    (add-to-list 'agda-input-user-translations '("split" "▵"))
    (add-to-list 'agda-input-user-translations '("join" "▿"))
    (add-to-list 'agda-input-user-translations '("adj" "⊣"))
    (add-to-list 'agda-input-user-translations '(";;" "﹔"))
    (add-to-list 'agda-input-user-translations '(";;" "⨾"))
    (add-to-list 'agda-input-user-translations '(";;" "∘"))

    ;; lattices
    (add-to-list 'agda-input-user-translations '("meet" "⊓"))
    (add-to-list 'agda-input-user-translations '("join" "⊔"))

    ;; residuals
    (add-to-list 'agda-input-user-translations '("syq"  "╳"))
    (add-to-list 'agda-input-user-translations '("over" "╱"))
    (add-to-list 'agda-input-user-translations '("under" "╲"))
	;; Maybe “\\” shortcut?

    ;; Z-quantification range notation, e.g., “∀ x ❙ R • P”
    (add-to-list 'agda-input-user-translations '("|" "❙"))
    (add-to-list 'agda-input-user-translations '("with" "❙"))

    ;; adjunction isomorphism pair
    (add-to-list 'agda-input-user-translations '("floor"  "⌊⌋"))
    (add-to-list 'agda-input-user-translations '("lower"  "⌊⌋"))
    (add-to-list 'agda-input-user-translations '("lad"    "⌊⌋"))
    (add-to-list 'agda-input-user-translations '("ceil"   "⌈⌉"))
    (add-to-list 'agda-input-user-translations '("raise"  "⌈⌉"))
    (add-to-list 'agda-input-user-translations '("rad"    "⌈⌉"))

    ;; silly stuff
    ;;
    ;; angry, cry, why-you-no
    (add-to-list 'agda-input-user-translations
       '("whyme" "ლ(ಠ益ಠ)ლ" "ヽ༼ಢ_ಢ༽ﾉ☂" "щ(゜ロ゜щ)"))
    ;; confused, disapprove, dead, shrug
    (add-to-list 'agda-input-user-translations
       '("what" "「(°ヘ°)" "(ಠ_ಠ)" "(✖╭╮✖)" "¯\\_(ツ)_/¯"))
    ;; dance, csi
    (add-to-list 'agda-input-user-translations
       '("cool" "┏(-_-)┓┏(-_-)┛┗(-_-﻿ )┓" "•_•)
    ( •_•)>⌐■-■
    (⌐■_■)
    "))
    ;; love, pleased, success, yesss
    (add-to-list 'agda-input-user-translations
       '("smile" "♥‿♥" "(─‿‿─)" "(•̀ᴗ•́)و" "(งಠ_ಠ)ง"))

Finally let's effect such translations.

    ;; activate translations
    (agda-input-setup)

Note that the effect of [Emacs unicode input](http://ergoemacs.org/emacs/emacs_n_unicode.html) could be approximated using
`abbrev-mode`.


<a id="org616f99c"></a>

## Locally `toggle` a variable

It is dangerous to load a file with local variables;
instead we should load files without evaluating locals,
read the locals to ensure they are safe &#x2013;e.g., there's nothing
malicious like `eval: (delete-file your-important-file.txt)`&#x2013;
then revert the buffer to load the locals.

However, when preprocessing my own files I sometimes wish
to accept all locals without being queried and so have the following
combinator.

    (defmacro toggle (variable value &rest code)
      "Locally set the value of ‘variable’ to be ‘value’ in the scope of ‘code’.
       In particular, the value of ‘variable’, if any, *is* affected
       to produce useful sideffects. It retains its orginal value outside this call.

       This is a feature of Lisp's dynamic scope.
       Essentilly this macro behaves like a let-statement with one item;
       rather than use, say “-let”, I've used a possibly more informative name.

       Example uses include terse replacements for one-off let-statements,
       or, more likely, of temporarily toggeling important values, such as
       ‘kill-buffer-query-functions’ for killing a process buffer without confirmation.

       Another example: ‘(toggle enable-local-variables :all ⋯)’ to preprocess files
       without being queried about possibly dangerous local variables.
      "
      `(let ((,variable ,value))
	,@code
      )
    )

Since emacs-lisp interprets definitions sequentially, I define `toggle` here
since I employ it in the next section.


<a id="orgd6ff30c"></a>

## Syncing to the System's `$PATH`

For one reason or another, on OS X it seems that an Emacs instance
begun from the terminal may not inherit the terminal's environment
variables, thus making it difficult to use utilities like `pdflatex`
when Org-mode attempts to produce a PDF.

    (use-package exec-path-from-shell
      :init
	(when (memq window-system '(mac ns x))
	 (exec-path-from-shell-initialize))
    )

See these [docs](https://github.com/purcell/exec-path-from-shell) for setting other environment variables.


<a id="orge459615"></a>

## Keeping My System Up to Date

    (defun my/stay-up-to-date ()

      "Ensure that OS and Emacs pacakges are up to date.

       Takes ~5 secons when everything is up to date.
      "

      (async-shell-command "brew update && brew upgrade")
      (other-window 1)
      (rename-buffer "Keeping-system-up-to-date")

      (package-refresh-contents)
      (insert "Emacs packages have been updated.")

      (other-window 1)
    )

    (add-hook 'after-init-hook 'my/stay-up-to-date)


<a id="org3064804"></a>

## Who am I? ─Using Gnus for Gmail

Let's set the following personal
Emacs-wide variables ─to be used in other locations besides email.

    (setq user-full-name    "Musa Al-hassy"
	  user-mail-address "alhassy@gmail.com")

By default, in Emacs, we may send mail: Write it in Emacs with `C-x m`,
then press `C-c C-c` to have it sent via your OS's default mailing system
&#x2013;mine appears to be Gmail via the browser. Or cancel sending mail with
`C-c C-k` &#x2013;the same commands for capturing, discussed below (•̀ᴗ•́)و

To send and read email in Emacs we use
[GNUS](https://en.wikipedia.org/wiki/Gnus) &#x2013;which, like many GNU itself, it a recursive acronym:
GNUS Network User Service.

1.  Execute, rather place in your init:

	(setq message-send-mail-function 'smtpmail-send-it)

    Revert to the default OS mailing method by setting this variable to
    `mailclient-send-it`.

2.  Follow only the [quickstart here](https://www.emacswiki.org/emacs/GnusGmail#toc1); namely, make a file named `~/.gnus` containing:

	     ;; user-full-name and user-mail-address should be defined

	(setq gnus-select-method
	      '(nnimap "gmail"
		       (nnimap-address "imap.gmail.com")
		       (nnimap-server-port "imaps")
		       (nnimap-stream ssl)))

	(setq smtpmail-smtp-server "smtp.gmail.com"
	      smtpmail-smtp-service 587
	      gnus-ignored-newsgroups "^to\\.\\|^[0-9. ]+\\( \\|$\\)\\|^[\"]\"[#'()]")

3.  Enable “2 step authentication” for Gmail following [these](https://emacs.stackexchange.com/a/33309/10352) instructions.

4.  You will then obtain a secret password, the `x` marks below, which you insert in a file
    named `~/.authinfo` as follows &#x2013;using your email address.

	machine imap.gmail.com login alhassy@gmail.com password xxxxxxxxxxxxxxxx port imaps
	machine smtp.gmail.com login alhassy@gmail.com password xxxxxxxxxxxxxxxx port 587

5.  In Emacs, `M-x gnus` to see what's there.

    Or compose mail with `C-x m` then send it with `C-c C-c`.

    -   Press `C-h m` to learn more about message mode for mail composition;
	or read [the Message Manual](https://www.gnus.org/manual/message.pdf).

In gnus, by default items you've looked at disappear &#x2013;i.e., are archived.
They can still be viewed in, say, the online browser if you like.
In the `Group` view, `R` resets gnus, possibly retriving mail or alterations
from other mail clients. `q` exits gnus in `Group` mode, `q` exits the particular
view to go back to summary mode. Only after pressing `q` from within a group
do changes take effect on articles &#x2013;such as moves, reads, deletes, etc.

-   **RET:** Open an article.

-   **B m:** Move an article, in its current state, to another group
    &#x2013;i.e., ‘label’ using Gmail parlance.

    Something to consider doing when finished with an article.

    To delete an article, simply move it to ‘trash’ &#x2013;of course this will delete it
    in other mail clients as well. There is no return from trash.

    Emails can always be achieved &#x2013;never delete, maybe?

-   **!:** mark an article as read, but to be kept around
    &#x2013;e.g., you have not replied to it, or it requires more reading at a later time.

-   **R:** Reply to email with sender's content there in place.
    -   `r` to reply to an email with sender's content in adjacent buffer.

-   **d:** mark an article as done, i.e., read it and it can be archived.

Learn more by reading [The Gnus Manual](https://www.gnus.org/manual.html); also available within Emacs by `C-h i m gnus` (•̀ᴗ•́)و

-   Or look at the [Gnus Reference Card](https://www.gnu.org/software/emacs/refcards/pdf/gnus-refcard.pdf).
-   Or, less comprehensively, this [outline](https://github.com/redguardtoo/mastering-emacs-in-one-year-guide/blob/master/gnus-guide-en.org#subscribe-groups).


<a id="org5729b97"></a>

## Emacs keybindings for my brower

I've downloaded the [Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb/related) extension for Google Chrome,
and have copy-pasted [these](https://gist.github.com/dmgerman/6f0e5f9ffc6484dfaf53) Emacs key bindings into it.
Now `C-h` in my browser shows which Emacs-like bindings
can be used to navigate my browser ^\_^


<a id="org50647ce"></a>

## Using Emacs in any text area on my OS

Using the [Emacs-Anywhere](https://github.com/zachcurry/emacs-anywhere/#usage) tool, I can press `Cmd Shift e` to have an Emacs frame
appear, produce text with Emacs editing capabilities, then `C-x 5 0` to have the
resulting text dumped into the text area I was working in.

This way I can use Emacs literally anywhere for textual input!

For my Mac OSX:

    (shell-command "curl -fsSL https://raw.github.com/zachcurry/emacs-anywhere/master/install | bash")

    (server-start)

The tools that use emacs-anywhere &#x2013;such as my web browser&#x2013; and emacs-anywhere
itself need to be given sufficient OS permissions:

    System Preferences → Security & Privacy → Accessibility

Then check the emacs-anywhere box from the following gui and provide a keyboard shortcut:

    System Preferences → Keyboard → Shortcuts → Services

(•̀ᴗ•́)و

I always want to be in Org-mode and input unicode:

    (add-hook 'ea-popup-hook
      (lambda (app-name window-title x y w h)
       (org-mode)
       (set-input-method "Agda")
      )
    )


<a id="org9846282"></a>

# Cosmetics

    ;; Make it very easy to see the line with the cursor.
    (global-hl-line-mode t)

    ;; Clean up any accidental trailing whitespace and in other places,
    ;; upon save.
    (add-hook 'before-save-hook 'whitespace-cleanup)

    ;; Keep self motivated!
    (setq frame-title-format '("" "%b - Living The Dream (•̀ᴗ•́)و"))


<a id="org591d9a4"></a>

## Themes

    ;; Treat all themes as safe; no query before use.
    (setf custom-safe-themes t)

    ;; Nice looking themes ^_^
    (use-package solarized-theme)
    (use-package doom-themes)
    ;; (use-package spacemacs-theme)
    ;; this gives me an error for some reason

    (defun my/disable-all-themes ()
      (dolist (th custom-enabled-themes)
	  (disable-theme th))
    )

    (defun my/load-dark-theme ()
      ;;   (load-theme 'spacemacs-dark)   ;; orginally
      (my/disable-all-themes)
      (load-theme 'doom-vibrant)
    )

    (defun my/load-light-theme ()
      ;;   (load-theme 'spacemacs-light)   ;; orginally
      ;; Recently I'm liking this ordered mixture.
      (load-theme 'solarized-light) (load-theme 'doom-solarized-light)
    )

    ;; “C-x t” to toggle between light and dark themes.
    (defun my/toggle-theme () "Toggle between dark and light themes."
      (interactive)
      ;; Load dark if light is top-most enabled theme, else load light.
      (if (equal (car custom-enabled-themes) 'doom-vibrant)
	  (my/load-light-theme)
	  (my/load-dark-theme)
      )

      ;; The dark theme's modeline separator is ugly.
      ;; Keep reading below regarding “powerline”.
      ;; (setq powerline-default-separator 'arrow)
      ;; (spaceline-spacemacs-theme)
    )

    (global-set-key "\C-x\ t" 'my/toggle-theme)

    ;; Initially begin with the light theme.
    (load-theme 'spacemacs-light t)

The [Doom Themes](https://github.com/hlissner/emacs-doom-themes/tree/screenshots) also look rather appealing.
A showcase of many themes can be found [here](https://emacsthemes.com/).


<a id="org0a8b872"></a>

## Startup message: Emacs & Org versions

    ;; Silence the usual message: Get more info using the about page via C-h C-a.
    (setq inhibit-startup-message t)

    (defun display-startup-echo-area-message ()
      (message
	  (concat "Welcome "      user-full-name
	      "! Emacs "      emacs-version
	      "; Org-mode "   org-version
	      "; System "    (system-name)
	  )
      )
    )

Now my startup message is,

    ;; Welcome Musa Al-hassy! Emacs 26.1; Org-mode 9.2.3; System alhassy-air.local

For some fun, run this cute method.

    (animate-birthday-present user-full-name)

Moreover, since I end up using org-mode most of the time, let's make that the default mode.

    (setq initial-major-mode 'org-mode)


<a id="orgfbfd3cd"></a>

## Persistent Scratch Buffer

The `*scratch*` buffer is a nice playground for temporary data.

I use Org-mode often, so that's how I want things to appear.

    (setq initial-scratch-message (concat
      "#+Title: Persistent Scratch Buffer"
      "\n#\n # Welcome! This’ a place for trying things out. \n"))

We might accidentally close this buffer, so we could utilise the following.

    ;; A very simple function to recreate the scratch buffer:
    ;; ( http://emacswiki.org/emacs/RecreateScratchBuffer )
    (defun my/create-scratch-buffer nil
       "create a scratch buffer"
       (interactive)
       (switch-to-buffer (get-buffer-create "*scratch*"))
       (insert initial-scratch-message)
       (org-mode))

However, by default its contents are not saved &#x2013;which may be an issue if we have
not relocated our playthings to their appropriate files. Whence let's save & restore
the scratch buffer by default.

    (use-package persistent-scratch
      :config
      (persistent-scratch-setup-default))


<a id="org1cedb22"></a>

## Spaceline: A sleek mode line

I may not use the spacemacs [starter kit](https://www.emacswiki.org/emacs/StarterKits), since I do not like evil-mode and find spacemacs
to “hide things” from me &#x2013;whereas Emacs “”encourages” me to learn more&#x2013;,
however it is a configuration and I enjoy reading Emacs configs in order to
improve my own setup. From Spacemacs I've adopted Helm for list completion,
its sleek light & dark themes, and its modified powerline setup.

The ‘modeline’ is a part near the bottom of Emacs that gives information
about the current mode, as well as other matters &#x2013;such as time & date, for example.

    (use-package spaceline
      :config
      (require 'spaceline-config)
      (setq spaceline-buffer-encoding-abbrev-p nil)
      (setq spaceline-line-column-p nil)
      (setq spaceline-line-p nil)
      (setq powerline-default-separator 'arrow)
      :init
     (spaceline-helm-mode) ;; When using helm, mode line looks prettier.
     (spaceline-spacemacs-theme)
    )

Other separators I've considered include `'brace` instead of an arrow,
and `'contour, 'chamfer, 'wave, 'zigzag` which look like browser tabs
that are curved, boxed, wavy, or in the style of driftwood.


<a id="orgc5c373e"></a>

## Flashing when something goes wrong ─no blinking

Make top and bottom of screen flash when something unexpected happens thereby observing a warning message in the minibuffer. E.g., C-g, or calling an unbound key sequence, or misspelling a word.

    (setq visible-bell 1)
    ;; Enable flashing mode-line on errors
    ;; On MacOS, this shows a caution symbol ^_^

    ;; Blinking cursor rushes me to type; let's slow down.
    (blink-cursor-mode -1)


<a id="org4f64043"></a>

## My to-do list: The initial buffer when Emacs opens up

    (find-file "~/Dropbox/todo.org")
    ;; (setq initial-buffer-choice "~/Dropbox/todo.org")

    (split-window-right)			  ;; C-x 3
    (other-window 1)                                  ;; C-x 0
    (toggle enable-local-variables :all           ;; Load *all* locals.
	(toggle org-confirm-babel-evaluate nil    ;; Eval *all* blocks.
	  (find-file "~/.emacs.d/init.org")))


<a id="org43f6e65"></a>

## Showing date, time, and battery life

    (setq display-time-day-and-date t)
    (display-time)

    ;; (display-battery-mode 1)
    ;; Nope; let's use a fancy indicator …

    (use-package fancy-battery
      :diminish
      :config
	(setq fancy-battery-show-percentage t)
	(setq battery-update-interval 15)
	(fancy-battery-mode)
	(display-battery-mode)
    )

This will show remaining battery life, coloured green if charging
and coloured yellow otherwise. It is important to note that
this package is no longer maintained. It works on my machine.


<a id="org67e6b57"></a>

## Hiding Scrollbar, tool bar, and menu

    (tool-bar-mode -1)
    (scroll-bar-mode -1)
    (menu-bar-mode -1)


<a id="org90a2894"></a>

## Increase/decrease text size

    (global-set-key (kbd "C-+") 'text-scale-increase)
    (global-set-key (kbd "C--") 'text-scale-decrease)
      ;; C-x C-0 restores the default font size

    (add-hook 'text-mode-hook
	    '(lambda ()
	       (visual-line-mode 1)))


<a id="org54e8f4d"></a>

## Delete Selection mode

Delete Selection mode lets you treat an Emacs region much like a typical text
selection outside of Emacs: You can replace the active region.
We can delete selected text just by hitting the backspace key.

    (delete-selection-mode 1)


<a id="orgb2a72f3"></a>

## Highlight & complete parenthesis pair when cursor is near ;-

    ;; Highlight expression within matching parens when near one of them.
    (setq show-paren-delay 0)
    (setq blink-matching-paren nil)
    (setq show-paren-style 'expression)
    (show-paren-mode)

    ;; Colour parens, and other delimiters, depending on their depth.
    ;; Very useful for parens heavy languages like Lisp.
    (use-package rainbow-delimiters)

    (add-hook 'org-mode-hook
      '(lambda () (rainbow-delimiters-mode 1)))
    (add-hook 'prog-mode-hook
      '(lambda () (rainbow-delimiters-mode 1)))

For example,

    (blue (purple (forest (green (yellow (blue))))))

There is a powerful package called ‘smartparens’ for working with pair-able
characters, but I've found it to be too much for my uses. Instead I'll utilise
the lightweight package `electric`, which provided by Emacs out of the box.

    (electric-pair-mode 1)

It supports, by default, ACSI pairs `{}, [], ()` and Unicode `‘’, “”, ⟪⟫, ⟨⟩`.


<a id="org6707e11"></a>

## Minibuffer should display line and column numbers

    (global-display-line-numbers-mode t)
    ; (line-number-mode t)
    (column-number-mode t)


<a id="org2b6dcae"></a>

## Neotree: Directory Tree Listing

We open a nifty file manager upon startup.

    ;; neotree --sidebar for project file navigation
    (use-package neotree
      :config (global-set-key "\C-x\ d" 'neotree-toggle))

    ;; Only do this once:
    (when nil
      (use-package all-the-icons)
      (all-the-icons-install-fonts 'install-without-asking))

    (setq neo-theme 'icons)
    (neotree-refresh)

    ;; Open it up upon startup.
    (neotree-toggle)

By default `C-x d` invokes `dired`, but I prefer `neotree` for file management.

Useful navigational commands include

-   `U` to go up a directory.
-   `C-c C-c` to change directory focus; `C-C c` to type the directory out.
-   `?` or `h` to get help and `q` to quit.

As always, to go to the neotree pane when it's the only other window,
execute `C-x o`.

I *rarely* make use of this feature; company mode & Helm together quickly provide
an automatic replacement for nearly all of my uses.


<a id="org1f6eeaf"></a>

## Window resizing using the golden ratio     :Disabled:

Let's load the following package, which automatically resizes windows so that
the window containing the cursor is the largest, according to the golden ratio.
Consequently, the window we're working with is nice and large yet the other windows
are still readable.

    (use-package golden-ratio
      :diminish golden-ratio-mode
      :init (golden-ratio-mode 1))

After some time this got a bit annoying and I'm no longer  using this.


<a id="org2b8adc2"></a>

# Life within Org-mode

Let's obtain Org-mode along with the extras that allow us to ignore
heading names, but still utilise their contents &#x2013;e.g., such as a heading
named ‘preamble’ that contains org-mode setup for a file.

    (use-package org
      :ensure org-plus-contrib
      :config
      (require 'ox-extra)
      (ox-extras-activate '(ignore-headlines)))

This lets us use the `:ignore:` tag on headlines you'd like to have ignored,
while not ignoring their content &#x2013;see [here](https://emacs.stackexchange.com/a/17677/10352).

-   Use the `:noexport:` tag to omit a headline *and* its contents.

Now, let's replace the content marker, “⋯”, with a nice
unicode arrow.

    (setq org-ellipsis " ⤵")

Also:

    ;; Fold all source blocks on startup.
    (setq org-hide-block-startup t)

    ;; Avoid accidentally editing folded regions, say by adding text after an Org “⋯”.
    (setq org-catch-invisible-edits 'show)

    ;; I use indentation-sensitive programming languages.
    ;; Tangling should preserve my indentation.
    (setq org-src-preserve-indentation t)

    ;; Qive quote and verse blocks a nice look.
    (setq org-fontify-quote-and-verse-blocks t)

I rarely use tables, but here is a useful [Org-Mode Table Editing Cheatsheet.](http://notesyoujustmightwanttosave.blogspot.com/)


<a id="orge3c039f"></a>

## High Speed Literate Programming


### Manipulating Sections

Let's enable the [Org Speed Keys](http://notesyoujustmightwanttosave.blogspot.com/2011/12/org-speed-keys.html) so that when the cursor is at the beginning of
a headline, we can perform fast manipulation & navigation using the standard Emacs movement
controls, such as

-   `#` toggle `COMMENT`-ing for an org-header.
-   `s` toggles “narrowing” to a subtree; i.e., hide the rest of the document.

    If you narrow to a subtree then any export, `C-c C-e`, will only consider
    the narrowed detail.

-   `I/O` clock In/Out to the task defined by the current heading.
    -   Keep track of your work times!
    -   `v` view agenda.
-   `u` for jumping upwards to the parent heading.
-   `c` for cycling structure below current heading, or `C` for cycling global structure.
-   `i` insert a new same-level heading below current heading.
-   `w` refile current heading; options list pops-up to select which heading to move it to. Neato!
-   `t` cycle through the available TODO states.
-   `^` sort children of current subtree; brings up a list of sorting options.
-   `n/p` for next/previous *visible* heading.
-   `f/b` for jumping forward/backward to the next/previous *same-level* heading.
-   `D/U` move a heading down/up.
-   `L/R` recursively promote (move leftwards) or demote (more rightwards) a heading.
-   `1,2,3` to mark a heading with priority, highest to lowest.

We can add our own speed keys by altering the `org-speed-commands-user` variable.

Moreover, `?` to see a complete list of keys available.

    (setq org-use-speed-commands t)


### Seamless Navigation Between Source Blocks

Finally, let's use the “super key” &#x2013;aka the command or windows key&#x2013;
to jump to the previous, next, or toggle editing org-mode source blocks.

    ;; Overriding keys for printing buffer, duplicating gui frame, and isearch-yank-kill.
    ;;
    (define-key org-mode-map (kbd "s-p") #'org-babel-previous-src-block)
    (define-key org-mode-map (kbd "s-n") #'org-babel-next-src-block)
    (define-key org-mode-map (kbd "s-e") #'org-edit-src-code)
    (define-key org-src-mode-map (kbd "s-e") #'org-edit-src-exit)

Interestingly, `s-l` is “goto line”.


### Modifying `<return>`

-   `C-RET, C-S-RET` make a new heading where the latter marks it as a `TODO`.
-   By default `M-RET` makes it easy to work with existing list items, headings, tables, etc
    by creating a new item, heading, etc.
-   Usually we want a newline then we indent, let's make that the default.

	(add-hook 'org-mode-hook '(lambda ()
	  (local-set-key (kbd "<return>") 'org-return-indent))
	  (local-set-key (kbd "C-M-<return>") 'electric-indent-just-newline))

    Notice that I've also added another kind of return, for when I want to
    break-out of the indentation approach and start working at the beginning of
    the line.

In summary,

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">key</th>
<th scope="col" class="org-left">method</th>
<th scope="col" class="org-left">behaviour</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`<return>`</td>
<td class="org-left">`org-return-indent`</td>
<td class="org-left">Newline with indentation</td>
</tr>


<tr>
<td class="org-left">`M-<return>`</td>
<td class="org-left">`org-meta-return`</td>
<td class="org-left">Newline with new org item</td>
</tr>


<tr>
<td class="org-left">`C-M-<return>`</td>
<td class="org-left">`electric-indent-just-newline`</td>
<td class="org-left">Newline, cursor at start</td>
</tr>


<tr>
<td class="org-left">`C-<return>`</td>
<td class="org-left">`org-insert-heading-respect-content`</td>
<td class="org-left">New heading *after* current content</td>
</tr>


<tr>
<td class="org-left">`C-S-<return>`</td>
<td class="org-left">`org-insert-todo-heading-respect-content`</td>
<td class="org-left">Ditto, but with a `TODO` marker</td>
</tr>
</tbody>
</table>


### `C-a,e,k` and Yanking of sections

    ;; On an org-heading, C-a goes to after the star, heading markers.
    ;; To use speed keys, run C-a C-a to get to the star markers.
    ;;
    ;; C-e goes to the end of the heading, not including the tags.
    ;;
    (setq org-special-ctrl-a/e t)

    ;; C-k no longer removes tags, if activated in the middle of a heading's name.
    (setq org-special-ctrl-k t)

    ;; When you yank a subtree and paste it alongside a subtree of depth ‘d’,
    ;; then the yanked tree's depth is adjusted to become depth ‘d’ as well.
    ;; If you don't want this, then refile instead of copy pasting.
    (setq org-yank-adjusted-subtrees t)


<a id="org24091ac"></a>

## Using org-mode as a Day Planner

⟪ This section is based on a dated, yet delightful, tutorial
  of the same title by [John Wiegley](http://newartisans.com/2007/08/using-org-mode-as-a-day-planner/). ⟫

We want a day-planner with the following use:

1.  “Mindlessly” & rapidly create new tasks.
2.  Schedule and archive tasks at the end, or start, of the work day.
3.  Glance at a week's tasks, shuffle if need be.
4.  Prioritise the day's tasks. Aim for ≤15 tasks.
5.  Progress towards `A` tasks completion by documenting work completed.
6.  Repeat! During the day, if anything comes up, capture it and intentionally
    forget about it.

[Capture](https://orgmode.org/org.html#Setting-up-capture) lets me quickly make notes & capture ideas, with associated reference material,
without any interruption to the current work flow. Without losing focus on what you're doing,
quickly jot down a note of something important that just came up.

E.g., I have a task, or something I wish to note down, rather than opening
some file, then making a heading, then writing it; instead, I press
`C-c c t` and a pop-up appears, I make my note, and it disappears with my
notes file(s) now being altered! Moreover, by default it provide a timestamp
and a link to the file location where I made the note &#x2013;helpful for tasks, tickets,
to be tackled later on.

    (setq org-default-notes-file "~/Dropbox/todo.org")
    (define-key global-map "\C-cc" 'org-capture)

By default we only get a ‘tasks’ form of capture, let's add some more.

    (cl-defun my/make/org-capture-template
       (shortcut heading &optional (no-todo nil) (description heading) (category heading))
      "Quickly produce an org-capture-template.

      After adding the result of this function to ‘org-capture-templates’,
      we will be able perform a capture with “C-c c ‘shortcut’”
      which will have description ‘description’.
      It will be added to the tasks file under heading ‘heading’
      and be marked with category  ‘category’.

      ‘no-todo’ omits the ‘TODO’ tag from the resulting item; e.g.,
      when it's merely an interesting note that needn't be acted upon.
      ─Probably a bad idea─

      Defaults for ‘description’ and ‘category’ are set to the same as
      the ‘heading’. Default for ‘no-todo’ is ‘nil’.
      "
      `(,shortcut ,description entry
	  (file+headline org-default-notes-file
	 ,(concat heading "\n#+CATEGORY: " category))
	  , (concat "*" (unless no-todo " TODO") " %?\n:PROPERTIES:\n:CREATED: %U\n:END:\n\n")
	  :empty-lines 1)
    )

    (setq org-capture-templates
      `(
	 ,(my/make/org-capture-template "t" "Tasks, Getting Things Done")
	 ,(my/make/org-capture-template "r" "Research")
	 ,(my/make/org-capture-template "m" "Email")
	 ,(my/make/org-capture-template "e" "Emacs (•̀ᴗ•́)و")
	 ,(my/make/org-capture-template "b" "Blog")
	 ,(my/make/org-capture-template "a" "Arbitrary Reading and Learning")
	 ,(my/make/org-capture-template "p" "Personal Matters")
    ))

For now I capture everything into a single file.
One would ideally keep separate client, project, information in its own org file.
The `#+CATEGORY` appears alongside each task in the agenda view &#x2013;keep reading.

**Where am I currently capturing?**

-   During meetings, when a nifty idea pops into my mind, I quickly capture it.
    -   I've found taking my laptop to meetings makes me an active listener
	and I get much more out of my meetings since I'm taking notes.
-   Through out the day, as I browse the web, read, and work; random ideas pop-up, and I capture them indiscriminately.
-   I envision that for a phone call, I would open up a capture to make note of what the call entailed so I can review it later.
-   Anywhere you simply want to make a note, for the current heading, just press
    `C-c C-z`. The notes are just your remarks along with a timestamp; they are
    collected at the top of the tree, under the heading.

	;; Ensure notes are stored at the top of a tree.
	(setq org-reverse-note-order nil)

Anyhow…

Step 1: When new tasks come up
Isn't it great that we can squirrel away info into some default location
then immediately return to what we were doing before &#x2013;with speed & minimal distraction! ♥‿♥
Indeed, if our system for task management were slow then we may not produce tasks and so forget them altogether! щ(゜ロ゜щ)

-   Entering tasks is a desirably impulsive act;
    do not make any further scheduling considerations.

    The next step, the review stage occurring at the end or the start of
    the workday, is for processing.

> *The reason for this is that entering new tasks should be impulsive, not reasoned./*
> *Your reasoning skills are required for the task at hand, not every new tidbit./*
> *You may even find that during the few hours that transpire between creating a*
> *task and categorizing it, you’ve either already done it or discovered it doesn’t*
> *need to be done at all!* &#x2013; [John Wiegley](http://newartisans.com/2007/08/using-org-mode-as-a-day-planner/)

When my computer isn't handy, make a note on my phone then transfer it later.

**Step 2: Filing your tasks**
At a later time, a time of reflection, we go to our tasks list and actually schedule time to get them done
by `C-c C-s` then pick a date by entering a number in the form `+n` to mean that task is due `n` days from now.

-   Tasks with no due date are ones that “could happen anytime”, most likely no time at all.
-   At least schedule tasks reasonably far off in the future, then reassess when the time comes.
-   An uncompleted task is by default rescheduled to the current day, each day, along with how overdue it is.

    -   Aim to consciously reschedule such tasks!

    With time, it will become clear what is an unreasonable day
    verses what is an achievable day.

**Step 3: Quickly review the upcoming week**
The next day we begin our work, we press `C-c a a` to see the
scheduled tasks for this week --`C-c C-s` to re-schedule the
task under the cursor and `r` to refresh the agenda.

    (define-key global-map "\C-ca" 'org-agenda)

**Step 4: Getting ready for the day**
After having seen our tasks for the week, we press `d` to enter daily view
for the current day. Now we decide whether the items for today are
`A`: of high urgency & important; `B`: of moderate urgency & importance; or
`C`: Pretty much optional, or very quick or fun to do.

-   `A` tasks should be both important *and* urgently done on the day they were scheduled.
    -   Such tasks should be relatively rare!
    -   If you have too many, you're anxious about priorities and rendering
	priorities useless.
-   `C` tasks can always be scheduled for another day without much worry.
    -   Act! If the thought of rescheduling causes you to worry, upgrade it to a
	`B` or `A`.
-   As such, most tasks will generally be priority `B`:
    Tasks that need to be done, but the exact day isn't as critical as with an
    `A` task. These are the “bread and butter” tasks that make up your day to day
    life.

On a task item, press `,` then one of `A, B, C` to set its priority.
Then `r` to refresh.

**Step 5: Doing the work**
Since `A` tasks are the important and urgent ones, if you do all of the `A` tasks and
nothing else today, no one would suffer. It's a good day (─‿‿─).

There should be no scheduling nor prioritising at this stage.
You should not be touching your tasks file until your next review session:
Either at the end of the day or the start of the next.

-   Leverage priorities! E.g., When a full day has several `C` tasks, reschedule
    them for later in the week without a second thought.
    -   You've already provided consideration when assigning priorities.

**Step 6: Moving a task toward completion**
My workflow states are described in the section
[4.5](#WorkflowStates) and contain states: `TODO, STARTED, WAITING, ON_HOLD, CANCELLED, DONE`.

-   Tasks marked `WAITING` are ones for which we are awaiting some event, like someone
    to reply to our query. As such, these tasks can be rescheduled until I give up
    or the awaited event happens &#x2013;in which case I go to `STARTED` and document
    the reply to my query.
-   The task may be put off indefinitely with `ON_HOLD`, or I may choose never to do it
    with `CANCELLED`. Along with `DONE`, these three mark a task as completed
    and so it needn't appear in any agenda view.

I personally clock-in and clock-out of tasks &#x2013;keep reading&#x2013;,
where upon clocking-out I'm prompted for a note about what I've accomplished
so far.
Entering a comment about what I've done, even if it's very little,
feels like I'm getting something done. It's an explicit marker of progress.

In the past, I would make a “captain's log” at the end of the day, but that's
like commenting code after it's written, I didn't always feel like doing it and
it wasn't that important after the fact. The continuous approach of noting after
every clock-out is much more practical, for me at least.

**Step 7: Archiving Tasks**
During the review state,
when a task is completed, ‘archive’ it with `C-c C-x C-s`: This marks it as done, adds a time stamp,
and moves it to a local `*.org_archive` file. This was our ‘to do’ list becomes a ‘ta da’ list showcasing
all we have done (•̀ᴗ•́)و

Archiving keeps task lists clutter free, but unlike deletion it allows
us, possibly rarely, to look up details of a task or what tasks were completed
in a certain time frame &#x2013;which may be a motivational act, to see that you have
actually completed more than you thought, provided you make and archive tasks
regularly. We can use `(org-search-view)` to search an org file *and* the
archive file too, if we enable it so.

    ;; Include agenda archive files when searching for things
    (setq org-agenda-text-search-extra-files (quote (agenda-archives)))

    ;; Invoing the agenda command shows the agenda and enables
    ;; the org-agenda variables.
    (org-agenda "a" "a")

Let's install some helpful views for our agenda.

-   `C-c a c`: See completed tasks at the end of the day and archive them.

	;; Pressing ‘c’ in the org-agenda view shows all completed tasks,
	;; which should be archived.
	(add-to-list 'org-agenda-custom-commands
	  '("c" todo "DONE|ON_HOLD|CANCELLED" nil))
-   `C-c a u`: See unscheduled, undeadlined, and undated tasks in my todo files.
    Which should then be scheduled or archived.

	(add-to-list 'org-agenda-custom-commands
	  '("u" alltodo ""
	     ((org-agenda-skip-function
		(lambda ()
		      (org-agenda-skip-entry-if 'scheduled 'deadline 'regexp  "\n]+>")))
		      (org-agenda-overriding-header "Unscheduled TODO entries: "))))


<a id="orgf715be6"></a>

## Automating [Pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) &#x2013;Dealing with dreadful tasks

Effort estimates are for an entire task.
Yet, sometimes it's hard to even get started on some tasks.

-   The code below ensures a 25 minute timer is started whenever clocking in happens.
    -   The timer is in the lower right of the modeline.

-   When the timer runs out, we get a notification.

-   We may have the momentum to continue on the dreadful task, or clock-out and take a break after
    documenting what was accomplished.

    ;; Tasks get a 25 minute count down timer
    (setq org-timer-default-timer 25)

    ;; Use the timer we set when clocking in happens.
    (add-hook 'org-clock-in-hook
      (lambda () (org-timer-set-timer '(16))))

    ;; unless we clocked-out with less than a minute left,
    ;; show disappointment message.
    (add-hook 'org-clock-out-hook
      (lambda ()
      (unless (s-prefix? "0:00" (org-timer-value-string))
	 (message-box "The basic 25 minutes on this dreadful task are not up; it's a shame to see you leave."))
	 (org-timer-stop)
	 ))

Note that this does not conflict with the total effort estimate for the task.


<a id="orgf4d7519"></a>

## Journaling

Thus far I've made it easy to quickly capture ideas and tasks,
not so much on the analysis phase:

-   What was accomplished today?
-   What are some notably bad habits? Good habits?
-   What are some future steps?

Rather than overloading the capture mechanism for such thoughts,
let's employ `org-journal` &#x2013;journal entries are stored in files such as
`journal/20190407`, where the file name is simply the date, or only one
file per year as I've set it up below.
Each entry is the week day, along with the date,
then each child tree is an actual entry with a personal
title preceded by the time the entry was made.
Unlike capture and its agenda support, journal ensures entries are maintained in
chronological order with calendar support.

Since org files are plain text files, an entry can
be written anywhere and later ported to the journal.

The separation of concerns is to emphasise the capture stage
as being quick and relatively mindless, whereas the Journaling
stage as being mindful.
Even though we may utilise capture to provide quick support for including
journal entries, I have set my journal to be on a yearly basis &#x2013;one file per year&#x2013;
since I want to be able to look at previous entries when making the current entry;
after all, it's hard to compare and contrast easily unless there's multiple entries
opened already.

As such, ideally at the end of the day, I can review what
has happened, and what has not, and why this is the case,
and what I intend to do about it, and what problems were encountered
and how they were solved &#x2013;in case the problem is encountered again in the future.
**Consequently, if I encounter previously confronted situations, problems,**
**all I have to do is reread my journal to get an idea of how to progress.**
Read more about [the importance of reviewing your day on a daily basis](https://www.google.com/search?q=on+the+importance+of+reviwing+your+day+daily&oq=on+the+importance+of+reviwing+your+day+daily&aqs=chrome..69i57.367j0j7&sourceid=chrome&ie=UTF-8).

Moreover, by journaling with Org on a daily basis, it can be
relatively easy to produce a report on what has been happening
recently, at work for example. For now, there is no need to
have multiple journals, for work and for personal life, as
such I will utilise the tag `:work:` for non-personal matters.

Anyhow, the setup:

    (use-package org-journal
      :bind (("C-c j" . org-journal-new-entry))
      :config
      (setq org-journal-dir "~/Dropbox/journal/")
      (setq org-journal-file-type 'yearly)
    )

Bindings available in `org-journal-mode`, when journaling:

-   `C-c C-j`: Insert a new entry into the current journal file.
    -   Note keys for `org-journal-new-entry` overwrite those for `org-goto`.
-   `C-c C-s`: Search the journal for a string.
    -   Note keys for `org-journal-search` overwrite those for `org-schedule`.

All journal entries are registered in the Emacs Calendar.
To see available journal entries do `M-x calendar`.
Bindings available in the calendar-mode:

-   `j`: View an entry in a new buffer.
-   `i j`: add a new entry into the day’s file
-   `f w/m/y/f/F`: Search in all entries of the current week, month, year, all of time,
    of in all entries in the future.


<a id="WorkflowStates"></a>

## Workflow States

Here are some of my common workflow states, &#x2013;the ‘!’ indicates a timestamp should be generated&#x2013;

    (setq org-todo-keywords
	  (quote ((sequence "TODO(t)" "STARTED(s@/!)" "|" "DONE(d/!)")
	      (sequence "WAITING(w@/!)" "ON_HOLD(h@/!)" "|" "CANCELLED(c@/!)")
	     )
	  )
    )

The `@` brings up a pop-up to make a local note about why the state changed.
**Super cool stuff!**
In particular, we transition from `TODO` to `STARTED` once 15 minutes, or a
reasonable amount, of work has transpired.
Since all but one state are marked for logging, we could use the
`lognotestate` logging facility of org-mode, which prompts for a note
every time a task’s state is changed.

Entering a comment about what I've done, even if it's very little,
feels like I'm getting something done. It's an explicit marker of progress
and motivates me to want to change my task's states more often until I see
it marked `DONE`.

Here's how they are coloured,

    (setq org-todo-keyword-faces
	  (quote (("TODO" :foreground "red" :weight bold)
	      ("STARTED" :foreground "blue" :weight bold)
	      ("DONE" :foreground "forest green" :weight bold)
	      ("WAITING" :foreground "orange" :weight bold)
	      ("ON_HOLD" :foreground "magenta" :weight bold)
	      ("CANCELLED" :foreground "forest green" :weight bold))))

Now we press `C-c C-t` then the letter shortcut to actually make the state of an org heading.

    (setq org-use-fast-todo-selection t)

We can also change through states using Shift- left, or right.

Let's draw a state diagram to show what such a workflow looks like.

[PlantUML](http://plantuml.com/index) supports drawing diagrams in a tremendously simple format
&#x2013;it even supports Graphviz/DOT directly and many other formats.
Super simple setup instructions can be found [here](http://eschulte.github.io/babel-dev/DONE-integrate-plantuml-support.html); below are a bit more
involved instructions. Read the manual [here](http://plantuml.com/guide).

    ;; Install the tool
    ; (async-shell-command "brew cask install java") ;; Dependency
    ; (async-shell-command "brew install plantuml")

    ;; Tell emacs where it is.
    ;; E.g., (async-shell-command "find / -name plantuml.jar")
    (setq org-plantuml-jar-path
	  (expand-file-name "/usr/local/Cellar/plantuml/1.2019.5/libexec/plantuml.jar"))

    ;; Enable C-c C-c to generate diagrams from plantuml src blocks.
    (add-to-list 'org-babel-load-languages '(plantuml . t) )
    (require 'ob-plantuml)

    ; Use fundamental mode when editing plantuml blocks with C-c '
    (add-to-list 'org-src-lang-modes (quote ("plantuml" . fundamental)))

Let's use this!

    skinparam defaultTextAlignment center  /' Text alignment '/

    skinparam titleBorderRoundCorner 15
    skinparam titleBorderThickness 2
    skinparam titleBorderColor red
    skinparam titleBackgroundColor Aqua-CadetBlue
    title My Personal Task States

    [*] -> Todo  /' This is my starting state '/
    Done -right-> [*]  /' This is an end state '/
    Cancelled -up-> [*]  /' This is an end state '/

    /'A task is “Todo”, then it's “started”, then finally it's “done”. '/
    Todo    -right-> Started
    Started -down->  Waiting
    Waiting -up->    Started
    Started -right-> Done

    /'Along the way, I may put pause the task for some reason then
      return to it. This may be since I'm “Blocked” since I need
      something, or the task has been put on “hold” since it may not
      be important right now, and it may be “cancelled” eventually.
    '/

    Todo    -down-> Waiting
    Waiting -up-> Todo
    Waiting -up-> Done

    Todo -down-> On_Hold
    On_Hold -> Todo

    On_Hold -down-> Cancelled
    Waiting -down-> Cancelled
    Todo    -down-> Cancelled

    /' The Org-mode shortcuts for these states are as follows. '/
    Todo      : t
    On_Hold   : h
    Started   : s
    Waiting   : w
    Cancelled : c
    Done      : d

    /' If a task is paused, we should document why this is the case. '/
    note right of Waiting: Note what is\nblocking us.
    note right of Cancelled: Note reason\nfor cancellation.
    note bottom of On_Hold: Note reason\nfor reduced priority.

    center footer  ♥‿♥ Org-mode is so cool (•̀ᴗ•́)و
    /' Note that we could omit the “center, left, right” if we wished,
       or used a “header” instead.'/

<img src="../assets/img/workflow.png" alt="My Personal Task States">

Of note:

-   Multiline comments are with `/' comment here '/`, single quote starts a one-line comment.
-   Nodes don't need to be declared, and their names may contain spaces if they are enclosed in double-quotes.
-   One forms an arrow between two nodes by writing a line with `x ->[label here] y`
    or `y <- x`; or using `-->` and `<--` for dashed lines. The label is optional.

    To enforce a particular layout, use `-X->` where `X ∈ {up, down, right, left}`.

-   To declare that a node `x` has fields `d, f` we make two new lines having
    `x : f` and `x : d`.
-   One adds a note by a node `x` as follows: `note right of x: words then newline\nthen more words`.
    Likewise for notes on the `left, top, bottom`.
    -   Interesting sprites and many other things can be done with PlantUML. Read the docs.

This particular workflow is inspired by [Bernt Hansen](http://doc.norang.ca/org-mode.html)
&#x2013;while quickly searching through the PlantUML [manual](http://plantuml.com/guide):
The above is known as an “activity diagram” and it's covered in §4.


<a id="org4be7077"></a>

## Show off-screen Heading at the top of the window

In case we forgot which heading we're under, let's keep
the current heading stuck at the top of the window.

     (use-package org-sticky-header
      :config
      (setq
       org-sticky-header-full-path 'full
       ;; Child and parent headings are seperated by a /.
       org-sticky-header-outline-path-separator " / ")
      :init (org-sticky-header-mode 1)
    )


<a id="org7190df8"></a>

## Clocking Work Time

Let's keep track of the time we spend working on tasks that we may have captured for ourselves the previous day.
Such statistics provides a good idea of how long it actually takes me to accomplish a certain task in the future
and it lets me know where my time has gone.

-   **Clock in:** on a heading with `I`, or in the subtree with `C-c C-x C-i`.
-   **Clock out:** of a heading with `O`, or in the subtree with `C-c C-x C-o`.
-   **Clock report:** See clocked times with `C-c C-x C-r`.

After clocking out, the start and end times, as well as the elapsed time, are added to a drawer
to the heading. We can punch in and out of tasks as many times as desired, say we took a break or
switched to another task, and they will all be recorded into the drawer.

    ;; Record a note on what was acciomplished when clocking out of an item.
    (setq org-log-note-clock-out t)

To get started, we could estimate how long a task will take and clock-in;
then clock-out and see how long it actually took.

Moreover, we can overlay due dates and priorities to tasks in a non-intrusive way that is
easy to edit by hand.

    ;; List of all the files where todo items can be found. Only one for now.
    (setq org-agenda-files '("~/Dropbox/todo.org"))

    ;; How many days ahead the default agenda view should look
    (setq org-agenda-ndays 7)

    ;; How many days early a deadline item will begin showing up in your agenda list.
    (setq org-deadline-warning-days 14)

    ;; In the agenda view, days that have no associated tasks will still have a line showing the date.
    (setq org-agenda-show-all-dates t)

    (setq org-agenda-skip-deadline-if-done t)

    ;; Scheduled items marked as complete will not show up in your agenda view.
    (setq org-agenda-skip-scheduled-if-done t)

    ;; The agenda view – even in the 7-days-at-a-time view – will always begin on the current day.
    ;; This is important, since while using org-mode as a day planner, you never want to think of
    ;; days gone past. That’s something you do in other ways, such as when reviewing completed tasks.
    (setq org-agenda-start-on-weekday nil)

Sometimes, at the beginning at least, I would accidentally invoke the transposed
command `C-x C-c`, which saves all buffers and quits Emacs. So here's a helpful
way to ensure I don't quit Emacs accidentally.

    (setq confirm-kill-emacs 'yes-or-no-p)

    ;; Resume clocking task when emacs is restarted
    (org-clock-persistence-insinuate)

    ;; Show lot of clocking history
    (setq org-clock-history-length 23)

    ;; Resume clocking task on clock-in if the clock is open
    (setq org-clock-in-resume t)

    ;; Sometimes I change tasks I'm clocking quickly - this removes clocked tasks with 0:00 duration
    (setq org-clock-out-remove-zero-time-clocks t)

    ;; Clock out when moving task to a done state
    (setq org-clock-out-when-done t)

    ;; Save the running clock and all clock history when exiting Emacs, load it on startup
    (setq org-clock-persist t)

    ;; Do not prompt to resume an active clock
    ;; (setq org-clock-persist-query-resume nil)

    ;; Include current clocking task in clock reports
    (setq org-clock-report-include-clocking-task t)

**Finding tasks to clock in**
Use one of the following options, with the top-most being the first to be tried.

-   From anywhere, `C-u C-c C-x C-i` yields a pop-up for recently clocked in tasks.
-   Pick something off today's agenda scheduled items.
-   Pick a `Started` task from the agenda view, work on this unfinished task.
-   Pick something from the `TODO` tasks list in the agenda view.

-   `C-c C-x C-d` also provides a quick summary of clocked time for the current org file.

**Estimates versus actual time**
Before clocking into a task, add to the properties drawer `:Effort: 1:25` or `C-c C-x C-e`, for a task
that you estimate will take an hour an twenty-five minutes, for example. Now the modeline
will have will mention the time elapsed alongside the task name.

-   This is also useful when you simply want to put a time limit on a task that wont be
    completed anytime soon, say writing a thesis or a long article, but you still want
    to work on it for an hour a day and be warned when you exceed such a time constraint.

    When you've gone above your estimate time, the modeline shows it to be red.


<a id="orge0d531d"></a>

## [Reveal.JS](https://revealjs.com/?transition=zoom#/) &#x2013; The HTML Presentation Framework

Org-mode documents can be transformed into beautiful slide decks
with [org-reveal](https://github.com/yjwen/org-reveal/blob/master/Readme.org) with the following two simple lines.

    (use-package ox-reveal
     :config (setq org-reveal-root "https://cdn.jsdelivr.net/reveal.js/3.0.0/"))

For example, execute --`C-c C-c`&#x2013;  the following block to see an example slide-deck (─‿‿─)

    (shell-command "curl https://raw.githubusercontent.com/yjwen/org-reveal/master/Readme.org >> Trying_out_reveal.org")
    (with-temp-buffer (find-file "Trying_out_reveal.org")
     (org-reveal-export-to-html-and-browse)
    )

Org-mode exporting --`C-c C-e`&#x2013; now includes an option `R` for such reveal slide decks.


<a id="orga487bbe"></a>

## Coloured LaTeX using Minted

Execute the following for bib ref as well as minted
Org-mode uses the Minted package for source code highlighting in PDF/LaTeX
&#x2013;which in turn requires the pygmentize system tool.

    (setq org-latex-listings 'minted
	  org-latex-packages-alist '(("" "minted"))
	  org-latex-pdf-process
	  '("pdflatex -shell-escape -interaction nonstopmode -output-directory %o %f"
	"biber %b"
	"pdflatex -shell-escape -interaction nonstopmode -output-directory %o %f"
	"pdflatex -shell-escape -interaction nonstopmode -output-directory %o %f")
    )

For faster pdf generation, may consider invoking:

    (setq org-latex-pdf-process
	  '("pdflatex -interaction nonstopmode -output-directory %o %f"))


<a id="org02b92ef"></a>

## Executing code from `src` blocks

For example, to execute a shell command in emacs,
write a `src` with a shell command, then `C-c c-c` to see the results.
Emacs will generally query you to ensure you're sure about executing the
(possibly dangerous) code block; let's stop that:

    ; Seamless use of babel: No confirmation upon execution.
    ;; Downside: Could accidentally evaluate harmful code.
    (setq org-confirm-babel-evaluate nil)

A worked out example can be obtained as follows: `<g TAB` then `C-c C-C` to make a nice
simple graph &#x2013;the code for this is in the next section.

Some initial languages we want org-babel to support:

     (org-babel-do-load-languages
       'org-babel-load-languages
       '(
	 (emacs-lisp . t)
	 ;; (shell	 . t)
	 (python . t)
	 (haskell . t)
	 (ruby	 . t)
	 (ocaml	 . t)
	 (dot	 . t)
	 (latex	 . t)
	 (org	 . t)
	 (makefile	 . t)
	 ))

    ;; Preserve my indentation for source code during export.
    (setq org-src-preserve-indentation t)

    ;; The export process hangs Emacs, let's avoid this.
    ;; MA: For one reason or another, this crashes more than I'd like.
    ;; (setq org-export-in-background t)

More languages can be added using `add-to-list`.


<a id="org4db7ff7"></a>

## Hiding Emphasise Markers & Inlining Images

    ;; org-mode math is now highlighted ;-)
    (setq org-highlight-latex-and-related '(latex))

    ;; Hide the *,=,/ markers
    (setq org-hide-emphasis-markers t)

    ;; (setq org-pretty-entities t)
    ;; to have \alpha, \to and others display as utf8 http://orgmode.org/manual/Special-symbols.html

The following is now disabled &#x2013;it makes my system slower than I'd like.

    ;; Let's set inline images.
    (setq org-display-inline-images t)
    (setq org-redisplay-inline-images t)
    (setq org-startup-with-inline-images "inlineimages")

    ;; Automatically convert LaTeX fragments to inline images.
    (setq org-startup-with-latex-preview t)


<a id="org8ab89a9"></a>

## Jumping without hassle

    (defun my/org-goto-line (line)
      "Go to the indicated line, unfolding the parent Org header.

       Implementation: Go to the line, then look at the 1st previous
       org header, now we can unfold it whence we do so, then we go
       back to the line we want to be at.
      "
      (interactive)
      (goto-line line)
      (org-previous-visible-heading 1)
      (org-cycle)
      (goto-line line)
    )


<a id="org53c2e53"></a>

## Folding within a subtree

    (defun my/org-fold-current-subtree-anywhere-in-it ()
      "Hide the current heading, while being anywhere inside it."
      (interactive)
      (save-excursion
	(org-narrow-to-subtree)
	(org-shifttab)
	(widen))
    )

    (add-hook 'org-mode-hook '(lambda ()
      (local-set-key (kbd "C-c C-h") 'my/org-fold-current-subtree-anywhere-in-it)))


<a id="org197f9d3"></a>

## Making then opening html's from org's

    (cl-defun my/org-html-export-to-html (&optional (filename (buffer-name)))
      "Produce an HTML from the given ‘filename’, or otherwise current buffer,
       then open it in my default brower.
      "
     (interactive)
     (org-html-export-to-html)
     (let ((it (concat (file-name-sans-extension buffer-file-name) ".html")))
       (browse-url it)
       (message (concat it " has been opened in Chromium."))
       'success ;; otherwise we obtain a "compiler error".
     )
    )


<a id="org3d5d009"></a>

## Making then opening pdf's from org's

    (cl-defun my/org-latex-export-to-pdf (&optional (filename (buffer-name)))
      "Produce a PDF from the given ‘filename’, or otherwise current buffer,
       then open it in my default viewer.
      "
     (interactive)
     (org-latex-export-to-pdf)
     (let ((it (concat (file-name-sans-extension filename) ".pdf")))
       (eshell-command (concat "open " it  " & ")))
       (message (concat it " has been opened in your PDF viewer."))
       'success ;; otherwise we obtain a "compiler error".
    )


<a id="org5f1bafd"></a>

## Interpret the Haskell source blocks in a file

    (defvar *current-module* "NoModuleNameSpecified"
      "The name of the module, file, that source blocks are
       currently being tangled to.

       This technique is insipired by “Interactive Way to C”;
       see https://alhassy.github.io/InteractiveWayToC/.
      ")

    (defun current-module ()
      "Returns the current module under focus."
      *current-module*)

    (defun set-module (name)
       "Set the name of the module currently under focus.

	Usage: When a module is declared, i.e., a new file has begun,
	then that source blocks header should be “:tangle (set-module ”name-here”)”.
	succeeding source blocks now inherit this name and so are tangled
	to the same module file. How? By placing the following line at the top
	of your Org file: “‘#+PROPERTY: header-args :tangle (current-module))’.

	This technique structures “Interactive Way to C”.
       "
       (setq *current-module* name)
    )

    (cl-defun my/org-run-haskell (&optional target (filename (buffer-name)))
      "Tangle Haskell source blocks of given ‘filename’, or otherwise current buffer,
       and load the resulting ‘target’ file into a ghci buffer.

       If no name is provided for the ‘target’ file that is generated from the
       tangeling process, it is assumed to be the buffer's name with a ‘hs’ extension.

       Note that this only loads the blocks tangled to ‘target’.

       For example, file ‘X.org’ may have haskell blocks that tangle to files
       ‘X.hs’, ‘Y.hs’ and ‘Z.hs’. If no target name is supplied, we tangle all blocks
       but only load ‘X.hs’ into the ghci buffer. A helpful technique to load the
       last, bottom most, defined haskell module, is to have the module declaration's
       source block be ‘:tangle (setq CODE “Y.hs”)’, for example; then the following
       code blocks will inherit this location provided our Org file has at the top
       ‘#+PROPERTY: header-args :tangle (current-module))’.
       Finally, our ‘compile-command’ suffices to be ‘(my/org-run-haskell CODE)’.
       ─
       This technique structures “Interactive Way to C”.
      "
       (let* ((it  (if target target (concat (file-name-sans-extension filename) ".hs")))
	 (buf (concat "*GHCI* " it)))

	 (toggle kill-buffer-query-functions nil (ignore-errors (kill-buffer buf)))
	 (org-babel-tangle it "haskell")
	 (async-shell-command (concat "ghci " it) buf)
	 (switch-to-buffer-other-window buf)
	 (end-of-buffer)
       )
    )

    ;; Set this as the ‘compile-command’ in ‘Local Variables’, for example.


<a id="org47aa639"></a>

# Summary of Utilities Provided

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<tbody>
<tr>
<td class="org-left"><span class="underline">Command</span></td>
<td class="org-left"><span class="underline">Action</span></td>
</tr>


<tr>
<td class="org-left">`C-c C-m`</td>
<td class="org-left">recompile file</td>
</tr>


<tr>
<td class="org-left">`<f5>`</td>
<td class="org-left">revert buffer</td>
</tr>


<tr>
<td class="org-left">`M-x k`</td>
<td class="org-left">kill to start of line</td>
</tr>


<tr>
<td class="org-left">`C-∣`</td>
<td class="org-left">toggle 2 windows from horizontal to vertical view</td>
</tr>


<tr>
<td class="org-left">`(file-as-list   pathHere)`</td>
<td class="org-left">construe a file as a list of lines</td>
</tr>


<tr>
<td class="org-left">`(file-as-string pathHere)`</td>
<td class="org-left">construe a file as a string</td>
</tr>


<tr>
<td class="org-left">(`re-replace-in-file file regex whatDo)`</td>
<td class="org-left">perform an in-file regular expression rewrite</td>
</tr>


<tr>
<td class="org-left">`(mapsto this that)`</td>
<td class="org-left">regex rewrite in current buffer: this ↦ that</td>
</tr>


<tr>
<td class="org-left">`M-x create-scratch-buffer`</td>
<td class="org-left">&#x2013;self evident--</td>
</tr>


<tr>
<td class="org-left">`M-x kill-other-buffers`</td>
<td class="org-left">&#x2013;self evident--</td>
</tr>


<tr>
<td class="org-left">`M-$`</td>
<td class="org-left">check spelling of word at point</td>
</tr>


<tr>
<td class="org-left">`M-#`</td>
<td class="org-left">thesaurus look-up word at point</td>
</tr>


<tr>
<td class="org-left">`(toggle name val ⋯)`</td>
<td class="org-left">*Effectfully* set `name` to `val` only for scope `⋯`.</td>
</tr>


<tr>
<td class="org-left">`(my/org-run-haskell &optional file)`</td>
<td class="org-left">Interpret the Haskell org-blocks from a file into ghci.</td>
</tr>


<tr>
<td class="org-left">`C-+/-`</td>
<td class="org-left">increase/decrease text size</td>
</tr>


<tr>
<td class="org-left">`M-x my-org-html-export-to-html`</td>
<td class="org-left">make then open html from an org file</td>
</tr>


<tr>
<td class="org-left">`C-c C-c`</td>
<td class="org-left">execute code in an org `src` block</td>
</tr>


<tr>
<td class="org-left">`<E`</td>
<td class="org-left">produce an emacs-lisp `src` block</td>
</tr>


<tr>
<td class="org-left">`<g`</td>
<td class="org-left">produce a graph template `src` block</td>
</tr>


<tr>
<td class="org-left">`C-x t`</td>
<td class="org-left">open a new untitled org template file</td>
</tr>


<tr>
<td class="org-left">`(org-keywords)`</td>
<td class="org-left">get `#+Property: Value` pairs from an org file</td>
</tr>


<tr>
<td class="org-left">`(org-keyword property)`</td>
<td class="org-left">get the `value` of a given org `#+property`</td>
</tr>
</tbody>
</table>

Since I'm using `use-package`, I can invoke `M-x describe-personal-keybindings` to see what key bindings I've defined.
Since not all my bindings are via `use-package`, it does not yet cover all of my bindings.

We could run `C-h b` to see our bindings:

    (use-package helm-descbinds
      :defer t
      :bind (("C-h b" . helm-descbinds)))

Finally, we can observe which features are active in our current Emacs with,

    (message "Features: %s" features)
