---
layout: post
title: "Dancer::Introduction Notes"
date: 2014-06-16 00:05:17 +0800
comments: true
categories: Dancer
---

1.A route pattern can contain one or more tokens, and tokens can be optional.

```perl
get '/hello/:name?' => sub {
    "Hello there " . (param('name') || "whoever you are!");
};
```  

2.A route can contain a wildcard (represented by a '*'). Each wildcard match will be returned in an arrayref, accessible via the `splat' keyword:

```perl    
get '/download/*.*' => sub {
    my ($file, $ext) = splat;
    # do something with $file.$ext here
};    
```

3.A route can be defined with a Perl regular expression. In order to tell Dancer to consider the route as a real regexp, the route must be defined explicitly with qr{}, like the following:

```perl
get qr{/hello/([\w]+)} => sub {
    my ($name) = splat;
    return "Hello $name";
};
```  

4.Routes may include some matching conditions (on the useragent and the hostname at the moment):     
  
```perl    
get '/foo', {agent => 'Songbird (\d\.\d)[\d\/]*?'} => sub {
  'foo method for songbird'
}
 
get '/foo' => sub {
  'all browsers except songbird'
}
```  

5.An action can choose not to serve the current request and ask Dancer to process the request with the next matching route. This is done with the pass keyword, like in the following example:    

```perl
get '/say/:word' => sub {
    return pass if (params->{word} =~ /^\d+$/);
    "I say a word: ".params->{word};
};
 
get '/say/:number' => sub {
    "I say a number: ".params->{number};
};
```   

6.Before hooks, after hooks, before_template_render hooks. 

7.You can use the load method to include additional routes into your application.

8.A Dancer application can access the information from its config file easily with the config keyword:    

```perl    

get '/appname' => sub {
    return "This is " . config->{appname};
};
```   

9.In order to enable the logging system for your application, you first have to start the logger engine in your config.yml:   

```perl
logger: 'file'
```

10.Dancer configures the Template::Toolkit engine to use <% %> brackets instead of its default [% %] brackets, although you can change this in your config file. Of course you have to import the "Template" module.  

11.A layout is a special view, located in the 'layouts' directory (inside the views directory) which must have a token named `content'. That token marks the place where to render the action view. This lets you define a global layout for your actions. Any tokens that you defined when you called the 'template' keyword are available in the layouts, as well as the standard session, request, and params tokens. This allows you to insert per-page content into the HTML boilerplate, such as page titles, current-page tags for navigation, etc. (refer to the standard document for more details).

12.Through  "set serializer => 'JSON';"  we can do data serializer;