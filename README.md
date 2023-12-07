<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>replit</title>
  <link href="style.css" rel="stylesheet" type="text/css" />
</head>

<body>
  
  <script src="script.js"></script>

  <!--
  This script places a badge on your repl's full-browser view back to your repl's cover
  page. Try various colors for the theme: dark, light, red, orange, yellow, lime, green,
  teal, blue, blurple, magenta, pink!
  -->
  <script src="https://replit.com/public/js/replit-badge-v2.js" theme="dark" position="bottom-right"></script>
</body>

</html>
<script type="text/javascript">
// <![CDATA[
var colours=new Array("#ffdbe8"); // colours of the hearts
var minisize=15; // smallest size of hearts in pixels
var maxisize=30; // biggest size of hearts in pixels
var hearts=69; // maximum number of hearts on screen
var over_or_under="over"; // set to "over" for hearts to always be on top, or "under" to allow them to float behind other objects

/*****************************
*JavaScript Love Heart Cursor*
*  (c)2013+ mf2fm web-design *
*   https://www.mf2fm.com/rv  *
*  DON'T EDIT BELOW THIS BOX *
*****************************/
var x=ox=400;
var y=oy=300;
var swide=800;
var shigh=600;
var sleft=sdown=0;
var herz=new Array();
var herzx=new Array();
var herzy=new Array();
var herzs=new Array();
var kiss=false;

if (typeof('addRVLoadEvent')!='function') function addRVLoadEvent(funky) {
  var oldonload=window.onload;
  if (typeof(oldonload)!='function') window.onload=funky;
  else window.onload=function() {
    if (oldonload) oldonload();
    funky();
  }
}

addRVLoadEvent(mwah);

function mwah() { if (document.getElementById) {
  var i, heart;
  for (i=0; i<hearts; i++) {
    heart=createDiv("auto", "auto");
    heart.style.visibility="hidden";
  heart.style.zIndex=(over_or_under=="over")?"1001":"0";
    heart.style.color=colours[i%colours.length];
  heart.style.pointerEvents="none";
    if (navigator.appName=="Microsoft Internet Explorer") heart.style.filter="alpha(opacity=75)";
    else heart.style.opacity=0.75;
    heart.appendChild(document.createTextNode(String.fromCharCode(9829)));
    document.body.appendChild(heart);
    herz[i]=heart;
  herzy[i]=false;
  }
  set_scroll();
  set_width();
  herzle();
}}

function herzle() {
  var c;
  if (Math.abs(x-ox)>1 || Math.abs(y-oy)>1) {
    ox=x;
    oy=y;
    for (c=0; c<hearts; c++) if (herzy[c]===false) {
    herz[c].firstChild.nodeValue=String.fromCharCode(9829);
      herz[c].style.left=(herzx[c]=x-minisize/2)+"px";
      herz[c].style.top=(herzy[c]=y-minisize)+"px";
      herz[c].style.fontSize=minisize+"px";
    herz[c].style.fontWeight='normal';
      herz[c].style.visibility='visible';
      herzs[c]=minisize;
      break;
    }
  }
  for (c=0; c<hearts; c++) if (herzy[c]!==false) blow_me_a_kiss(c);
  setTimeout("herzle()", 40);
}

document.onmousedown=pucker;
document.onmouseup=function(){clearTimeout(kiss);};

function pucker() {
  ox=-1;
  oy=-1;
  kiss=setTimeout('pucker()', 100);
}

function blow_me_a_kiss(i) {
  herzy[i]-=herzs[i]/minisize+i%2;
  herzx[i]+=(i%5-2)/5;
  if (herzy[i]<sdown-herzs[i] || herzx[i]<sleft-herzs[i] || herzx[i]>sleft+swide-herzs[i]) {
    herz[i].style.visibility="hidden";
    herzy[i]=false;
  }
  else if (herzs[i]>minisize+2 && Math.random()<.5/hearts) break_my_heart(i);
  else {
    if (Math.random()<maxisize/herzy[i] && herzs[i]<maxisize) herz[i].style.fontSize=(++herzs[i])+"px";
    herz[i].style.top=herzy[i]+"px";
    herz[i].style.left=herzx[i]+"px";
  }
}

function break_my_heart(i) {
  var t;
  herz[i].firstChild.nodeValue=String.fromCharCode(9676);
  herz[i].style.fontWeight='bold';
  herzy[i]=false;
  for (t=herzs[i]; t<=maxisize; t++) setTimeout('herz['+i+'].style.fontSize="'+t+'px"', 60*(t-herzs[i]));
  setTimeout('herz['+i+'].style.visibility="hidden";', 60*(t-herzs[i]));
}

document.onmousemove=mouse;
function mouse(e) {
  if (e) {
    y=e.pageY;
    x=e.pageX;
  }
  else {
    set_scroll();
    y=event.y+sdown;
    x=event.x+sleft;
  }
}

window.onresize=set_width;
function set_width() {
  var sw_min=999999;
  var sh_min=999999;
  if (document.documentElement && document.documentElement.clientWidth) {
    if (document.documentElement.clientWidth>0) sw_min=document.documentElement.clientWidth;
    if (document.documentElement.clientHeight>0) sh_min=document.documentElement.clientHeight;
  }
  if (typeof(self.innerWidth)=='number' && self.innerWidth) {
    if (self.innerWidth>0 && self.innerWidth<sw_min) sw_min=self.innerWidth;
    if (self.innerHeight>0 && self.innerHeight<sh_min) sh_min=self.innerHeight;
  }
  if (document.body.clientWidth) {
    if (document.body.clientWidth>0 && document.body.clientWidth<sw_min) sw_min=document.body.clientWidth;
    if (document.body.clientHeight>0 && document.body.clientHeight<sh_min) sh_min=document.body.clientHeight;
  }
  if (sw_min==999999 || sh_min==999999) {
    sw_min=800;
    sh_min=600;
  }
  swide=sw_min;
  shigh=sh_min;
}

window.onscroll=set_scroll;
function set_scroll() {
  if (typeof(self.pageYOffset)=='number') {
    sdown=self.pageYOffset;
    sleft=self.pageXOffset;
  }
  else if (document.body && (document.body.scrollTop || document.body.scrollLeft)) {
    sdown=document.body.scrollTop;
    sleft=document.body.scrollLeft;
  }
  else if (document.documentElement && (document.documentElement.scrollTop || document.documentElement.scrollLeft)) {
    sleft=document.documentElement.scrollLeft;
    sdown=document.documentElement.scrollTop;
  }
  else {
    sdown=0;
    sleft=0;
  }
}

function createDiv(height, width) {
  var div=document.createElement("div");
  div.style.position="absolute";
  div.style.height=height;
  div.style.width=width;
  div.style.overflow="hidden";
  div.style.backgroundColor="transparent";
  return (div);
}
// ]]>
</script>

<style>
  body{ 
  color:#555555; 
  background-color:#ffe8f4;
  background-image:url('');

</style>
<style>

.brown {
border-width:7px;
border-style:solid;
border-image: url("https://static.tumblr.com/yn7vk7p/DfHmp40xm/bo-ha26.gif") 8 fill round;
}
}

  <style>
  <style>
  a {
  transition: 0.5s ease;
  }
  a:hover {
  filter: blur(1px);
  }
  
  #news {
   text-shadow: -1px 0 #000, 0 1px #000, 1px 0 #000, 0 -1px #000, 0 0;
   font-size:200%;
   font-weight:bold; 
   color: #fff;
   }
  </style>
  <head>
  <script type="text/javascript">
  // <![CDATA[
    var news=Array("짜잔-!ପ(｡ᵔ ⩊ ᵔ｡)ଓ", "zin임니다-♡(쑥스)", "반가워요(˶ ᵔ ̫ ᵔ ˶)♡", "늘 건강하고 행복하세요💗 ͜ (ᵔ ̮ ᵔ)›", "사랑합니다✩゜*⸜(ू ◜࿁◝ )");
  var cursor="_"; // set cursor
  var delay=6; // seconds between each news item

  /***************************\
  * News Ticker Text Effect   *
  *(c)2004-14 mf2fm web-design*
  *  http://www.mf2fm.com/rv  *
  * DON'T EDIT BELOW THIS BOX *
  \***************************/
  var newsp, cursp, flash, item=0;

  if (typeof('addRVLoadEvent')!='function') function addRVLoadEvent(funky) {
    var oldonload=window.onload;
    if (typeof(oldonload)!='function') window.onload=funky;
    else window.onload=function() {
      if (oldonload) oldonload();
      funky();
    }
  }

  addRVLoadEvent(teleprint);

  function teleprint () { if (document.getElementById) {
    var span=document.getElementById("news");
    while (span.childNodes.length) span.removeChild(span.childNodes[0]);
    delay*=1000;
    newsp=document.createElement("span");
    cursp=document.createElement("span");
    cursp.appendChild(document.createTextNode(String.fromCharCode(160)+cursor));
    span.appendChild(newsp);
    span.appendChild(cursp);
    ticker();
  }}

  function ticker() {
    var i;
    while (newsp.childNodes.length) newsp.removeChild(newsp.childNodes[0]);
    newsp.appendChild(document.createTextNode(news[item].substring(0,1)));
    for (i=1; i<news[item].length; i++) setTimeout('newsp.firstChild.nodeValue="'+news[item].substring(0, i+1)+'"', 100*i);
    if (news[item].indexOf("www")!=-1) setTimeout('linkit('+item+')', 100*i);
    setTimeout('flash=setInterval("cursp.style.visibility=(cursp.style.visibility==\'visible\')?\'hidden\':\'visible\'", 234)', 100*i)
    setTimeout('clearInterval(flash)', delay);
    setTimeout('cursp.style.visibility="visible"', delay);
    setTimeout('ticker()', delay);
    item=++item%news.length;
  }

  function linkit(q) {
    var a,p,e,l;
    p=news[q].indexOf("www");
    e=news[q].indexOf(" ", p);
    if (e==-1) e=news[q].length;
    l=news[q].substring(p, e);
    while (newsp.childNodes.length) newsp.removeChild(newsp.childNodes[0]);
    newsp.appendChild(document.createTextNode(news[q].substring(0, p)));
    a=document.createElement("a");
    a.href="http://"+l;
    a.appendChild(document.createTextNode(l));
    newsp.appendChild(a);
    newsp.appendChild(document.createTextNode(news[q].substring(e)));
  }
  // ]]>
  </script>
  </head>
  <span id="news">ପ(｡ᵔ ⩊ ᵔ｡)ଓ</span>
</style>

<img class=brown src="https://64.media.tumblr.com/tumblr_m381zlKuF61rv0o6uo1_1280.jpg" alt="" style="width:90%;height:auto;border-radius:1px;">


<style>
  <script>
