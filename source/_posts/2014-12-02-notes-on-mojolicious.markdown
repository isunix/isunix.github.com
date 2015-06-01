---
layout: post
title: "notes on mojolicious"
date: 2014-12-02 20:52:52 +0800
comments: true
categories: Mojo
---
Will keep notes of some of the mojo tips I got.

1.A helper command to generate app for us.

```pl
mojo generate app
```
This will generate Mojolicious application directory structure.

```pl
mojo generate lite_app
```
This will generate Mojolicious::Lite application for us.

```pl
mojo generate lite_app hello
``` 
This will generate the app with the name "hello"

2.about deploying your app to heroku

```pl
cpanm Mojolicious::Command::deploy::heroku
mojo generate lite_app bigfan
./bigfan deploy heroku --create
or we can assign our app name like the following:
./bigfan deploy heroku -n bigfan
```

3.In mojo, something like "hello.html.ep", here "ep" stands for "embedded perl", we can have html.ep, json.ep, txt.ep.

4.Three kinds of placeholders.

generic placeholders:

```pl
get '/:fname/:lname' => sub{
	shift->render('capture);
};
```

relaxed placeholders: 

```pl
get '/:fname/(.lname)' => sub{
	shift->render('capture);
};
```

wildcard placeholders:

```pl
get '/:fname/(*lname)' => sub{
	shift->render('capture);
};
```



