---
layout: post
subtitle: "Where's the manual?"
date: "2016-01-06"
published: false
title: "Authentication with Meteor, Angular and Ionic"
---

Well, the Meteor authentication works out of the box and it's great but what if you need to use it with Angular (in particular [Angular-Meteor](http://www.angular-meteor.com/) package) and Ionic. I had to do that recently and it did take me a while and gave me some grief but in the end it came out to be pretty simple.

I looked at the following tutorials:
- [http://www.angular-meteor.com/tutorials/socially/angular1/user-accounts-authentication-and-permissions](http://www.angular-meteor.com/tutorials/socially/angular1/user-accounts-authentication-and-permissions)
- [http://www.angular-meteor.com/tutorials/socially/angular1/user-accounts-authentication-and-permissions](http://www.angular-meteor.com/tutorials/socially/angular1/user-accounts-authentication-and-permissions)
- [https://www.codetutorial.io/meteor-accounts-custom-ui-tutorial/](https://www.codetutorial.io/meteor-accounts-custom-ui-tutorial/)
- [https://github.com/aaronksaunders/meteor-ionic-demo2/blob/master/README.md](https://github.com/aaronksaunders/meteor-ionic-demo2/blob/master/README.md)

#### So do I really have to have custom UI for the Ionic project?
ehhh... no...

#### So what's the solution dude?
Include the following packages:

```
urigo:angular-blaze-template
accounts-password
useraccounts:ionic
```


#### Checkout this code being using in my side project
[Sehaj Paath Tracker](https://github.com/kmlprtsng/SehajPaathTracker)

In Draft.

