# Microsoft365_E5_Renew_X 自己搭建网页版续签服务
Save From : [Microsoft365_E5_Renew_X 自己搭建网页版续签服务](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html) 

## Content
### Microsoft365\_E5\_Renew_X 自己搭建网页版续签服务

*   获取链接
*   Facebook
*   Twitter
*   Pinterest
*   电子邮件
*   其他应用

\-  [  一月 18, 2023  ](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html "permanent link") 

[![](https://blogger.googleusercontent.com/img/a/AVvXsEhLD84GT0Rfz1M7X5rjUE_2BtaPmSKh09oMqQjlDzQYkoC81ISecEz2Lwa1zckcXxej-zefuvFcGNhi3uyZv51yF1FXzciC2q40RLApauuVAQJ_Xkg5XUOejT9_9SiSkTGHEBpa0sVHM7vzRxAGgjbudNkFKNQ5-rAXMQTVzEgC3k63kLHKYM0kMCW3=w640-h314)
](https://blogger.googleusercontent.com/img/a/AVvXsEhLD84GT0Rfz1M7X5rjUE_2BtaPmSKh09oMqQjlDzQYkoC81ISecEz2Lwa1zckcXxej-zefuvFcGNhi3uyZv51yF1FXzciC2q40RLApauuVAQJ_Xkg5XUOejT9_9SiSkTGHEBpa0sVHM7vzRxAGgjbudNkFKNQ5-rAXMQTVzEgC3k63kLHKYM0kMCW3)

  
  

E5 账号大家都白嫖上了吧！

续签服务搭建在自己服务器上或许会安全点。我找了一个 GitHub 上的 docker 搭建方法，结合我自己经验。应该可行，比较简单。

  

  

**买台 VPS**

RN VPS 使用教学（推荐视频）

[https://youtu.be/Eru03pm-_GA](https://youtu.be/Eru03pm-_GA)

科技 lion 推荐的热门 VPS 购买

[https://kejilion.pro/index.php/topVPS/](https://kejilion.pro/index.php/topVPS/)

  

  

**连接 VPS**

买好 VPS 后获取 VPS 的公网 IP 地址

端口默认 22

SSH 连接你的 VPS

  

  

**更新环境**

apt update -y && apt install -y curl && apt install -y socat && apt install wget -y

  

**安装 sudo**

apt-get install sudo

  

**安装 Docker**

sudo apt install docker.io -y && sudo apt install docker-compose

  

**自启动 docker**

sudo systemctl enable --now docker

  

**下载镜像**

docker pull hanhongyong/ms365-e5-renew-x:latest

  

**部署容器**

docker run -d -p 1066:1066 -e TZ=Asia/Shanghai --name ms365  hanhongyong/ms365-e5-renew-x:latest

  

**初始密码**

123456

  

**修改密码**

docker exec -it ms365 /bin/bash

cd Deploy

vim Config.xml

  

输入 i 启动编辑模式

修改密码

输入 esc 退出编辑

:wq! 回车 退出

重启密码才会生效

  

**重启续签服务**

重启服务器后 E5 续签网页不会跟随重启

需要以下命令

docker start ms365

  

**更多 docker 常用命令**

docker ps -a 查看已经创建的容器

docker ps -s 查看已经启动的容器

docker start con\_name 启动容器名为 con\_name 的容器

docker stop con\_name 停止容器名为 con\_name 的容器

docker rm con\_name 删除容器名为 con\_name 的容器

  

**原作者 GitHub 地址**

[https://github.com/hongyonghan/Docker\_Microsoft365\_E5\_Renew\_X](https://github.com/hongyonghan/Docker_Microsoft365_E5_Renew_X)

  

  

  

  

  

  

  

  

*   获取链接
*   Facebook
*   Twitter
*   Pinterest
*   电子邮件
*   其他应用

### 评论

(function(){/* Copyright The Closure Library Authors. SPDX-License-Identifier: Apache-2.0 */ var ba=function(a){var b=0;return function(){return b<a.length?{done:!1,value:a\[b++\]}:{done:!0}}},n="function"==typeof Object.defineProperties?Object.defineProperty:function(a,b,c){if(a==Array.prototype||a==Object.prototype)return a;a\[b\]=c.value;return a},ca=function(a){a=\["object"==typeof globalThis&&globalThis,a,"object"==typeof window&&window,"object"==typeof self&&self,"object"==typeof global&&global\];for(var b=0;b<a.length;++b){var c=a\[b\];if(c&&c.Math==Math)return c}throw Error("Cannot find global object"); },r=ca(this),t=function(a,b){if(b)a:{var c=r;a=a.split(".");for(var e=0;e<a.length-1;e++){var d=a\[e\];if(!(d in c))break a;c=c\[d\]}a=a\[a.length-1\];e=c\[a\];b=b(e);b!=e&&null!=b&&n(c,a,{configurable:!0,writable:!0,value:b})}}; t("Symbol",function(a){if(a)return a;var b=function(g,p){this.$jscomp$symbol$id_=g;n(this,"description",{configurable:!0,writable:!0,value:p})};b.prototype.toString=function(){return this.$jscomp$symbol$id_};var c="jscomp\_symbol\_"+(1E9\*Math.random()>>>0)+"_",e=0,d=function(g){if(this instanceof d)throw new TypeError("Symbol is not a constructor");return new b(c+(g||"")+"_"+e++,g)};return d}); t("Symbol.iterator",function(a){if(a)return a;a=Symbol("Symbol.iterator");for(var b="Array Int8Array Uint8Array Uint8ClampedArray Int16Array Uint16Array Int32Array Uint32Array Float32Array Float64Array".split(" "),c=0;c<b.length;c++){var e=r\[b\[c\]\];"function"===typeof e&&"function"!=typeof e.prototype\[a\]&&n(e.prototype,a,{configurable:!0,writable:!0,value:function(){return da(ba(this))}})}return a}); var da=function(a){a={next:a};a\[Symbol.iterator\]=function(){return this};return a},ea=function(a,b){a instanceof String&&(a+="");var c=0,e=!1,d={next:function(){if(!e&&c<a.length){var g=c++;return{value:b(g,a\[g\]),done:!1}}e=!0;return{done:!0,value:void 0}}};d\[Symbol.iterator\]=function(){return d};return d};t("Array.prototype.entries",function(a){return a?a:function(){return ea(this,function(b,c){return\[b,c\]})}}); var v=this||self,w=function(a,b){function c(){}c.prototype=b.prototype;a.superClass_=b.prototype;a.prototype=new c;a.prototype.constructor=a;a.base=function(e,d,g){for(var p=Array(arguments.length-2),q=2;q<arguments.length;q++)p\[q-2\]=arguments\[q\];return b.prototype\[d\].apply(e,p)}},x=function(a){return a};function y(a,b){if(Error.captureStackTrace)Error.captureStackTrace(this,y);else{var c=Error().stack;c&&(this.stack=c)}a&&(this.message=String(a));void 0!==b&&(this.cause=b)}w(y,Error);y.prototype.name="CustomError";function z(a,b){a=a.split("%s");for(var c="",e=a.length-1,d=0;d<e;d++)c+=a\[d\]+(d<b.length?b\[d\]:"%s");y.call(this,c+a\[e\])}w(z,y);z.prototype.name="AssertionError";var A=function(a,b){throw new z("Failure"+(a?": "+a:""),Array.prototype.slice.call(arguments,1));};var E;var G=function(a,b){this.privateDoNotAccessOrElseTrustedResourceUrlWrappedValue_=b===F?a:""};G.prototype.toString=function(){return this.privateDoNotAccessOrElseTrustedResourceUrlWrappedValue_+""};var F={};var fa=function(){var a=document;var b="SCRIPT";"application/xhtml+xml"===a.contentType&&(b=b.toLowerCase());return a.createElement(b)};var H=function(a,b){this.name=a;this.value=b};H.prototype.toString=function(){return this.name};var I=new H("OFF",Infinity),ha=new H("WARNING",900),ia=new H("CONFIG",700),J=function(){this.capacity_=0;this.clear()},K;J.prototype.clear=function(){this.buffer_=Array(this.capacity_);this.curIndex_=-1;this.isFull_=!1};var L=function(a,b,c){this.reset(a||I,b,c,void 0,void 0)};L.prototype.reset=function(){}; var M=function(a,b){this.level=null;this.handlers=\[\];this.parent=(void 0===b?null:b)||null;this.children=\[\];this.logger={getName:function(){return a}}},O=function(a){if(a.level)return a.level;if(a.parent)return O(a.parent);A("Root logger has no level set.");return I},ja=function(a,b){for(;a;)a.handlers.forEach(function(c){c(b)}),a=a.parent},ka=function(){this.entries={};var a=new M("");a.level=ia;this.entries\[""\]=a},P,Q=function(a,b){var c=a.entries\[b\];if(c)return c;c=Q(a,b.slice(0,Math.max(b.lastIndexOf("."), 0)));var e=new M(b,c);a.entries\[b\]=e;c.children.push(e);return e},R=function(){P||(P=new ka);return P};/\* SPDX-License-Identifier: Apache-2.0 */ var S=\[\],T=function(a){var b;if(b=Q(R(),"safevalues").logger){var c="A URL with content '"+a+"' was sanitized away.",e=ha;if(a=b)if(a=b&&e){a=e.value;var d=b?O(Q(R(),b.getName())):I;a=a>=d.value}if(a){e=e||I;a=Q(R(),b.getName());"function"===typeof c&&(c=c());K||(K=new J);d=K;b=b.getName();if(0<d.capacity_){var g=(d.curIndex_+1)%d.capacity_;d.curIndex_=g;d.isFull_?(d=d.buffer_\[g\],d.reset(e,c,b),b=d):(d.isFull_=g==d.capacity_-1,b=d.buffer_\[g\]=new L(e,c,b))}else b=new L(e,c,b);ja(a,b)}}}; -1===S.indexOf(T)&&S.push(T);function la(a,b){if(b instanceof G&&b.constructor===G)b=b.privateDoNotAccessOrElseTrustedResourceUrlWrappedValue_;else{var c=typeof b;A("expected object of type TrustedResourceUrl, got '"+b+"' of type "+("object"!=c?c:b?Array.isArray(b)?"array":c:"null"));b="type\_error:TrustedResourceUrl"}a.src=b;var e,d;(e=(b=null==(d=(e=(a.ownerDocument&&a.ownerDocument.defaultView||window).document).querySelector)?void 0:d.call(e,"script\[nonce\]"))?b.nonce||b.getAttribute("nonce")||"":"")&&a.setAttribute("nonce", e)};function ma(a){a=null===a?"null":void 0===a?"undefined":a;if("string"!==typeof a)throw Error("Expected a string");if(void 0===E){var b=null;var c=v.trustedTypes;if(c&&c.createPolicy)try{b=c.createPolicy("goog#html",{createHTML:x,createScript:x,createScriptURL:x})}catch(e){v.console&&v.console.error(e.message)}E=b}a=(b=E)?b.createScriptURL(a):a;return new G(a,F)};var na=function(a,b,c){var e=null;a&&0<a.length&&(e=parseInt(a\[a.length-1\].timestamp,10)+1);var d=null,g=null,p=void 0,q=null,B=(window.location.hash||"#").substring(1),X,Y;/^comment-form\_/.test(B)?X=B.substring(13):/^c\[0-9\]+$/.test(B)&&(Y=B.substring(1));var oa={id:c.postId,data:a,loadNext:function(l){if(e){var k=c.feed+"?alt=json&v=2&orderby=published&reverse=false&max-results=50";e&&(k+="&published-min="+(new Date(e)).toISOString());window.bloggercomments=function(C){e=null;var u=\[\];if(C&&C.feed&& C.feed.entry)for(var f,Z=0;f=C.feed.entry\[Z\];Z++){var m={},h=/blog-(\\d+).post-(\\d+)/.exec(f.id.$t);m.id=h?h\[2\]:null;a:{h=void 0;var aa=f&&(f.content&&f.content.$t||f.summary&&f.summary.$t)||"";if(f&&f.gd$extendedProperty)for(h in f.gd$extendedProperty)if("blogger.contentRemoved"==f.gd$extendedProperty\[h\].name){h='<span class="deleted-comment">'+aa+"</span>";break a}h=aa}m.body=h;m.timestamp=Date.parse(f.published.$t)+"";f.author&&f.author.constructor===Array&&(h=f.author\[0\])&&(m.author={name:h.name? h.name.$t:void 0,profileUrl:h.uri?h.uri.$t:void 0,avatarUrl:h.gd$image?h.gd$image.src:void 0});f.link&&(f.link\[2\]&&(m.link=m.permalink=f.link\[2\].href),f.link\[3\]&&(h=/.\*comments\\/default\\/(\\d+)\\?.\*/.exec(f.link\[3\].href))&&h\[1\]&&(m.parentId=h\[1\]));m.deleteclass="item-control blog-admin";if(f.gd$extendedProperty)for(var D in f.gd$extendedProperty)"blogger.itemClass"==f.gd$extendedProperty\[D\].name?m.deleteclass+=" "+f.gd$extendedProperty\[D\].value:"blogger.displayTime"==f.gd$extendedProperty\[D\].name&& (m.displayTime=f.gd$extendedProperty\[D\].value);u.push(m)}e=50>u.length?null:parseInt(u\[u.length-1\].timestamp,10)+1;l(u);window.bloggercomments=null};var N=fa();N.type="text/javascript";la(N,ma(k+"&callback=bloggercomments"));document.getElementsByTagName("head")\[0\].appendChild(N)}},hasMore:function(){return!!e},getMeta:function(l,k){return"iswriter"==l?k.author&&k.author.name==c.authorName&&k.author.profileUrl==c.authorUrl?"true":"":"deletelink"==l?c.baseUri+"/delete-comment.g?blogID="+c.blogId+"&postID="+ k.id:"deleteclass"==l?k.deleteclass:""},onReply:function(l,k){null==d&&(d=document.getElementById("comment-editor"),null!=d&&(q=d.style.height,d.style.display="block",g=d.src.split("#")));d&&l&&l!==p&&(document.getElementById(k).insertBefore(d,null),k=g\[0\]+(l?"&parentID="+l:""),g\[1\]&&(k=k+"#"+g\[1\]),d.src=k,d.style.height=q||d.style.height,p=l,d.removeAttribute("data-resized"),d.dispatchEvent(new Event("iframeMoved")))},rendered:!0,initComment:Y,initReplyThread:X,config:{maxDepth:c.maxThreadDepth}, messages:b};a=function(){if(window.goog&&window.goog.comments){var l=document.getElementById("comment-holder");window.goog.comments.render(l,oa)}};window.goog&&window.goog.comments?a():(window.goog=window.goog||{},window.goog.comments=window.goog.comments||{},window.goog.comments.loadQueue=window.goog.comments.loadQueue||\[\],window.goog.comments.loadQueue.push(a))},U=\["blogger","widgets","blog","initThreadedComments"\],V=v;U\[0\]in V||"undefined"==typeof V.execScript||V.execScript("var "+U\[0\]); for(var W;U.length&&(W=U.shift());)U.length||void 0===na?V=V\[W\]&&V\[W\]!==Object.prototype\[W\]?V\[W\]:V\[W\]={}:V\[W\]=na;}).call(this); blogger.widgets.blog.initThreadedComments( null, null, {});

1.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/19/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674106879413#c914335780925860148)
    
    密码呢
    
    [回复](javascript:;)[删除](https://www.blogger.com/delete-comment.g?blogID=8943566632081215369&postID=914335780925860148)
    
    [回复](javascript:;)
    
    [回复](javascript:;)
    
2.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/19/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674107429234#c1119778151782837724)
    
    好像用群晖更简单
    
    [回复](javascript:;)[删除](https://www.blogger.com/delete-comment.g?blogID=8943566632081215369&postID=1119778151782837724)
    
    [回复](javascript:;)
    
    [回复](javascript:;)
    
3.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/22/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674376538040#c1374173635169996971)
    
    能否出一期详细视频啊。。。
    
    [回复](javascript:;)[删除](https://www.blogger.com/delete-comment.g?blogID=8943566632081215369&postID=1374173635169996971)
    
    [回复](javascript:;)
    
    [回复](javascript:;)
    
4.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/22/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674393971966#c2572450637340079980)
    
    感谢分享，不过个人觉得镜像作者的 Github readme 要写得清楚一些
## Note