```javascript
javascript:(function(g){var a,i=g.localStorage;if(i){var h=function(a,b){return 2==arguments.length?i[a]=b:i[a]},j=function(e,b,c){var f=a("<div>").css({background:"#000",opacity:0.75,"z-index":1E4,position:"absolute",left:0,top:0,right:0,bottom:0}).appendTo("body").click(function(){d.remove();f.remove();c(null)}),d=a("<div>").css({position:"absolute",border:"1px solid #000",padding:"16px",width:300,top:64,left:(a(g).width()-200)/2,background:"#fff","z-index":1E5}).appendTo("body");a("<div>").html(e).appendTo(d);
var k=a("<input>").css({width:"100%","margin-top":"8px"}).appendTo(d).toggle(b);a("<div>").text("OK").css({width:"100%","text-align":"center",border:"1px solid #000",background:"#eee","margin-top":"8px",cursor:"pointer"}).appendTo(d).click(function(){var b=k.val();d.remove();f.remove();c(b)});return d};(function(a){var b=function(){a.length&&a.shift().apply(null,Array.prototype.slice.call(arguments).concat([b]))};b()})([function(a){if(g.jQuery)a(null);else{var b=document.createElement("script");b.src=
"http://code.jquery.com/jquery-1.7.1.min.js";b.onload=a;document.getElementsByTagName("head")[0].appendChild(b)}},function(e,b){a=g.jQuery;var c=h("trelloAppKey");c?b(c):j("Please specify your Trello API Key (you'll only need to do this once per site)<br><br>You can get your API Key <a href='https://trello.com/1/appKey/generate' target='apikey'>here</a><br><br>",!0,function(a){a&&b(a)})},function(e,b){a.getScript("https://trello.com/1/client.js?key="+e,b)},function(a,b,c,f){h("trelloAppKey",Trello.key());
Trello.authorize({interactive:!1,success:f,error:function(){j("You need to authorize Trello",!1,function(){Trello.authorize({type:"popup",expiration:"never",scope:{read:!0,write:!0},success:f})})}})},function(e){var b=h("trelloIdList");b?e(b):Trello.get("members/me/boards",{fields:"name"},function(c){$prompt=j('Which list should cards be sent to?<hr><div class="boards"></div>',!1,function(){b=$prompt.find("input:checked").attr("id");e(b)});a.each(c,function(c,d){$board=a("<div>").appendTo($prompt.find(".boards"));
Trello.get("boards/"+d.id+"/lists",function(c){a.each(c,function(c,e){var f=a("<div>").appendTo($board);b=e.id;a("<input type='radio'>").attr("id",b).attr("name","idList").appendTo(f);a("<label>").text(d.name+" : "+e.name).attr("for",b).appendTo(f)})})})})},function(a,b){a&&(h("trelloIdList",a),b(Trello,a))},function(e,b){var c,f=location.href;g.goBug?c=goBug.ixBug+": "+goBug.sTitle:a("#issue_header_summary").length?c=a("#key-val").text()+": "+a("#issue_header_summary").text():a("#show_issue").length?
c=a("#show_issue .number strong").text()+" "+a("#show_issue .content-title").text():a("#all_commit_comments").length&&(c=a(".js-current-repository").text().trim()+": "+a(".commit .commit-title").text().trim());var d;g.getSelection?d=""+g.getSelection():document.selection&&document.selection.createRange&&(d=document.selection.createRange().text);d&&(c?f+="\n\n"+d:c=d);c&&e.post("lists/"+b+"/cards",{name:c,desc:f},function(b){var c=a("<a>").attr({href:b.url,target:"card"}).text("Created a Trello Card").css({position:"absolute",
left:0,top:0,padding:"4px",border:"1px solid #000",background:"#fff","z-index":1E3}).appendTo("body");setTimeout(function(){c.fadeOut(3E3)},5E3)})}])}})(window);
```

This is a <a href="http://en.wikipedia.org/wiki/Bookmarklet">bookmarklet</a> you can use to create a card in <a href="https://trello.com">Trello</a> from ...

 - FogBugz cases
 - JIRA issues
 - GitHub issues and commits
 - The selected text from an arbitrary URL

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


**Note:** This basic concept originated with https://github.com/markdrago/cardorizer; this approach doesn't require you to run a server