---
layout: post
subtitle: "Where's the manual?"
date: "2016-01-06"
published: true
title: "Authentication with Meteor, Angular and Ionic"
---

Well, the Meteor authentication works out of the box and it's great but what if you want to use it with [Angular-Meteor](http://www.angular-meteor.com/) package and Ionic. I had to do that recently and it tooke me a while and gave me some grief but in the end it came out to be pretty simple. So let me share my secret recepie with you.

I looked at the following tutorials initially to see how I would be able to achieve this:

- [Step 8 - User accounts, authentication and permissions](http://www.angular-meteor.com/tutorials/socially/angular1/user-accounts-authentication-and-permissions)
- [Meteor Accounts with custom UI Tutorial](https://www.codetutorial.io/meteor-accounts-custom-ui-tutorial/)
- [Meteor Ionic Basic Accounts Demo](https://github.com/aaronksaunders/meteor-ionic-demo2/blob/master/README.md)
- [UserAccounts for Meteor](https://useraccounts.meteor.com/)


#### So do I really have to have custom UI for the Ionic project? Is that the only way?
ehhh... no... unless you really really want to create one and if you do then please share your solution in the comments below. It would be great to see another alternative.

#### So what's your solution dude?
Include the following packages. The key ingredient is Urigo's [Angular-blaze-template](https://github.com/Urigo/angular-blaze-template/) package.

```
urigo:angular-blaze-template
accounts-password
useraccounts:ionic
```

Add a **authentication-template.hooks.js** file in your client folder.

```
angular
    .module('yourModule')
    .run(function ($ionicHistory, $state) {
		AccountsTemplates.options.onSubmitHook = onSubmitHook;
		AccountsTemplates.options.onLogoutHook = onLogoutHook;
		
		//////////////////
		function onSubmitHook(error, state) {
			if (!error) {
				if (state === "signIn" || state === "signUp") {
					$ionicHistory.nextViewOptions({
						historyRoot: true
					});

					$state.go("logged-in-greeting-page");
				}
			}
		}

		function onLogoutHook() {
			$ionicHistory.nextViewOptions({
				historyRoot: true
			});

			$state.go("login");
		}

    });
```

Include the authentication form in your login page:

```
<ion-view title="Login" class="pane-login" hide-nav-bar="true">
    <ion-content padding="false">
    	<!-- INCLUDE THE FOLLOWING IN YOUR VIEW -->
        <blaze-template name="atForm"></blaze-template>
    </ion-content>
</ion-view>
```

For more information about what forms are available and other UserAccounts options have a look at their [documentation](https://github.com/meteor-useraccounts/core/blob/master/Guide.md).

Also, you probably also want to configure your account templates. I included this in my **lib/authentication/account-template.config.js**.

```
AccountsTemplates.configure({
    //defaultLayout: 'emptyLayout',
    showForgotPasswordLink: false,
    overrideLoginErrors: true,
    enablePasswordChange: true,
    sendVerificationEmail: false,

    //enforceEmailVerification: true,
    //confirmPassword: true,
    //continuousValidation: false,
    //displayFormLabels: true,
    //forbidClientAccountCreation: false,
    //formValidationFeedback: true,
    //homeRoutePath: 'paaths',
    //showAddRemoveServices: false,
    //showPlaceholders: true,

    negativeValidation: false,
    negativeFeedback: false,
    positiveValidation: false,
    positiveFeedback: false,

    // Privacy Policy and Terms of Use
    //privacyUrl: 'privacy',
    //termsUrl: 'terms-of-use',
	
	// onSubmitHook: mySubmitFunc
});
```

#### Checkout this code in use in my side project
[Sehaj Paath Tracker Source Code](https://github.com/kmlprtsng/SehajPaathTracker)

[Sehaj Paath Tracker Demo](http://sehajpaathtracker.meteor.com/)

#### Feedback
I am no expert in Meteor and Ionic so if you have any improvements to suggest or you apperciate this article then please leave a comment below :-).
