mapzen map scarab
=================

Branding, social sharing, and tracking UI component for standalone demos.

**NOTE:** Standalone usage is **deprecated.**

This module was originally called a “bug,” a term borrowed from broadcast television (officially, [“digital on-screen graphic”](http://en.wikipedia.org/wiki/Digital_on-screen_graphic)) where a show is branded in the lower corner to identify the broadcast network. Because of the other meaning of “bug” in computing, this is now called `scarab`.

![screenshot](https://cloud.githubusercontent.com/assets/2553268/7524364/87423646-f4cf-11e4-897f-df25b01ec905.png)

**NOTE:** We have updated this to display the current brand imagery of Mapzen.

The scarab is designed for the following functionality:

1. __Branding:__ Show the Mapzen attribution and provide a link to our website.
2. __Sharing:__ Provide UI for viewers to easily share via social networks.
3. __Tracking:__ Tracks interactions through Google Analytics.

This is as a standalone, drop-in JavaScript “library”. It has no hard dependencies (jQuery is not required) and should work on all modern browsers and IE9+ at minimum, although in practice, the demos will be driving the minimum compatibility of the page.

## Including the scarab (deprecated)

Standalone JS is not currently published.

Instantiate the scarab in JavaScript:

```js
var scarab = new MapzenScarab();
```

The scarab works without any additional configuration, but you can customize its behavior with by passing in an object like so:

```js
var scarab = new MapzenScarab({
  name: 'Tangram',
  link: 'https://mapzen.com/projects/',
  tweet: 'Wow, what a cool WebGL map renderer by @mapzen!',
  repo: 'https://github.com/tangrams/tangram/'
});
```

### Basic options

These are optional. Defaults will be provided if not set.

key       | default value         | description
----------|-----------------------|-------------
__link__  | 'https://mapzen.com/' | _String._ URL to go to when viewer clicks on the Mapzen logo. This should be a valid absolute URL.
__name__  | 'Mapzen demo'         | _String._ Name of the demo or product. This will be used in analytics tracking and pre-populating tweets.
__tweet__ | (depends)             | _String._ Set a custom pre-written tweet message. The current URL of the page will be automatically appended to the end of the message. If not included, a default tweet (based on the _name_ option, if provided) will be used. ([see below](#twitter))
__repo__  | 'https://github.com/mapzen/' | _String._ URL to source code repository. This should be a valid absolute URL. The logo is the GitHub logo but it won't magically prepend the GitHub domain for you.


### Advanced options

key           | default value         | description
--------------|-----------------------|-------------
__analytics__ | true                  | _Boolean._ Whether to send custom tracking events to Google Analytics for this demo. Set to false to prevent this demo from sending events or loading Google Analytics (if not already present). If Google Analytics is loaded separately, it behaves normally (as if the bug is not there).

## Features

### Automatic iframe detection

The scarab detects if the page being viewed is in an iframe or not. If it is in an iframe, it naively assumes that its parent page is giving the demo proper context, so its script stops executing immediately and does nothing else.

### Google Analytics event tracking

If Google Analytics is detected on the page, the scarab will send [custom tracking events](https://developers.google.com/analytics/devguides/collection/gajs/eventTrackerGuide) to it.

If Google Analytics is not detected on the page, the scarab will insert Google Analytics, reporting to the Mapzen website's analytics property.

You can use the options property `analytics: false` to disable event tracking or loading a fallback Analytics.

The following events are currently tracked:

- The scarab is active (that is, the viewer has opened this page outside of an iframe)
- If the scarab is loading its own Analytics property
- The viewer has clicked the Mapzen logo (which opens the Mapzen website or the URL provided in the `link` option)
- The viewer has clicked the Twitter icon
- The viewer has clicked the Facebook icon

### Custom styling

The scarab loads an external stylesheet. Elements created by the scarab have class names attached (prefixed in the `.mz-bug-*` namespace), so you can override the preset styles if you wish. However, this is generally discouraged since we can't guarantee that class names or styles will be backwards-compatible forever.

### Social network sharing

Currently, sharing functionality is borrowed from [RRSSB](https://github.com/kni-labs/rrssb), the library used to create the social sharing buttons used on the Mapzen [blog](https://mapzen.com/blog/).

#### Twitter

You may specify what the pre-filled tweet message is with the `tweet` option. If you don't set it, the default values are:

- If the `name` option is set, the pre-filled tweet is "_name_, powered by @mapzen"
- If the `name` option is _not_ set, the pre-filled tweet is "Check out this demo by @mapzen!"

Tweets automatically include the viewer's current URL (including hash data), so there is no need to provide this yourself.

#### Facebook

Facebook sharing is currently done via “[sharer.php](http://www.joshuawinn.com/facebooks-sharer-php-longer-deprecated-2014/)” which is actually their legacy endpoint for sharing things. (Normally, they would require an app id, which is difficult to set up for each individual demo.) Unfortunately, it's not very “smart.” So there is no pre-populated Facebook sharing message, for example.

It *will* automatically link to the viewer's current URL (including hash data).

If you want to customize the image, title, and description that appears in the Facebook post, you will need to add OpenGraph `meta` tags into the `head` of your demo page. [Read the Facebook documentation for more information.](https://developers.facebook.com/docs/sharing/best-practices#tags)

#### Other sharing options

Other sharing options are not currently planned.


## Building

There is no build process for this. Please import and conduct minification etc. downstream.
