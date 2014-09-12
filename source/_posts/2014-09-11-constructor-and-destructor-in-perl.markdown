---
layout: post
title: "constructor and destructor in perl"
date: 2014-09-11 13:46:23 +0800
comments: true
categories: Perl
---
For Perl constructor, we can seperate the process of object creation from the process of initialization.  

```pl
package CD::Music;use strict;sub new {	my $self = {};	bless $self, shift;	$self->_incr_count();	$self->_init(@_);	return $self;}{	my @_init_mems =	qw( _name _artist _publisher _ISBN _tracks _room _shelf _rating );	sub _init {		my ($self,@args) = @_;		my %inits;		@inits{@_init_mems} = @args;		%$self = %inits;	}}
```  



