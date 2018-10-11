---
layout: post
title: "named arguments"
date: 2014-09-10 15:58:10 +0800
comments: true
categories: Perl
---
For named argument, it many uses the trick of changing a list into a hash. Take a look at the following code.  

```pl
listdir(cols=>4, page=>1, hidden=>1, sep_dirs=>1);    

sub listdir {
	%arg = @_;# Convert argument list to hash

	$arg{match} = "*" unless exists $arg{match}; 
	$arg{cols} = 1unless exists $arg{cols};# etc.# Use arguments to control behaviour...	@files = get_files( $arg{match} );	push @files, get_hidden_files() if $arg{hidden}; # etc.}
```   

Apart from documenting the call better, this approach has another important advantage. Since the entries of a hash can be initialized in any convenient order, we no longer need to re- member the order of the nine potential arguments, as long as we remember their names. In addition, because hashes are flattened inside lists, if we have several calls that require the same subset of arguments, we can store that subset in a separate hash and reuse it:    

```pl
%std_listing = (cols=>2, page=>1, sort_by=>"date");   

listdir(file=>"*.txt", %std_listing);     
listdir(file=>"*.log", %std_listing);      
listdir(file=>"*.dat", %std_listing);
```    

We can even override specific elements of the standard set of arguments, by placing an explicit version after the standard set. Then the explicit version will reinitialize (i.e., overwrite) the corresponding entry in the hash:      

```pl
listdir(file=>"*.exe", %std_listing, sort_by=>"size");
```    

This idea of a standard argument set, overridden by explicitly specified arguments, can also be used within the subroutine to simplify the handling of default values. For example:   

```pl
sub listdir {	%defaults = (match=>"*", cols=>1, sort_by=>"name"); %arg = (%defaults, @_);	# Use arguments to control behaviour...		# etc.}
```   
In this version, the default values are stored in the %defaults hash, and are then flat- tened into the list used to initialize the %arg hash. The default values appear first in the ini- tializer list. Any entry of the same name passed in via @_ will therefore overwrite the corresponding entry in %arg, replacing the default value with the user-specified one. As a final optimization, the default hash could be moved outside listdir, so that it need only be ini- tialized once, before the program runs, rather than each time listdir is called:    

```pl
%defaults = (match=>"*", cols=>1, sort_by=>"name");sub listdir {	%arg = (%defaults, @_);	# etc.}
```