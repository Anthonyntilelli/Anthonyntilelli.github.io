---
layout: post
title:      "Javascript in the Browser(s)"
date:       2020-08-29 11:20:03 -0400
permalink:  javascript
---


JavaScript runs different across browser vendors, versions, and extensions, making it difficult to determine if code will run as intended.  To minimize the chances of an issue, we must employ strategies:

- Learn about the audience we will be targeting.
- Converting newer syntax to older, more adopted versions and add new functions if needed.
- Check for the existence of specific browser APIs before using it.

## Get to know your Audience

Selecting who will use your website is one of the first steps to inform its design. Designing for the general public have different considerations than a corporate only audience. The general public will generally use a variety of browsers and technology stack while a corporate environment will be more uniform.

If you do not already have a website and traffic, it is helpful to look at globals [stats tracker](https://gs.statcounter.com/browser-market-share) or [similar sites](https://www.w3counter.com/globalstats.php). Once you have your website and traffic, you can use analytics tools to analyze your usage.

While it may be tempting to try and target 100% of all users' configurations, it can be exceedingly difficult. Setting reasonable requirements will help with sanity and ensure a stable product. Once you have browser data, you can look into what the oldest required browser supports. Site such as [CanIuse](https://caniuse.com/) or [MDN](https://developer.mozilla.org/en-US/) will show how browser adoption. For example, [BigInt](https://tc39.es/ecma262/#sec-bigint-objects) is, at this time, at a [lower adoption](https://caniuse.com/#search=BigInt) and should likely be avoided to be relied on.

## Converting modern JS to browser friendly code

You may still want to use modern syntax and functions in javascript in your development to take advantage of advancements. [BabelJS](https://babeljs.io/) will transpile your code into browser-friendly syntax. Additionally, BabelJS will let you take advantage of non-ECMAScript standard javascript syntax, such as type-checking offered by [Facebook Flow](https://flow.org/) and React JSX.

If you need to use a function that is not defined om older browsers, then a [Polyfills](https://en.wikipedia.org/wiki/Polyfill_(programming)) can be used to add it.  Polyfills are libraries that check for a set of functionally, and if it doesn't exist, it will add it's version, for example, [Fetch Polyfill](https://github.com/github/fetch). Since polyfill requires users to download additional files and run more code, it can slow down the start-up of a user's experience, and its usage should be strategic.

### [Babel Js example](https://babeljs.io/docs/en/index.html)

```js
// Babel Input: ES2015 arrow function
[1, 2, 3].map((n) => n + 1);

// Babel Output: ES5 equivalent
[1, 2, 3].map(function(n) {
  return n + 1;
});

```

## Checking for browser support

Even when using BabelJS and Polyfill, specific API may be missing or not add-able via polyfills, such as [WebStorage API/Cache](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Client-side_storage) and [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers). In this case you will need a test for the supportability at runtime. If WebStorage API is not available, you may want to store your data in cookies.  ServiceWorkers availability can vary based on many factors, such as secure context and if the user is in private browsing mode (firefox).

### Example of [Testing for WebStorage](https://www.w3schools.com/html/html5_webstorage.asp)

```js
if (typeof(Storage) !== "undefined") {
  // Code for localStorage/sessionStorage.
} else {
  // Sorry! No Web Storage support..
}
```

### Example of [Testing for Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/serviceWorker)

```js
if ('serviceWorker' in navigator) {
  // Supported!
}
```

