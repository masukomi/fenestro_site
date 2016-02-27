+++
date = "2016-02-27T11:07:26-05:00"
draft = true
title = "tips"

+++

## Ready to get started?

The easiest way to get started with Fenestro is to start piping output from 
your current command line apps into it. There are two unix utilities you'll 
want in your arsenal to make this happen.

### Converting command line output to HTML with aha

Aha is a simple utility that converts command line input to HTML. That's it. You
can install it with [Homebrew](http://brew.sh/) by saying `brew install aha`

I'd recommend running it with the `--black` option if you run a dark terminal
theme.

### Maintain colored output from your commands with unbuffer

When you pipe from one command to another you loose the ANSI Color Codes. 
For example `git diff HEAD^` would give you a colorized diff of your code, 
but when you pipe it to another tool like aha, it becomes plain, colorless, 
text. To maintain those colors you'll want to install "unbuffer". Again, you 
can find it in homebrew and install by saying 
`brew install homebrew/dupes/expect`

**Note**: Unbuffer works by convincing your tool that it's outputting to
an interactive buffer. Some tools, like git, expect you to page through
long output in interactive mode. You'll need to disable that on calls that
go through unbuffer. With git you just append `--no-pager` immediately after
`git` For example: `git --no-pager diff HEAD^`

### Putting it all together

Once you've got fenestro, unbuffer, and aha installed, you can chain them together like this:  

	unbuffer git --no-pager diff HEAD^ | aha --black \
	| fenestro --name "diff"

For things you'll use often, save yourself typing by making a function in your 
`~/.bashrc`

	function dtf{ #diff to fenestro
		unbuffer git --no-pager diff "$@" | aha --black \
		| fenestro --name "diff"
	}
	# call that with
	# dtf HEAD^
	# to get the same effect as the longer command above


