# PitchMoggots
A scripts set to block NMSLeses in https://music.douban.com/subject/35030138/

The scirpt seperated in 2 steps


STEP1:
  - OPEN chrome 
  - OPEN [music.douban.com](music.douban.com)
  - OPEN Console panel cmd+option+J(MAC) Ctrl+Shift+J(WIN)
  - COPY and PASTE the codes below into the pannel
  - PRESS enter
  - SAVE an auto popup list file to local

check [this link](https://github.com/CN-Chrome-DevTools/CN-Chrome-DevTools/blob/master/md/Reference/shortcuts.md) if you don't understand

```
function acquireMaggotListFromCollections(t=0,n=40){return new Promise((a,e)=>{$.ajax({url:"https://music.douban.com/subject/35030138/collections",data:"start="+t,success:t=>{var e=$("<div/>").html(t).contents(),o=e.find(".sub_ins tr").each((function(t){var a=$(this).find(".pl>span:last-child").attr("class"),e=/\d+/.exec(a)||"",o=parseInt(e[0]);return o&&o>=n})).map((function(t){const n=($(this).find("a").attr("href")||"").match(/(\d+)\/?$/);return n&&n[1]})).get();const i=e.find(".paginator .next").length>0;a({isContinue:i,data:o})},error:t=>{e(t)}})})}function acquireMaggotListFromComments(t=1,n=40,a="hot"){return new Promise((e,o)=>{$.ajax({url:"https://music.douban.com/subject/35030138/comments/"+a,data:`p=${t}&_=${(new Date).toString()}`,success:t=>{var a=$("<div/>").html(t.paginator).contents(),o=$("<div/>").html(t.content).contents(),i=/后一页/.test(a.find("li:last-child").text()||""),s=o.find("li .comment-info").each((function(t){var a=$(this).find(".rating").attr("class"),e=/\d+/.exec(a)||"";console.log("分值: "+e);var o=parseInt(e[0]);return o&&o>=n})).map((function(t){const n=($(this).find("a").attr("href")||"").match(/\/(\d+)\/?$/);return n&&n[1]})).get();e({isContinue:i,data:s})},error:t=>{o(t)}})})}function saveJsonFile(t,n,a){var e=document.createElement("a"),o=new Blob([t],{type:a});e.href=URL.createObjectURL(o),e.download=n,e.click()}async function joinMaggotList(){for(var t=!0,n=0,a=[];t;){n++,t=(e=await acquireMaggotListFromComments(n)).isContinue,a=a.concat(e.data)}for(;t;){var e;n++,t=(e=await acquireMaggotListFromComments(n,40,"new")).isContinue,a=a.concat(e.data)}return a}(async()=>{try{const t=await joinMaggotList();saveJsonFile(JSON.stringify(t),"moggotsList.json","text/plain")}catch(t){console.error(t)}})();

```


STEP2:
  - OPEN chrome 
  - OPEN [www.douban.com](www.douban.com)
  - OPEN Console panel cmd+option+J(MAC) Ctrl+Shift+J(WIN)
  - COPY and PASTE the codes below into the pannel
  - YOU will see a button added in the side board
  - CLICK the button and select the .json file you saved in STEP1
  - Have a rest to see moggots blocked

```
function openFile(e){var t=document.createElement("input");t.setAttribute("type","file"),t.setAttribute("id","load-moggots"),t.onchange=function(){readText(this,e),$("#load-moggots").remove()},$(".aside").prepend(t)}function readText(e,t){var o;if(!(window.File&&window.FileReader&&window.FileList&&window.Blob))return alert("The File APIs are not fully supported by your browser. Fallback required."),!1;o=new FileReader;var n="";return!(!e.files||!e.files[0])&&(o.onload=function(e){n=e.target.result,t(n)},o.readAsText(e.files[0]),!0)}function getCookie(e){for(var t=e+"=",o=decodeURIComponent(document.cookie).split(";"),n=0;n<o.length;n++){for(var r=o[n];" "==r.charAt(0);)r=r.substring(1);if(0==r.indexOf(t))return r.substring(t.length,r.length)}return""}function ban(e){return new Promise((t,o)=>{var n=getCookie("ck");$.ajax({type:"POST",headers:{Accept:"application/json","Content-Type":"application/x-www-form-urlencoded"},url:"https://www.douban.com/j/contact/addtoblacklist",data:`people=${e}&ck=${n}`,success:function(o){o.result?console.log(`已屏蔽<${e}>蛆`):console.log(`这只<${e}>蛆比较顽固,需要手动处理`),t(o.result)},error:function(e){o(e)}})})}openFile((async function(e){try{const o=JSON.parse(e);var t=0;for(let e=0;e<o.length;e++){await ban(o[e])&&t++}console.log(`本次共拉黑${t}只蛆`)}catch(e){alert("文件读取失败, 操作未能进行,多半是选错文件")}}));
```


LIMITATION: 

- Cuz douban.com doesn't show all rating records;
- So these script cannot grab all moggots' id;
- For now it loops records both in hot/new pannels as more as it could be;
- You better repeat it in a few hours, to block new added;
- For default, all rating higher than 3 (>3) will be blocked;
- But it's configuable if you know how to do;







--------

<a href="https://www.patreon.com/user/TakehisaYumeji">
  <img src="https://www.buymeacoffee.com/assets/img/logo-bmc.svg" align="left" width="240" >
</a>

