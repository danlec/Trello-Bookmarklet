This is a bookmarklet you can use to add

 - FogBugz cases
 - JIRA issues
 - GitHub issues
 - The selected text from an arbitrary URL

to a board in <a href="https://trello.com">Trello</a>

To use the bookmarklet, run the source through a javascript minifier 
(e.g. the <a href="http://closure-compiler.appspot.com/home">Closure Compiler</a>), 
prepend `javascript:` to the front, and add it as the location of a bookmark.

The first time you run it on a site, it will walk you through a simple setup:

 1. Input your API Key (which you can get at https://trello.com/1/appKey/generate)
 2. Authorize the site to interact with Trello
 3. Select the list that you'd like the bookmarklet to add cards too

You'll only need to go through those steps once per domain; from then on, you should be able to send your
issues/cases/whatever directly to Trello in a single click.