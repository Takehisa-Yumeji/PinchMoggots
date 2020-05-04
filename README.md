# PinchMoggots
A scripts set to block NMSLeses in https://music.douban.com/subject/35030138/

The scirpt seperated in 2 steps


ONLY RUN THIS IF YOU EXCUTED OTHERS BEFORE!!!
PATCH: ( According a bug issue provided by '水泥')
  - OPEN chrome 
  - OPEN [www.douban.com](www.douban.com)
  - OPEN Console panel cmd+option+J(MAC) Ctrl+Shift+J(WIN)
  - COPY and PASTE the codes below into the pannel
  - ROLLBACK people blocked by mistake

```
function getCookie(o){for(var e=o+"=",n=decodeURIComponent(document.cookie).split(";"),t=0;t<n.length;t++){for(var r=n[t];" "==r.charAt(0);)r=r.substring(1);if(0==r.indexOf(e))return r.substring(e.length,r.length)}return""}function rollback(o){return new Promise((e,n)=>{var t=getCookie("ck");$.ajax({type:"POST",headers:{Accept:"application/json","Content-Type":"application/x-www-form-urlencoded"},url:"https://www.douban.com/j/contact/unban",data:`people=${o}&ck=${t}`,success:function(n){n.result?console.log(`已复活<${o}>`):console.log(`你本来也木有关注<${o}>`),e(n.result)},error:function(o){n(o)}})})}(async()=>{const o=["182875304","182609562","120696660","164243765","211235160","56643693","155515520","211450695","190948384","4347027","131224684","212362176","179727074","197612014","185400312","210444168","178881410","210448976","188562284","209291351","184539248","204559937","174499755","213285529","192244299","209767090","177152086","147994612","183481748","182115730","212582511","212276099","156442518","205887767","171402928","2348667","212747771","104495794","167573042","216233933","60446235","148488371","191245940","2674588","194821178","205100778","209527742","121171769","185515489","205491694","62286203","206145840","184414356","140568271","215663916","158858069","171446709","180933049","207417253","157187649","214421387","170551851","53146753","96492247","152666923","63030688","171791898","197896422","147948455","45153530","4606815","198146729","132828745","210446576","208721358","216188848","175967336","85175134","215898788","215223383","211331378","195890281","197867710","157891509","154513955","215253352","2265138","55866737","3435193","161208957","1569518","67343965","106347535","49145944","3493039","171272363","78548715","137892066","164129483","54767000","196968387","11937927","153750613","122836378","50557669","156164436","174159365","142520899","4105139","194821178","2473154","121543501","1284902","169365129","181716875","168619468","52925540","148673338","144309115","2300798","3205834","98184088","75922870","53009579","2584407","59665595","53965857","1169459","155697123","66163956","196572579","44001140","130214180","4000937","4451458","119287570","146828897","43216888","62846512","163690904","57775848","43328284","37215822","153057971","4372093","87316420","43431279","59955092","57087441","123023655","62212839","207969614","136430516","142505098","53439530","160876692","137216748","137160827","135605290","177864253","59747131","164509265","204333577","134500558","1423518","3053229","4627124","93124222","89178219","53730188","139602082","52157663","6887494","26484263","72125334","45430569","35711522","33736944","50744981","156127104","60939723","52460978","81605101","48508118","134002125","158297823","48768575","27738698","2482689","39663981","149152146","171333036","90501682","4061743","159673853","49172586","130097686","65309880","144112444","201409687","18313578","80727852","60372839","28430698","3519597","177366045","47549670","87768468","52470092","3812638","121807969","207206956","182875304","120696660","164243765","155515520","211450695","185400312","210444168","178881410","210448976","188562284","184539248","174499755","213285529","209767090","183481748","182115730","212582511","212276099","205887767","171402928","210737421","212747771","104495794","60446235","148488371","194821178","205100778","206145840","158858069","207417253","214421387","171791898","147948455","198146729","132828745","215223383","211331378","195890281","65394267","159045724","172622557","148939399","202125312","141227539","212541786","195731839","156160487"];var e=0;for(let n=0;n<o.length;n++){await rollback(o[n])&&e++}console.log(`共拉回${e}个人`)})();
```

STEP1:
  - OPEN chrome 
  - OPEN [music.douban.com](music.douban.com)
  - OPEN Console panel cmd+option+J(MAC) Ctrl+Shift+J(WIN)
  - COPY and PASTE the codes below into the pannel
  - PRESS enter
  - SAVE an auto popup list file to local

check [this link](https://github.com/CN-Chrome-DevTools/CN-Chrome-DevTools/blob/master/md/Reference/shortcuts.md) if you don't understand

```
function acquireMaggotListFromCollections(t=0,n=40){return new Promise((o,e)=>{console.log("正在从听过中搜索..."),$.ajax({url:"https://music.douban.com/subject/35030138/collections",data:"start="+t,success:t=>{var e=$("<div/>").html(t).contents(),a=e.find(".sub_ins tr").filter((function(t){var o=$(this).find(".pl>span:last-child").attr("class"),e=/\d+/.exec(o)||"",a=parseInt(e[0]);return!!a&&a>=n})).map((function(t){const n=($(this).find("a").attr("href")||"").match(/\/(\d+)\/?$/);return n&&n[1]})).get();const i=e.find(".paginator .next").length>0;o({isContinue:i,data:a})},error:t=>{e(t)}})})}function acquireMaggotListFromReviews(t=0,n=5){return new Promise((o,e)=>{console.log(`正在从乐评${n}星中搜索...`),$.ajax({url:"https://music.douban.com/subject/35030138/reviews?rating="+n,data:"start="+t,success:t=>{var n=$("<div/>").html(t.html).contents().find(".review-item").map((function(t){console.log($(this).find(".main-title-rating").attr("title"));const n=($(this).find(" .main-hd a").attr("href")||"").match(/\/(\d+)\/?$/);return n&&n[1]})).get();const e=t.count>0;o({isContinue:e,data:n})},error:t=>{e(t)}})})}function acquireMaggotListFromComments(t=1,n=40,o="hot"){return new Promise((e,a)=>{console.log(`正在从短评/${o}中搜索...`),$.ajax({url:"https://music.douban.com/subject/35030138/comments/"+o,data:`p=${t}&_=${(new Date).toString()}`,success:t=>{var o=$("<div/>").html(t.paginator).contents(),a=$("<div/>").html(t.content).contents(),i=/后一页/.test(o.find("li:last-child").text()||""),s=a.find("li .comment-info").filter((function(t){var o=$(this).find(".rating").attr("class"),e=/\d+/.exec(o)||"",a=parseInt(e[0]);return console.log(o,!!a&&a>=n),!!a&&a>=n})).map((function(t){const n=($(this).find("a").attr("href")||"").match(/\/(\d+)\/?$/);return n&&n[1]})).get();e({isContinue:i,data:s})},error:t=>{a(t)}})})}function saveJsonFile(t,n,o){var e=document.createElement("a"),a=new Blob([t],{type:o});e.href=URL.createObjectURL(a),e.download=n,e.click()}async function loopWrapFunc(t,n=0,o=1,...e){for(var a=n,i=!0,s=[];i;){var r=await t(a*o,...e);i=r.isContinue,s=s.concat(r.data),a++}return s}async function joinMaggotList(){var t=await loopWrapFunc(acquireMaggotListFromComments,1),n=await loopWrapFunc(acquireMaggotListFromComments,1,1,40,"new"),o=await loopWrapFunc(acquireMaggotListFromCollections,0,20),e=await loopWrapFunc(acquireMaggotListFromReviews,0,10),a=await loopWrapFunc(acquireMaggotListFromReviews,0,10,4);const i=[].concat(o,t,n,e,a);return console.log(`从短评/热度收集${t.length}只蛆`),console.log(`从短评/最新收集${n.length}只蛆`),console.log(`从听过收集${o.length}只蛆`),console.log(`从乐评5收集${e.length}只蛆`),console.log(`从乐评4收集${a.length}只蛆`),console.log("======================"),console.log(`总计${i.length}只蛆`),i}(async()=>{try{const t=await joinMaggotList();saveJsonFile(JSON.stringify(t),"moggotsList.json","text/plain")}catch(t){console.error(t)}})();

```


STEP2:
  - OPEN chrome 
  - OPEN [www.douban.com](www.douban.com)
  - OPEN Console panel cmd+option+J(MAC) Ctrl+Shift+J(WIN)
  - COPY and PASTE the codes below into the pannel
  - YOU will see a button added in the side board
  - ![](tip.png)
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


TODO:
- [X] Will be add more filters for distinguishing
- [ ] Maybe a chrome extension with auto cronjob, but not be sure now, cuz it's only a trending not life

Some views:
- When the website is not on your side, you need to protect yourselves
- I don't think there are 95% moggots now, They are loud only cuz the totalitarianism is on their side
- The worst case scenario is to rebuild an Internet, no big deal
- Keep happy yourself
 
UPDATED:
- Clerifying the data source
- Support finding moggots from reviews\comments\collections and more
- Improve user experience, more console info


Copyright
Licensed under the MIT license.

--------

<a href="https://www.patreon.com/user/TakehisaYumeji">
  <img src="https://www.buymeacoffee.com/assets/img/logo-bmc.svg" align="left" width="240" >
</a>
