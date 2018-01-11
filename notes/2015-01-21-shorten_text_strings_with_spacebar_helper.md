title: Shorten text strings with spacebar helper
date: 2015-01-21
tags: Meteor.js, Node.js, programming, webdev, web development, JavaScript, fullstack

## Shorten Your title / name / link (You name it!) strings with spacebar helper

If You're building some lists view (e.g. posts list) and You want to shorten their names You can achieve that using this UI helper:

```
UI.registerHelper('shortIt', function(stringToShorten, maxCharsAmount){
	var shorter = stringToShorten.substr(0, maxCharsAmount);

	shorter = shorter.substr(0, Math.min(shorter.length, shorter.lastIndexOf(' '))) + '...';
	return shorter;
});
```

It will cut the string to the (whole) word placed after last space character.

Example usage:

```
{{#each PostList}}
	{{shortIt this.title 15}}
{{/each}}
```

And that's it! Enjoy!

-- mrmnmly