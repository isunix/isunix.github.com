---
layout: post
title: "practical vim notes"
date: 2014-06-16 00:24:14 +0800
comments: true
categories: Vim
---
接触VIM的日子已经颇长了， 自己现在的VIM的配置已经是非常的强大了，可惜是clone别人的。 只是在一些配置上稍稍做了些改动, 然后添加了一些自己喜欢的package。使用VIM的技艺还是得经常磨练的， 要不然很快就会手生还有遗忘的。 这片文章记录自己再学习<<Practical VIM>>这本书的时候做的一些笔记， 这些都是自己估计会在coding的时候经常遇到的， 记录下来可以经常查阅。

##Read the Forgotten Manual

1. The Normal mode cw command deletes to the end of the current word and switches to Insert mode.

2. 如果有这么一段：

```html
<a href="http://pragprog.com/dnvim/">Practical Vim</a>
```

在normal模式下， 按下vit会选择Practical Vim。

##Chapter 1--The Vim Way

1. The dot command lets us repeat the last change.

2. Press A in normal mode will put the cursor at the end of a file and go into insert mode.

3. The s command compounds two steps into one: it deletes the character under the cursor and then enters Insert mode.

4. The f{char} command tells Vim to look ahead for the next occurrence of the specified character and then move the cursor directly to it if a match is found.

5. By pressing the , key, it will repeat the last f{char} search in the reverse direction

6. The * command will executes a search for the word under the cursor at that moment.

##Chapter 2--Normal Mode

1. Pressing db deletes from the cursor’s starting position to the beginning of the word.

2. Pressing b will go to the beginning of a word backwordly, while w will do it forwardly.

3. The daw command is easily remembered by the mnemonic delete a word.

4. The <C-a> and <C-x> commands perform addition and subtraction on numbers.

5. yyp will copy the current line and paste it to the next line.

6. c3w will change 3 words after the cursor.

7. The d{motion} command can operate on a single character ( dl), a complete word ( daw), or an entire paragraph ( dap). Its reach is defined by the motion. The same goes for c{motion}, y{motion}, and a handful of others. Collectively, these commands are called operators. You can find the complete list by looking up :h operator

8. \> will shilt right, = will do auto-indent;

9. \\\\\\\\\ will comment the current line.  (I tested\\\\\\ will be enough.)

10. If we wanted to autoindent the entire file using the = command, we could run gg=G (that is, gg to jump to the top of the file and then =G to autoindent everything from the cursor position to the end of the file).

##Chapter 3--Insert Mode

1. In insert mode, <C-h> Delete back one character (backspace), <C-w> Delete back one word, <C-u> Delete back to start of line.

2. In normal node, yt{char} will copy till the char(not including).

3. From Normal mode, we can engage Replace mode with the R command.



##Chapter 4--Visual Mode

1. <C-v> Enable block-wise Visual mode, gv Reselect the last visual selection, o Go to other end of highlighted text.

2. gU{motion} will make {motion} text uppercase. (In visual mode).

3. In normal mode, vit, which can be read as: visually select inside the tag.

4. e in normal mode will forward to the end of word (inclusively).

For more about how to use visual mode to append and substitute text, please refer to the book.

##Chapter 5--Command-Line Mode

基本上跳过了这一章， 只学会：

1. :%s///g;来进行替换。

2. Note the difference between :!ls and :ls—the former calls the ls command in the shell, whereas :ls calls Vim’s built-in command, which shows the contents of the buffer list.

3. On Vim’s command line, the % symbol is shorthand for the current file name. So :!ruby % will run the current file.

##Chapter 6--Manage Multiple Files

1. In vim, we’re editing an in-memory representation of a file, which is called a buffer in Vim’s terminology. Files are stored on the disk, whereas buffers exist in memory. When we open a file in Vim, its contents are read into a buffer, which takes the same name as the file. Initially, the contents of the buffer will be identical to those of the file, but the two will diverge as we make changes to the buffer. If we decide that we want to keep our changes, we can write the contents of the buffer back into the file.

2. We can divide this window horizontally with the <C-w>s command, which creates two windows of equal height. Or we can use the <C-w>v command to split the window vertically, producing two windows of equal width.

3. <C-w>c Close the active window, <C-w>o Keep only the active window, closing all others.

4. <C-w>= Equalize width and height of all windows, <C-w>_ Maximize height of the active window.

5. Alternatively, if the current tab page contains more than one window, we can use the <C-w>T command, which moves the current window into a new tab page (see :h CTRL-W_T ).

6. :tabc[lose] Close the current tab page and all of its windows, :tabo[nly] Keep the active tab page, closing all others.

7. :tabn[ext], also gt Switch to the next tab page, :tabp[revious], also gT Switch to the previous tab page.

##Chapter 7--Open Files and Save Them to Disk

Just skipped over this chapter.

##Chapter 8--Navigate Inside Files with Motions

1. ge Backward to end of previous word.

2. Taken together, the ea commands can be read as “Append at the end of the current word” . The gea command can be read as “append at the end of the previous word”.

3. Vim keeps track of the most recent f{char} search, and we can repeat it using the ; command.

4. The , command repeats the last f{char} search but in the opposite direction.

5. t{char} Forward to the character before the next occurrence of {char}, T{char} Backward to the character after the previous occurrence of {char}.

6. dt. will delete till .

7. We can read the ci" command as “change inside the double quotes.” The cit command can be read as “change inside the tag.” We could just as easily use the yit command to yank the text from inside the tag, or dit to delete it.

8. Keystrokes Buffer Contents

```
iw         Current word
aw         Current word plus one space
iW         Current WORD
aW         Current WORD plus one space
is         Current sentence
as         Current sentence plus one space
ip         Current paragraph
ap         Current paragraph plus one blank line
```

9. As a general rule, we could say that the d{motion} command tends to work well with aw, as, and ap, whereas the c{motion} command works better with iw and similar.

10. Learn more about surround.vim;

##Chapter 9--Navigate Between Files with Jumps

1. gf command means go to file (:h gf ).

##Chapter 10--Copy and Paste

1. The p command pastes the contents of the unnamed register after the cursor position.

2. Taken together, the xp commands can be considered as “Transpose the next two characters.”

3. The ddp sequence could be considered to stand for “Transpose the order of this line and its successor.”

4. Rather than using a single clipboard for all cut, copy, and paste operations, Vim provides multiple registers. When we use the delete, yank, and put commands, we can specify which register we want to interact with.

5. We can specify which register we want to use by prefixing the command with "{register}. If we don’t specify a register, then Vim will use the unnamedregister.

6. For example, if we wanted to yank the current word into register a, we could run "ayiw. Or if we wanted to cut the current line into register b, we could run "bdd. Then we could paste the word from register a by typing "ap, or we could paste the line from register b by typing "bp.

##Chapter 11--Macros

1. Macros allow us to record a sequence of changes and then play them back.

2. The q key functions both as the “record” button and the “stop” button. To begin recording our keystrokes, we type q{register}, giving the address of the register where we want to save the macro. We can tell that we’ve done it right if the word “recording” appears in the status line. Every command that we execute will be captured, right up until we press q again to stop recording.

3. The @{register} command executes the contents of the specified register (see :h @ ). We can also use @@, which repeats the macro that was invoked most recently.

(I have to say I did not finish this chapter!)

##Chapter 12--Matching Patterns and Literals

1. We can override Vim’s default case sensitivity using the \c and \C items. Lowercase \c causes the search pattern to ignore case, while the uppercase \C item forces case sensitivity. If either of these items is used in a search pattern, the value of ‘ignorecase’ is overridden for that search.

2. For using regex in vim, The \v switch at the start causes all subsequent characters to take on a special meaning.

Miscelleneous

1. Tag navigation and tag autocompletion won’t work unless Vim knows where to look for an up-to-date index file.

2. Command Type of Completion

```
<C-n> Generic keywords

<C-x><C-n> Current buffer keywords

<C-x><C-i> Included file keywords

<C-x><C-]> tags file keywords

<C-x><C-k> Dictionary lookup

<C-x><C-l> Whole line completion

<C-x><C-f> Filename completion

<C-x><C-o> Omni-completion
```
