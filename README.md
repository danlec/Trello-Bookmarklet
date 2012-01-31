```javascript
javascript:(function(g){var c,i=g.localStorage;if(i){var h=function(a,b){return 2==arguments.length?i[a]=b:i[a]},j=function(a,b,d){var f=c("<div>").css({background:"#000",opacity:0.75,"z-index":1E4,position:"absolute",left:0,top:0,right:0,bottom:0}).appendTo("body").click(function(){e.remove();f.remove();d(null)}),e=c("<div>").css({position:"absolute",border:"1px solid #000",padding:"16px",width:300,top:64,left:(c(g).width()-200)/2,background:"#fff","z-index":1E5}).appendTo("body");c("<div>").html(a).appendTo(e);
var k=c("<input>").css({width:"100%","margin-top":"8px"}).appendTo(e).toggle(b);c("<div>").text("OK").css({width:"100%","text-align":"center",border:"1px solid #000",background:"#eee","margin-top":"8px",cursor:"pointer"}).appendTo(e).click(function(){var b=k.val();e.remove();f.remove();d(b)});return e};(function(a){var b=function(){a.length&&a.shift().apply(null,Array.prototype.slice.call(arguments).concat([b]))};b()})([function(a){if(g.jQuery)a(null);else{var b=document.createElement("script");b.src=
"http://code.jquery.com/jquery-1.7.1.min.js";b.onload=a;document.getElementsByTagName("head")[0].appendChild(b)}},function(a,b){c=g.jQuery;var d=h("trelloAppKey");d?b(d):j("Please specify your Trello API Key (you'll only need to do this once per site)<br><br>You can get your API Key <a href='https://trello.com/1/appKey/generate' target='apikey'>here</a><br><br>",!0,function(a){a&&b(a)})},function(a,b){c.getScript("https://trello.com/1/client.js?key="+a,b)},function(a,b,c,f){h("trelloAppKey",Trello.key());
Trello.authorize({interactive:!1,success:f,error:function(){j("You need to authorize Trello",!1,function(){Trello.authorize({type:"popup",expiration:"never",scope:{read:!0,write:!0},success:f})})}})},function(a){var b=h("trelloIdList");b?a(b):Trello.get("members/me/boards",{fields:"name"},function(d){$prompt=j('Which list should cards be sent to?<hr><div class="boards"></div>',!1,function(){b=$prompt.find("input:checked").attr("id");a(b)});c.each(d,function(a,d){$board=c("<div>").appendTo($prompt.find(".boards"));
Trello.get("boards/"+d.id+"/lists",function(a){c.each(a,function(a,f){var g=c("<div>").appendTo($board);b=f.id;c("<input type='radio'>").attr("id",b).attr("name","idList").appendTo(g);c("<label>").text(d.name+" : "+f.name).attr("for",b).appendTo(g)})})})})},function(a,b){a&&(h("trelloIdList",a),b(Trello,a))},function(a,b){var d,f=location.href;g.goBug?d=goBug.ixBug+": "+goBug.sTitle:c("#issue_header_summary").length?d=c("#key-val").text()+": "+c("#issue_header_summary").text():c("#show_issue").length&&
(d=c("#show_issue .number strong").text()+" "+c("#show_issue .content-title").text());var e;g.getSelection?e=""+g.getSelection():document.selection&&document.selection.createRange&&(e=document.selection.createRange().text);e&&(d?f+="\n\n"+e:d=e);d&&a.post("lists/"+b+"/cards",{name:d,desc:f},function(a){var b=c("<a>").attr({href:a.url,target:"card"}).text("Created a Trello Card").css({position:"absolute",left:0,top:0,padding:"4px",border:"1px solid #000",background:"#fff","z-index":1E3}).appendTo("body");
setTimeout(function(){b.fadeOut(3E3)},5E3)})}])}})(window);
```

This is a <a href="http://en.wikipedia.org/wiki/Bookmarklet">bookmarklet</a> you can use to create a card in <a href="https://trello.com">Trello</a> from ...

 - FogBugz cases
 - JIRA issues
 - GitHub issues
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