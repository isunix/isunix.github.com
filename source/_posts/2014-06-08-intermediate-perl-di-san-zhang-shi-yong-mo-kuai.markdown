---
layout: post
title: "Intermediate Perl 第三章 使用模块"
date: 2014-06-08 01:16:53 +0800
comments: true
categories: Perl
---
模块是我们的程序的基础部分。他们提供可重用的子程序，变量，甚至面向对象的类。在我们建造自己的模块的过程中， 我们会向你展现一些你可能会感兴趣的。我们同样会看一些别人已经写好的模块的用法。   

##标准发布版本  
     
Perl本身已经自带了很多的流行的模块。事实上， 最新进的50+MB的发布版本中的绝大部分都是来自于模块。在1996年10月， Perl 5.003_07版本中有98个模块。今天， 在2006年年初， Perl5.8.8有359个模块。事实上这是Perl的一个优势之一:它已经自带了很多的你在写有用的还有复杂的程序的时候所需要的东西， 那样就省了你的很多的工作了。   

在整本书中， 我们都会试着识别出哪些模块是Perl自带的(在大部分情况下， 识别出它们是自哪一版开始进入Perl的)。我们将称呼这些为"核心模块" 或者强调它们是在"标准发布版本"中。如果你安装了Perl, 你应该就有了这些模块。由于当我们在写作本书的时候， 我们使用的是Perl 5.8.7, 我们将假定这就是当前的Perl的版本。    

当你在开发自己的代码的时候， 你可能会考虑自己是否想要只使用核心模块，那样你就可以确信任何其他只要是和你的Perl版本是一样的人， 都将会有那些模块。我们将会避开这个争论， 主要是因为我们太爱CPAN了， 简直离不开它了。   

##使用模块   
几乎每一个Perl模块都跟有文档，即使我们可能不知道所有的幕后的魔术是怎么运作的，当我们知道如何使用接口的时候我们真的没必要担心那些。毕竟那就是接口存在的原因: 隐藏细节。   

在我们的本地机器上， 我们可以使用perldoc命令来阅读模块的文档。我们把感兴趣的模块的名称给它，它就会帮我们输出模块的文档。   

```perl
NAME	fileparse − split a pathname into pieces 
	basename − extract just the filename from a path 
	dirname − extract just the directory from a path
	SYNOPSIS	use File::Basename;
	($name,$path,$suffix) = fileparse($fullname,@suffixlist)    
	fileparse_set_fstype($os_string);	$basename = basename($fullname,@suffixlist);	$dirname = dirname($fullname);
```    

我们把文档的顶部的那段包含了进来是为了向你展示最重要的部分(至少是在你刚开始的时候是最重要的)。模块的文档一般都会遵循过去的unix主页的格式， 也就是以NAME还有SYNOPSIS部分开始。   

大纲部分给出了模块使用的例子。如果我们能够停止一会儿理解， 然后跟着例子来， 我们就可以使用某个模块了。也就是说，可能你还不是很熟悉大纲中的某些Perl的技巧和语法，但是你可以仅仅是跟着例子来然后让一切运行完好。   

现在由于Perl是过程式，函数式，面向对象以及其它的语言类型的综合体， Perl的模块也有着不同接口。我们将会以稍微有点不同的方式来使用这些模块，但是只要我们能够去查阅文档，就应该不会有问题的。   

##功能性接口   
为了加载一个模块，我们使用Perl内建的use。我们在这里不会进入所有具体的细节，但是在第10章还有第15章我们会的。现在我们只是想使用模块。让我们以File::Basename这个核心发布版本中的模块来开始。为了把它加载到我们的脚本中去， 我们来：

```perl
use File::Basename;
```   
当我们这么做的时候， File::Basename向我们的脚本中引进三个子例程，fileparse, basename 以及 dirname， 从此刻起， 我们可以这么来:   

```perl
my $basename = basename( $some_full_path );
my $dirname = dirname( $some_full_path);
```   
这就好像是我们自己写了basename还有dirname这两个子例程， 或者它们像是(接近是)内建的Perl函数一样。 这些子程序会把路径名中的文件名还有目录名找出来。例如， 如果 $some_full_path 是 D:\Projects\IsIandRescue\plan7.rtf(假定程序是在windows机器上运行的), 那么$basename将会是plan7.rtf, $dirname将会是D:\Projects\IsIandRescue。    

File::Basename这个模块自己会知道它是在何种机器上运行的, 因此它的函数能够明白怎么正确地针对我们可能遇到的分隔符来解析字符串。   

然而，假定我们已经有了一个叫dirname的子程序， 现在我们就会用File::Basename中的定义把它覆盖掉了. 如果我们已经开启了warnings，我们将会看到一个消息声明。否则的话，Perl就完全地不关心了。   

##选择引入什么   

幸运的是， 我们可以告诉use操作通过在模块名的后面明确一组子程序的名字，也叫做引入列表， 来限制它的行为:   

```perl
use File::Basename('fileparse', 'basename);
```   
现在这个模块仅仅给我们提供了两个子程序， 不会干扰我们自己的dirname子程序了。当然，那样输入起来很别扭, 所以更经常的我们看到的是用引用字操作符写出来的形:   

```perl
use File::Basename qw(fileparse basename);
```   
事实上，即使只有一个条款，为了连贯还有维护我们也倾向于用qw()列表来写出来；经常地我们会返回去说"在这了再给我加一条", 这个时候如果已经是个qw()列表的话会更容易的。   

我们已经保护了本地的dirname子程序，但是如果我们依然想要File::Basename提供的功能呢？没问题，我们只要用它的完整的包的指定形式写出来就可以了：  

```perl
my $dirname = File::Basename::dirname($some_path);
```   
use后面的一组名字不会改变到底有哪些子程序在模块的包中定义好了(在我们的情况下是File::Basename)。 我们总是可以使用完整的包的名字的形式而不用管引用列表， 就如同下面一样:   

```perl
my $basename = File::Basename::basename($some_path);
```   

在极端的情况下(但是极其的有用)，我们可以指定为引用列表制定一个空的列表， 如下： 

```perl
use File::Basename();
my $base = File::Basename::basename($some_path);
```   
一个空的列表和一个缺失的列表是有所不同的。 一个空的列表意味着"不要给我任何的东西", 而一个缺失的列表意味着给我默认的"。如果模块的作者做的很好的话，默认的情况就是我们所需要的。  

##面向对象接口    

通过看下File::Spec模块， 我们来比较下File::Basename引入的子程序和其之间的区别。File::Spec模块是设计来支持通常作用在文件指定上的操作的。(一个文件指定通常是一个文件或者一个路径名，但它可能是一个不存在的文件-在这种情况下，它就不是一个真正的文件名，对不对？) 

同File::Basename模块不同的是，File::Spec有着一个主要的面向对象接口。如同我们之前的那样， 我们也用use来加载模块:  

```perl
use File::Spec;
```   
然而，由于这个模块有着面向对象的接口，它不支持任何的子程序。作为替代，这个接口告诉我们使用它的类方法来获取它的模块的功能。catfile方法把一组字符串用合适的目录分割符来连接起来:    

```perl
my $filespec = File::Spec->catfile( $homedir{gilligan}, 'web_docs', 'photos',           	'USS_Minnow.gif');
```  
这样就会调用File::Spec类中的catfile类方法， 它会构造一个适合于本地的操作系统的路径然后返回一个单一的字符串。 在语法上这同File::Spec所提供的将近两打的其他的操作是相似的。  

File::Spec模块以一种可移植的方式为处理文件路径提供了好几个其他的方式。 你可以在perlport文档中阅读更多的关于可移植性的问题。   

##一个更典型的面向对象模块:Math::BigInt   

由于File::Spec模块没有对象，为了不被它看起来非面向对象的特征所失望，让我们看一下另外的一个核心的模块，Math::BigInt, 他可以在Perl的一般能力范围之外处理整数。   

```perl
use Math::BigInt;
my $value = Math::BigInt->new(2); #以2开始；
$value->bpow(1000);   			   #2**100-
print $value->bstr(), "\n"; 	   #打印出来
```  
同之前的一样，这个模块什么都没有引入。它的完整的接口使用类方法，诸如new, 接在类名后面来生成实例，然后接在这些实例之后调用实例方法，像bpow还有bstr。   

##详尽的Perl存档网络(CPAN)   

(未翻!)   
 
 
##从CPAN来安装模块   

从CPAN来安装一个简单的模块可以是很直接的：我们下载模块发布版本的存档，解压出来，切换到它的目录中去。 我们在这儿使用wget，但其实你使用哪个工具是无关紧要的。

```perl
% wget http://www.cpan.org/.../HTTP−Cookies−Safari−1.10.tar.gz 
% tar −xzf HTTP−Cookies−Safari−1.10.tar.gz% cd HTTP−Cookies−Safari−1.10
```  
从那儿起我们可以走两条路中的一种。如果我们找到一个叫Makefile.PL的文件，我们可以运行下面的命令来build, test还有最终的安装这个源码:   

```perl
% perl Makefile.PL % make% make test% make install
```   
如果你没有权限在系统范围的目录中安装模块，我们可以通过使用PREFIX参数来告诉Perl在别的路径下安装：  

```perl
% perl Makefile.PL INSTALL_BASE=/Users/home/Ginger
```   
为了让Perl在那个目录中寻找模块，我们可以设置PERL5LIB环境变量。Perl会把那些目录添加到它的模块搜获列表中去。

```perl
% export PERL5LIB=/Users/home/Ginger 
```  
我们也可以使用lib指令来添加到模块搜索路径中去，尽管这看起来不是很友好，因为我们得改变代码，但也因为可能它不是我们在其他的我们想要代码跑起来的机器上的路径:  

```perl
#!/usr/bin/perluse lib qw(/Users/home/Ginger);
```  
先后退一小会儿，如果我们找到的是Build.PL这个文件而不是Makefile.Pl这个文件，过程将会是一样的。 这些发布版本使用Module::Build来build还有install代码。由于Module::Build不是核心的Perl模块，我们得在我们能够安装使用它的发布版本之前安装它:  

```perl
% perl Build.PL% perl Build% perl Build test% perl Build install
```   
为了用Module::Build安装到我们的私有的目录，我们添加 --install_base 参数。我们以和前面的同样的方式告诉Perl如何来找到模块:  

```perl
% perl Build.PL −−install_base /Users/home/Ginger
```   
有的时候我们会在一个发布版本中看到Makefile.PL还有Build.PL这两个文件。那个时候我们该怎么做呢？我们可以使用任意一个。选择你最喜欢的来玩！  

##在合适的时间来设定路径  

Perl通过在特殊的Perl数组@INC中定义的路径来查找模块。use声明在编译时执行，所以它会在编译时查看模块搜索路径@INC。除非我们把@INC考虑在内，否则那会以一种很难理解的方式让我们的程序崩溃掉。   

例如，假设我们有自己的目录/home/giliigan/lib, 我们把自己的模块Navigation::SeatOfPants放在/home/gilligan/lib/Navigation/SeatOfPants.pm里。当我们加载自己的模块的时候，Perl就找不到了。 

```perl
use Navigation::SeatOfPants;
```    
Perl会向我们抱怨它在@INC中找不到模块， 并且会展现给我们看在那个数组里的所有的路径:    

```perl
Can't locate Navigation/SeatofPants.pm in @INC (@INC contains: ...)
```   
你可能会想我们应该仅仅在调用use之前把我们的模块的路径添加到@INC中去。然而，即使添加如下的东西:  

```perl
unshift @INC, '/Users/gilligan/lib'; # 崩溃use Navigation::SeatOfPants;
```  
也不会起作用的。为什么呢？因为unshift在运行时才起作用，这是use在编译之后的很长时间才发生的。这两个声明在词法上很接近， 但是在时间上并不接近。仅仅因为我们把它们写在了一块并不表示它们是以那样的顺序来执行的。我们想在use执行前改变@INC。一种处理这个的方式是在unshift周围添加一个BEGIN块:    

```perl
BEGIN { unshift @INC, '/Users/gilligan/lib'; }use Navigation::SeatOfPants;
```   
现在这个BEGIN块就会在编译时编译还有运行了, 会接下来的use设置合适的路径。   

然而，这很烦人而且需要的解释可能超出了你觉得舒服的范围了，尤其是对于那些后来的可能需要维护修改你的代码的人。让我们以一种我们之前用过的一种简单的声明来代替那一团东西:  

```perl
use lib '/Users/gilligan/lib';use Navigation::SeatOfPants;
```   
这里， lib声明会接收一个或者多个参数然后把它们添加到@INC数组的开头，就如同之前的unshift所做的。这是行得通是因为它是在编译时执行的，而不是在运行时。因此它对紧接着的use是适时的。 

一个use lib声明通常总是有一个地址依赖的路径名，一般情况下我们鼓励大家把它放到文件的开头的部分。这样当我们得移动文件到一个新的系统或者lib的路径有变化的时候，我们在找的时候还有更新的时候会方便点的。(当然，如果我们能够在标准的@INC地址中安装我们的模块的话，我们就可以避免使用use lib了， 但那并不总是实际的.)    

要把use lib想成是“使用这个路径来找到我的库(还有模块)” 而不是使用这个目录。很经常的，我们会看到如下的代码:     

```perl
use lib '/Users/gilligan/lib/Navigation/SeatOfPants.pm'; # 错误
```   
然后这个程序要会想为什么没有把定义给加载进来. 要注意use lib事实上是在编译时运行的，所以下面的也是不会起作用的:   

```perl
my $LIB_DIR = '/Users/gilligan/lib';...use lib $LIB_DIR; # 崩溃use Navigation::SeatOfPants;
```  
当然，Perl在编译时就会建立起$LIB_DIR的声明（所以用use strict的时候我们是不会得到错误警告的，尽管真正的use lib是会抱怨的)， 但是真正的/home/gilligan/lib的值是直到运行时才会赋值的。呀，又太迟了。  

此时此刻，我们得在BEGIN块里放进一些东西，或者依靠另一个编译时操作:用use constant来设置一个常数:    

```perl
use constant LIB_DIR => '/Users/gilligan/lib';...use lib LIB_DIR;use Navigation::SeatOfPants;
```  
啊哈，又解决了。就是这个样子了，除非我们需要模块依赖一个计算的结果。(啥时该休止啊，快来人让这个疯狂的行为停止掉吧!)这应该会解决99%我们的需要了。  

##解决模块的依赖性  

我们刚刚看到如果我们想要安装一个需要使用Module::Build的模块，我们得先安装Module::Build。那只是令我们头疼的依赖性问题中的很小的一个例子了。 我们可能得安装好几个其他的模块，它们当中的每一个又都反过来得依赖更多的模块。   

幸运的是， 我们有工具来帮助我们。CPAM.pm模块自从Perl5.004就是核心发布版本的一个部分了。它给了我们一个交互的安装shell.

```perl
$ perl -MCPAN -e shell
cpan shell --CPAN exploration ....
Readline support 

cpan>
```  
为了安装一个模块还有它的依赖，我们使用命令install然后跟着模块的名字.现在CPAN.pm处理所有的下载，解压，building, 测试嗨哟安装模块的过程， 而且它会递归地处理那些依赖:

```perl
cpan> install CGI::Prototype
```   
只是那也太多了，所以Brian创建了一个脚本cpan，它也是跟着Perl发行版本的。我们只要把我们想要安装的模块列出来，它就会帮我们处理接下来的情况了:  

```perl
cpan CGI::Prototype HTTP::Cookies::Safari Test::Pod
``` 

另一个很酷的工具是CPANPLUS，是CPAN.pm的完全的重写，但是在我么写作本书的时候它还不是核心发布版本中的一部分.   

```perl
$ perl -MCPANPLUS -e shell
CPAN Terminal>
```  

为了安装一个模块，我们使用i命令.  

```perl
CPAN Terminal> i CGI::Prototype
```   

CPANPLUS模块带了一个很方便的脚本，叫cpanp。我们我们给它i开关还有一组模块，它就会像之前那样安装它们了    

```perl
cpan i CGI::Prototype HTTP::Cookies::Safari Test::Pod
```  

##练习   
(未翻)

 
























