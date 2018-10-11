---
layout: post
title: "use of surround.vim"
date: 2014-09-19 09:56:45 +0800
comments: true
categories: Vim
---
I use the vim plugin, surround.vim, but I am familiar with it. Before I get to know it, I usually do those things which surround.vim can help us do in a very clumsy way. Thus I keep those notes down thus I can look up it later.

Two links are of use for this post, you can regard this post as an excerpt for the contents of those two links.

http://www.catonmat.net/blog/vim-plugins-surround-vim/
https://github.com/tpope/vim-surround


```
it's easiest to explain with examples. Press cs"' inside

"Hello world!"
to change it to

'Hello world!'
Now press cs'<q> to change it to

<q>Hello world!</q>
To go full circle, press cst" to get

"Hello world!"
To remove the delimiters entirely, press ds".

Hello world!
Now with the cursor on "Hello", press ysiw] (iw is a text object).

[Hello] world!
Let's make that braces and add some space (use } instead of { for no space): cs]{

{ Hello } world!
Now wrap the entire line in parentheses with yssb or yss).

({ Hello } world!)
Revert to the original text: ds{ds)

Hello world!
Emphasize hello: ysiw<em>

<em>Hello</em> world!
Finally, let's try out visual mode. Press a capital V (for linewise visual mode) followed by S<p class="important">.

<p class="important">
  <em>Hello</em> world!
</p>
This plugin is very powerful for HTML and XML editing, a niche which currently seems underfilled in Vim land. (As opposed to HTML/XML inserting, for which many plugins are available). Adding, changing, and removing pairs of tags simultaneously is a breeze.

The . command will work with ds, cs, and yss if you install repeat.vim.


Text              Command      New Text
---------------   -------      -----------
Hello w|orld!     ysiw)        Hello (world)!
Hello w|orld!     csw)         Hello (world)!
fo|o              ysiwt<html>  <html>foo</html>
foo quu|x baz     yss"         "foo quux baz"
foo quu|x baz     ySS"         "
                                   foo quux baz
                               "

(| is the position of cursor in these examples)

```
