# Switchboard - easy A/B testing for your mobile app
---

## What it does

A/B testing and feature flags for Android built on top of [Switchboard](https://github.com/KeepSafe/Switchboard). 

Use Switchboard to
* Stage-rollout new features to users
* A/B-test user flows, messaging, colors, features, etc.
* Add a feature flag to anything you want to remotely enable/disable

Switchboard lets you control what happens in your app. Quick, easy, useful.

Additionally, Switchboard segments your users consistently; because user segmentation is based upon a UUID that is computed once, the experience you switch on and off using Switchboard is consistent across sessions.

## What it does not do (i.e. what you have to do yourself)

Switchboard does not give you analytics, nor does it automatically administer and optimize your A/B tests. It also doesn't give you nice graphs and stuff. You can get all of that by plugging an analytics package into your app which you're probably doing anyway.

## Features

* Highly scalable and incredibly lightweight
* Consistent user segmentation based off a computed UUID
* Define experiments for specific application versions, OS version, language settings and more
* Comes with built-in configurations for production and staging environment
* Preserves state when device is offline; configurations are cached on clients across sessions
* Flexible custom parameters for experiments

## What Switchboard was designed for

Switchboard was designed as a super lightweight and flexible mobile A/B testing framework. 

### Infrastructure

The goal was to serve millions of requests very reliablly without much infrastructure. It should easily scale horizontally to avoid overhead in maintaining it while your application scales. It is designed without a database or any other type of persistent storage that would slow it down.

### User segmentation
Consistency in user segmentation is one of the most important things in A/B testing. This means that one individual user will always have a consistent experience over a long period of time. 

Switchboard does consistent user segmentation based on a unique device id.

## How to use it

Link the Switchboard project to your Android project as a library project. You only need to initialize the Switchboard core at the application start once. 

Then, you can add switches to your app and have the Switchboard give you the current state.

You can customize the DynamicConfigManager to send all sorts of information to the Switchboard server for control decisions, e.g. location, OS version, device, language.

Here's some on/off switch example code on Android:

```java
Context myContext = this.getApplicationContext();
String experimentName = "showSmiley";

//get settings from Switchboard
boolean isSmiling = Switchboard.isInExperiment(myContext, experimentName);

//Switching code for testing
if (isSmiling) //variant A
	showSmileyWelcomeMessage();
else //variant B
	showFrownyFace();
```

And it works for varying any value too:

```java
if (isSmiling) {
	if(Switchboard.hasExperimentValues(myContext, experimentName)) {
		
		//get remote controlled values from Switchboard
		JSONObject smileValues = Switchboard.getExperimentValueFromJson(myContext, experimentName);

		int smileWidth = smileValues.getInt("width");

		//do something with it
		prepareSmiley(smileWidth);
		showSmileyWelcomeMessage();
	}
}
```

## More information about it:

* [Keepsafe Engineering Blog](https://medium.com/keepsafe-engineering/a-b-testing-for-mobile-apps-made-easy-348b68e68362#.j7f2x848n)
* [Quora](http://qr.ae/TUTJcZ)

## Problems & Bugs

Please report issues in the [Issues](https://github.com/KeepSafe/Switchboard-Android/issues) area above.

## License
Switchboard is licensed under the [Apache Software License, 2.0 ("Apache 2.0")](http://www.apache.org/licenses/LICENSE-2.0)

## Authors

Switchboard is brought to you by [Philipp Berner](https://github.com/philippb) and [Zouhair Belkoura](https://github.com/zouhairb), founders of Keepsafe, and the rest of the [Keepsafe team](https://www.getkeepsafe.com/about.html). 

We'd love to have you contribute or [join us](https://www.getkeepsafe.com/careers.html)!

## Used in production for many millions of users

* Keepsafe (www.getkeepsafe.com)
