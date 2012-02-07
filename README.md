```javascript
javascript:(function(a){window.trelloAppKey="optional";window.trelloIdList="optional";var b=a.createElement("script");b.src="https://raw.github.com/danlec/Trello-Bookmarklet/master/trello_bookmarklet.js";a.getElementsByTagName("head")[0].appendChild(b)})(document);
```

This is a <a href="http://en.wikipedia.org/wiki/Bookmarklet">bookmarklet</a> you can use to create a card in <a href="https://trello.com">Trello</a> from ...

 - FogBugz cases
 - JIRA issues
 - GitHub issues and commits
 - The selected text from an arbitrary URL
 - ... more?  I'm happy to take pull requests that add support for other websites!

The first time you run it on a site, it will walk you through a simple setup:

 1. Input your API Key (which you can get at https://trello.com/1/appKey/generate)
 2. Authorize the site to interact with Trello
 3. Select the list that you'd like the bookmarklet to add cards too

You'll only need to go through those steps once per domain; from then on, you should be able to send your
issues/cases/whatever directly to Trello in a single click.

The card created in Trello will 

- attempt to use the name of the FogBugz/JIRA/GitHub/etc case
- include a link to the case in the card description
- (optionally) include any selected text in the description

If you modify the unminified bookmarklet, you can re-build it by running the source through a javascript minifier 
(e.g. the <a href="http://closure-compiler.appspot.com/home">Closure Compiler</a>), 
and prepending `javascript:` to the front.

If you'd rather not add your appKey and idList for every new domain, you can modify the bookmarklet and include values for `window.trelloAppKey` and `window.trelloIdList` (currently both have the value `"optional"`)

**Note:** This basic concept originated with https://github.com/markdrago/cardorizer; this approach doesn't require you to run a server