if(navigator.userAgent.match(/MSIE|Internet Explorer/i)||navigator.userAgent.match(/Trident\\/7\\..\*?rv:11/i)){var href=document.location.href;if(!href.match(/\[?&\]nowprocket/)){if(href.indexOf("?")==-1){if(href.indexOf("#")==-1){document.location.href=href+"?nowprocket=1"}else{document.location.href=href.replace("#","?nowprocket=1#")}}else{if(href.indexOf("#")==-1){document.location.href=href+"&nowprocket=1"}else{document.location.href=href.replace("#","&nowprocket=1#")}}}}class RocketLazyLoadScripts{constructor(){this.triggerEvents=\["keydown","mousedown","mousemove","touchmove","touchstart","touchend","wheel"\],this.userEventHandler=this.\_triggerListener.bind(this),this.touchStartHandler=this.\_onTouchStart.bind(this),this.touchMoveHandler=this.\_onTouchMove.bind(this),this.touchEndHandler=this.\_onTouchEnd.bind(this),this.clickHandler=this.\_onClick.bind(this),this.interceptedClicks=\[\],window.addEventListener("pageshow",(e=>{this.persisted=e.persisted})),window.addEventListener("DOMContentLoaded",(()=>{this.\_preconnect3rdParties()})),this.delayedScripts={normal:\[\],async:\[\],defer:\[\]},this.allJQueries=\[\]}\_addUserInteractionListener(e){document.hidden?e.\_triggerListener():(this.triggerEvents.forEach((t=>window.addEventListener(t,e.userEventHandler,{passive:!0}))),window.addEventListener("touchstart",e.touchStartHandler,{passive:!0}),window.addEventListener("mousedown",e.touchStartHandler),document.addEventListener("visibilitychange",e.userEventHandler))}\_removeUserInteractionListener(){this.triggerEvents.forEach((e=>window.removeEventListener(e,this.userEventHandler,{passive:!0}))),document.removeEventListener("visibilitychange",this.userEventHandler)}\_onTouchStart(e){"HTML"!==e.target.tagName&&(window.addEventListener("touchend",this.touchEndHandler),window.addEventListener("mouseup",this.touchEndHandler),window.addEventListener("touchmove",this.touchMoveHandler,{passive:!0}),window.addEventListener("mousemove",this.touchMoveHandler),e.target.addEventListener("click",this.clickHandler),this.\_renameDOMAttribute(e.target,"onclick","rocket-onclick"))}\_onTouchMove(e){window.removeEventListener("touchend",this.touchEndHandler),window.removeEventListener("mouseup",this.touchEndHandler),window.removeEventListener("touchmove",this.touchMoveHandler,{passive:!0}),window.removeEventListener("mousemove",this.touchMoveHandler),e.target.removeEventListener("click",this.clickHandler),this.\_renameDOMAttribute(e.target,"rocket-onclick","onclick")}\_onTouchEnd(e){window.removeEventListener("touchend",this.touchEndHandler),window.removeEventListener("mouseup",this.touchEndHandler),window.removeEventListener("touchmove",this.touchMoveHandler,{passive:!0}),window.removeEventListener("mousemove",this.touchMoveHandler)}\_onClick(e){e.target.removeEventListener("click",this.clickHandler),this.\_renameDOMAttribute(e.target,"rocket-onclick","onclick"),this.interceptedClicks.push(e),e.preventDefault(),e.stopPropagation(),e.stopImmediatePropagation()}\_replayClicks(){window.removeEventListener("touchstart",this.touchStartHandler,{passive:!0}),window.removeEventListener("mousedown",this.touchStartHandler),this.interceptedClicks.forEach((e=>{e.target.dispatchEvent(new MouseEvent("click",{view:e.view,bubbles:!0,cancelable:!0}))}))}\_renameDOMAttribute(e,t,n){e.hasAttribute&&e.hasAttribute(t)&&(event.target.setAttribute(n,event.target.getAttribute(t)),event.target.removeAttribute(t))}\_triggerListener(){this.\_removeUserInteractionListener(this),"loading"===document.readyState?document.addEventListener("DOMContentLoaded",this.\_loadEverythingNow.bind(this)):this.\_loadEverythingNow()}\_preconnect3rdParties(){let e=\[\];document.querySelectorAll("script\[type=rocketlazyloadscript\]").forEach((t=>{if(t.hasAttribute("src")){const n=new URL(t.src).origin;n!==location.origin&&e.push({src:n,crossOrigin:t.crossOrigin||"module"===t.getAttribute("data-rocket-type")})}})),e=\[...new Map(e.map((e=>\[JSON.stringify(e),e\]))).values()\],this.\_batchInjectResourceHints(e,"preconnect")}async \_loadEverythingNow(){this.lastBreath=Date.now(),this.\_delayEventListeners(),this.\_delayJQueryReady(this),this.\_handleDocumentWrite(),this.\_registerAllDelayedScripts(),this.\_preloadAllScripts(),await this.\_loadScriptsFromList(this.delayedScripts.normal),await this.\_loadScriptsFromList(this.delayedScripts.defer),await this.\_loadScriptsFromList(this.delayedScripts.async);try{await this.\_triggerDOMContentLoaded(),await this.\_triggerWindowLoad()}catch(e){}window.dispatchEvent(new Event("rocket-allScriptsLoaded")),this.\_replayClicks()}\_registerAllDelayedScripts(){document.querySelectorAll("script\[type=rocketlazyloadscript\]").forEach((e=>{e.hasAttribute("src")?e.hasAttribute("async")&&!1!==e.async?this.delayedScripts.async.push(e):e.hasAttribute("defer")&&!1!==e.defer||"module"===e.getAttribute("data-rocket-type")?this.delayedScripts.defer.push(e):this.delayedScripts.normal.push(e):this.delayedScripts.normal.push(e)}))}async \_transformScript(e){return await this.\_littleBreath(),new Promise((t=>{const n=document.createElement("script");\[...e.attributes\].forEach((e=>{let t=e.nodeName;"type"!==t&&("data-rocket-type"===t&&(t="type"),n.setAttribute(t,e.nodeValue))})),e.hasAttribute("src")?(n.addEventListener("load",t),n.addEventListener("error",t)):(n.text=e.text,t());try{e.parentNode.replaceChild(n,e)}catch(e){t()}}))}async \_loadScriptsFromList(e){const t=e.shift();return t?(await this.\_transformScript(t),this.\_loadScriptsFromList(e)):Promise.resolve()}\_preloadAllScripts(){this.\_batchInjectResourceHints(\[...this.delayedScripts.normal,...this.delayedScripts.defer,...this.delayedScripts.async\],"preload")}\_batchInjectResourceHints(e,t){var n=document.createDocumentFragment();e.forEach((e=>{if(e.src){const i=document.createElement("link");i.href=e.src,i.rel=t,"preconnect"!==t&&(i.as="script"),e.getAttribute&&"module"===e.getAttribute("data-rocket-type")&&(i.crossOrigin=!0),e.crossOrigin&&(i.crossOrigin=e.crossOrigin),n.appendChild(i)}})),document.head.appendChild(n)}\_delayEventListeners(){let e={};function t(t,n){!function(t){function n(n){return e\[t\].eventsToRewrite.indexOf(n)>=0?"rocket-"+n:n}e\[t\]||(e\[t\]={originalFunctions:{add:t.addEventListener,remove:t.removeEventListener},eventsToRewrite:\[\]},t.addEventListener=function(){arguments\[0\]=n(arguments\[0\]),e\[t\].originalFunctions.add.apply(t,arguments)},t.removeEventListener=function(){arguments\[0\]=n(arguments\[0\]),e\[t\].originalFunctions.remove.apply(t,arguments)})}(t),e\[t\].eventsToRewrite.push(n)}function n(e,t){let n=e\[t\];Object.defineProperty(e,t,{get:()=>n||function(){},set(i){e\["rocket"+t\]=n=i}})}t(document,"DOMContentLoaded"),t(window,"DOMContentLoaded"),t(window,"load"),t(window,"pageshow"),t(document,"readystatechange"),n(document,"onreadystatechange"),n(window,"onload"),n(window,"onpageshow")}\_delayJQueryReady(e){let t=window.jQuery;Object.defineProperty(window,"jQuery",{get:()=>t,set(n){if(n&&n.fn&&!e.allJQueries.includes(n)){n.fn.ready=n.fn.init.prototype.ready=function(t){e.domReadyFired?t.bind(document)(n):document.addEventListener("rocket-DOMContentLoaded",(()=>t.bind(document)(n)))};const t=n.fn.on;n.fn.on=n.fn.init.prototype.on=function(){if(this\[0\]===window){function e(e){return e.split(" ").map((e=>"load"===e||0===e.indexOf("load.")?"rocket-jquery-load":e)).join(" ")}"string"==typeof arguments\[0\]||arguments\[0\]instanceof String?arguments\[0\]=e(arguments\[0\]):"object"==typeof arguments\[0\]&&Object.keys(arguments\[0\]).forEach((t=>{delete Object.assign(arguments\[0\],{\[e(t)\]:arguments\[0\]\[t\]})\[t\]}))}return t.apply(this,arguments),this},e.allJQueries.push(n)}t=n}})}async \_triggerDOMContentLoaded(){this.domReadyFired=!0,await this.\_littleBreath(),document.dispatchEvent(new Event("rocket-DOMContentLoaded")),await this.\_littleBreath(),window.dispatchEvent(new Event("rocket-DOMContentLoaded")),await this.\_littleBreath(),document.dispatchEvent(new Event("rocket-readystatechange")),await this.\_littleBreath(),document.rocketonreadystatechange&&document.rocketonreadystatechange()}async \_triggerWindowLoad(){await this.\_littleBreath(),window.dispatchEvent(new Event("rocket-load")),await this.\_littleBreath(),window.rocketonload&&window.rocketonload(),await this.\_littleBreath(),this.allJQueries.forEach((e=>e(window).trigger("rocket-jquery-load"))),await this.\_littleBreath();const e=new Event("rocket-pageshow");e.persisted=this.persisted,window.dispatchEvent(e),await this.\_littleBreath(),window.rocketonpageshow&&window.rocketonpageshow({persisted:this.persisted})}\_handleDocumentWrite(){const e=new Map;document.write=document.writeln=function(t){const n=document.currentScript,i=document.createRange(),r=n.parentElement;let o=e.get(n);void 0===o&&(o=n.nextSibling,e.set(n,o));const s=document.createDocumentFragment();i.setStart(s,0),s.appendChild(i.createContextualFragment(t)),r.insertBefore(s,o)}}async \_littleBreath(){Date.now()-this.lastBreath>45&&(await this.\_requestAnimFrame(),this.lastBreath=Date.now())}async \_requestAnimFrame(){return document.hidden?new Promise((e=>setTimeout(e))):new Promise((e=>requestAnimationFrame(e)))}static run(){const e=new RocketLazyLoadScripts;e.\_addUserInteractionListener(e)}}RocketLazyLoadScripts.run();   var gtm4wp\_datalayer\_name = "dataLayer"; var dataLayer = dataLayer || \[\]; Linux Commands Cheat Sheet: Definitive List With Examples.wp-block-image{margin:0 0 1em}.wp-block-image img{height:auto;max-width:100%;vertical-align:bottom}.wp-block-image:not(.is-style-rounded) img{border-radius:inherit}.wp-block-image .aligncenter{display:table}.wp-block-image .aligncenter{margin-left:auto;margin-right:auto}.wp-block-image figure{margin:0}ol,ul{box-sizing:border-box}:root{--wp--preset--font-size--normal:16px;--wp--preset--font-size--huge:42px}.aligncenter{clear:both}.screen-reader-text{border:0;clip:rect(1px,1px,1px,1px);-webkit-clip-path:inset(50%);clip-path:inset(50%);height:1px;margin:-1px;overflow:hidden;padding:0;position:absolute;width:1px;word-wrap:normal!important}.screen-reader-text{clip:rect(1px,1px,1px,1px);height:1px;overflow:hidden;position:absolute!important;width:1px;word-wrap:normal!important;border:0}header{position:relative;-webkit-box-shadow:0 0 20px rgba(0,0,0,.05);box-shadow:0 0 20px rgba(0,0,0,.05)}#menu-primary .fas.fa-search{font-size:16px}.genesis-nav-menu{clear:both;line-height:1;width:100%;padding-left:0;margin-top:0;margin-bottom:0}.genesis-nav-menu .menu-item{display:block;float:none;position:relative}.genesis-nav-menu a{padding-top:20px;padding-left:20px;padding-right:20px;padding-bottom:20px;text-transform:uppercase;font-weight:700;color:#fff;font-size:12px;font-family:Roboto;letter-spacing:.6px}.genesis-responsive-menu{display:none;padding-bottom:15px;position:relative}.nav-primary{clear:left;width:100%}@media only screen and (min-width:960px){.genesis-nav-menu .menu-item{display:inline-block;text-align:center;padding-top:20px;padding-left:20px;padding-right:20px;padding-bottom:20px}.genesis-responsive-menu{display:block;padding-top:15px}.nav-primary{clear:none;float:right;width:auto;position:static;padding:15px 0;border-bottom:none;background-color:transparent}.nav-primary .genesis-nav-menu a{padding-left:15px;padding-right:15px}}@media only screen and (max-width:960px){.mobile-hidden{display:none!important}.nav-button a{border:1px solid #fff;border-radius:3px}.genesis-nav-menu .menu-item{text-align:center;padding-top:15px;padding-left:20px;padding-right:20px;padding-bottom:15px;margin-bottom:10px}.genesis-nav-menu .menu-item a{padding-top:15px;padding-left:20px;padding-right:20px;padding-bottom:15px}.mobile-search #searchform input\[type=text\]{height:36px;line-height:1}.mobile-search #searchform input\[type="submit"\]{-webkit-appearance:unset;background-color:#0074db;height:36px;border:none;padding:5px 10px;color:#fff;line-height:1}}button,input{overflow:visible}html{line-height:1.15;-ms-text-size-adjust:100%;-webkit-text-size-adjust:100%}body,h1{margin:0}figure,header,nav,section{display:block}figure{margin:1em 40px}code{font-family:monospace,monospace;font-size:1em}a{background-color:transparent;-webkit-text-decoration-skip:objects}strong{font-weight:bolder}img{border-style:none}svg:not(:root){overflow:hidden}button,input{font-size:100%;line-height:1.15;margin:0}button{text-transform:none}\[type="submit"\],button,html \[type="button"\]{-webkit-appearance:button}\[type="button"\]::-moz-focus-inner,\[type="submit"\]::-moz-focus-inner,button::-moz-focus-inner{border-style:none;padding:0}\[type="button"\]:-moz-focusring,\[type="submit"\]:-moz-focusring,button:-moz-focusring{outline:ButtonText dotted 1px}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}html{box-sizing:border-box}body{font-size:16px;color:rgba(64,64,64,1)}\*,::after,::before{box-sizing:inherit}.ct-section-inner-wrap{margin-left:auto;margin-right:auto;height:100%}div.ct-fancy-icon{display:inline-flex;border-radius:50%}.ct-fancy-icon>svg{fill:currentColor}.oxy-nav-menu-list{display:flex;padding:0;margin:0}.oxy-nav-menu .oxy-nav-menu-list li.menu-item{list-style-type:none;display:flex;flex-direction:column}.oxy-nav-menu .oxy-nav-menu-list li.menu-item a{text-decoration:none;border-style:solid;border-width:0;border-color:transparent}.oxy-nav-menu .menu-item,.oxy-nav-menu .sub-menu{position:relative}.oxy-nav-menu .menu-item .sub-menu{padding:0;flex-direction:column;white-space:nowrap;visibility:hidden;opacity:0;display:flex;position:absolute;top:100%}.oxy-nav-menu .sub-menu li.menu-item{flex-direction:column}.oxy-menu-toggle{display:none}.oxy-nav-menu:not(.oxy-nav-menu-open) .sub-menu{background-color:#fff;z-index:2147483641}.oxy-nav-menu-hamburger-wrap{display:flex;align-items:center;justify-content:center}.oxy-nav-menu-hamburger{display:flex;justify-content:space-between;flex-direction:column}.oxy-nav-menu-hamburger-line{border-radius:2px}.oxy-nav-menu .menu-item a{display:flex;align-items:center}.oxy-nav-menu-dropdowns.oxy-nav-menu-dropdown-arrow .menu-item-has-children>a::after{width:.35em;height:.35em;margin-left:.5em;border-right:.1em solid;border-top:.1em solid;transform:rotate(135deg);content:""}.oxy-stock-content-styles .aligncenter{margin-left:auto;margin-right:auto}.oxy-stock-content-styles img{max-width:100%}.oxy-modal-backdrop{display:flex;align-items:center;justify-content:center}body:not(.oxygen-builder-body) .oxy-modal-backdrop{display:none}.oxy-modal-backdrop .ct-modal{background-color:#fff;max-height:100vh;overflow-y:auto}.fas{-moz-osx-font-smoothing:grayscale;-webkit-font-smoothing:antialiased;display:inline-block;font-style:normal;font-variant:normal;text-rendering:auto;line-height:1}.fa-search:before{content:"\\f002"}@font-face{font-family:"font awesome 5 free";font-style:normal;font-weight:400;font-display:swap;src:url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-regular-400.eot);src:url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-regular-400.eot?#iefix) format("embedded-opentype"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-regular-400.woff2) format("woff2"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-regular-400.woff) format("woff"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-regular-400.ttf) format("truetype"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-regular-400.svg#fontawesome) format("svg")}@font-face{font-family:"font awesome 5 free";font-style:normal;font-weight:900;font-display:swap;src:url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-solid-900.eot);src:url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-solid-900.eot?#iefix) format("embedded-opentype"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-solid-900.woff2) format("woff2"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-solid-900.woff) format("woff"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-solid-900.ttf) format("truetype"),url(https://use.fontawesome.com/releases/v5.15.3/css/../webfonts/fa-solid-900.svg#fontawesome) format("svg")}.fas{font-family:"font awesome 5 free"}.fas{font-weight:900}@font-face{font-display:swap;src:url(https://phoenixnap.com/kb/wp-content/plugins/fixed-toc/frontend/assets/fonts/icons.eot?45335921);src:url(https://phoenixnap.com/kb/wp-content/plugins/fixed-toc/frontend/assets/fonts/icons.eot?45335921#iefix) format("embedded-opentype"),url(https://phoenixnap.com/kb/wp-content/plugins/fixed-toc/frontend/assets/fonts/icons.woff2?45335921) format("woff2"),url(https://phoenixnap.com/kb/wp-content/plugins/fixed-toc/frontend/assets/fonts/icons.woff?45335921) format("woff"),url(https://phoenixnap.com/kb/wp-content/plugins/fixed-toc/frontend/assets/fonts/icons.ttf?45335921) format("truetype"),url(https://phoenixnap.com/kb/wp-content/plugins/fixed-toc/frontend/assets/fonts/icons.svg?45335921#fontello) format("svg");font-family:"ftwp-icon"}#ftwp-container.ftwp-wrap,#ftwp-container.ftwp-wrap a,#ftwp-container.ftwp-wrap a:link,#ftwp-container.ftwp-wrap a:visited,#ftwp-container.ftwp-wrap button,#ftwp-container.ftwp-wrap header,#ftwp-container.ftwp-wrap li,#ftwp-container.ftwp-wrap li::after,#ftwp-container.ftwp-wrap li::before,#ftwp-container.ftwp-wrap nav,#ftwp-container.ftwp-wrap ol,#ftwp-container.ftwp-wrap span{margin:0;padding:0;line-height:inherit;font:inherit;color:inherit;background:0 0;box-shadow:none;text-shadow:none;text-decoration:none;text-align:inherit;border:0;outline:0;box-sizing:border-box;border-radius:0;clear:none}#ftwp-container.ftwp-wrap button{min-height:initial}#ftwp-container.ftwp-wrap li{list-style:none}#ftwp-container.ftwp-wrap header::before,#ftwp-container.ftwp-wrap li::after,#ftwp-container.ftwp-wrap li::before,#ftwp-container.ftwp-wrap nav::before{display:none}#ftwp-container.ftwp-wrap{font-family:inherit;font-size:12px}#ftwp-container.ftwp-wrap #ftwp-list .ftwp-anchor::before,#ftwp-container.ftwp-wrap .ftwp-icon-collapse,#ftwp-container.ftwp-wrap .ftwp-icon-expand,#ftwp-container.ftwp-wrap .ftwp-icon-menu{display:inline-block;font-family:"ftwp-icon";font-style:normal;font-weight:400;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}#ftwp-container.ftwp-wrap .ftwp-icon-menu::before{content:""}#ftwp-container.ftwp-wrap .ftwp-icon-expand::before{content:""}#ftwp-container.ftwp-wrap .ftwp-icon-collapse::before{content:""}#ftwp-container.ftwp-wrap #ftwp-trigger{display:inline-block;width:50px;height:50px;background:rgba(238,238,238,.95);color:#333;font-size:30px;position:relative}#ftwp-container.ftwp-wrap #ftwp-trigger .ftwp-trigger-icon{position:absolute;top:50%;left:50%;-webkit-transform:translate(-50%,-50%);-ms-transform:translate(-50%,-50%);transform:translate(-50%,-50%)}#ftwp-container.ftwp-wrap #ftwp-contents{width:250px;max-width:100%;overflow:hidden;height:auto;max-height:100%}#ftwp-container.ftwp-wrap #ftwp-header{color:#333;background:rgba(238,238,238,.95);padding:10px;font-size:19.2px;line-height:1.5}#ftwp-container.ftwp-wrap #ftwp-header-control{float:left;margin-right:5px}#ftwp-container.ftwp-wrap #ftwp-header-title{font-weight:700;display:block;overflow:hidden;width:auto}#ftwp-container.ftwp-wrap #ftwp-header-minimize{float:right;margin-left:5px;width:25px;text-align:center;opacity:.5}#ftwp-container.ftwp-wrap #ftwp-header::after{content:"";display:table;clear:both}#ftwp-container.ftwp-wrap #ftwp-list{color:#333;font-size:12px;background:rgba(238,238,238,.95);line-height:1.2;overflow-y:auto;width:100%}#ftwp-container.ftwp-wrap #ftwp-list .ftwp-item{text-indent:0}#ftwp-container.ftwp-wrap #ftwp-list .ftwp-anchor{display:block;padding:5px 10px;z-index:10;overflow:hidden;position:relative}#ftwp-container #ftwp-contents.ftwp-border-thin,#ftwp-container #ftwp-trigger.ftwp-border-thin{border-color:rgba(51,51,51,.95);border-style:solid;border-width:1px}#ftwp-container #ftwp-trigger.ftwp-border-thin{font-size:29.5px}#ftwp-container.ftwp-wrap .ftwp-shape-round{border-radius:7px}#ftwp-container #ftwp-list .ftwp-anchor::before{float:left;font-size:4.8px;line-height:3;margin-right:10px}#ftwp-container #ftwp-list .ftwp-text{display:block;overflow:hidden}#ftwp-container #ftwp-list.ftwp-list-nest.ftwp-liststyle-decimal ol,#ftwp-container #ftwp-list.ftwp-liststyle-decimal{counter-reset:List}#ftwp-container #ftwp-list.ftwp-liststyle-decimal .ftwp-item{counter-increment:List}#ftwp-container #ftwp-list.ftwp-liststyle-decimal .ftwp-anchor::before{font-size:12px;line-height:1.2;font-family:inherit;content:counters(List,".")}#ftwp-container #ftwp-list.ftwp-list-nest .ftwp-sub .ftwp-anchor::before{margin-left:20px}#ftwp-container #ftwp-list.ftwp-list-nest.ftwp-colexp-icon .ftwp-anchor{padding-left:32px}#ftwp-container #ftwp-list.ftwp-list-nest.ftwp-colexp .ftwp-has-sub{position:relative}#ftwp-container #ftwp-list.ftwp-list-nest.ftwp-colexp .ftwp-icon-expand{position:absolute;left:0;top:0;padding:5px 10px;box-sizing:content-box;opacity:.5;z-index:20}#ftwp-container #ftwp-list.ftwp-strong-first.ftwp-liststyle-decimal>.ftwp-item>.ftwp-anchor::before,#ftwp-container #ftwp-list.ftwp-strong-first>.ftwp-item>.ftwp-anchor .ftwp-text{font-size:13.2px;font-weight:700}.ftwp-in-post#ftwp-container-outer{margin-bottom:20px;max-width:100%}.ftwp-in-post#ftwp-container-outer,.ftwp-in-post#ftwp-container-outer #ftwp-contents{height:auto;overflow-y:hidden;position:relative;z-index:1}.ftwp-in-post#ftwp-container-outer.ftwp-float-none,.ftwp-in-post#ftwp-container-outer.ftwp-float-none #ftwp-contents{width:100%}.ftwp-in-post#ftwp-container-outer #ftwp-trigger{position:absolute;top:-9999px;z-index:-10;visibility:hidden}#ftwp-container.ftwp-hidden-state{opacity:0;visibility:hidden;z-index:-9999;position:absolute;top:0;left:0}#div\_block-6-156{position:fixed;right:0;bottom:0}#div\_block-8-156{position:fixed;bottom:55px;right:50px;padding-top:5px;padding-left:5px;padding-right:5px;padding-bottom:5px;background-color:rgba(0,116,219,.5);border-radius:50%}@media (max-width:991px){#div\_block-6-156{display:none}}@media (max-width:991px){#div\_block-8-156{display:none}}#link-9-156{url-encoded:true}#fancy\_icon-10-156{color:rgba(255,255,255,.5)}#fancy\_icon-10-156>svg{width:36px;height:36px}#\_nav\_menu-133-7 .oxy-nav-menu-hamburger-line{background-color:rgba(255,255,255,.7)}#\_nav\_menu-133-7 .oxy-nav-menu-hamburger-wrap{width:40px;height:40px;margin-top:10px;margin-bottom:10px}#\_nav\_menu-133-7 .oxy-nav-menu-hamburger{width:40px;height:32px}#\_nav\_menu-133-7 .oxy-nav-menu-hamburger-line{height:6px}#\_nav\_menu-11-156 .oxy-nav-menu-hamburger-line{background-color:rgba(255,255,255,.7)}#\_nav\_menu-11-156 .oxy-nav-menu-hamburger-wrap{width:40px;height:40px;margin-top:10px;margin-bottom:10px}#\_nav\_menu-11-156 .oxy-nav-menu-hamburger{width:40px;height:32px}#\_nav\_menu-11-156 .oxy-nav-menu-hamburger-line{height:6px}#\_nav\_menu-36-155 .oxy-nav-menu-hamburger-line{background-color:#00a7e0}#\_nav\_menu-36-155 .oxy-nav-menu-hamburger-wrap{width:40px;height:40px;margin-top:10px;margin-bottom:10px}#\_nav\_menu-36-155 .oxy-nav-menu-hamburger{width:40px;height:32px}#\_nav\_menu-36-155 .oxy-nav-menu-hamburger-line{height:6px}#section-164-137>.ct-section-inner-wrap{max-width:100%;padding-top:5px;padding-right:0;padding-bottom:5px;padding-left:0;display:flex;flex-direction:row;align-items:center;justify-content:flex-end}#section-164-137{background-color:#f7f7f7;text-align:right}@media (max-width:991px){#section-164-137>.ct-section-inner-wrap{display:none;flex-direction:unset}}#\_nav\_menu-9-7 .oxy-nav-menu-hamburger-line{background-color:#000}#\_nav\_menu-9-7 .oxy-nav-menu-hamburger-wrap{width:40px;height:40px;margin-top:10px;margin-bottom:10px}#\_nav\_menu-9-7 .oxy-nav-menu-hamburger{width:40px;height:32px}#\_nav\_menu-9-7 .oxy-nav-menu-hamburger-line{height:6px}#\_nav\_menu-9-7{z-index:9999}#\_nav\_menu-9-7 .menu-item a{padding-top:4px;padding-left:8px;padding-right:8px;padding-bottom:4px;color:#000;font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:1px}#\_nav\_menu-9-7.oxy-nav-menu:not(.oxy-nav-menu-open) .sub-menu{background-color:#fff}#\_nav\_menu-9-7.oxy-nav-menu:not(.oxy-nav-menu-open) .sub-menu .menu-item a{border:0;padding-top:4px;padding-bottom:4px;color:#1d7cb1;padding-top:10px;padding-left:5px;padding-right:5px;padding-bottom:10px}#section-205-157>.ct-section-inner-wrap{max-width:100%;padding-top:0;padding-right:0;padding-bottom:0;padding-left:0;display:flex;flex-direction:column;align-items:center;justify-content:space-between}#section-205-157{text-align:center;background-color:#08557f}#section-78-157>.ct-section-inner-wrap{max-width:100%;padding-top:10px;padding-bottom:10px;align-items:center}#section-78-157{text-align:center}@media (max-width:991px){#section-205-157>.ct-section-inner-wrap{padding-top:0;padding-right:0;padding-bottom:0;padding-left:0}}#div\_block-206-157{width:100%;padding-left:36px;padding-right:36px;flex-direction:row;display:flex;align-items:center;justify-content:space-between;text-align:justify;border-bottom-color:#fff;border-bottom-width:1px;border-bottom-style:solid}#div\_block-210-157{margin-top:36px;margin-bottom:36px;align-items:center;text-align:center;flex-direction:column;display:flex}#div\_block-213-157{flex-direction:row;display:flex;justify-content:space-between;text-align:justify;align-items:flex-start}#div\_block-81-157{width:20%}#div\_block-82-157{width:60%}#div\_block-83-157{width:20%}@media (max-width:991px){#div\_block-206-157{display:block;padding-left:0;padding-right:0}}@media (max-width:767px){#div\_block-210-157{width:100%;padding-left:36px;padding-right:36px;flex-direction:column;display:flex}}@media (max-width:767px){#div\_block-213-157{flex-direction:column;display:flex;align-items:center;text-align:center}}@media (max-width:991px){#new\_columns-80-157>.ct-div-block{width:100%!important}}#new\_columns-80-157{width:100%;max-width:1320px}#headline-211-157{color:#fff;font-size:38px;font-weight:700;margin-bottom:36px}@media (max-width:767px){#headline-211-157{font-size:28px;word-break:break-word}}#text\_block-214-157{color:#fff;font-family:'Roboto';font-size:16px;margin-right:18px}#text\_block-86-157{text-align:left}#link-207-157{url-encoded:true}@media (max-width:991px){#link-207-157{float:left;margin-top:10px;margin-left:20px}}#shortcode-181-157{width:100%}@media (max-width:991px){#shortcode-209-157{background-color:rgba(0,0,0,.7)}}#modal-203-157{width:70%;background-color:rgba(255,255,255,0);flex-direction:column;display:flex;text-align:center;align-items:center;justify-content:center;modal-position:center;backdrop-color:rgba(0,0,0,.7)}div.ct-section-inner-wrap{max-width:1600px}.ct-section{width:100%;background-size:cover;background-repeat:repeat}.ct-section>.ct-section-inner-wrap{display:flex;flex-direction:column;align-items:flex-start}.ct-div-block{display:flex;flex-wrap:nowrap;flex-direction:column;align-items:flex-start}.ct-new-columns{display:flex;width:100%;flex-direction:row;align-items:stretch;justify-content:center;flex-wrap:wrap}.ct-link{display:flex;flex-wrap:wrap;text-align:center;text-decoration:none;flex-direction:column;align-items:center;justify-content:center}.ct-image{max-width:100%}.ct-fancy-icon>svg{width:55px;height:55px}.ct-modal{flex-direction:column;align-items:flex-start}.ct-span{display:inline-block;text-decoration:inherit}@media screen and (-ms-high-contrast:active),(-ms-high-contrast:none){.ct-div-block,.ct-text-block,.ct-headline{max-width:100%}img{flex-shrink:0}body \*{min-height:1px}}.ct-section-inner-wrap{max-width:1600px}body{font-family:roboto}body{line-height:1.6;font-size:16px;font-weight:400;color:#404040}.oxy-nav-menu-hamburger-line{background-color:#404040}h1{font-family:poppins;font-size:38px;font-weight:700}a{color:#0074db;text-decoration:none}.ct-link{text-decoration:}.ct-section-inner-wrap{padding-top:75px;padding-right:20px;padding-bottom:75px;padding-left:20px}.ct-new-columns>.ct-div-block{padding-top:20px;padding-right:20px;padding-bottom:20px;padding-left:20px}h1{font-family:poppins,sans-serif;word-break:break-word}p{font-family:roboto,sans-serif;word-break:break-word;margin-block-start:0;margin-block-end:1em}li{word-break:break-word}p.h3{font-size:24px;font-weight:900}code{background-color:#f7f7f7;overflow:auto;white-space:pre-wrap;word-wrap:break-word;word-break:break-all}ul{display:block;list-style-type:disc;margin-block-start:0;margin-block-end:20px;margin-inline-start:0;margin-inline-end:0;padding-inline-start:20px}li.widget{list-style:none}img{height:auto;max-width:100%}figure{margin:0}a{word-break:break-word}.ct-span{display:block}.ct-code-block{word-break:break-all}#menu-top-menu li.bordered-top-nav{border:1px solid #000;line-height:1.5;border-radius:.2rem;margin-right:10px;will-change:box-shadow,transform}.tag-wrapper a{font-size:11px;padding:2px 5px;display:inline-block;border:1px solid;border-radius:4px;margin:0 5px 9px 0;text-transform:uppercase;font-weight:600;color:#fff}#menu-top-menu ul.sub-menu{padding:5px 10px!important;background-color:#fff!important}#menu-top-menu ul.sub-menu .menu-item a{font-weight:400;text-transform:capitalize;color:##212529;font-size:14px!important;background-color:#fff!important}.single-post .single-post-header .ct-section-inner-wrap{padding-left:0!important;padding-right:0!important}@media (min-width:1025px){.desktop-hidden{display:none!important}}@media (max-width:767px){.oxy-nav-menu-hamburger-line{height:3px!important}}@font-face{font-family:Roboto;font-style:normal;font-weight:400;font-display:swap;src:local("Roboto"),local("Roboto-Regular"),url(/wp-content/themes/pnap-cpt/dist/fonts/roboto-v20-latin-regular\_479970ff.woff2) format("woff2")}@font-face{font-family:Roboto;font-style:normal;font-weight:700;font-display:swap;src:local("Roboto Bold"),local("Roboto-Bold"),url(/wp-content/themes/pnap-cpt/dist/fonts/roboto-v20-latin-700\_2735a3a6.woff2) format("woff2")}                     {"@context":"https://schema.org","@graph":\[{"@type":"Article","@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#article","isPartOf":{"@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet"},"author":{"name":"Sofija Simic","@id":"https://phoenixnap.com/kb/#/schema/person/7e705ff0dcd3af981debc836e5afd6b9"},"headline":"Linux Commands Cheat Sheet: With Examples","datePublished":"2020-02-21T19:17:44+00:00","dateModified":"2023-02-14T14:48:39+00:00","mainEntityOfPage":{"@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet"},"wordCount":1409,"publisher":{"@id":"https://phoenixnap.com/kb/#organization"},"image":{"@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#primaryimage"},"thumbnailUrl":"https://phoenixnap.com/kb/wp-content/uploads/2021/04/linux-command-cheat-sheet.png","keywords":\["commands","linux"\],"articleSection":\["SysAdmin","Web Servers"\],"inLanguage":"en-US"},{"@type":"WebPage","@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet","url":"https://phoenixnap.com/kb/linux-commands-cheat-sheet","name":"Linux Commands Cheat Sheet: Definitive List With Examples","isPartOf":{"@id":"https://phoenixnap.com/kb/#website"},"primaryImageOfPage":{"@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#primaryimage"},"image":{"@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#primaryimage"},"thumbnailUrl":"https://phoenixnap.com/kb/wp-content/uploads/2021/04/linux-command-cheat-sheet.png","datePublished":"2020-02-21T19:17:44+00:00","dateModified":"2023-02-14T14:48:39+00:00","description":"Linux command syntax may seem difficult to remember. Use our 2020 Linux Command Cheat Sheet with examples. All the important commands in one pdf.","breadcrumb":{"@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#breadcrumb"},"inLanguage":"en-US","potentialAction":\[{"@type":"ReadAction","target":\["https://phoenixnap.com/kb/linux-commands-cheat-sheet"\]}\]},{"@type":"ImageObject","inLanguage":"en-US","@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#primaryimage","url":"https://phoenixnap.com/kb/wp-content/uploads/2021/04/linux-command-cheat-sheet.png","contentUrl":"https://phoenixnap.com/kb/wp-content/uploads/2021/04/linux-command-cheat-sheet.png","width":800,"height":400},{"@type":"BreadcrumbList","@id":"https://phoenixnap.com/kb/linux-commands-cheat-sheet#breadcrumb","itemListElement":\[{"@type":"ListItem","position":1,"name":"Home","item":"https://phoenixnap.com/kb/"},{"@type":"ListItem","position":2,"name":"SysAdmin","item":"https://phoenixnap.com/kb/category/sysadmin"},{"@type":"ListItem","position":3,"name":"Linux Commands Cheat Sheet: With Examples"}\]},{"@type":"WebSite","@id":"https://phoenixnap.com/kb/#website","url":"https://phoenixnap.com/kb/","name":"Knowledge Base by phoenixNAP","description":"","publisher":{"@id":"https://phoenixnap.com/kb/#organization"},"potentialAction":\[{"@type":"SearchAction","target":{"@type":"EntryPoint","urlTemplate":"https://phoenixnap.com/kb/?s={search\_term\_string}"},"query-input":"required name=search\_term\_string"}\],"inLanguage":"en-US"},{"@type":"Organization","@id":"https://phoenixnap.com/kb/#organization","name":"phoenixNAP","url":"https://phoenixnap.com/kb/","logo":{"@type":"ImageObject","inLanguage":"en-US","@id":"https://phoenixnap.com/kb/#/schema/logo/image/","url":"https://phoenixnap.com/kb/wp-content/uploads/2021/04/pnap-authors.png","contentUrl":"https://phoenixnap.com/kb/wp-content/uploads/2021/04/pnap-authors.png","width":200,"height":200,"caption":"phoenixNAP"},"image":{"@id":"https://phoenixnap.com/kb/#/schema/logo/image/"},"sameAs":\["https://www.linkedin.com/company/phoenix-nap/","https://www.youtube.com/user/PhoenixNAPdatacenter","https://www.facebook.com/phoenixnap","https://twitter.com/phoenixNAP"\]},{"@type":"Person","@id":"https://phoenixnap.com/kb/#/schema/person/7e705ff0dcd3af981debc836e5afd6b9","name":"Sofija Simic","image":{"@type":"ImageObject","inLanguage":"en-US","@id":"https://phoenixnap.com/kb/#/schema/person/image/","url":"https://secure.gravatar.com/avatar/f294f4ff5c2ada61b6f006327af47bfc?s=96&d=mm&r=g","contentUrl":"https://secure.gravatar.com/avatar/f294f4ff5c2ada61b6f006327af47bfc?s=96&d=mm&r=g","caption":"Sofija Simic"},"description":"Sofija Simic is an experienced Technical Writer. Alongside her educational background in teaching and writing, she has had a lifelong passion for information technology. She is committed to unscrambling confusing IT concepts and streamlining intricate software installations."}\]}     body{--wp--preset--color--black: #000000;--wp--preset--color--cyan-bluish-gray: #abb8c3;--wp--preset--color--white: #ffffff;--wp--preset--color--pale-pink: #f78da7;--wp--preset--color--vivid-red: #cf2e2e;--wp--preset--color--luminous-vivid-orange: #ff6900;--wp--preset--color--luminous-vivid-amber: #fcb900;--wp--preset--color--light-green-cyan: #7bdcb5;--wp--preset--color--vivid-green-cyan: #00d084;--wp--preset--color--pale-cyan-blue: #8ed1fc;--wp--preset--color--vivid-cyan-blue: #0693e3;--wp--preset--color--vivid-purple: #9b51e0;--wp--preset--gradient--vivid-cyan-blue-to-vivid-purple: linear-gradient(135deg,rgba(6,147,227,1) 0%,rgb(155,81,224) 100%);--wp--preset--gradient--light-green-cyan-to-vivid-green-cyan: linear-gradient(135deg,rgb(122,220,180) 0%,rgb(0,208,130) 100%);--wp--preset--gradient--luminous-vivid-amber-to-luminous-vivid-orange: linear-gradient(135deg,rgba(252,185,0,1) 0%,rgba(255,105,0,1) 100%);--wp--preset--gradient--luminous-vivid-orange-to-vivid-red: linear-gradient(135deg,rgba(255,105,0,1) 0%,rgb(207,46,46) 100%);--wp--preset--gradient--very-light-gray-to-cyan-bluish-gray: linear-gradient(135deg,rgb(238,238,238) 0%,rgb(169,184,195) 100%);--wp--preset--gradient--cool-to-warm-spectrum: linear-gradient(135deg,rgb(74,234,220) 0%,rgb(151,120,209) 20%,rgb(207,42,186) 40%,rgb(238,44,130) 60%,rgb(251,105,98) 80%,rgb(254,248,76) 100%);--wp--preset--gradient--blush-light-purple: linear-gradient(135deg,rgb(255,206,236) 0%,rgb(152,150,240) 100%);--wp--preset--gradient--blush-bordeaux: linear-gradient(135deg,rgb(254,205,165) 0%,rgb(254,45,45) 50%,rgb(107,0,62) 100%);--wp--preset--gradient--luminous-dusk: linear-gradient(135deg,rgb(255,203,112) 0%,rgb(199,81,192) 50%,rgb(65,88,208) 100%);--wp--preset--gradient--pale-ocean: linear-gradient(135deg,rgb(255,245,203) 0%,rgb(182,227,212) 50%,rgb(51,167,181) 100%);--wp--preset--gradient--electric-grass: linear-gradient(135deg,rgb(202,248,128) 0%,rgb(113,206,126) 100%);--wp--preset--gradient--midnight: linear-gradient(135deg,rgb(2,3,129) 0%,rgb(40,116,252) 100%);--wp--preset--duotone--dark-grayscale: url('#wp-duotone-dark-grayscale');--wp--preset--duotone--grayscale: url('#wp-duotone-grayscale');--wp--preset--duotone--purple-yellow: url('#wp-duotone-purple-yellow');--wp--preset--duotone--blue-red: url('#wp-duotone-blue-red');--wp--preset--duotone--midnight: url('#wp-duotone-midnight');--wp--preset--duotone--magenta-yellow: url('#wp-duotone-magenta-yellow');--wp--preset--duotone--purple-green: url('#wp-duotone-purple-green');--wp--preset--duotone--blue-orange: url('#wp-duotone-blue-orange');--wp--preset--font-size--small: 13px;--wp--preset--font-size--medium: 20px;--wp--preset--font-size--large: 36px;--wp--preset--font-size--x-large: 42px;}.has-black-color{color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-color{color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-color{color: var(--wp--preset--color--white) !important;}.has-pale-pink-color{color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-color{color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-color{color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-color{color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-color{color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-color{color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-color{color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-color{color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-color{color: var(--wp--preset--color--vivid-purple) !important;}.has-black-background-color{background-color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-background-color{background-color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-background-color{background-color: var(--wp--preset--color--white) !important;}.has-pale-pink-background-color{background-color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-background-color{background-color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-background-color{background-color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-background-color{background-color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-background-color{background-color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-background-color{background-color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-background-color{background-color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-background-color{background-color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-background-color{background-color: var(--wp--preset--color--vivid-purple) !important;}.has-black-border-color{border-color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-border-color{border-color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-border-color{border-color: var(--wp--preset--color--white) !important;}.has-pale-pink-border-color{border-color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-border-color{border-color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-border-color{border-color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-border-color{border-color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-border-color{border-color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-border-color{border-color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-border-color{border-color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-border-color{border-color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-border-color{border-color: var(--wp--preset--color--vivid-purple) !important;}.has-vivid-cyan-blue-to-vivid-purple-gradient-background{background: var(--wp--preset--gradient--vivid-cyan-blue-to-vivid-purple) !important;}.has-light-green-cyan-to-vivid-green-cyan-gradient-background{background: var(--wp--preset--gradient--light-green-cyan-to-vivid-green-cyan) !important;}.has-luminous-vivid-amber-to-luminous-vivid-orange-gradient-background{background: var(--wp--preset--gradient--luminous-vivid-amber-to-luminous-vivid-orange) !important;}.has-luminous-vivid-orange-to-vivid-red-gradient-background{background: var(--wp--preset--gradient--luminous-vivid-orange-to-vivid-red) !important;}.has-very-light-gray-to-cyan-bluish-gray-gradient-background{background: var(--wp--preset--gradient--very-light-gray-to-cyan-bluish-gray) !important;}.has-cool-to-warm-spectrum-gradient-background{background: var(--wp--preset--gradient--cool-to-warm-spectrum) !important;}.has-blush-light-purple-gradient-background{background: var(--wp--preset--gradient--blush-light-purple) !important;}.has-blush-bordeaux-gradient-background{background: var(--wp--preset--gradient--blush-bordeaux) !important;}.has-luminous-dusk-gradient-background{background: var(--wp--preset--gradient--luminous-dusk) !important;}.has-pale-ocean-gradient-background{background: var(--wp--preset--gradient--pale-ocean) !important;}.has-electric-grass-gradient-background{background: var(--wp--preset--gradient--electric-grass) !important;}.has-midnight-gradient-background{background: var(--wp--preset--gradient--midnight) !important;}.has-small-font-size{font-size: var(--wp--preset--font-size--small) !important;}.has-medium-font-size{font-size: var(--wp--preset--font-size--medium) !important;}.has-large-font-size{font-size: var(--wp--preset--font-size--large) !important;}.has-x-large-font-size{font-size: var(--wp--preset--font-size--x-large) !important;}     .scriptlesssocialsharing\_\_buttons a.button { padding: 12px; flex: 1; }@media only screen and (max-width: 767px) { .scriptlesssocialsharing .sss-name { position: absolute; clip: rect(1px, 1px, 1px, 1px); height: 1px; width: 1px; border: 0; overflow: hidden; } }     .ftwp-in-post#ftwp-container-outer { height: auto; } #ftwp-container.ftwp-wrap #ftwp-contents { width: 250px; height: auto; } .ftwp-in-post#ftwp-container-outer #ftwp-contents { height: auto; } .ftwp-in-post#ftwp-container-outer.ftwp-float-none #ftwp-contents { width: 250px; } #ftwp-container.ftwp-wrap #ftwp-trigger { width: 56px; height: 56px; font-size: 33.6px; } #ftwp-container #ftwp-trigger.ftwp-border-thin { font-size: 33.1px; } #ftwp-container.ftwp-wrap #ftwp-header { font-size: 18px; font-family: inherit; } #ftwp-container.ftwp-wrap #ftwp-header-title { font-weight: bold; } #ftwp-container.ftwp-wrap #ftwp-list { font-size: 14px; font-family: inherit; } #ftwp-container #ftwp-list.ftwp-liststyle-decimal .ftwp-anchor::before { font-size: 14px; } #ftwp-container #ftwp-list.ftwp-strong-first>.ftwp-item>.ftwp-anchor .ftwp-text { font-size: 15.4px; } #ftwp-container #ftwp-list.ftwp-strong-first.ftwp-liststyle-decimal>.ftwp-item>.ftwp-anchor::before { font-size: 15.4px; } #ftwp-container.ftwp-wrap #ftwp-trigger { color: #af2028; background: rgba(255,255,255,0.95); } #ftwp-container.ftwp-wrap #ftwp-trigger { border-color: rgba(227,227,227,0.95); } #ftwp-container.ftwp-wrap #ftwp-contents { border-color: rgba(227,227,227,0.95); } #ftwp-container.ftwp-wrap #ftwp-header { color: #777777; background: rgba(255,255,255,0.95); } #ftwp-container.ftwp-wrap #ftwp-contents:hover #ftwp-header { background: #ffffff; } #ftwp-container.ftwp-wrap #ftwp-list { color: #999999; background: rgba(255,255,255,0.95); } #ftwp-container.ftwp-wrap #ftwp-contents:hover #ftwp-list { background: #ffffff; } #ftwp-container.ftwp-wrap #ftwp-list .ftwp-anchor:hover { color: #555555; } #ftwp-container.ftwp-wrap #ftwp-list .ftwp-anchor:focus, #ftwp-container.ftwp-wrap #ftwp-list .ftwp-active, #ftwp-container.ftwp-wrap #ftwp-list .ftwp-active:hover { color: #555555; } #ftwp-container.ftwp-wrap #ftwp-list .ftwp-text::before { background: rgba(227,227,227,0.95); } .ftwp-heading-target::before { background: rgba(85,85,85,0.95); } #ftwp-container #ftwp-list.ftwp-effect-fade .ftwp-anchor.ftwp-active, #ftwp-container #ftwp-list.ftwp-effect-fade .ftwp-anchor:focus { background: rgba(227,227,227,0.95); } .ftwp-in-post#ftwp-container-outer.ftwp-float-none #ftwp-contents { width: 100%; } #ftwp-container.ftwp-wrap #ftwp-header-title { text-align: left; } #ftwp-container #ftwp-list .ftwp-text { text-align: left; }  @font-face { font-family: "FontAwesome"; font-display: block; src: url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-brands-400.eot"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-brands-400.eot?#iefix") format("embedded-opentype"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-brands-400.woff2") format("woff2"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-brands-400.woff") format("woff"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-brands-400.ttf") format("truetype"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-brands-400.svg#fontawesome") format("svg"); } @font-face { font-family: "FontAwesome"; font-display: block; src: url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-solid-900.eot"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-solid-900.eot?#iefix") format("embedded-opentype"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-solid-900.woff2") format("woff2"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-solid-900.woff") format("woff"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-solid-900.ttf") format("truetype"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-solid-900.svg#fontawesome") format("svg"); } @font-face { font-family: "FontAwesome"; font-display: block; src: url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-regular-400.eot"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-regular-400.eot?#iefix") format("embedded-opentype"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-regular-400.woff2") format("woff2"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-regular-400.woff") format("woff"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-regular-400.ttf") format("truetype"), url("https://use.fontawesome.com/releases/v5.15.3/webfonts/fa-regular-400.svg#fontawesome") format("svg"); unicode-range: U+F004-F005,U+F007,U+F017,U+F022,U+F024,U+F02E,U+F03E,U+F044,U+F057-F059,U+F06E,U+F070,U+F075,U+F07B-F07C,U+F080,U+F086,U+F089,U+F094,U+F09D,U+F0A0,U+F0A4-F0A7,U+F0C5,U+F0C7-F0C8,U+F0E0,U+F0EB,U+F0F3,U+F0F8,U+F0FE,U+F111,U+F118-F11A,U+F11C,U+F133,U+F144,U+F146,U+F14A,U+F14D-F14E,U+F150-F152,U+F15B-F15C,U+F164-F165,U+F185-F186,U+F191-F192,U+F1AD,U+F1C1-F1C9,U+F1CD,U+F1D8,U+F1E3,U+F1EA,U+F1F6,U+F1F9,U+F20A,U+F247-F249,U+F24D,U+F254-F25B,U+F25D,U+F267,U+F271-F274,U+F279,U+F28B,U+F28D,U+F2B5-F2B6,U+F2B9,U+F2BB,U+F2BD,U+F2C1-F2C2,U+F2D0,U+F2D2,U+F2DC,U+F2ED,U+F328,U+F358-F35B,U+F3A5,U+F3D1,U+F410,U+F4AD; }  (function(d,s,i,w,o){ var js,cjs=d.getElementsByTagName(s)\[0\]; if(d.getElementById(i))return; js=d.createElement('script'); js.id=i; js.src="https://widget.clym-sdk.net/clym.js"; js.onload=function(){Clym&&Clym.load(i,w,o);}; cjs.parentNode.insertBefore(js, cjs); }(document,'script','clym-privacy','5fba9912471741fca95e8fc7e1ivzba6',{})); var dataLayer\_content = {"pagePostType":"post","pagePostType2":"single-post","pageCategory":\["sysadmin","web-servers"\],"pageAttributes":\["commands","linux"\],"pagePostAuthor":"Sofija Simic"}; dataLayer.push( dataLayer\_content ); (function(w,d,s,l,i){w\[l\]=w\[l\]||\[\];w\[l\].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)\[0\], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src= '//www.googletagmanager.com/gtm.'+'js?id='+i+dl;f.parentNode.insertBefore(j,f); })(window,document,'script','dataLayer','GTM-MLJ5W8M'); .copy-the-code-wrap.copy-the-code-style-svg-icon .copy-the-code-button svg { fill: rgba(0,0,0,0.2); transition: fill 0.3s; } .copy-the-code-wrap.copy-the-code-style-svg-icon .copy-the-code-button:hover svg { fill: rgba(0,0,0,0.4); } .gitlab-embed-snippets .file-content { max-height:250px; overflow: scroll; } .ai-viewports {--ai: 1;} .ai-viewport-3 { display: none !important;} .ai-viewport-2 { display: none !important;} .ai-viewport-1 { display: inherit !important;} .ai-viewport-0 { display: none !important;} @media (min-width: 768px) and (max-width: 979px) { .ai-viewport-1 { display: none !important;} .ai-viewport-2 { display: inherit !important;} } @media (max-width: 767px) { .ai-viewport-1 { display: none !important;} .ai-viewport-3 { display: inherit !important;} }     

.rll-youtube-player, \[data-lazy-src\]{display:none !important;}

/\*! loadCSS rel=preload polyfill. \[c\]2017 Filament Group, Inc. MIT License \*/ (function(w){"use strict";if(!w.loadCSS){w.loadCSS=function(){}} var rp=loadCSS.relpreload={};rp.support=(function(){var ret;try{ret=w.document.createElement("link").relList.supports("preload")}catch(e){ret=!1} return function(){return ret}})();rp.bindMediaToggle=function(link){var finalMedia=link.media||"all";function enableStylesheet(){link.media=finalMedia} if(link.addEventListener){link.addEventListener("load",enableStylesheet)}else if(link.attachEvent){link.attachEvent("onload",enableStylesheet)} setTimeout(function(){link.rel="stylesheet";link.media="only x"});setTimeout(enableStylesheet,3000)};rp.poly=function(){if(rp.support()){return} var links=w.document.getElementsByTagName("link");for(var i=0;i<links.length;i++){var link=links\[i\];if(link.rel==="preload"&&link.getAttribute("as")==="style"&&!link.getAttribute("data-loadcss")){link.setAttribute("data-loadcss",!0);rp.bindMediaToggle(link)}}};if(!rp.support()){rp.poly();var run=w.setInterval(rp.poly,500);if(w.addEventListener){w.addEventListener("load",function(){rp.poly();w.clearInterval(run)})}else if(w.attachEvent){w.attachEvent("onload",function(){rp.poly();w.clearInterval(run)})}} if(typeof exports!=="undefined"){exports.loadCSS=loadCSS} else{w.loadCSS=loadCSS}}(typeof global!=="undefined"?global:this))

*   [Call](#)
    *   [Support](tel:1-855-330-1509)
    *   [Sales](tel:1-877-588-5918)
*   [Login](#)
    *   [Bare Metal Cloud](https://bmc.phoenixnap.com/)
    *   [Channel Partners](https://partners.phoenixnap.com/)
    *   [Billing Portal](https://admin.phoenixnap.com/)
*   [Partners](https://phoenixnap.com/partners)

[![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20200%2044'%3E%3C/svg%3E)

![](https://phoenixnap.com/kb/wp-content/uploads/2021/04/phoenixnap-logo-white.png)

](https://phoenixnap.com/kb)

*   [Phoenixnap home](https://phoenixnap.com/)
*   [contact support](https://phoenixnap.com/contact-us)
*   [blog](https://phoenixnap.com/blog)
*   [Glossary](https://phoenixnap.com/glossary/)
*   [Support](tel:1-855-330-1509)
*   [Sales](tel:1-877-588-5918)
*   [Login](https://admin.phoenixnap.com/)
*   [Partners](https://phoenixnap.com/partners)
*   [Search for:](#)  
*   [](#)

Linux Commands Cheat Sheet: With Examples
=========================================

February 21, 2020

[commands](https://phoenixnap.com/kb/tag/commands)[linux](https://phoenixnap.com/kb/tag/linux)

.single-post .single-post-header { background-image: linear-gradient(rgba(0, 108, 168, 0.7) 50%, rgba(0, 108, 168, 0.7) 50%), url(https://phoenixnap.com/kb/wp-content/uploads/2021/04/webservers-new.jpg); background-repeat: no-repeat; background-size: cover; }

[Home](https://phoenixnap.com/kb/) » [SysAdmin](https://phoenixnap.com/kb/category/sysadmin) » Linux Commands Cheat Sheet: With Examples

Contents

1.  [Linux Commands Cheat Sheet PDF](#linux-commands-cheat-sheet-pdf)
2.  [Linux Commands List](#linux-commands-list)
    1.  [Hardware Information](#hardware-information)
    2.  [Searching](#searching)
    3.  [File Commands](#file-commands)
    4.  [Directory Navigation](#directory-navigation)
    5.  [File Compression](#file-compression)
    6.  [File Transfer](#file-transfer)
    7.  [Users and Groups](#users-and-groups)
    8.  [Package Installation](#package-installation)
    9.  [Process Related](#process-related)
    10.  [System Management and Information](#system-management-and-information)
    11.  [Disk Usage](#disk-usage)
    12.  [SSH Login](#ssh-login)
    13.  [File Permission](#file-permission)
    14.  [Network](#network)
    15.  [Variables](#variables)
    16.  [Shell Command Management](#shell-command-management)
    17.  [Linux Keyboard Shortcuts](#linux-keyboard-shortcuts)

Contents

1.  [Linux Commands Cheat Sheet PDF](#linux-commands-cheat-sheet-pdf)
2.  [Linux Commands List](#linux-commands-list)
    1.  [Hardware Information](#hardware-information)
    2.  [Searching](#searching)
    3.  [File Commands](#file-commands)
    4.  [Directory Navigation](#directory-navigation)
    5.  [File Compression](#file-compression)
    6.  [File Transfer](#file-transfer)
    7.  [Users and Groups](#users-and-groups)
    8.  [Package Installation](#package-installation)
    9.  [Process Related](#process-related)
    10.  [System Management and Information](#system-management-and-information)
    11.  [Disk Usage](#disk-usage)
    12.  [SSH Login](#ssh-login)
    13.  [File Permission](#file-permission)
    14.  [Network](#network)
    15.  [Variables](#variables)
    16.  [Shell Command Management](#shell-command-management)
    17.  [Linux Keyboard Shortcuts](#linux-keyboard-shortcuts)

Introduction

Linux commands may seem intimidating at first glance if you are not used to using the terminal. There are many commands for performing operations and processes on your Linux system.

No matter whether you are new to Linux or an experienced user, having a list of common commands close at hand is helpful.

**In this tutorial, you will find commonly used Linux commands as well as a downloadable cheat sheet with syntax and examples.**

![list of common Linux commands with a downloadable cheat sheet](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20800%20400'%3E%3C/svg%3E)

![list of common Linux commands with a downloadable cheat sheet](https://phoenixnap.com/kb/wp-content/uploads/2021/04/linux-command-cheat-sheet.png)

**Important**: Depending on your system setup, some of the commands below may require invoking **`sudo`** to be executed.

Linux Commands Cheat Sheet PDF
------------------------------

If you prefer having all the commands on a one-page reference sheet, we created a helpful **Linux command line cheat sheet**. You can save the **list of linux commands** in PDF format by clicking the **Download Linux Cheat Sheet** button below.

[**Download Linux Commands Cheat Sheet PDF**](https://phoenixnap.com/kb/wp-content/uploads/2022/11/linux-commands-cheat-sheet-pdf.pdf)

![Linux commands cheat sheet PDF preview](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20800%20542'%3E%3C/svg%3E)

![Linux commands cheat sheet PDF preview](https://phoenixnap.com/kb/wp-content/uploads/2020/02/linux-commands-cheat-sheet-pdf-preview.png)

Linux Commands List
-------------------

The commands found in the downloadable cheat sheet are listed below.

### Hardware Information

[Show **bootup messages**](https://phoenixnap.com/kb/dmesg-linux):

    dmesg

See **CPU information**:

    cat /proc/cpuinfo

Display **free and used memory** with:

    free -h

List **hardware configuration** information:

    lshw

See information about **block devices**:

    lsblk

[Show **PCI devices**](https://phoenixnap.com/kb/lspci-command) in a tree-like diagram:

    lspci -tv

Display **USB devices** in a tree-like diagram:

    lsusb -tv

Show **hardware information** from the BIOS:

    dmidecode

Display **disk data** information:

    hdparm -i /dev/disk

Conduct a **read-speed test** on device/disk:

    hdparm -tT /dev/[device]

Test for **unreadable blocks** on device/disk:

    badblocks -s /dev/[device]

[Run a disk check](https://phoenixnap.com/kb/fsck-command-linux) on an unmounted disk or partition:

    fsck [disk-or-partition-location]

### Searching

[Search for a specific pattern](https://phoenixnap.com/kb/grep-multiple-strings) in a file with [grep](https://phoenixnap.com/kb/grep-command-linux-unix-examples):

    grep [pattern] [file_name]

**Recursively search for a pattern** in a directory:

    grep -r [pattern] [directory_name]

[Find all files and directories](https://phoenixnap.com/kb/locate-command-in-linux) **related to a particular name**:

    locate [name]

List names that **begin with a specified character** **`[a]`** in a specified location **`[/folder/location]`** by using the [**`find`** command](https://phoenixnap.com/kb/guide-linux-find-command):

    find [/folder/location] -name [a]

See **files larger than a specified size** **`[+100M]`** in a folder:

    find [/folder/location] -size [+100M]

**Note:** Some commands are not recommended to use. Learn about them in our list of [dangerous Linux commands](https://phoenixnap.com/kb/dangerous-linux-terminal-commands).

### File Commands

**List files** in the directory:

    ls

**List all files** ([shows hidden files](https://phoenixnap.com/kb/show-hidden-files-linux)):

    ls -a

[Show directory](https://phoenixnap.com/kb/pwd-linux) you are currently working in:

    pwd

[Create a new directory](https://phoenixnap.com/kb/create-directory-linux-mkdir-command):

    mkdir [directory]

[Remove a file](https://phoenixnap.com/kb/how-to-remove-files-directories-linux-command-line):

    rm [file_name] 

**Remove a directory** recursively:

    rm -r [directory_name]

**Recursively remove a directory** without requiring confirmation:

    rm -rf [directory_name]

[Copy the contents of one file](https://phoenixnap.com/kb/how-to-copy-files-directories-linux) to another file:

    cp [file_name1] [file_name2]

**Recursively copy the contents of one file** to a second file:

    cp -r [directory_name1] [directory_name2]

**Rename** **`[file_name1]`** to **`[file_name2]`** with the command:

    mv [file_name1] [file_name2]

[Create a symbolic link](https://phoenixnap.com/kb/symbolic-link-linux) to a file:

    ln -s /path/to/[file_name] [link_name]

Create a **new file** using [touch](https://phoenixnap.com/kb/touch-command-in-linux):

    touch [file_name]

**Show the contents** of a file:

    more [file_name]

or use the [**`cat`** command](https://phoenixnap.com/kb/linux-cat-command):

    cat [file_name]

Append file contents to another file:

    cat [file_name1] >> [file_name2]

Display the **first 10 lines** of a file with [head command](https://phoenixnap.com/kb/linux-head):

    head [file_name]

Show the **last 10 lines** of a file with [tail command](https://phoenixnap.com/kb/linux-tail):

    tail [file_name]

**Encrypt** a file:

    gpg -c [file_name]

**Decrypt** a file:

    gpg [file_name.gpg]

Show the **number of words, lines, and bytes** in a file using [wc](https://phoenixnap.com/kb/wc-linux):

    wc

List number of lines/words/characters in each file in a directory with [the xargs command](https://phoenixnap.com/kb/xargs-command):

    ls | xargs wc

[Cut a section of a file](https://phoenixnap.com/kb/linux-cut) and print the result to standard output:

    cut -d[delimiter] [filename]

Cut a section of piped data and print the result to standard output:

    [data] | cut -d[delimiter]

[Print all lines matching a pattern](https://phoenixnap.com/kb/awk-command-in-linux) in a file:

    awk '[pattern] {print $0}' [filename]

**Note:** Learn also about [gawk command](https://phoenixnap.com/kb/gawk-linux), the GNU version of awk.

[Overwrite a file](https://phoenixnap.com/kb/shred-linux) to prevent its recovery, then delete it:

    shred -u [filename]

[Compare two files](https://phoenixnap.com/kb/linux-diff) and display differences:

    diff [file1] [file2]

[Read and execute the file content](https://phoenixnap.com/kb/linux-source-command) in the current shell:

    source [filename]

[Sort file contents](https://phoenixnap.com/kb/linux-sort) and print the result in standard output:

    sort [options] filename

[Store the command output in a file](https://phoenixnap.com/kb/linux-tee) and skip the terminal output:

    [command] | tee [filename] >/dev/null

**Note:** Want to read more about file creation? Check out an article about [how to create a file in Linux using the command line](https://phoenixnap.com/kb/how-to-create-a-file-in-linux).

And if you want to find out how to determine the type of a file and its data, read our article about [Linux file command](https://phoenixnap.com/kb/linux-file-command).  
To view a file's contents one screen at a time read about [less command in Linux](https://phoenixnap.com/kb/less-command-in-linux).

### Directory Navigation

Move **up one level** in the directory tree structure:

    cd ..

[Change directory](https://phoenixnap.com/kb/linux-cd-command) **to** **`$HOME`**:

    cd

**Change location** to a specified directory:

    cd /chosen/directory

### File Compression

Archive an existing file:

    tar cf [compressed_file.tar] [file_name]

[Extract an archived file](https://phoenixnap.com/kb/extract-tar-gz-files-linux-command-line#htoc-using-tar-utility):

    tar xf [compressed_file.tar]

Create a **gzip compressed tar file** by running:

    tar czf [compressed_file.tar.gz]

**Compress** a file with the **`.gz`** extension:

    gzip [file_name]

**Note:** For a more comprehensive overview of how to use **`tar`** refer to our guide [tar Command in Linux With Examples](https://phoenixnap.com/kb/tar-command-in-linux).

### File Transfer

Copy a file to a server directory securely using the [Linux scp command](https://phoenixnap.com/kb/linux-scp-command):

    scp [file_name.txt] [server/tmp]

**Synchronize** the contents of a directory **with a backup directory** using the [rsync command](https://phoenixnap.com/kb/rsync-command-linux-examples):

    rsync -a [/your/directory] [/backup/] 

### Users and Groups

See details about the **active users**:

    id

Show **last system logins**:

    last

Display who is **currently logged into the system** with the [who command](https://phoenixnap.com/kb/linux-who-command):

    who

Show which users are **logged in** and **their activity**:

    w

**Add a new group** by typing:

    groupadd [group_name]

Add a **new user**:

    adduser [user_name]

Add a **user to a group**:

    usermod -aG [group_name] [user_name]

Temporarily **elevate user privileges** to superuser or root using the [sudo command](https://phoenixnap.com/kb/linux-sudo-command):

    sudo [command_to_be_executed_as_superuser]

**Delete** a user:

    userdel [user_name] 

[Modify user information](https://phoenixnap.com/kb/usermod-linux) with:

    usermod

[Change directory group](https://phoenixnap.com/kb/chgrp-command):

    chgrp [group-name] [directory-name]

**Note:** If you want to learn more about users and groups, take a look at our article on [how to add a user to a group in Linux](https://phoenixnap.com/kb/how-to-add-user-to-group-linux).

### Package Installation

[List all installed packages](https://phoenixnap.com/kb/how-to-list-installed-packages-on-centos) with **`yum`**:

    yum list installed

Find a package by a **related keyword**:

    yum search [keyword]

Show **package information and summary**:

    yum info [package_name]

Install a package using the **YUM package manager**:

    yum install [package_name.rpm]

Install a package using the **DNF package manager**:

    dnf install [package_name.rpm]

Install a package [using the **APT package manager**](https://phoenixnap.com/kb/how-to-use-apt-get-commands):

    apt install [package_name]

**Install** an **`.rpm`** package from a local file:

    rpm -i  [package_name.rpm]

**Remove** an **`.rpm`** package:

    rpm -e [package_name.rpm]

Install software from **source code**:

    tar zxvf [source_code.tar.gz]
    cd [source_code]
    ./configure
    make
    make install

### Process Related

See a **snapshot of active processes**:

    ps

Show **processes in a tree-like diagram**:

    pstree

Display a **memory usage map** of processes:

    pmap

See [all running processes](https://phoenixnap.com/kb/top-command-in-linux):

    top

[Terminate a Linux process](https://phoenixnap.com/kb/how-to-kill-a-process-in-linux) under a **given ID**:

    kill [process_id]

Terminate a process under a **specific name**:

    pkill [proc_name]

Terminate all processes **labelled** **“proc”**:

    killall [proc_name]

**List and resume stopped jobs** in the background:

    bg

Bring the most **recently suspended job to the** **foreground**:

    fg

Bring a **particular job to the** **foreground**:

    fg [job]

List **files opened by running processes** with [lsof command](https://phoenixnap.com/kb/lsof-command):

    lsof

[Catch a system error signal](https://phoenixnap.com/kb/bash-trap-command) in a shell script:

    trap "[commands-to-execute-on-trapping]" [signal]

[Pause terminal or a Bash script](https://phoenixnap.com/kb/bash-wait-command) until a running process is completed:

    wait

[Run a Linux process](https://phoenixnap.com/kb/linux-nohup) in the background:

    nohup [command] &

**Note:** If you want to learn more about shell jobs, how to terminate jobs or keep them running after you log off, check out our article on [how to use disown command](https://phoenixnap.com/kb/disown-command-linux).

### System Management and Information

Show **system information** via [uname command](https://phoenixnap.com/kb/uname-linux):

    uname -r 

See [kernel release information](https://phoenixnap.com/kb/check-linux-kernel-version):

    uname -a  

Display **how long the system has been running**, including load average:

    uptime 

See system **hostname**:

    hostname

Show the **IP address** of the system:

    hostname -i 

List system **reboot history**:

    last reboot 

See [current time and date](https://phoenixnap.com/kb/linux-date-command):

    date

Query and **change the system clock** with:

    timedatectl 

Show current **calendar** (month and day):

    cal

[List logged in users](https://phoenixnap.com/kb/w-command-in-linux):

    w

[See which **user you are using**](https://phoenixnap.com/kb/whoami-linux):

    whoami

Show **information about a particular user**:

    finger [username]

[View or limit](https://phoenixnap.com/kb/ulimit-linux-command) system resource amounts:

    ulimit [flags] [limit]

[Schedule a system shutdown](https://phoenixnap.com/kb/linux-shutdown-command):

    shutdown [hh:mm]

Shut Down the system immediately:

    shutdown now

[Add a new kernel module](https://phoenixnap.com/kb/modprobe-command):

    modprobe [module-name]

### Disk Usage

You can use the df and du commands to [check disk space in Linux](https://phoenixnap.com/kb/linux-check-disk-space).

See **free and used space** on mounted systems:

    df -h

Show **free inodes** on mounted filesystems:

    df -i

Display **disk partitions, sizes, and types** with the command:

    fdisk -l

See [**disk usage** for all files and directory](https://phoenixnap.com/kb/show-linux-directory-size):

    du -ah

Show **disk usage of the directory** you are currently in:

    du -sh

Display **target mount point** for all filesystem:

    findmnt

**[Mount a device](https://phoenixnap.com/kb/linux-mount-command)**:

    mount [device_path] [mount_point]

### SSH Login

**Connect to host** as user:

    ssh [email protected]

Securely **connect to host via SSH** default port 22:

    ssh host

Connect to host **using a particular port**:

    ssh -p [port] [email protected]

Connect to host **via telnet default port 23**:

    telnet host

**Note**: For a detailed explanation of SSH Linux Commands, refer to our [19 Common SSH Commands in Linux](https://phoenixnap.com/kb/linux-ssh-commands) tutorial.

### File Permission

[Chown command in Linux](https://phoenixnap.com/kb/linux-chown-command-with-examples) changes file and directory ownership.

Assign **read, write, and execute permission** to everyone:

    chmod 777 [file_name]

Give **read, write, and execute permission to owner**, and r**ead and execute permission to group and others**:

    chmod 755 [file_name]

Assign **full permission to owner**, and **read and write permission to group and others**:

    chmod 766 [file_name]

Change the **ownership of a file**:

    chown [user] [file_name]

Change the **owner and group ownership of a file**:

    chown [user]:[group] [file_name]

**Note**: To learn more about how to check and change permissions, refer to our [Linux File Permission Tutorial](https://phoenixnap.com/kb/linux-file-permissions).

### Network

[List IP addresses](https://phoenixnap.com/kb/linux-ip-command-examples) and **network interfaces**:

    ip addr show

Assign an **IP address to interface eth0**:

    ip address add [IP_address]

Display **IP addresses of all network interfaces** with:

    ifconfig

See **active (listening) ports** with the [netstat command](https://phoenixnap.com/kb/netstat-command):

    netstat -pnltu

Show **tcp** and **udp** **ports** and their programs:

    netstat -nutlp

Display more **information about a domain**:

    whois [domain]

Show **DNS information** about a domain using the [dig command](https://phoenixnap.com/kb/linux-dig-command-examples):

    dig [domain] 

Do a **reverse lookup** **on domain**:

    dig -x host

Do **reverse lookup of an IP address**:

    dig -x [ip_address]

Perform an **IP lookup for a domain**:

    host [domain]

Show the **local IP address**:

    hostname -I

**Download a file** from a domain using the [**`wget`** command](https://phoenixnap.com/kb/wget-command-with-examples):

    wget [file_name]

Receive [information about an internet domain](https://phoenixnap.com/kb/nslookup-command):

    nslookup [domain-name]

[Save a remote file to your system](https://phoenixnap.com/kb/curl-command) using the filename that corresponds to the filename on the server:

    curl -O [file-url]

### Variables

[Assign an integer value](https://phoenixnap.com/kb/bash-let) to a variable:

    let "[variable]=[value]"

[Export a Bash variable](https://phoenixnap.com/kb/bash-export-variable):

    export [variable-name]

[Declare a Bash variable](https://phoenixnap.com/kb/bash-declare):

    declare [variable-name]= "[value]"

List the names of [all the shell variables and functions](https://phoenixnap.com/kb/linux-set):

    set

[Display the value](https://phoenixnap.com/kb/echo-command-linux) of a variable:

    echo $[variable-name]

### Shell Command Management

[Create an alias](https://phoenixnap.com/kb/linux-alias-command) for a command:

    alias [alias-name]='[command]'

[Set a custom interval](https://phoenixnap.com/kb/linux-watch-command) to run a user-defined command:

    watch -n [interval-in-seconds] [command]

[Postpone the execution](https://phoenixnap.com/kb/linux-sleep) of a command:

    sleep [time-interval] && [command]

Create a job to be executed at a certain time (**Ctrl+D** to exit prompt after you type in the command):

    at [hh:mm]

[Display a built-in manual](https://phoenixnap.com/kb/linux-man) for a command:

    man [command]

Print the history of the commands you used in the terminal:

    history

### Linux Keyboard Shortcuts

**Kill process** running in the terminal:

    Ctrl + C

Stop **current process**:

    Ctrl + Z

The process can be **resumed** in the **foreground** with **`fg`** or in the **background** with **`bg`**.

Cut **one word before the cursor** and add it to clipboard:

    Ctrl + W

Cut **part of the line before the cursor** and add it to clipboard:

    Ctrl + U

Cut **part of the line after the cursor** and add it to clipboard:

    Ctrl + K

**Paste** from clipboard:

    Ctrl + Y

**Recall last command** that matches the provided characters:

    Ctrl + R

**Run** the previously recalled command:

    Ctrl + O

**Exit command history** without running a command:

    Ctrl + G

**Run the last command** again:

    !!

**Log out** of current session:

    exit

Conclusion

The more you use Linux commands, the better you will get at remembering them. Do not stress about memorizing their syntax; use our cheat sheet.

Whenever in doubt, refer to this helpful guide for the most common Linux commands.

Was this article helpful?

YesNo

[Share on Twitter](https://twitter.com/intent/tweet?text=Linux%20Commands%20Cheat%20Sheet%3A%20With%20Examples&url=https%3A%2F%2Fphoenixnap.com%2Fkb%2Flinux-commands-cheat-sheet) [Share on Facebook](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fphoenixnap.com%2Fkb%2Flinux-commands-cheat-sheet) [Share on LinkedIn](https://www.linkedin.com/shareArticle?mini=1&url=https%3A%2F%2Fphoenixnap.com%2Fkb%2Flinux-commands-cheat-sheet&title=Linux%20Commands%20Cheat%20Sheet%3A%20With%20Examples&source=https%3A%2F%2Fphoenixnap.com%2Fkb&summary=A%20list%20of%20all%20the%20important%20Linux%20commands%20in%20one%20place.%20Find%20the%20command%20you%20need%2C%20whenever%20you%20need%20it%20or%20download%20our%20Linux%20Commands%20Cheat%20Sheet%20and%20save%20it%20for%20future%20reference.) [Share on Email](/cdn-cgi/l/email-protection#122d707d766b2f5b37202260777376372022667a7b61372022627d6166372022737c7637202265737c667776372022667d372022617a7360773720227b66372022657b667a3720226b7d673c3720225a77607737202561372022667a773720227e7b7c793721533720227a66666261372153372054372054627a7d777c7b6a7c73623c717d7f37205479703720547e7b7c676a3f717d7f7f737c76613f717a7773663f617a777766343122212a29616770787771662f53372022627d6166372022657d60667a372022617a73607b7c753721533720225e7b7c676a372022517d7f7f737c7661372022517a777366372022417a777766372153372022457b667a372022576a737f627e7761)

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%200%200'%3E%3C/svg%3E)

![](https://secure.gravatar.com/avatar/f294f4ff5c2ada61b6f006327af47bfc?s=96&d=mm&r=g)

Sofija Simic

Sofija Simic is an experienced Technical Writer. Alongside her educational background in teaching and writing, she has had a lifelong passion for information technology. She is committed to unscrambling confusing IT concepts and streamlining intricate software installations.

Next you should read

[SysAdmin](https://phoenixnap.com/kb/category/sysadmin) [Web Servers](https://phoenixnap.com/kb/category/web-servers)

[How to Start, Stop, and Restart Services in Linux](https://phoenixnap.com/kb/start-stop-restart-linux-services)

December 6, 2019

* * *

In most modern Linux operating systems, managing a service is quite simple....

[Read more](https://phoenixnap.com/kb/start-stop-restart-linux-services)

[SysAdmin](https://phoenixnap.com/kb/category/sysadmin) [Web Servers](https://phoenixnap.com/kb/category/web-servers)

[How to Check Memory Usage in Linux](https://phoenixnap.com/kb/linux-commands-check-memory-usage)

June 18, 2019

* * *

In this tutorial, learn the five most commonly used commands to check...

[Read more](https://phoenixnap.com/kb/linux-commands-check-memory-usage)

[SysAdmin](https://phoenixnap.com/kb/category/sysadmin) [Web Servers](https://phoenixnap.com/kb/category/web-servers)

[How to Remove (Delete) a File or Directory in Linux](https://phoenixnap.com/kb/how-to-remove-files-directories-linux-command-line)

August 8, 2019

* * *

This article lists the most commonly used commands and tools to remove...

[Read more](https://phoenixnap.com/kb/how-to-remove-files-directories-linux-command-line)

[Security](https://phoenixnap.com/kb/category/security) [SysAdmin](https://phoenixnap.com/kb/category/sysadmin)

[How to Use the su Command in Linux with Examples](https://phoenixnap.com/kb/su-command-linux-examples)

January 7, 2020

* * *

Learn how to use the su command with practical examples and explanations. Change users...

[Read more](https://phoenixnap.com/kb/su-command-linux-examples)

*   RECENT POSTS
    
*   *   ### [Kubernetes Pods: Basics for Beginners](https://phoenixnap.com/kb/kubernetes-pod)
        
    *   ### [How to Remove Untracked Git Files and Folders](https://phoenixnap.com/kb/git-remove-untracked-files)
        
    *   ### [Structured vs. Unstructured Data: Understanding Differences](https://phoenixnap.com/kb/structured-vs-unstructured-data)
        
    *   ### [How to Check Apache Version](https://phoenixnap.com/kb/check-apache-version)
        
    *   ### [How to Uninstall MySQL in Linux, Windows, and macOS](https://phoenixnap.com/kb/uninstall-mysql)
        
    
*   CATEGORIES
    
*   *   [SysAdmin](https://phoenixnap.com/kb/category/sysadmin)
    *   [Virtualization](https://phoenixnap.com/kb/category/virtualization)
    *   [DevOps and Development](https://phoenixnap.com/kb/category/devops-and-development)
    *   [Security](https://phoenixnap.com/kb/category/security)
    *   [Backup and Recovery](https://phoenixnap.com/kb/category/backup-and-recovery)
    *   [Bare Metal Servers](https://phoenixnap.com/kb/category/bare-metal-servers)
    *   [Web Servers](https://phoenixnap.com/kb/category/web-servers)
    *   [Networking](https://phoenixnap.com/kb/category/networking)
    *   [Databases](https://phoenixnap.com/kb/category/databases)
    

*   [COLOCATION](https://phoenixnap.com/colocation)
    
*   *   [Phoenix](https://phoenixnap.com/colocation/phoenix)
    *   [Ashburn](https://phoenixnap.com/colocation/ashburn)
    *   [Amsterdam](https://phoenixnap.com/colocation/amsterdam)
    *   [Atlanta](https://phoenixnap.com/colocation/atlanta)
    *   [Belgrade](https://phoenixnap.com/colocation/belgrade)
    *   [Singapore](https://phoenixnap.com/colocation/singapore)
    
*   [PROMOTIONS](https://phoenixnap.com/promotions)
    

*   [SERVERS](https://phoenixnap.com/servers/dedicated)
    
*   *   [Dedicated Servers](https://phoenixnap.com/servers/dedicated)
    *   [Database Servers](https://phoenixnap.com/servers/database)
    *   [Virtualization Servers](https://phoenixnap.com/servers/virtualization)
    *   [High Performance Computing (HPC) Servers](https://phoenixnap.com/servers/high-performance-computing-hpc)
    *   [Dedicated Streaming Servers](https://phoenixnap.com/servers/streaming)
    *   [Dedicated Game Servers](https://phoenixnap.com/servers/dedicated-game-servers)
    *   [Dedicated Storage Servers](https://phoenixnap.com/servers/storage)
    *   [SQL Server Hosting](https://phoenixnap.com/servers/sql-server-hosting)
    *   [Dedicated Servers in Amsterdam](https://phoenixnap.com/dedicated-servers-amsterdam-netherlands)
    *   [Cloud Servers in Europe](https://phoenixnap.com/cloud-services/cloud-servers-europe)
    *   [Big Memory Infrastructure](https://phoenixnap.com/bare-metal-cloud/big-memory-infrastructure)
    
*   [BUY NOW](https://admin.phoenixnap.com/wap-pncpadmin-shell/orderForm?bmbPath=/order-form?currencyCode=usd)
    

*   CLOUD SERVICES
    
*   *   [Data Security Cloud](https://phoenixnap.com/security/data-security-cloud)
    *   [VPDC](https://phoenixnap.com/cloud-services/virtual-private-data-center)
    *   [Managed Private Cloud](https://phoenixnap.com/private)
    *   [Object Storage](https://phoenixnap.com/object-storage)
    
*   [SERVERS](https://phoenixnap.com/infrastructure-solutions)
    
*   *   [Disaster Recovery](https://phoenixnap.com/infrastructure-solutions/disaster-recovery-services)
    *   [Web Hosting Reseller](https://phoenixnap.com/reseller-hosting)
    *   [SaaS Hosting](https://phoenixnap.com/infrastructure-solutions/saas-hosting)
    

*   INDUSTRIES
    
*   *   [Web Hosting Providers](https://phoenixnap.com/reseller-hosting)
    *   [Legal](https://phoenixnap.com/infrastructure-solutions/legal-it)
    *   [MSPs & VARs](https://phoenixnap.com/infrastructure-solutions/it-partners)
    *   [Media Hosting](https://phoenixnap.com/infrastructure-solutions/media-hosting)
    *   [Online Gaming](https://phoenixnap.com/infrastructure-solutions/online-gaming)
    *   [SaaS Hosting Solutions](https://phoenixnap.com/infrastructure-solutions/saas-hosting)
    *   [Ecommerce Hosting Solutions](https://phoenixnap.com/infrastructure-solutions/ecommerce-hosting)
    
*   COMPLIANCE
    
*   *   [HIPAA Ready Hosting](https://phoenixnap.com/compliance/hipaa-compliant-hosting)
    *   [PCI Compliant Hosting](https://phoenixnap.com/compliance/pci-compliant-hosting)
    
*   NEEDS
    
*   *   [Disaster Recovery Solutions](https://phoenixnap.com/infrastructure-solutions/disaster-recovery-services)
    *   [High Availability Solutions](https://phoenixnap.com/infrastructure-solutions/high-availability-solutions)
    *   [Cloud Evaluation](https://phoenixnap.com/offers/cloud-evaluation-demo)
    

*   COMPANY
    
*   *   [About Us](https://phoenixnap.com/company/about-us)
    *   [GitHub](https://github.com/phoenixnap)
    *   [Blog](https://phoenixnap.com/blog)
    *   [RFP Template](https://phoenixnap.com/company/it-resources/data-center-rfp-template)
    *   [Careers](https://techjobs.dev)
    
*   CONNECT
    
*   *   [Events](https://phoenixnap.com/company/it-events)
    *   [Press](https://phoenixnap.com/company/press)
    *   [Contact Us](https://phoenixnap.com/contact-us)
    

*   [PhoenixNAP Home](https://phoenixnap.com/)
*   [Blog](https://phoenixnap.com/blog)
*   [Resources](https://phoenixnap.com/company/it-resources)
*   [Glossary](https://phoenixnap.com/glossary)
*   [GitHub](https://github.com/phoenixnap)
*   [RFP Template](https://phoenixnap.com/company/it-resources/data-center-rfp-template)

*    [Live Chat](https://phoenixnap.com/)
*    [Get a Quote](https://phoenixnap.com/contact-us)
*    Support | [1-855-330-1509](tel:1-855-330-1509)
*    Sales | [1-877-588-5918](tel:1-877-588-5918)

[

](https://www.facebook.com/phoenixnap)[

](https://www.linkedin.com/company/phoenix-nap/)[

](https://twitter.com/phoenixNAP)[

](https://www.instagram.com/phoenixnap/)[

](https://www.youtube.com/user/PhoenixNAPdatacenter)

*   [Contact Us](https://phoenixnap.com/contact-us)
*   [Legal](https://phoenixnap.com/cs/legal/)
*   [Privacy Policy](https://phoenixnap.com/infrastructure-solutions/legal-it/privacy-shield-compliant-privacy-policy)
*   [Terms of Use](https://phoenixnap.com/cs/legal/aup.html)
*   [DMCA](https://phoenixnap.com/cs/legal/dmca.html)
*   [GDPR](https://phoenixnap.com/gdpr)
*   [Sitemap](https://phoenixnap.com/sitemap)

[Privacy Center](#) [Do not sell or share my personal information](#)

*   [Contact Us](https://phoenixnap.com/contact-us)
*   [Legal](https://phoenixnap.com/cs/legal/)
*   [Privacy Policy](https://phoenixnap.com/infrastructure-solutions/legal-it/privacy-shield-compliant-privacy-policy)
*   [Terms of Use](https://phoenixnap.com/cs/legal/aup.html)
*   [DMCA](https://phoenixnap.com/cs/legal/dmca.html)
*   [GDPR](https://phoenixnap.com/gdpr)
*   [Sitemap](https://phoenixnap.com/sitemap)

© 2022 Copyright phoenixNAP | Global IT Services. All Rights Reserved.  

Live Chat ↗

[

](#)

window.addEventListener('DOMContentLoaded', function() {jQuery(document).ready(function($){ var offset = 100; var speed = 250; var duration = 750; $(window).scroll(function(){ if ($(this).scrollTop() < offset) { $('.topbutton') .fadeOut(duration); } else { $('.topbutton') .fadeIn(duration); } }); $('.topbutton').on('click', function(){ $('html, body').animate({scrollTop:0}, speed); return false; }); });}); .ct-FontAwesomeicon-twitter{width:0.92857142857143em} .ct-FontAwesomeicon-facebook{width:0.57142857142857em} .ct-FontAwesomeicon-linkedin{width:0.85714285714286em} .ct-FontAwesomeicon-chevron-circle-up{width:0.85714285714286em} .ct-FontAwesomeicon-instagram{width:0.85714285714286em} twitterfacebooklinkedinchevron-circle-upyoutube-playinstagram

.wp-container-1 {display: flex;gap: 0.5em;flex-wrap: wrap;align-items: center;justify-content: center;}.wp-container-1 > \* { margin: 0; } window.addEventListener('DOMContentLoaded', function() { jQuery(document).ready(function() { jQuery('body').on('click', '.oxy-menu-toggle', function() { jQuery(this).parent('.oxy-nav-menu').toggleClass('oxy-nav-menu-open'); jQuery('body').toggleClass('oxy-nav-menu-prevent-overflow'); jQuery('html').toggleClass('oxy-nav-menu-prevent-overflow'); }); var selector = '.oxy-nav-menu-open .menu-item a\[href\*="#"\]'; jQuery('body').on('click', selector, function(){ jQuery('.oxy-nav-menu-open').removeClass('oxy-nav-menu-open'); jQuery('body').removeClass('oxy-nav-menu-prevent-overflow'); jQuery('html').removeClass('oxy-nav-menu-prevent-overflow'); jQuery(this).click(); }); }); }); .wp-container-2 {display: flex;gap: 0.5em;flex-wrap: wrap;align-items: center;justify-content: center;}.wp-container-2 > \* { margin: 0; } window.addEventListener('DOMContentLoaded', function() { // Initialize Oxygen Modals jQuery(document).ready(function() { function showModal( modal ) { var $modal = jQuery( modal ); $modal.addClass("live"); var modalId = $modal\[0\].querySelector('.ct-modal').id; var focusable = modal.querySelector('a\[href\]:not(\[disabled\]), button:not(\[disabled\]), textarea:not(\[disabled\]), input\[type="text"\]:not(\[disabled\]), input\[type="radio"\]:not(\[disabled\]), input\[type="checkbox"\]:not(\[disabled\]), select:not(\[disabled\])'); if(focusable) { setTimeout(() => { focusable.focus(); }, 500); console.log(focusable); } setTimeout(() => { $modal.focus(); }, 500) // Check if this modal can be shown according to settings and last shown time // Current and last time in milliseconds var currentTime = new Date().getTime(); var lastShownTime = localStorage && localStorage\['oxy-' + modalId + '-last-shown-time'\] ? JSON.parse( localStorage\['oxy-' + modalId + '-last-shown-time'\] ) : false; // manual triggers aren't affected by last shown time if( $modal.data( 'trigger' ) != 'user\_clicks\_element' ) { switch( $modal.data( 'open-again' ) ) { case 'never\_show\_again': // if it was shown at least once, don't show it again if( lastShownTime !== false ) return; break; case 'show\_again\_after': var settingDays = parseInt( $modal.data( 'open-again-after-days' ) ); var actualDays = ( currentTime - lastShownTime ) / ( 60\*60\*24\*1000 ); if( actualDays < settingDays ) return; break; default: //always show break; } } // save current time as last shown time if( localStorage ) localStorage\['oxy-' + modalId + '-last-shown-time'\] = JSON.stringify( currentTime ); // trick to make jQuery fadeIn with flex $modal.css("display", "flex"); $modal.hide(); // trick to force AOS trigger on elements inside the modal $modal.find(".aos-animate").removeClass("aos-animate").addClass("aos-animate-disabled"); // show the modal $modal.fadeIn(250, function(){ // trick to force AOS trigger on elements inside the modal $modal.find(".aos-animate-disabled").removeClass("aos-animate-disabled").addClass("aos-animate"); }); if( $modal.data( 'close-automatically' ) == 'yes' ) { var time = parseInt( $modal.data( 'close-after-time' ) ); if( $modal.data( 'close-after-time-unit' ) == 'seconds' ) { time = parseInt( parseFloat( $modal.data( 'close-after-time' ) ) \* 1000 ); } setTimeout( function(){ hideModal(modal); }, time ); } // close modal automatically after form submit (Non-AJAX) if( $modal.data( 'close-after-form-submit' ) == 'yes' && $modal.data("trigger") == "after\_specified\_time" ) { // WPForms // WPForms replaces the form with a confirmation message on page refresh if( $modal.find(".wpforms-confirmation-container-full").length > 0 ) { setTimeout(function () { hideModal(modal); }, 3000); } // Formidable Forms // Formidable Forms replaces the form with a confirmation message on page refresh if( $modal.find(".frm\_message").length > 0 ) { setTimeout(function () { hideModal(modal); }, 3000); } // Caldera Forms // Caldera Forms replaces the form with a confirmation message on page refresh if( $modal.find(".caldera-grid .alert-success").length > 0 ) { setTimeout(function () { hideModal(modal); }, 3000); } } } var hideModal = function ( modal ) { // The function may be called by third party code, without argument, so we must close the first visible modal if( typeof modal === 'undefined' ) { var openModals = jQuery(".oxy-modal-backdrop.live"); if( openModals.length == 0 ) return; modal = openModals\[0\]; } var $modal = jQuery( modal ); // refresh any iframe so media embedded this way is stopped $modal.find( 'iframe').each(function(index){ this.src = this.src; }); // HTML5 videos can be stopped easily $modal.find( 'video' ).each(function(index){ this.pause(); }); // If there are any forms in the modal, reset them $modal.find("form").each(function(index){ this.reset(); }); $modal.fadeOut(400, function(){ $modal.removeClass("live"); }); }; window.oxyCloseModal = hideModal; jQuery( ".oxy-modal-backdrop" ).each(function( index ) { var modal = this; (function( modal ){ var $modal = jQuery( modal ); var exitIntentFunction = function( e ){ if( e.clientY <= 0 ) { showModal( modal ); document.removeEventListener( "mouseleave", exitIntentFunction ); document.removeEventListener( "mouseout", exitIntentFunction ); } } switch ( jQuery( modal ).data("trigger") ) { case "on\_exit\_intent": document.addEventListener( "mouseleave", exitIntentFunction, false); document.addEventListener( "mouseout", exitIntentFunction, false); break; case "user\_clicks\_element": jQuery( jQuery( modal ).data( 'trigger-selector' ) ).click( function( event ) { showModal( modal ); event.preventDefault(); } ); break; case "after\_specified\_time": var time = parseInt( jQuery( modal ).data( 'trigger-time' ) ); if( jQuery( modal ).data( 'trigger-time-unit' ) == 'seconds' ) { time = parseInt( parseFloat( jQuery( modal ).data( 'trigger-time' ) ) \* 1000 ); } setTimeout( function(){ showModal( modal ); }, time ); break; case "after\_scrolled\_amount": window.addEventListener("scroll", function scrollDetection(){ var winheight= window.innerHeight || (document.documentElement || document.body).clientHeight; var docheight = jQuery(document).height(); var scrollTop = window.pageYOffset || (document.documentElement || document.body.parentNode || document.body).scrollTop; var isScrollUp = false; var oxyPreviousScrollTop = parseInt( jQuery( modal ).data( 'previous\_scroll\_top' ) ); if( !isNaN( oxyPreviousScrollTop ) ) { if( oxyPreviousScrollTop > scrollTop) isScrollUp = true; } jQuery( modal ).data( 'previous\_scroll\_top', scrollTop ); var trackLength = docheight - winheight; var pctScrolled = Math.floor(scrollTop/trackLength \* 100); if( isNaN( pctScrolled ) ) pctScrolled = 0; if( ( isScrollUp && jQuery( modal ).data( 'trigger\_scroll\_direction' ) == 'up' ) || ( !isScrollUp && jQuery( modal ).data( 'trigger\_scroll\_direction' ) == 'down' && pctScrolled >= parseInt( jQuery( modal ).data( 'trigger\_scroll\_amount' ) ) ) ) { showModal( modal ); window.removeEventListener( "scroll", scrollDetection ); } }, false); break; case "on\_scroll\_to\_element": window.addEventListener("scroll", function scrollDetection(){ var $element = jQuery( jQuery( modal ).data( 'scroll\_to\_selector' ) ); if( $element.length == 0 ) { window.removeEventListener( "scroll", scrollDetection ); return; } var top\_of\_element = $element.offset().top; var bottom\_of\_element = $element.offset().top + $element.outerHeight(); var bottom\_of\_screen = jQuery(window).scrollTop() + jQuery(window).innerHeight(); var top\_of\_screen = jQuery(window).scrollTop(); if ((bottom\_of\_screen > bottom\_of\_element - $element.outerHeight() /2 ) && (top\_of\_screen < top\_of\_element + $element.outerHeight() /2 )){ showModal( modal ); window.removeEventListener( "scroll", scrollDetection ); } }, false); break; case "after\_number\_of\_clicks": document.addEventListener("click", function clickDetection(){ var number\_of\_clicks = parseInt( jQuery( modal ).data( 'number\_of\_clicks' ) ); var clicks\_performed = isNaN( parseInt( jQuery( modal ).data( 'clicks\_performed' ) ) ) ? 1 : parseInt( jQuery( modal ).data( 'clicks\_performed' ) ) + 1; jQuery( modal ).data( 'clicks\_performed', clicks\_performed ); if ( clicks\_performed == number\_of\_clicks ){ showModal( modal ); document.removeEventListener( "click", clickDetection ); } }, false); break; case "after\_time\_inactive": var time = parseInt( jQuery( modal ).data( 'time\_inactive' ) ); if( jQuery( modal ).data( 'time-inactive-unit' ) == 'seconds' ) { time = parseInt( parseFloat( jQuery( modal ).data( 'time\_inactive' ) ) \* 1000 ); } var activityDetected = function(){ jQuery( modal ).data( 'millis\_idle', 0 ); }; document.addEventListener( "click", activityDetected); document.addEventListener( "mousemove", activityDetected); document.addEventListener( "keypress", activityDetected); document.addEventListener( "scroll", activityDetected); var idleInterval = setInterval(function(){ var millis\_idle = isNaN( parseInt( jQuery( modal ).data( 'millis\_idle' ) ) ) ? 100 : parseInt( jQuery( modal ).data( 'millis\_idle' ) ) + 100; jQuery( modal ).data( 'millis\_idle', millis\_idle ); if( millis\_idle > time ){ clearInterval( idleInterval ); document.removeEventListener( "click", activityDetected ); document.removeEventListener( "mousemove", activityDetected ); document.removeEventListener( "keypress", activityDetected ); document.removeEventListener( "scroll", activityDetected ); showModal( modal ); } }, 100); break; case "after\_number\_of\_page\_views": var modalId = modal.querySelector('.ct-modal').id; var pageViews = localStorage && localStorage\['oxy-' + modalId + '-page-views'\] ? parseInt( localStorage\['oxy-' + modalId + '-page-views'\] ) : 0; pageViews++; if( localStorage ) localStorage\['oxy-' + modalId + '-page-views'\] = pageViews; if( parseInt( jQuery( modal ).data( 'number\_of\_page\_views' ) ) == pageViews ) { if( localStorage ) localStorage\['oxy-' + modalId + '-page-views'\] = 0; showModal( modal ); } break; } // add event handler to close modal automatically after AJAX form submit if( $modal.data( 'close-after-form-submit' ) == 'yes' ) { // Contact Form 7 if (typeof wpcf7 !== 'undefined') { $modal.find('div.wpcf7').each(function () { var $form = jQuery(this).find('form'); this.addEventListener('wpcf7submit', function (event) { if (event.detail.contactFormId == $form.attr("id")) { setTimeout(function () { hideModal(modal); }, 3000); } }, false); }); } // Caldera Forms document.addEventListener( "cf.submission", function(event){ // Pending, Caldera AJAX form submissions aren't working since Oxygen 2.2, see: https://github.com/soflyy/oxygen/issues/1638 console.log( event ); }); // Ninja Forms jQuery(document).on("nfFormSubmitResponse", function(event, response){ // Only close the modal if the event was triggered from a Ninja Form inside the modal if( $modal.find("#nf-form-" + response.id + "-cont").length > 0 ) { setTimeout(function () { hideModal(modal); }, 3000); } }); } })( modal ); }); // handle clicks on modal backdrop and on .oxy-close-modal jQuery("body").on('click touchend', '.oxy-modal-backdrop, .oxy-close-modal', function( event ) { var $this = jQuery( this ); var $target = jQuery( event.target ); // Click event in the modal div and it's children is propagated to the backdrop if( !$target.hasClass( 'oxy-modal-backdrop' ) && !$this.hasClass( 'oxy-close-modal' ) ) { event.stopPropagation(); return; } if( $target.hasClass( 'oxy-modal-backdrop' ) && $this.hasClass( 'oxy-not-closable' ) ) { return; } if( $this.hasClass( 'oxy-close-modal' ) ) event.preventDefault(); var $modal = $this.hasClass( 'oxy-close-modal' ) ? $this.closest('.oxy-modal-backdrop') : $this; hideModal( $modal\[0\] ); }); jQuery(document).keyup( function(e){ if( e.key == 'Escape' ){ jQuery(".oxy-modal-backdrop:visible").each(function(index){ if( jQuery(this).data("close\_on\_esc") == 'on' ) hideModal(this); }); } } ); }); }); /\* <!\[CDATA\[ \*/ var copyTheCode = {"trim\_lines":"","remove\_spaces":"1","copy\_content\_as":"","previewMarkup":"<h2>Hello World<\\/h2>","buttonMarkup":"<button class=\\"copy-the-code-button\\" title=\\"\\"><\\/button>","buttonSvg":"<svg viewBox=\\"-21 0 512 512\\" xmlns=\\"http:\\/\\/www.w3.org\\/2000\\/svg\\"><path d=\\"m186.667969 416c-49.984375 0-90.667969-40.683594-90.667969-90.667969v-218.664062h-37.332031c-32.363281 0-58.667969 26.300781-58.667969 58.664062v288c0 32.363281 26.304688 58.667969 58.667969 58.667969h266.664062c32.363281 0 58.667969-26.304688 58.667969-58.667969v-37.332031zm0 0\\"><\\/path><path d=\\"m469.332031 58.667969c0-32.40625-26.261719-58.667969-58.664062-58.667969h-224c-32.40625 0-58.667969 26.261719-58.667969 58.667969v266.664062c0 32.40625 26.261719 58.667969 58.667969 58.667969h224c32.402343 0 58.664062-26.261719 58.664062-58.667969zm0 0\\"><\\/path><\\/svg>","selectors":\[{"selector":"pre","style":"svg-icon","button\_text":"Copy","button\_title":"Copy to Clipboard","button\_copy\_text":"Copied!","button\_position":"inside","copy\_format":""}\],"selector":"pre","settings":{"selector":"pre","button-text":"Copy","button-title":"Copy to Clipboard","button-copy-text":"Copied!","button-position":"inside","copy-format":"default"},"string":{"title":"Copy to Clipboard","copy":"Copy","copied":"Copied!"},"image-url":"https:\\/\\/phoenixnap.com\\/kb\\/wp-content\\/plugins\\/copy-the-code\\/\\/assets\\/images\\/copy-1.svg","redirect\_url":""}; /\* \]\]> \*/ /\* <!\[CDATA\[ \*/ var genesis\_responsive\_menu = {"mainMenu":"<span class=\\"hamburger-box\\"><span class=\\"hamburger-inner\\"><\\/span><\\/span><span class=\\"hamburger-label\\">Menu<\\/span>","menuIconClass":"hamburger hamburger--slider","subMenu":"Submenu","subMenuIconClass":"dashicons-before dashicons-arrow-down-alt2","menuClasses":{"combine":\[".nav-primary"\],"others":\[\]}}; /\* \]\]> \*/ var nonce\_wthf = "44f99027a8";var ajaxurl = "https://phoenixnap.com/kb/wp-admin/admin-ajax.php"; "use strict";var \_createClass=function(){function defineProperties(target,props){for(var i=0;i<props.length;i++){var descriptor=props\[i\];descriptor.enumerable=descriptor.enumerable||!1,descriptor.configurable=!0,"value"in descriptor&&(descriptor.writable=!0),Object.defineProperty(target,descriptor.key,descriptor)}}return function(Constructor,protoProps,staticProps){return protoProps&&defineProperties(Constructor.prototype,protoProps),staticProps&&defineProperties(Constructor,staticProps),Constructor}}();function \_classCallCheck(instance,Constructor){if(!(instance instanceof Constructor))throw new TypeError("Cannot call a class as a function")}var RocketBrowserCompatibilityChecker=function(){function RocketBrowserCompatibilityChecker(options){\_classCallCheck(this,RocketBrowserCompatibilityChecker),this.passiveSupported=!1,this.\_checkPassiveOption(this),this.options=!!this.passiveSupported&&options}return \_createClass(RocketBrowserCompatibilityChecker,\[{key:"\_checkPassiveOption",value:function(self){try{var options={get passive(){return!(self.passiveSupported=!0)}};window.addEventListener("test",null,options),window.removeEventListener("test",null,options)}catch(err){self.passiveSupported=!1}}},{key:"initRequestIdleCallback",value:function(){!1 in window&&(window.requestIdleCallback=function(cb){var start=Date.now();return setTimeout(function(){cb({didTimeout:!1,timeRemaining:function(){return Math.max(0,50-(Date.now()-start))}})},1)}),!1 in window&&(window.cancelIdleCallback=function(id){return clearTimeout(id)})}},{key:"isDataSaverModeOn",value:function(){return"connection"in navigator&&!0===navigator.connection.saveData}},{key:"supportsLinkPrefetch",value:function(){var elem=document.createElement("link");return elem.relList&&elem.relList.supports&&elem.relList.supports("prefetch")&&window.IntersectionObserver&&"isIntersecting"in IntersectionObserverEntry.prototype}},{key:"isSlowConnection",value:function(){return"connection"in navigator&&"effectiveType"in navigator.connection&&("2g"===navigator.connection.effectiveType||"slow-2g"===navigator.connection.effectiveType)}}\]),RocketBrowserCompatibilityChecker}(); /\* <!\[CDATA\[ \*/ var RocketPreloadLinksConfig = {"excludeUris":"\\/kb(-content\\/cache\\/min\\/1\\/kb\\/wp-content\\/uploads\\/oxygen\\/css\\/main-navigation-154.css|\\/(?:.+\\/)?feed(?:\\/(?:.+\\/?)?)?$|\\/(?:.+\\/)?embed\\/|\\/(index\\\\.php\\/)?wp\\\\-json(\\/.\*|$))|\\/refer\\/|\\/go\\/|\\/recommend\\/|\\/recommends\\/","usesTrailingSlash":"","imageExt":"jpg|jpeg|gif|png|tiff|bmp|webp|avif|pdf|doc|docx|xls|xlsx|php","fileExt":"jpg|jpeg|gif|png|tiff|bmp|webp|avif|pdf|doc|docx|xls|xlsx|php|html|htm","siteUrl":"https:\\/\\/phoenixnap.com\\/kb","onHoverDelay":"100","rateThrottle":"3"}; /\* \]\]> \*/ (function() { "use strict";var r="function"==typeof Symbol&&"symbol"==typeof Symbol.iterator?function(e){return typeof e}:function(e){return e&&"function"==typeof Symbol&&e.constructor===Symbol&&e!==Symbol.prototype?"symbol":typeof e},e=function(){function i(e,t){for(var n=0;n<t.length;n++){var i=t\[n\];i.enumerable=i.enumerable||!1,i.configurable=!0,"value"in i&&(i.writable=!0),Object.defineProperty(e,i.key,i)}}return function(e,t,n){return t&&i(e.prototype,t),n&&i(e,n),e}}();function i(e,t){if(!(e instanceof t))throw new TypeError("Cannot call a class as a function")}var t=function(){function n(e,t){i(this,n),this.browser=e,this.config=t,this.options=this.browser.options,this.prefetched=new Set,this.eventTime=null,this.threshold=1111,this.numOnHover=0}return e(n,\[{key:"init",value:function(){!this.browser.supportsLinkPrefetch()||this.browser.isDataSaverModeOn()||this.browser.isSlowConnection()||(this.regex={excludeUris:RegExp(this.config.excludeUris,"i"),images:RegExp(".("+this.config.imageExt+")$","i"),fileExt:RegExp(".("+this.config.fileExt+")$","i")},this.\_initListeners(this))}},{key:"\_initListeners",value:function(e){-1<this.config.onHoverDelay&&document.addEventListener("mouseover",e.listener.bind(e),e.listenerOptions),document.addEventListener("mousedown",e.listener.bind(e),e.listenerOptions),document.addEventListener("touchstart",e.listener.bind(e),e.listenerOptions)}},{key:"listener",value:function(e){var t=e.target.closest("a"),n=this.\_prepareUrl(t);if(null!==n)switch(e.type){case"mousedown":case"touchstart":this.\_addPrefetchLink(n);break;case"mouseover":this.\_earlyPrefetch(t,n,"mouseout")}}},{key:"\_earlyPrefetch",value:function(t,e,n){var i=this,r=setTimeout(function(){if(r=null,0===i.numOnHover)setTimeout(function(){return i.numOnHover=0},1e3);else if(i.numOnHover>i.config.rateThrottle)return;i.numOnHover++,i.\_addPrefetchLink(e)},this.config.onHoverDelay);t.addEventListener(n,function e(){t.removeEventListener(n,e,{passive:!0}),null!==r&&(clearTimeout(r),r=null)},{passive:!0})}},{key:"\_addPrefetchLink",value:function(i){return this.prefetched.add(i.href),new Promise(function(e,t){var n=document.createElement("link");n.rel="prefetch",n.href=i.href,n.onload=e,n.onerror=t,document.head.appendChild(n)}).catch(function(){})}},{key:"\_prepareUrl",value:function(e){if(null===e||"object"!==(void 0===e?"undefined":r(e))||!1 in e||-1===\["http:","https:"\].indexOf(e.protocol))return null;var t=e.href.substring(0,this.config.siteUrl.length),n=this.\_getPathname(e.href,t),i={original:e.href,protocol:e.protocol,origin:t,pathname:n,href:t+n};return this.\_isLinkOk(i)?i:null}},{key:"\_getPathname",value:function(e,t){var n=t?e.substring(this.config.siteUrl.length):e;return n.startsWith("/")||(n="/"+n),this.\_shouldAddTrailingSlash(n)?n+"/":n}},{key:"\_shouldAddTrailingSlash",value:function(e){return this.config.usesTrailingSlash&&!e.endsWith("/")&&!this.regex.fileExt.test(e)}},{key:"\_isLinkOk",value:function(e){return null!==e&&"object"===(void 0===e?"undefined":r(e))&&(!this.prefetched.has(e.href)&&e.origin===this.config.siteUrl&&-1===e.href.indexOf("?")&&-1===e.href.indexOf("#")&&!this.regex.excludeUris.test(e.href)&&!this.regex.images.test(e.href))}}\],\[{key:"run",value:function(){"undefined"!=typeof RocketPreloadLinksConfig&&new n(new RocketBrowserCompatibilityChecker({capture:!0,passive:!0}),RocketPreloadLinksConfig).init()}}\]),n}();t.run(); }()); /\* <!\[CDATA\[ \*/ var q2w3\_sidebar\_options = \[{"sidebar":"bsf-sb-single-post-right-sidebar","use\_sticky\_position":false,"margin\_top":10,"margin\_bottom":0,"stop\_elements\_selectors":"section-115-7","screen\_max\_width":0,"screen\_max\_height":0,"widgets":\["#text-2","#text-3","#text-4","#text-5","#text-6","#text-7","#text-8","#text-9","#text-10","#text-11","#text-12","#text-13","#text-14","#text-15","#text-16","#text-17"\]}\]; /\* \]\]> \*/ /\* <!\[CDATA\[ \*/ var fixedtocOption = {"showAdminbar":"","inOutEffect":"fade","isNestedList":"1","isColExpList":"1","showColExpIcon":"1","isAccordionList":"","isQuickMin":"1","isEscMin":"1","isEnterMax":"1","fixedMenu":"","scrollOffset":"10","fixedOffsetX":"20","fixedOffsetY":"0","fixedPosition":"middle-left","contentsFixedHeight":"","inPost":"1","contentsFloatInPost":"none","contentsWidthInPost":"250","contentsHeightInPost":"","contentsColexpInitMobile":"1","inWidget":"","fixedWidget":"","triggerBorder":"thin","contentsBorder":"thin","triggerSize":"56","isClickableHeader":"","debug":"","contentsColexpInit":"1"}; /\* \]\]> \*/ const loadScriptsTimer=setTimeout(loadScripts,5\*1000);const userInteractionEvents=\["mouseover","keydown","touchstart","touchmove","wheel"\];userInteractionEvents.forEach(function(event){window.addEventListener(event,triggerScriptLoader,{passive:!0})});function triggerScriptLoader(){loadScripts();clearTimeout(loadScriptsTimer);userInteractionEvents.forEach(function(event){window.removeEventListener(event,triggerScriptLoader,{passive:!0})})} function loadScripts(){document.querySelectorAll("script\[data-type='lazy'\]").forEach(function(elem){elem.setAttribute("src",elem.getAttribute("data-src"))})} .comment-body .aligncenter, .oxy-stock-content-styles .aligncenter { margin-left: auto; margin-right: auto; display: table; } .notice-note { padding-top: 15px; padding-bottom: 15px; border-top: 2px solid #006ca8; border-bottom: 2px solid #006ca8; display: flex; margin-bottom: 20px; } .notice-warning { padding-top: 15px; padding-bottom: 15px; border-top: 2px solid #c52127 ; border-bottom: 2px solid #c52127 ; display: flex; margin-bottom: 20px; } .note-icon-wrapper { position: relative; display: inline-block; width: 96px; height: 96px; line-height: 104px; vertical-align: middle; border: 2px solid #006ca8; text-align: center; background-color: #006ca8; border-radius: 3px; } .warning-icon-wrapper { position: relative; display: inline-block; width: 96px; height: 96px; line-height: 104px; vertical-align: middle; border: 2px solid #c52127; text-align: center; background-color: #c52127; border-radius: 3px; } .notice-text { margin-left: 20px; width: 84%; } .fa-lightbulb:before, .fa-exclamation-triangle:before { font-size: 32px; color: #fff; } #was-this-helpful { background-color: #fff; border-radius: 3px; -webkit-box-shadow: 0px 3px 3px 0px rgb(50 50 50 / 30%); -moz-box-shadow: 0px 3px 3px 0px rgba(50, 50, 50, 0.3); box-shadow: 0px 3px 3px 0px rgb(50 50 50 / 30%); border: 1px solid #f7f7f7; justify-content: flex-start; } #wthf-yes-no span:first-child { margin-right: 0.4em; border: 1px solid #006ca8; color: #006ca8; } #wthf-yes-no span:last-child { margin-left: 0.4em; border: 1px solid #d12121; color: #d12121; } .single-related-post { list-style: none; width: 100%; max-width: 188px; text-align: left; padding: 10px; background-color: #f7f7f7; border: 1px solid #eaeaea; border-radius: 5px; word-break: break-word; } .srp-categories a:after { content: ","; } .srp-categories a:last-child:after { content: ""; } .srp-title { font-size: 20px; letter-spacing: 0em; font-weight: 900; font-family: Roboto,Sans-Serif; color: #006ca8; } .srp-date { display: block; font-size: 12px; font-weight: 600; } .single-related-post hr { display: block; height: 1px; border: 0; border-top: 1px solid #eaeaea; margin: 1em 0; padding: 0; } a.srp-read-more { font-weight: 600; font-family: Poppins; letter-spacing: .1em; text-transform: uppercase; color: #000; font-size: 12px; } a.srp-read-more:hover { color: #006ca8; } @media only screen and (max-width: 600px) { .related-posts { flex-direction: column; } .single-related-post { width: 100%; margin-bottom: 10px; max-width: 100%; } } .footer-link { margin-right: 12px; font-size: 14px; color: rgba(255,255,255,0.7); text-decoration: none; } .footer-link:hover { border-bottom: 1px solid rgba(255,255,255,0.7); } function myFunction() { window.open("https://secure.livechatinc.com/licence/7436521/v2/open\_chat.cgi?groups=4", "\_blank", "toolbar=yes,scrollbars=yes,resizable=yes,top=500,left=500,width=400,height=400"); } .live-chat-btn { background-color: rgb(198, 32, 32); border: 1px solid rgb(209, 33, 33); color: #fff; border-radius: 3px; padding: 10px 50px; display: inline-block; text-align: center; text-decoration: none; font-weight: 700; line-height: 1.6; font-family: 'Open Sans'; } .live-chat-btn:hover { cursor: pointer; background-color: rgb(209, 33, 33);; } .searchform-wrapper-modal { margin: 0; padding: 8px; height: 96px; background-color: transparent; border-bottom: 2px solid #fff; border-radius: 0 0 0 0; box-shadow: 0 0 0 0 #b5b5b5 inset; display: flex; -webkit-flex-direction: row; flex-direction: row; width: auto; overflow: hidden; } .search-field-modal { font-weight: normal; font-family: Open Sans; color: #fff; font-size: 24px; line-height: normal; text-shadow: 0 0 0 rgba(255,255,255,0); padding: 0; margin: 0; background: transparent; border: none; background-color: transparent; box-shadow: none; z-index: 10; position: relative; margin-left: 10px; width: 100%; } .search-field-modal:focus, .search-field-modal:active { background: transparent; border: none; background-color: transparent; box-shadow: none; outline: none; } .innericon-modal { width: 64px; height: 64px; cursor:pointer; } .innericon-modal svg { fill: #fff; height: 64px; width: 64px; vertical-align: baseline; display: inline-block; } .submit-button-modal { background: transparent; border: none; } @media only screen and (min-width: 1025px) { .searchform-wrapper-modal { width: 960px; } } @media only screen and (min-width: 768px) and (max-width: 1024px) { .searchform-wrapper-modal { width: 360px; } } @media only screen and (max-width: 767px) { .searchform-wrapper-modal { width: 320px; } } function b2a(a){var b,c=0,l=0,f="",g=\[\];if(!a)return a;do{var e=a.charCodeAt(c++);var h=a.charCodeAt(c++);var k=a.charCodeAt(c++);var d=e<<16|h<<8|k;e=63&d>>18;h=63&d>>12;k=63&d>>6;d&=63;g\[l++\]="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=".charAt(e)+"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=".charAt(h)+"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=".charAt(k)+"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=".charAt(d)}while(c< a.length);return f=g.join(""),b=a.length%3,(b?f.slice(0,b-3):f)+"===".slice(b||3)}function a2b(a){var b,c,l,f={},g=0,e=0,h="",k=String.fromCharCode,d=a.length;for(b=0;64>b;b++)f\["ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/".charAt(b)\]=b;for(c=0;d>c;c++)for(b=f\[a.charAt(c)\],g=(g<<6)+b,e+=6;8<=e;)((l=255&g>>>(e-=8))||d-2>c)&&(h+=k(l));return h}b64e=function(a){return btoa(encodeURIComponent(a).replace(/%(\[0-9A-F\]{2})/g,function(b,a){return String.fromCharCode("0x"+a)}))}; b64d=function(a){return decodeURIComponent(atob(a).split("").map(function(a){return"%"+("00"+a.charCodeAt(0).toString(16)).slice(-2)}).join(""))}; /\* <!\[CDATA\[ \*/ ai\_front = {"insertion\_before":"BEFORE","insertion\_after":"AFTER","insertion\_prepend":"PREPEND CONTENT","insertion\_append":"APPEND CONTENT","insertion\_replace\_content":"REPLACE CONTENT","insertion\_replace\_element":"REPLACE ELEMENT","visible":"VISIBLE","hidden":"HIDDEN","fallback":"FALLBACK","automatically\_placed":"Automatically placed by AdSense Auto ads code","cancel":"Cancel","use":"Use","add":"Add","parent":"Parent","cancel\_element\_selection":"Cancel element selection","select\_parent\_element":"Select parent element","css\_selector":"CSS selector","use\_current\_selector":"Use current selector","element":"ELEMENT","path":"PATH","selector":"SELECTOR"}; /\* \]\]> \*/ function ai\_run\_scripts(){var ai\_cookie\_js=!0,ai\_block\_class\_def="code-block"; /\* JavaScript Cookie v2.2.0 https://github.com/js-cookie/js-cookie Copyright 2006, 2015 Klaus Hartl & Fagner Brack Released under the MIT license \*/ "undefined"!==typeof ai\_cookie\_js&&(function(a){if("function"===typeof define&&define.amd){define(a);var c=!0}"object"===typeof exports&&(module.exports=a(),c=!0);if(!c){var d=window.Cookies,b=window.Cookies=a();b.noConflict=function(){window.Cookies=d;return b}}}(function(){function a(){for(var d=0,b={};d<arguments.length;d++){var f=arguments\[d\],e;for(e in f)b\[e\]=f\[e\]}return b}function c(d){function b(){}function f(h,k,g){if("undefined"!==typeof document){g=a({path:"/",sameSite:"Lax"},b.defaults, g);"number"===typeof g.expires&&(g.expires=new Date(1\*new Date+864E5\*g.expires));g.expires=g.expires?g.expires.toUTCString():"";try{var l=JSON.stringify(k);/^\[\\{\\\[\]/.test(l)&&(k=l)}catch(p){}k=d.write?d.write(k,h):encodeURIComponent(String(k)).replace(/%(23|24|26|2B|3A|3C|3E|3D|2F|3F|40|5B|5D|5E|60|7B|7D|7C)/g,decodeURIComponent);h=encodeURIComponent(String(h)).replace(/%(23|24|26|2B|5E|60|7C)/g,decodeURIComponent).replace(/\[\\(\\)\]/g,escape);l="";for(var n in g)g\[n\]&&(l+="; "+n,!0!==g\[n\]&&(l+="="+ g\[n\].split(";")\[0\]));return document.cookie=h+"="+k+l}}function e(h,k){if("undefined"!==typeof document){for(var g={},l=document.cookie?document.cookie.split("; "):\[\],n=0;n<l.length;n++){var p=l\[n\].split("="),m=p.slice(1).join("=");k||'"'!==m.charAt(0)||(m=m.slice(1,-1));try{var q=p\[0\].replace(/(%\[0-9A-Z\]{2})+/g,decodeURIComponent);m=(d.read||d)(m,q)||m.replace(/(%\[0-9A-Z\]{2})+/g,decodeURIComponent);if(k)try{m=JSON.parse(m)}catch(r){}g\[q\]=m;if(h===q)break}catch(r){}}return h?g\[h\]:g}}b.set=f;b.get= function(h){return e(h,!1)};b.getJSON=function(h){return e(h,!0)};b.remove=function(h,k){f(h,"",a(k,{expires:-1}))};b.defaults={};b.withConverter=c;return b}return c(function(){})}),AiCookies=Cookies.noConflict(),ai\_check\_block=function(a){if(null==a)return!0;var c=AiCookies.getJSON("aiBLOCKS");ai\_debug\_cookie\_status="";null==c&&(c={});"undefined"!==typeof ai\_delay\_showing\_pageviews&&(c.hasOwnProperty(a)||(c\[a\]={}),c\[a\].hasOwnProperty("d")||(c\[a\].d=ai\_delay\_showing\_pageviews));if(c.hasOwnProperty(a)){for(var d in c\[a\]){if("x"== d){var b="",f=document.querySelectorAll('span\[data-ai-block="'+a+'"\]')\[0\];"aiHash"in f.dataset&&(b=f.dataset.aiHash);f="";c\[a\].hasOwnProperty("h")&&(f=c\[a\].h);var e=new Date;e=c\[a\]\[d\]-Math.round(e.getTime()/1E3);if(0<e&&f==b)return ai\_debug\_cookie\_status=a="closed for "+e+" s = "+Math.round(1E4\*e/3600/24)/1E4+" days",!1;ai\_set\_cookie(a,"x","");c\[a\].hasOwnProperty("i")||c\[a\].hasOwnProperty("c")||ai\_set\_cookie(a,"h","")}else if("d"==d){if(0!=c\[a\]\[d\])return ai\_debug\_cookie\_status=a="delayed for "+c\[a\]\[d\]+ " pageviews",!1}else if("i"==d){b="";f=document.querySelectorAll('span\[data-ai-block="'+a+'"\]')\[0\];"aiHash"in f.dataset&&(b=f.dataset.aiHash);f="";c\[a\].hasOwnProperty("h")&&(f=c\[a\].h);if(0==c\[a\]\[d\]&&f==b)return ai\_debug\_cookie\_status=a="max impressions reached",!1;if(0>c\[a\]\[d\]&&f==b){e=new Date;e=-c\[a\]\[d\]-Math.round(e.getTime()/1E3);if(0<e)return ai\_debug\_cookie\_status=a="max imp. reached ("+Math.round(1E4\*e/24/3600)/1E4+" days = "+e+" s)",!1;ai\_set\_cookie(a,"i","");c\[a\].hasOwnProperty("c")||c\[a\].hasOwnProperty("x")|| ai\_set\_cookie(a,"h","")}}if("ipt"==d&&0==c\[a\]\[d\]&&(e=new Date,b=Math.round(e.getTime()/1E3),e=c\[a\].it-b,0<e))return ai\_debug\_cookie\_status=a="max imp. per time reached ("+Math.round(1E4\*e/24/3600)/1E4+" days = "+e+" s)",!1;if("c"==d){b="";f=document.querySelectorAll('span\[data-ai-block="'+a+'"\]')\[0\];"aiHash"in f.dataset&&(b=f.dataset.aiHash);f="";c\[a\].hasOwnProperty("h")&&(f=c\[a\].h);if(0==c\[a\]\[d\]&&f==b)return ai\_debug\_cookie\_status=a="max clicks reached",!1;if(0>c\[a\]\[d\]&&f==b){e=new Date;e=-c\[a\]\[d\]- Math.round(e.getTime()/1E3);if(0<e)return ai\_debug\_cookie\_status=a="max clicks reached ("+Math.round(1E4\*e/24/3600)/1E4+" days = "+e+" s)",!1;ai\_set\_cookie(a,"c","");c\[a\].hasOwnProperty("i")||c\[a\].hasOwnProperty("x")||ai\_set\_cookie(a,"h","")}}if("cpt"==d&&0==c\[a\]\[d\]&&(e=new Date,b=Math.round(e.getTime()/1E3),e=c\[a\].ct-b,0<e))return ai\_debug\_cookie\_status=a="max clicks per time reached ("+Math.round(1E4\*e/24/3600)/1E4+" days = "+e+" s)",!1}if(c.hasOwnProperty("G")&&c.G.hasOwnProperty("cpt")&&0==c.G.cpt&& (e=new Date,b=Math.round(e.getTime()/1E3),e=c.G.ct-b,0<e))return ai\_debug\_cookie\_status=a="max global clicks per time reached ("+Math.round(1E4\*e/24/3600)/1E4+" days = "+e+" s)",!1}ai\_debug\_cookie\_status="OK";return!0},ai\_check\_and\_insert\_block=function(a,c){if(null==a)return!0;var d=document.getElementsByClassName(c);if(d.length){d=d\[0\];var b=d.closest("."+ai\_block\_class\_def),f=ai\_check\_block(a);!f&&0!=parseInt(d.getAttribute("limits-fallback"))&&d.hasAttribute("data-fallback-code")&&(d.setAttribute("data-code", d.getAttribute("data-fallback-code")),null!=b&&b.hasAttribute("data-ai")&&d.hasAttribute("fallback-tracking")&&d.hasAttribute("fallback\_level")&&b.setAttribute("data-ai-"+d.getAttribute("fallback\_level"),d.getAttribute("fallback-tracking")),f=!0);d.removeAttribute("data-selector");if(f)ai\_insert\_code(d),b&&(f=b.querySelectorAll(".ai-debug-block"),f.length&&(b.classList.remove("ai-list-block"),b.classList.remove("ai-list-block-ip"),b.classList.remove("ai-list-block-filter"),b.style.visibility="",b.classList.contains("ai-remove-position")&& (b.style.position="")));else{f=d.closest("div\[data-ai\]");if(null!=f&&"undefined"!=typeof f.getAttribute("data-ai")){var e=JSON.parse(b64d(f.getAttribute("data-ai")));"undefined"!==typeof e&&e.constructor===Array&&(e\[1\]="",f.setAttribute("data-ai",b64e(JSON.stringify(e))))}b&&(f=b.querySelectorAll(".ai-debug-block"),f.length&&(b.classList.remove("ai-list-block"),b.classList.remove("ai-list-block-ip"),b.classList.remove("ai-list-block-filter"),b.style.visibility="",b.classList.contains("ai-remove-position")&& (b.style.position="")))}d.classList.remove(c)}d=document.querySelectorAll("."+c+"-dbg");b=0;for(f=d.length;b<f;b++)e=d\[b\],e.querySelector(".ai-status").textContent=ai\_debug\_cookie\_status,e.querySelector(".ai-cookie-data").textContent=ai\_get\_cookie\_text(a),e.classList.remove(c+"-dbg")},ai\_load\_cookie=function(){var a=AiCookies.getJSON("aiBLOCKS");null==a&&(a={});return a},ai\_set\_cookie=function(a,c,d){var b=ai\_load\_cookie();if(""===d){if(b.hasOwnProperty(a)){delete b\[a\]\[c\];a:{c=b\[a\];for(f in c)if(c.hasOwnProperty(f)){var f= !1;break a}f=!0}f&&delete b\[a\]}}else b.hasOwnProperty(a)||(b\[a\]={}),b\[a\]\[c\]=d;0===Object.keys(b).length&&b.constructor===Object?AiCookies.remove("aiBLOCKS"):AiCookies.set("aiBLOCKS",b,{expires:365,path:"/"});return b},ai\_get\_cookie\_text=function(a){var c=AiCookies.getJSON("aiBLOCKS");null==c&&(c={});var d="";c.hasOwnProperty("G")&&(d="G\["+JSON.stringify(c.G).replace(/"/g,"").replace("{","").replace("}","")+"\] ");var b="";c.hasOwnProperty(a)&&(b=JSON.stringify(c\[a\]).replace(/"/g,"").replace("{","").replace("}", ""));return d+b}); var ai\_insertion\_js=!0,ai\_block\_class\_def="code-block"; var $jscomp=$jscomp||{};$jscomp.scope={};$jscomp.arrayIteratorImpl=function(a){var f=0;return function(){return f<a.length?{done:!1,value:a\[f++\]}:{done:!0}}};$jscomp.arrayIterator=function(a){return{next:$jscomp.arrayIteratorImpl(a)}};$jscomp.makeIterator=function(a){var f="undefined"!=typeof Symbol&&Symbol.iterator&&a\[Symbol.iterator\];return f?f.call(a):$jscomp.arrayIterator(a)}; ai\_insert=function(a,f,n){for(var k=-1!=f.indexOf(":eq")?jQuery(f):document.querySelectorAll(f),u=0,y=k.length;u<y;u++){var c=k\[u\];selector\_string=c.hasAttribute("id")?"#"+c.getAttribute("id"):c.hasAttribute("class")?"."+c.getAttribute("class").replace(RegExp(" ","g"),"."):"";var v=document.createElement("div");v.innerHTML=n;var p=v.getElementsByClassName("ai-selector-counter")\[0\];null!=p&&(p.innerText=u+1);p=v.getElementsByClassName("ai-debug-name ai-main")\[0\];if(null!=p){var m="";"undefined"!=typeof ai\_front&& ("before"==a?m=ai\_front.insertion\_before:"after"==a?m=ai\_front.insertion\_after:"prepend"==a?m=ai\_front.insertion\_prepend:"append"==a?m=ai\_front.insertion\_append:"replace-content"==a?m=ai\_front.insertion\_replace\_content:"replace-element"==a&&(m=ai\_front.insertion\_replace\_element));-1==selector\_string.indexOf(".ai-viewports")&&(p.innerText=m+" "+f+" ("+c.tagName.toLowerCase()+selector\_string+")")}p=document.createRange();m=!0;try{var w=p.createContextualFragment(v.innerHTML)}catch(t){m=!1}"before"== a?m?c.parentNode.insertBefore(w,c):jQuery(v.innerHTML).insertBefore(jQuery(c)):"after"==a?m?c.parentNode.insertBefore(w,c.nextSibling):jQuery(v.innerHTML).insertBefore(jQuery(c.nextSibling)):"prepend"==a?m?c.insertBefore(w,c.firstChild):jQuery(v.innerHTML).insertBefore(jQuery(c.firstChild)):"append"==a?m?c.insertBefore(w,null):jQuery(v.innerHTML).appendTo(jQuery(c)):"replace-content"==a?(c.innerHTML="",m?c.insertBefore(w,null):jQuery(v.innerHTML).appendTo(jQuery(c))):"replace-element"==a&&(m?c.parentNode.insertBefore(w, c):jQuery(v.innerHTML).insertBefore(jQuery(c)),c.parentNode.removeChild(c))}}; ai\_insert\_code=function(a){function f(p,m){return null==p?!1:p.classList?p.classList.contains(m):-1<(" "+p.className+" ").indexOf(" "+m+" ")}function n(p,m){null!=p&&(p.classList?p.classList.add(m):p.className+=" "+m)}function k(p,m){null!=p&&(p.classList?p.classList.remove(m):p.className=p.className.replace(new RegExp("(^|\\\\b)"+m.split(" ").join("|")+"(\\\\b|$)","gi")," "))}if("undefined"!=typeof a){var u=!1;if(f(a,"no-visibility-check")||a.offsetWidth||a.offsetHeight||a.getClientRects().length){u= a.getAttribute("data-code");var y=a.getAttribute("data-insertion-position"),c=a.getAttribute("data-selector");if(null!=u)if(null!=y&&null!=c){if(-1!=c.indexOf(":eq")?jQuery(c).length:document.querySelectorAll(c).length)ai\_insert(y,c,b64d(u)),k(a,"ai-viewports")}else{y=document.createRange();c=!0;try{var v=y.createContextualFragment(b64d(u))}catch(p){c=!1}c?a.parentNode.insertBefore(v,a.nextSibling):jQuery(b64d(u)).insertBefore(jQuery(a.nextSibling));k(a,"ai-viewports")}u=!0}else v=a.previousElementSibling, f(v,"ai-debug-bar")&&f(v,"ai-debug-script")&&(k(v,"ai-debug-script"),n(v,"ai-debug-viewport-invisible")),k(a,"ai-viewports");return u}}; ai\_insert\_list\_code=function(a){var f=document.getElementsByClassName(a)\[0\];if("undefined"!=typeof f){var n=ai\_insert\_code(f),k=f.closest("div."+ai\_block\_class\_def);if(k){n||k.removeAttribute("data-ai");var u=k.querySelectorAll(".ai-debug-block");k&&u.length&&(k.classList.remove("ai-list-block"),k.classList.remove("ai-list-block-ip"),k.classList.remove("ai-list-block-filter"),k.style.visibility="",k.classList.contains("ai-remove-position")&&(k.style.position=""))}f.classList.remove(a);n&&ai\_process\_elements()}}; ai\_insert\_viewport\_code=function(a){var f=document.getElementsByClassName(a)\[0\];if("undefined"!=typeof f){var n=ai\_insert\_code(f);f.classList.remove(a);n&&(a=f.closest("div."+ai\_block\_class\_def),null!=a&&(n=f.getAttribute("style"),null!=n&&a.setAttribute("style",a.getAttribute("style")+" "+n)));setTimeout(function(){f.removeAttribute("style")},2);ai\_process\_elements()}}; ai\_insert\_adsense\_fallback\_codes=function(a){a.style.display="none";var f=a.closest(".ai-fallback-adsense"),n=f.nextElementSibling;n.getAttribute("data-code")?ai\_insert\_code(n)&&ai\_process\_elements():n.style.display="block";f.classList.contains("ai-empty-code")&&(a=a.closest("."+ai\_block\_class\_def).getElementsByClassName("code-block-label"),0!=a.length&&(a\[0\].style.display="none"))}; ai\_insert\_code\_by\_class=function(a){var f=document.getElementsByClassName(a)\[0\];"undefined"!=typeof f&&(ai\_insert\_code(f),f.classList.remove(a))};ai\_insert\_client\_code=function(a,f){var n=document.getElementsByClassName(a)\[0\];if("undefined"!=typeof n){var k=n.getAttribute("data-code");null!=k&&ai\_check\_block()&&ai\_check\_and\_insert\_block()&&(n.setAttribute("data-code",k.substring(Math.floor(f/19))),ai\_insert\_code\_by\_class(a),n.remove())}};ai\_process\_elements\_active=!1; function ai\_process\_elements(){ai\_process\_elements\_active||setTimeout(function(){ai\_process\_elements\_active=!1;"function"==typeof ai\_process\_rotations&&ai\_process\_rotations();"function"==typeof ai\_process\_lists&&ai\_process\_lists(jQuery(".ai-list-data"));"function"==typeof ai\_process\_ip\_addresses&&ai\_process\_ip\_addresses(jQuery(".ai-ip-data"));"function"==typeof ai\_process\_filter\_hooks&&ai\_process\_filter\_hooks(jQuery(".ai-filter-check"));"function"==typeof ai\_adb\_process\_blocks&&ai\_adb\_process\_blocks(); "function"==typeof ai\_process\_impressions&&1==ai\_tracking\_finished&&ai\_process\_impressions();"function"==typeof ai\_install\_click\_trackers&&1==ai\_tracking\_finished&&ai\_install\_click\_trackers();"function"==typeof ai\_install\_close\_buttons&&ai\_install\_close\_buttons(document)},5);ai\_process\_elements\_active=!0} var targetNode=document.querySelector("body"),config={attributes:!0,childList:!1,subtree:!0},ai\_adsense\_callback=function(a,f){for(var n=$jscomp.makeIterator(a),k=n.next();!k.done;k=n.next())k=k.value,"attributes"===k.type&&"data-ad-status"==k.attributeName&&"unfilled"==k.target.dataset.adStatus&&k.target.closest(".ai-fallback-adsense")&&ai\_insert\_adsense\_fallback\_codes(k.target)},observer=new MutationObserver(ai\_adsense\_callback);observer.observe(targetNode,config); var Arrive=function(a,f,n){function k(t,d,e){c.addMethod(d,e,t.unbindEvent);c.addMethod(d,e,t.unbindEventWithSelectorOrCallback);c.addMethod(d,e,t.unbindEventWithSelectorAndCallback)}function u(t){t.arrive=m.bindEvent;k(m,t,"unbindArrive");t.leave=w.bindEvent;k(w,t,"unbindLeave")}if(a.MutationObserver&&"undefined"!==typeof HTMLElement){var y=0,c=function(){var t=HTMLElement.prototype.matches||HTMLElement.prototype.webkitMatchesSelector||HTMLElement.prototype.mozMatchesSelector||HTMLElement.prototype.msMatchesSelector; return{matchesSelector:function(d,e){return d instanceof HTMLElement&&t.call(d,e)},addMethod:function(d,e,g){var b=d\[e\];d\[e\]=function(){if(g.length==arguments.length)return g.apply(this,arguments);if("function"==typeof b)return b.apply(this,arguments)}},callCallbacks:function(d,e){e&&e.options.onceOnly&&1==e.firedElems.length&&(d=\[d\[0\]\]);for(var g=0,b;b=d\[g\];g++)b&&b.callback&&b.callback.call(b.elem,b.elem);e&&e.options.onceOnly&&1==e.firedElems.length&&e.me.unbindEventWithSelectorAndCallback.call(e.target, e.selector,e.callback)},checkChildNodesRecursively:function(d,e,g,b){for(var h=0,l;l=d\[h\];h++)g(l,e,b)&&b.push({callback:e.callback,elem:l}),0<l.childNodes.length&&c.checkChildNodesRecursively(l.childNodes,e,g,b)},mergeArrays:function(d,e){var g={},b;for(b in d)d.hasOwnProperty(b)&&(g\[b\]=d\[b\]);for(b in e)e.hasOwnProperty(b)&&(g\[b\]=e\[b\]);return g},toElementsArray:function(d){"undefined"===typeof d||"number"===typeof d.length&&d!==a||(d=\[d\]);return d}}}(),v=function(){var t=function(){this.\_eventsBucket= \[\];this.\_beforeRemoving=this.\_beforeAdding=null};t.prototype.addEvent=function(d,e,g,b){d={target:d,selector:e,options:g,callback:b,firedElems:\[\]};this.\_beforeAdding&&this.\_beforeAdding(d);this.\_eventsBucket.push(d);return d};t.prototype.removeEvent=function(d){for(var e=this.\_eventsBucket.length-1,g;g=this.\_eventsBucket\[e\];e--)d(g)&&(this.\_beforeRemoving&&this.\_beforeRemoving(g),(g=this.\_eventsBucket.splice(e,1))&&g.length&&(g\[0\].callback=null))};t.prototype.beforeAdding=function(d){this.\_beforeAdding= d};t.prototype.beforeRemoving=function(d){this.\_beforeRemoving=d};return t}(),p=function(t,d){var e=new v,g=this,b={fireOnAttributesModification:!1};e.beforeAdding(function(h){var l=h.target;if(l===a.document||l===a)l=document.getElementsByTagName("html")\[0\];var q=new MutationObserver(function(x){d.call(this,x,h)});var r=t(h.options);q.observe(l,r);h.observer=q;h.me=g});e.beforeRemoving(function(h){h.observer.disconnect()});this.bindEvent=function(h,l,q){l=c.mergeArrays(b,l);for(var r=c.toElementsArray(this), x=0;x<r.length;x++)e.addEvent(r\[x\],h,l,q)};this.unbindEvent=function(){var h=c.toElementsArray(this);e.removeEvent(function(l){for(var q=0;q<h.length;q++)if(this===n||l.target===h\[q\])return!0;return!1})};this.unbindEventWithSelectorOrCallback=function(h){var l=c.toElementsArray(this);e.removeEvent("function"===typeof h?function(q){for(var r=0;r<l.length;r++)if((this===n||q.target===l\[r\])&&q.callback===h)return!0;return!1}:function(q){for(var r=0;r<l.length;r++)if((this===n||q.target===l\[r\])&&q.selector=== h)return!0;return!1})};this.unbindEventWithSelectorAndCallback=function(h,l){var q=c.toElementsArray(this);e.removeEvent(function(r){for(var x=0;x<q.length;x++)if((this===n||r.target===q\[x\])&&r.selector===h&&r.callback===l)return!0;return!1})};return this},m=new function(){function t(g,b,h){return c.matchesSelector(g,b.selector)&&(g.\_id===n&&(g.\_id=y++),-1==b.firedElems.indexOf(g.\_id))?(b.firedElems.push(g.\_id),!0):!1}var d={fireOnAttributesModification:!1,onceOnly:!1,existing:!1};m=new p(function(g){var b= {attributes:!1,childList:!0,subtree:!0};g.fireOnAttributesModification&&(b.attributes=!0);return b},function(g,b){g.forEach(function(h){var l=h.addedNodes,q=h.target,r=\[\];null!==l&&0<l.length?c.checkChildNodesRecursively(l,b,t,r):"attributes"===h.type&&t(q,b,r)&&r.push({callback:b.callback,elem:q});c.callCallbacks(r,b)})});var e=m.bindEvent;m.bindEvent=function(g,b,h){"undefined"===typeof h?(h=b,b=d):b=c.mergeArrays(d,b);var l=c.toElementsArray(this);if(b.existing){for(var q=\[\],r=0;r<l.length;r++)for(var x= l\[r\].querySelectorAll(g),z=0;z<x.length;z++)q.push({callback:h,elem:x\[z\]});if(b.onceOnly&&q.length)return h.call(q\[0\].elem,q\[0\].elem);setTimeout(c.callCallbacks,1,q)}e.call(this,g,b,h)};return m},w=new function(){function t(g,b){return c.matchesSelector(g,b.selector)}var d={};w=new p(function(){return{childList:!0,subtree:!0}},function(g,b){g.forEach(function(h){h=h.removedNodes;var l=\[\];null!==h&&0<h.length&&c.checkChildNodesRecursively(h,b,t,l);c.callCallbacks(l,b)})});var e=w.bindEvent;w.bindEvent= function(g,b,h){"undefined"===typeof h?(h=b,b=d):b=c.mergeArrays(d,b);e.call(this,g,b,h)};return w};f&&u(f.fn);u(HTMLElement.prototype);u(NodeList.prototype);u(HTMLCollection.prototype);u(HTMLDocument.prototype);u(Window.prototype);f={};k(m,f,"unbindAllArrive");k(w,f,"unbindAllLeave");return f}}(window,"undefined"===typeof jQuery?null:jQuery,void 0); ;!function(a,b){a(function(){"use strict";function a(a,b){return null!=a&&null!=b&&a.toLowerCase()===b.toLowerCase()}function c(a,b){var c,d,e=a.length;if(!e||!b)return!1;for(c=b.toLowerCase(),d=0;d<e;++d)if(c===a\[d\].toLowerCase())return!0;return!1}function d(a){for(var b in a)i.call(a,b)&&(a\[b\]=new RegExp(a\[b\],"i"))}function e(a){return(a||"").substr(0,500)}function f(a,b){this.ua=e(a),this.\_cache={},this.maxPhoneWidth=b||600}var g={};g.mobileDetectRules={phones:{iPhone:"\\\\biPhone\\\\b|\\\\biPod\\\\b",BlackBerry:"BlackBerry|\\\\bBB10\\\\b|rim\[0-9\]+|\\\\b(BBA100|BBB100|BBD100|BBE100|BBF100|STH100)\\\\b-\[0-9\]+",Pixel:"; \\\\bPixel\\\\b",HTC:"HTC|HTC.\*(Sensation|Evo|Vision|Explorer|6800|8100|8900|A7272|S510e|C110e|Legend|Desire|T8282)|APX515CKT|Qtek9090|APA9292KT|HD\_mini|Sensation.\*Z710e|PG86100|Z715e|Desire.\*(A8181|HD)|ADR6200|ADR6400L|ADR6425|001HT|Inspire 4G|Android.\*\\\\bEVO\\\\b|T-Mobile G1|Z520m|Android \[0-9.\]+; Pixel",Nexus:"Nexus One|Nexus S|Galaxy.\*Nexus|Android.\*Nexus.\*Mobile|Nexus 4|Nexus 5|Nexus 5X|Nexus 6",Dell:"Dell\[;\]? (Streak|Aero|Venue|Venue Pro|Flash|Smoke|Mini 3iX)|XCD28|XCD35|\\\\b001DL\\\\b|\\\\b101DL\\\\b|\\\\bGS01\\\\b",Motorola:"Motorola|DROIDX|DROID BIONIC|\\\\bDroid\\\\b.\*Build|Android.\*Xoom|HRI39|MOT-|A1260|A1680|A555|A853|A855|A953|A955|A956|Motorola.\*ELECTRIFY|Motorola.\*i1|i867|i940|MB200|MB300|MB501|MB502|MB508|MB511|MB520|MB525|MB526|MB611|MB612|MB632|MB810|MB855|MB860|MB861|MB865|MB870|ME501|ME502|ME511|ME525|ME600|ME632|ME722|ME811|ME860|ME863|ME865|MT620|MT710|MT716|MT720|MT810|MT870|MT917|Motorola.\*TITANIUM|WX435|WX445|XT300|XT301|XT311|XT316|XT317|XT319|XT320|XT390|XT502|XT530|XT531|XT532|XT535|XT603|XT610|XT611|XT615|XT681|XT701|XT702|XT711|XT720|XT800|XT806|XT860|XT862|XT875|XT882|XT883|XT894|XT901|XT907|XT909|XT910|XT912|XT928|XT926|XT915|XT919|XT925|XT1021|\\\\bMoto E\\\\b|XT1068|XT1092|XT1052",Samsung:"\\\\bSamsung\\\\b|SM-G950F|SM-G955F|SM-G9250|GT-19300|SGH-I337|BGT-S5230|GT-B2100|GT-B2700|GT-B2710|GT-B3210|GT-B3310|GT-B3410|GT-B3730|GT-B3740|GT-B5510|GT-B5512|GT-B5722|GT-B6520|GT-B7300|GT-B7320|GT-B7330|GT-B7350|GT-B7510|GT-B7722|GT-B7800|GT-C3010|GT-C3011|GT-C3060|GT-C3200|GT-C3212|GT-C3212I|GT-C3262|GT-C3222|GT-C3300|GT-C3300K|GT-C3303|GT-C3303K|GT-C3310|GT-C3322|GT-C3330|GT-C3350|GT-C3500|GT-C3510|GT-C3530|GT-C3630|GT-C3780|GT-C5010|GT-C5212|GT-C6620|GT-C6625|GT-C6712|GT-E1050|GT-E1070|GT-E1075|GT-E1080|GT-E1081|GT-E1085|GT-E1087|GT-E1100|GT-E1107|GT-E1110|GT-E1120|GT-E1125|GT-E1130|GT-E1160|GT-E1170|GT-E1175|GT-E1180|GT-E1182|GT-E1200|GT-E1210|GT-E1225|GT-E1230|GT-E1390|GT-E2100|GT-E2120|GT-E2121|GT-E2152|GT-E2220|GT-E2222|GT-E2230|GT-E2232|GT-E2250|GT-E2370|GT-E2550|GT-E2652|GT-E3210|GT-E3213|GT-I5500|GT-I5503|GT-I5700|GT-I5800|GT-I5801|GT-I6410|GT-I6420|GT-I7110|GT-I7410|GT-I7500|GT-I8000|GT-I8150|GT-I8160|GT-I8190|GT-I8320|GT-I8330|GT-I8350|GT-I8530|GT-I8700|GT-I8703|GT-I8910|GT-I9000|GT-I9001|GT-I9003|GT-I9010|GT-I9020|GT-I9023|GT-I9070|GT-I9082|GT-I9100|GT-I9103|GT-I9220|GT-I9250|GT-I9300|GT-I9305|GT-I9500|GT-I9505|GT-M3510|GT-M5650|GT-M7500|GT-M7600|GT-M7603|GT-M8800|GT-M8910|GT-N7000|GT-S3110|GT-S3310|GT-S3350|GT-S3353|GT-S3370|GT-S3650|GT-S3653|GT-S3770|GT-S3850|GT-S5210|GT-S5220|GT-S5229|GT-S5230|GT-S5233|GT-S5250|GT-S5253|GT-S5260|GT-S5263|GT-S5270|GT-S5300|GT-S5330|GT-S5350|GT-S5360|GT-S5363|GT-S5369|GT-S5380|GT-S5380D|GT-S5560|GT-S5570|GT-S5600|GT-S5603|GT-S5610|GT-S5620|GT-S5660|GT-S5670|GT-S5690|GT-S5750|GT-S5780|GT-S5830|GT-S5839|GT-S6102|GT-S6500|GT-S7070|GT-S7200|GT-S7220|GT-S7230|GT-S7233|GT-S7250|GT-S7500|GT-S7530|GT-S7550|GT-S7562|GT-S7710|GT-S8000|GT-S8003|GT-S8500|GT-S8530|GT-S8600|SCH-A310|SCH-A530|SCH-A570|SCH-A610|SCH-A630|SCH-A650|SCH-A790|SCH-A795|SCH-A850|SCH-A870|SCH-A890|SCH-A930|SCH-A950|SCH-A970|SCH-A990|SCH-I100|SCH-I110|SCH-I400|SCH-I405|SCH-I500|SCH-I510|SCH-I515|SCH-I600|SCH-I730|SCH-I760|SCH-I770|SCH-I830|SCH-I910|SCH-I920|SCH-I959|SCH-LC11|SCH-N150|SCH-N300|SCH-R100|SCH-R300|SCH-R351|SCH-R400|SCH-R410|SCH-T300|SCH-U310|SCH-U320|SCH-U350|SCH-U360|SCH-U365|SCH-U370|SCH-U380|SCH-U410|SCH-U430|SCH-U450|SCH-U460|SCH-U470|SCH-U490|SCH-U540|SCH-U550|SCH-U620|SCH-U640|SCH-U650|SCH-U660|SCH-U700|SCH-U740|SCH-U750|SCH-U810|SCH-U820|SCH-U900|SCH-U940|SCH-U960|SCS-26UC|SGH-A107|SGH-A117|SGH-A127|SGH-A137|SGH-A157|SGH-A167|SGH-A177|SGH-A187|SGH-A197|SGH-A227|SGH-A237|SGH-A257|SGH-A437|SGH-A517|SGH-A597|SGH-A637|SGH-A657|SGH-A667|SGH-A687|SGH-A697|SGH-A707|SGH-A717|SGH-A727|SGH-A737|SGH-A747|SGH-A767|SGH-A777|SGH-A797|SGH-A817|SGH-A827|SGH-A837|SGH-A847|SGH-A867|SGH-A877|SGH-A887|SGH-A897|SGH-A927|SGH-B100|SGH-B130|SGH-B200|SGH-B220|SGH-C100|SGH-C110|SGH-C120|SGH-C130|SGH-C140|SGH-C160|SGH-C170|SGH-C180|SGH-C200|SGH-C207|SGH-C210|SGH-C225|SGH-C230|SGH-C417|SGH-C450|SGH-D307|SGH-D347|SGH-D357|SGH-D407|SGH-D415|SGH-D780|SGH-D807|SGH-D980|SGH-E105|SGH-E200|SGH-E315|SGH-E316|SGH-E317|SGH-E335|SGH-E590|SGH-E635|SGH-E715|SGH-E890|SGH-F300|SGH-F480|SGH-I200|SGH-I300|SGH-I320|SGH-I550|SGH-I577|SGH-I600|SGH-I607|SGH-I617|SGH-I627|SGH-I637|SGH-I677|SGH-I700|SGH-I717|SGH-I727|SGH-i747M|SGH-I777|SGH-I780|SGH-I827|SGH-I847|SGH-I857|SGH-I896|SGH-I897|SGH-I900|SGH-I907|SGH-I917|SGH-I927|SGH-I937|SGH-I997|SGH-J150|SGH-J200|SGH-L170|SGH-L700|SGH-M110|SGH-M150|SGH-M200|SGH-N105|SGH-N500|SGH-N600|SGH-N620|SGH-N625|SGH-N700|SGH-N710|SGH-P107|SGH-P207|SGH-P300|SGH-P310|SGH-P520|SGH-P735|SGH-P777|SGH-Q105|SGH-R210|SGH-R220|SGH-R225|SGH-S105|SGH-S307|SGH-T109|SGH-T119|SGH-T139|SGH-T209|SGH-T219|SGH-T229|SGH-T239|SGH-T249|SGH-T259|SGH-T309|SGH-T319|SGH-T329|SGH-T339|SGH-T349|SGH-T359|SGH-T369|SGH-T379|SGH-T409|SGH-T429|SGH-T439|SGH-T459|SGH-T469|SGH-T479|SGH-T499|SGH-T509|SGH-T519|SGH-T539|SGH-T559|SGH-T589|SGH-T609|SGH-T619|SGH-T629|SGH-T639|SGH-T659|SGH-T669|SGH-T679|SGH-T709|SGH-T719|SGH-T729|SGH-T739|SGH-T746|SGH-T749|SGH-T759|SGH-T769|SGH-T809|SGH-T819|SGH-T839|SGH-T919|SGH-T929|SGH-T939|SGH-T959|SGH-T989|SGH-U100|SGH-U200|SGH-U800|SGH-V205|SGH-V206|SGH-X100|SGH-X105|SGH-X120|SGH-X140|SGH-X426|SGH-X427|SGH-X475|SGH-X495|SGH-X497|SGH-X507|SGH-X600|SGH-X610|SGH-X620|SGH-X630|SGH-X700|SGH-X820|SGH-X890|SGH-Z130|SGH-Z150|SGH-Z170|SGH-ZX10|SGH-ZX20|SHW-M110|SPH-A120|SPH-A400|SPH-A420|SPH-A460|SPH-A500|SPH-A560|SPH-A600|SPH-A620|SPH-A660|SPH-A700|SPH-A740|SPH-A760|SPH-A790|SPH-A800|SPH-A820|SPH-A840|SPH-A880|SPH-A900|SPH-A940|SPH-A960|SPH-D600|SPH-D700|SPH-D710|SPH-D720|SPH-I300|SPH-I325|SPH-I330|SPH-I350|SPH-I500|SPH-I600|SPH-I700|SPH-L700|SPH-M100|SPH-M220|SPH-M240|SPH-M300|SPH-M305|SPH-M320|SPH-M330|SPH-M350|SPH-M360|SPH-M370|SPH-M380|SPH-M510|SPH-M540|SPH-M550|SPH-M560|SPH-M570|SPH-M580|SPH-M610|SPH-M620|SPH-M630|SPH-M800|SPH-M810|SPH-M850|SPH-M900|SPH-M910|SPH-M920|SPH-M930|SPH-N100|SPH-N200|SPH-N240|SPH-N300|SPH-N400|SPH-Z400|SWC-E100|SCH-i909|GT-N7100|GT-N7105|SCH-I535|SM-N900A|SGH-I317|SGH-T999L|GT-S5360B|GT-I8262|GT-S6802|GT-S6312|GT-S6310|GT-S5312|GT-S5310|GT-I9105|GT-I8510|GT-S6790N|SM-G7105|SM-N9005|GT-S5301|GT-I9295|GT-I9195|SM-C101|GT-S7392|GT-S7560|GT-B7610|GT-I5510|GT-S7582|GT-S7530E|GT-I8750|SM-G9006V|SM-G9008V|SM-G9009D|SM-G900A|SM-G900D|SM-G900F|SM-G900H|SM-G900I|SM-G900J|SM-G900K|SM-G900L|SM-G900M|SM-G900P|SM-G900R4|SM-G900S|SM-G900T|SM-G900V|SM-G900W8|SHV-E160K|SCH-P709|SCH-P729|SM-T2558|GT-I9205|SM-G9350|SM-J120F|SM-G920F|SM-G920V|SM-G930F|SM-N910C|SM-A310F|GT-I9190|SM-J500FN|SM-G903F|SM-J330F|SM-G610F|SM-G981B|SM-G892A|SM-A530F",LG:"\\\\bLG\\\\b;|LG\[- \]?(C800|C900|E400|E610|E900|E-900|F160|F180K|F180L|F180S|730|855|L160|LS740|LS840|LS970|LU6200|MS690|MS695|MS770|MS840|MS870|MS910|P500|P700|P705|VM696|AS680|AS695|AX840|C729|E970|GS505|272|C395|E739BK|E960|L55C|L75C|LS696|LS860|P769BK|P350|P500|P509|P870|UN272|US730|VS840|VS950|LN272|LN510|LS670|LS855|LW690|MN270|MN510|P509|P769|P930|UN200|UN270|UN510|UN610|US670|US740|US760|UX265|UX840|VN271|VN530|VS660|VS700|VS740|VS750|VS910|VS920|VS930|VX9200|VX11000|AX840A|LW770|P506|P925|P999|E612|D955|D802|MS323|M257)|LM-G710",Sony:"SonyST|SonyLT|SonyEricsson|SonyEricssonLT15iv|LT18i|E10i|LT28h|LT26w|SonyEricssonMT27i|C5303|C6902|C6903|C6906|C6943|D2533|SOV34|601SO|F8332",Asus:"Asus.\*Galaxy|PadFone.\*Mobile",Xiaomi:"^(?!.\*\\\\bx11\\\\b).\*xiaomi.\*$|POCOPHONE F1|MI 8|Redmi Note 9S|Redmi Note 5A Prime|N2G47H|M2001J2G|M2001J2I|M1805E10A|M2004J11G|M1902F1G|M2002J9G|M2004J19G|M2003J6A1G",NokiaLumia:"Lumia \[0-9\]{3,4}",Micromax:"Micromax.\*\\\\b(A210|A92|A88|A72|A111|A110Q|A115|A116|A110|A90S|A26|A51|A35|A54|A25|A27|A89|A68|A65|A57|A90)\\\\b",Palm:"PalmSource|Palm",Vertu:"Vertu|Vertu.\*Ltd|Vertu.\*Ascent|Vertu.\*Ayxta|Vertu.\*Constellation(F|Quest)?|Vertu.\*Monika|Vertu.\*Signature",Pantech:"PANTECH|IM-A850S|IM-A840S|IM-A830L|IM-A830K|IM-A830S|IM-A820L|IM-A810K|IM-A810S|IM-A800S|IM-T100K|IM-A725L|IM-A780L|IM-A775C|IM-A770K|IM-A760S|IM-A750K|IM-A740S|IM-A730S|IM-A720L|IM-A710K|IM-A690L|IM-A690S|IM-A650S|IM-A630K|IM-A600S|VEGA PTL21|PT003|P8010|ADR910L|P6030|P6020|P9070|P4100|P9060|P5000|CDM8992|TXT8045|ADR8995|IS11PT|P2030|P6010|P8000|PT002|IS06|CDM8999|P9050|PT001|TXT8040|P2020|P9020|P2000|P7040|P7000|C790",Fly:"IQ230|IQ444|IQ450|IQ440|IQ442|IQ441|IQ245|IQ256|IQ236|IQ255|IQ235|IQ245|IQ275|IQ240|IQ285|IQ280|IQ270|IQ260|IQ250",Wiko:"KITE 4G|HIGHWAY|GETAWAY|STAIRWAY|DARKSIDE|DARKFULL|DARKNIGHT|DARKMOON|SLIDE|WAX 4G|RAINBOW|BLOOM|SUNSET|GOA(?!nna)|LENNY|BARRY|IGGY|OZZY|CINK FIVE|CINK PEAX|CINK PEAX 2|CINK SLIM|CINK SLIM 2|CINK +|CINK KING|CINK PEAX|CINK SLIM|SUBLIM",iMobile:"i-mobile (IQ|i-STYLE|idea|ZAA|Hitz)",SimValley:"\\\\b(SP-80|XT-930|SX-340|XT-930|SX-310|SP-360|SP60|SPT-800|SP-120|SPT-800|SP-140|SPX-5|SPX-8|SP-100|SPX-8|SPX-12)\\\\b",Wolfgang:"AT-B24D|AT-AS50HD|AT-AS40W|AT-AS55HD|AT-AS45q2|AT-B26D|AT-AS50Q",Alcatel:"Alcatel",Nintendo:"Nintendo (3DS|Switch)",Amoi:"Amoi",INQ:"INQ",OnePlus:"ONEPLUS",GenericPhone:"Tapatalk|PDA;|SAGEM|\\\\bmmp\\\\b|pocket|\\\\bpsp\\\\b|symbian|Smartphone|smartfon|treo|up.browser|up.link|vodafone|\\\\bwap\\\\b|nokia|Series40|Series60|S60|SonyEricsson|N900|MAUI.\*WAP.\*Browser"},tablets:{iPad:"iPad|iPad.\*Mobile",NexusTablet:"Android.\*Nexus\[\\\\s\]+(7|9|10)",GoogleTablet:"Android.\*Pixel C",SamsungTablet:"SAMSUNG.\*Tablet|Galaxy.\*Tab|SC-01C|GT-P1000|GT-P1003|GT-P1010|GT-P3105|GT-P6210|GT-P6800|GT-P6810|GT-P7100|GT-P7300|GT-P7310|GT-P7500|GT-P7510|SCH-I800|SCH-I815|SCH-I905|SGH-I957|SGH-I987|SGH-T849|SGH-T859|SGH-T869|SPH-P100|GT-P3100|GT-P3108|GT-P3110|GT-P5100|GT-P5110|GT-P6200|GT-P7320|GT-P7511|GT-N8000|GT-P8510|SGH-I497|SPH-P500|SGH-T779|SCH-I705|SCH-I915|GT-N8013|GT-P3113|GT-P5113|GT-P8110|GT-N8010|GT-N8005|GT-N8020|GT-P1013|GT-P6201|GT-P7501|GT-N5100|GT-N5105|GT-N5110|SHV-E140K|SHV-E140L|SHV-E140S|SHV-E150S|SHV-E230K|SHV-E230L|SHV-E230S|SHW-M180K|SHW-M180L|SHW-M180S|SHW-M180W|SHW-M300W|SHW-M305W|SHW-M380K|SHW-M380S|SHW-M380W|SHW-M430W|SHW-M480K|SHW-M480S|SHW-M480W|SHW-M485W|SHW-M486W|SHW-M500W|GT-I9228|SCH-P739|SCH-I925|GT-I9200|GT-P5200|GT-P5210|GT-P5210X|SM-T311|SM-T310|SM-T310X|SM-T210|SM-T210R|SM-T211|SM-P600|SM-P601|SM-P605|SM-P900|SM-P901|SM-T217|SM-T217A|SM-T217S|SM-P6000|SM-T3100|SGH-I467|XE500|SM-T110|GT-P5220|GT-I9200X|GT-N5110X|GT-N5120|SM-P905|SM-T111|SM-T2105|SM-T315|SM-T320|SM-T320X|SM-T321|SM-T520|SM-T525|SM-T530NU|SM-T230NU|SM-T330NU|SM-T900|XE500T1C|SM-P605V|SM-P905V|SM-T337V|SM-T537V|SM-T707V|SM-T807V|SM-P600X|SM-P900X|SM-T210X|SM-T230|SM-T230X|SM-T325|GT-P7503|SM-T531|SM-T330|SM-T530|SM-T705|SM-T705C|SM-T535|SM-T331|SM-T800|SM-T700|SM-T537|SM-T807|SM-P907A|SM-T337A|SM-T537A|SM-T707A|SM-T807A|SM-T237|SM-T807P|SM-P607T|SM-T217T|SM-T337T|SM-T807T|SM-T116NQ|SM-T116BU|SM-P550|SM-T350|SM-T550|SM-T9000|SM-P9000|SM-T705Y|SM-T805|GT-P3113|SM-T710|SM-T810|SM-T815|SM-T360|SM-T533|SM-T113|SM-T335|SM-T715|SM-T560|SM-T670|SM-T677|SM-T377|SM-T567|SM-T357T|SM-T555|SM-T561|SM-T713|SM-T719|SM-T813|SM-T819|SM-T580|SM-T355Y?|SM-T280|SM-T817A|SM-T820|SM-W700|SM-P580|SM-T587|SM-P350|SM-P555M|SM-P355M|SM-T113NU|SM-T815Y|SM-T585|SM-T285|SM-T825|SM-W708|SM-T835|SM-T830|SM-T837V|SM-T720|SM-T510|SM-T387V|SM-P610|SM-T290|SM-T515|SM-T590|SM-T595|SM-T725|SM-T817P|SM-P585N0|SM-T395|SM-T295|SM-T865|SM-P610N|SM-P615|SM-T970|SM-T380|SM-T5950|SM-T905|SM-T231|SM-T500|SM-T860",Kindle:"Kindle|Silk.\*Accelerated|Android.\*\\\\b(KFOT|KFTT|KFJWI|KFJWA|KFOTE|KFSOWI|KFTHWI|KFTHWA|KFAPWI|KFAPWA|WFJWAE|KFSAWA|KFSAWI|KFASWI|KFARWI|KFFOWI|KFGIWI|KFMEWI)\\\\b|Android.\*Silk/\[0-9.\]+ like Chrome/\[0-9.\]+ (?!Mobile)",SurfaceTablet:"Windows NT \[0-9.\]+; ARM;.\*(Tablet|ARMBJS)",HPTablet:"HP Slate (7|8|10)|HP ElitePad 900|hp-tablet|EliteBook.\*Touch|HP 8|Slate 21|HP SlateBook 10",AsusTablet:"^.\*PadFone((?!Mobile).)\*$|Transformer|TF101|TF101G|TF300T|TF300TG|TF300TL|TF700T|TF700KL|TF701T|TF810C|ME171|ME301T|ME302C|ME371MG|ME370T|ME372MG|ME172V|ME173X|ME400C|Slider SL101|\\\\bK00F\\\\b|\\\\bK00C\\\\b|\\\\bK00E\\\\b|\\\\bK00L\\\\b|TX201LA|ME176C|ME102A|\\\\bM80TA\\\\b|ME372CL|ME560CG|ME372CG|ME302KL| K010 | K011 | K017 | K01E |ME572C|ME103K|ME170C|ME171C|\\\\bME70C\\\\b|ME581C|ME581CL|ME8510C|ME181C|P01Y|PO1MA|P01Z|\\\\bP027\\\\b|\\\\bP024\\\\b|\\\\bP00C\\\\b",BlackBerryTablet:"PlayBook|RIM Tablet",HTCtablet:"HTC\_Flyer\_P512|HTC Flyer|HTC Jetstream|HTC-P715a|HTC EVO View 4G|PG41200|PG09410",MotorolaTablet:"xoom|sholest|MZ615|MZ605|MZ505|MZ601|MZ602|MZ603|MZ604|MZ606|MZ607|MZ608|MZ609|MZ615|MZ616|MZ617",NookTablet:"Android.\*Nook|NookColor|nook browser|BNRV200|BNRV200A|BNTV250|BNTV250A|BNTV400|BNTV600|LogicPD Zoom2",AcerTablet:"Android.\*; \\\\b(A100|A101|A110|A200|A210|A211|A500|A501|A510|A511|A700|A701|W500|W500P|W501|W501P|W510|W511|W700|G100|G100W|B1-A71|B1-710|B1-711|A1-810|A1-811|A1-830)\\\\b|W3-810|\\\\bA3-A10\\\\b|\\\\bA3-A11\\\\b|\\\\bA3-A20\\\\b|\\\\bA3-A30|A3-A40",ToshibaTablet:"Android.\*(AT100|AT105|AT200|AT205|AT270|AT275|AT300|AT305|AT1S5|AT500|AT570|AT700|AT830)|TOSHIBA.\*FOLIO",LGTablet:"\\\\bL-06C|LG-V909|LG-V900|LG-V700|LG-V510|LG-V500|LG-V410|LG-V400|LG-VK810\\\\b",FujitsuTablet:"Android.\*\\\\b(F-01D|F-02F|F-05E|F-10D|M532|Q572)\\\\b",PrestigioTablet:"PMP3170B|PMP3270B|PMP3470B|PMP7170B|PMP3370B|PMP3570C|PMP5870C|PMP3670B|PMP5570C|PMP5770D|PMP3970B|PMP3870C|PMP5580C|PMP5880D|PMP5780D|PMP5588C|PMP7280C|PMP7280C3G|PMP7280|PMP7880D|PMP5597D|PMP5597|PMP7100D|PER3464|PER3274|PER3574|PER3884|PER5274|PER5474|PMP5097CPRO|PMP5097|PMP7380D|PMP5297C|PMP5297C\_QUAD|PMP812E|PMP812E3G|PMP812F|PMP810E|PMP880TD|PMT3017|PMT3037|PMT3047|PMT3057|PMT7008|PMT5887|PMT5001|PMT5002",LenovoTablet:"Lenovo TAB|Idea(Tab|Pad)( A1|A10| K1|)|ThinkPad(\[ \]+)?Tablet|YT3-850M|YT3-X90L|YT3-X90F|YT3-X90X|Lenovo.\*(S2109|S2110|S5000|S6000|K3011|A3000|A3500|A1000|A2107|A2109|A1107|A5500|A7600|B6000|B8000|B8080)(-|)(FL|F|HV|H|)|TB-X103F|TB-X304X|TB-X304F|TB-X304L|TB-X505F|TB-X505L|TB-X505X|TB-X605F|TB-X605L|TB-8703F|TB-8703X|TB-8703N|TB-8704N|TB-8704F|TB-8704X|TB-8704V|TB-7304F|TB-7304I|TB-7304X|Tab2A7-10F|Tab2A7-20F|TB2-X30L|YT3-X50L|YT3-X50F|YT3-X50M|YT-X705F|YT-X703F|YT-X703L|YT-X705L|YT-X705X|TB2-X30F|TB2-X30L|TB2-X30M|A2107A-F|A2107A-H|TB3-730F|TB3-730M|TB3-730X|TB-7504F|TB-7504X|TB-X704F|TB-X104F|TB3-X70F|TB-X705F|TB-8504F|TB3-X70L|TB3-710F|TB-X704L",DellTablet:"Venue 11|Venue 8|Venue 7|Dell Streak 10|Dell Streak 7",YarvikTablet:"Android.\*\\\\b(TAB210|TAB211|TAB224|TAB250|TAB260|TAB264|TAB310|TAB360|TAB364|TAB410|TAB411|TAB420|TAB424|TAB450|TAB460|TAB461|TAB464|TAB465|TAB467|TAB468|TAB07-100|TAB07-101|TAB07-150|TAB07-151|TAB07-152|TAB07-200|TAB07-201-3G|TAB07-210|TAB07-211|TAB07-212|TAB07-214|TAB07-220|TAB07-400|TAB07-485|TAB08-150|TAB08-200|TAB08-201-3G|TAB08-201-30|TAB09-100|TAB09-211|TAB09-410|TAB10-150|TAB10-201|TAB10-211|TAB10-400|TAB10-410|TAB13-201|TAB274EUK|TAB275EUK|TAB374EUK|TAB462EUK|TAB474EUK|TAB9-200)\\\\b",MedionTablet:"Android.\*\\\\bOYO\\\\b|LIFE.\*(P9212|P9514|P9516|S9512)|LIFETAB",ArnovaTablet:"97G4|AN10G2|AN7bG3|AN7fG3|AN8G3|AN8cG3|AN7G3|AN9G3|AN7dG3|AN7dG3ST|AN7dG3ChildPad|AN10bG3|AN10bG3DT|AN9G2",IntensoTablet:"INM8002KP|INM1010FP|INM805ND|Intenso Tab|TAB1004",IRUTablet:"M702pro",MegafonTablet:"MegaFon V9|\\\\bZTE V9\\\\b|Android.\*\\\\bMT7A\\\\b",EbodaTablet:"E-Boda (Supreme|Impresspeed|Izzycomm|Essential)",AllViewTablet:"Allview.\*(Viva|Alldro|City|Speed|All TV|Frenzy|Quasar|Shine|TX1|AX1|AX2)",ArchosTablet:"\\\\b(101G9|80G9|A101IT)\\\\b|Qilive 97R|Archos5|\\\\bARCHOS (70|79|80|90|97|101|FAMILYPAD|)(b|c|)(G10| Cobalt| TITANIUM(HD|)| Xenon| Neon|XSK| 2| XS 2| PLATINUM| CARBON|GAMEPAD)\\\\b",AinolTablet:"NOVO7|NOVO8|NOVO10|Novo7Aurora|Novo7Basic|NOVO7PALADIN|novo9-Spark",NokiaLumiaTablet:"Lumia 2520",SonyTablet:"Sony.\*Tablet|Xperia Tablet|Sony Tablet S|SO-03E|SGPT12|SGPT13|SGPT114|SGPT121|SGPT122|SGPT123|SGPT111|SGPT112|SGPT113|SGPT131|SGPT132|SGPT133|SGPT211|SGPT212|SGPT213|SGP311|SGP312|SGP321|EBRD1101|EBRD1102|EBRD1201|SGP351|SGP341|SGP511|SGP512|SGP521|SGP541|SGP551|SGP621|SGP641|SGP612|SOT31|SGP771|SGP611|SGP612|SGP712",PhilipsTablet:"\\\\b(PI2010|PI3000|PI3100|PI3105|PI3110|PI3205|PI3210|PI3900|PI4010|PI7000|PI7100)\\\\b",CubeTablet:"Android.\*(K8GT|U9GT|U10GT|U16GT|U17GT|U18GT|U19GT|U20GT|U23GT|U30GT)|CUBE U8GT",CobyTablet:"MID1042|MID1045|MID1125|MID1126|MID7012|MID7014|MID7015|MID7034|MID7035|MID7036|MID7042|MID7048|MID7127|MID8042|MID8048|MID8127|MID9042|MID9740|MID9742|MID7022|MID7010",MIDTablet:"M9701|M9000|M9100|M806|M1052|M806|T703|MID701|MID713|MID710|MID727|MID760|MID830|MID728|MID933|MID125|MID810|MID732|MID120|MID930|MID800|MID731|MID900|MID100|MID820|MID735|MID980|MID130|MID833|MID737|MID960|MID135|MID860|MID736|MID140|MID930|MID835|MID733|MID4X10",MSITablet:"MSI \\\\b(Primo 73K|Primo 73L|Primo 81L|Primo 77|Primo 93|Primo 75|Primo 76|Primo 73|Primo 81|Primo 91|Primo 90|Enjoy 71|Enjoy 7|Enjoy 10)\\\\b",SMiTTablet:"Android.\*(\\\\bMID\\\\b|MID-560|MTV-T1200|MTV-PND531|MTV-P1101|MTV-PND530)",RockChipTablet:"Android.\*(RK2818|RK2808A|RK2918|RK3066)|RK2738|RK2808A",FlyTablet:"IQ310|Fly Vision",bqTablet:"Android.\*(bq)?.\*\\\\b(Elcano|Curie|Edison|Maxwell|Kepler|Pascal|Tesla|Hypatia|Platon|Newton|Livingstone|Cervantes|Avant|Aquaris (\[E|M\]10|M8))\\\\b|Maxwell.\*Lite|Maxwell.\*Plus",HuaweiTablet:"MediaPad|MediaPad 7 Youth|IDEOS S7|S7-201c|S7-202u|S7-101|S7-103|S7-104|S7-105|S7-106|S7-201|S7-Slim|M2-A01L|BAH-L09|BAH-W09|AGS-L09|CMR-AL19",NecTablet:"\\\\bN-06D|\\\\bN-08D",PantechTablet:"Pantech.\*P4100",BronchoTablet:"Broncho.\*(N701|N708|N802|a710)",VersusTablet:"TOUCHPAD.\*\[78910\]|\\\\bTOUCHTAB\\\\b",ZyncTablet:"z1000|Z99 2G|z930|z990|z909|Z919|z900",PositivoTablet:"TB07STA|TB10STA|TB07FTA|TB10FTA",NabiTablet:"Android.\*\\\\bNabi",KoboTablet:"Kobo Touch|\\\\bK080\\\\b|\\\\bVox\\\\b Build|\\\\bArc\\\\b Build",DanewTablet:"DSlide.\*\\\\b(700|701R|702|703R|704|802|970|971|972|973|974|1010|1012)\\\\b",TexetTablet:"NaviPad|TB-772A|TM-7045|TM-7055|TM-9750|TM-7016|TM-7024|TM-7026|TM-7041|TM-7043|TM-7047|TM-8041|TM-9741|TM-9747|TM-9748|TM-9751|TM-7022|TM-7021|TM-7020|TM-7011|TM-7010|TM-7023|TM-7025|TM-7037W|TM-7038W|TM-7027W|TM-9720|TM-9725|TM-9737W|TM-1020|TM-9738W|TM-9740|TM-9743W|TB-807A|TB-771A|TB-727A|TB-725A|TB-719A|TB-823A|TB-805A|TB-723A|TB-715A|TB-707A|TB-705A|TB-709A|TB-711A|TB-890HD|TB-880HD|TB-790HD|TB-780HD|TB-770HD|TB-721HD|TB-710HD|TB-434HD|TB-860HD|TB-840HD|TB-760HD|TB-750HD|TB-740HD|TB-730HD|TB-722HD|TB-720HD|TB-700HD|TB-500HD|TB-470HD|TB-431HD|TB-430HD|TB-506|TB-504|TB-446|TB-436|TB-416|TB-146SE|TB-126SE",PlaystationTablet:"Playstation.\*(Portable|Vita)",TrekstorTablet:"ST10416-1|VT10416-1|ST70408-1|ST702xx-1|ST702xx-2|ST80208|ST97216|ST70104-2|VT10416-2|ST10216-2A|SurfTab",PyleAudioTablet:"\\\\b(PTBL10CEU|PTBL10C|PTBL72BC|PTBL72BCEU|PTBL7CEU|PTBL7C|PTBL92BC|PTBL92BCEU|PTBL9CEU|PTBL9CUK|PTBL9C)\\\\b",AdvanTablet:"Android.\* \\\\b(E3A|T3X|T5C|T5B|T3E|T3C|T3B|T1J|T1F|T2A|T1H|T1i|E1C|T1-E|T5-A|T4|E1-B|T2Ci|T1-B|T1-D|O1-A|E1-A|T1-A|T3A|T4i)\\\\b ",DanyTechTablet:"Genius Tab G3|Genius Tab S2|Genius Tab Q3|Genius Tab G4|Genius Tab Q4|Genius Tab G-II|Genius TAB GII|Genius TAB GIII|Genius Tab S1",GalapadTablet:"Android \[0-9.\]+; \[a-z-\]+; \\\\bG1\\\\b",MicromaxTablet:"Funbook|Micromax.\*\\\\b(P250|P560|P360|P362|P600|P300|P350|P500|P275)\\\\b",KarbonnTablet:"Android.\*\\\\b(A39|A37|A34|ST8|ST10|ST7|Smart Tab3|Smart Tab2)\\\\b",AllFineTablet:"Fine7 Genius|Fine7 Shine|Fine7 Air|Fine8 Style|Fine9 More|Fine10 Joy|Fine11 Wide",PROSCANTablet:"\\\\b(PEM63|PLT1023G|PLT1041|PLT1044|PLT1044G|PLT1091|PLT4311|PLT4311PL|PLT4315|PLT7030|PLT7033|PLT7033D|PLT7035|PLT7035D|PLT7044K|PLT7045K|PLT7045KB|PLT7071KG|PLT7072|PLT7223G|PLT7225G|PLT7777G|PLT7810K|PLT7849G|PLT7851G|PLT7852G|PLT8015|PLT8031|PLT8034|PLT8036|PLT8080K|PLT8082|PLT8088|PLT8223G|PLT8234G|PLT8235G|PLT8816K|PLT9011|PLT9045K|PLT9233G|PLT9735|PLT9760G|PLT9770G)\\\\b",YONESTablet:"BQ1078|BC1003|BC1077|RK9702|BC9730|BC9001|IT9001|BC7008|BC7010|BC708|BC728|BC7012|BC7030|BC7027|BC7026",ChangJiaTablet:"TPC7102|TPC7103|TPC7105|TPC7106|TPC7107|TPC7201|TPC7203|TPC7205|TPC7210|TPC7708|TPC7709|TPC7712|TPC7110|TPC8101|TPC8103|TPC8105|TPC8106|TPC8203|TPC8205|TPC8503|TPC9106|TPC9701|TPC97101|TPC97103|TPC97105|TPC97106|TPC97111|TPC97113|TPC97203|TPC97603|TPC97809|TPC97205|TPC10101|TPC10103|TPC10106|TPC10111|TPC10203|TPC10205|TPC10503",GUTablet:"TX-A1301|TX-M9002|Q702|kf026",PointOfViewTablet:"TAB-P506|TAB-navi-7-3G-M|TAB-P517|TAB-P-527|TAB-P701|TAB-P703|TAB-P721|TAB-P731N|TAB-P741|TAB-P825|TAB-P905|TAB-P925|TAB-PR945|TAB-PL1015|TAB-P1025|TAB-PI1045|TAB-P1325|TAB-PROTAB\[0-9\]+|TAB-PROTAB25|TAB-PROTAB26|TAB-PROTAB27|TAB-PROTAB26XL|TAB-PROTAB2-IPS9|TAB-PROTAB30-IPS9|TAB-PROTAB25XXL|TAB-PROTAB26-IPS10|TAB-PROTAB30-IPS10",OvermaxTablet:"OV-(SteelCore|NewBase|Basecore|Baseone|Exellen|Quattor|EduTab|Solution|ACTION|BasicTab|TeddyTab|MagicTab|Stream|TB-08|TB-09)|Qualcore 1027",HCLTablet:"HCL.\*Tablet|Connect-3G-2.0|Connect-2G-2.0|ME Tablet U1|ME Tablet U2|ME Tablet G1|ME Tablet X1|ME Tablet Y2|ME Tablet Sync",DPSTablet:"DPS Dream 9|DPS Dual 7",VistureTablet:"V97 HD|i75 3G|Visture V4( HD)?|Visture V5( HD)?|Visture V10",CrestaTablet:"CTP(-)?810|CTP(-)?818|CTP(-)?828|CTP(-)?838|CTP(-)?888|CTP(-)?978|CTP(-)?980|CTP(-)?987|CTP(-)?988|CTP(-)?989",MediatekTablet:"\\\\bMT8125|MT8389|MT8135|MT8377\\\\b",ConcordeTablet:"Concorde(\[ \]+)?Tab|ConCorde ReadMan",GoCleverTablet:"GOCLEVER TAB|A7GOCLEVER|M1042|M7841|M742|R1042BK|R1041|TAB A975|TAB A7842|TAB A741|TAB A741L|TAB M723G|TAB M721|TAB A1021|TAB I921|TAB R721|TAB I720|TAB T76|TAB R70|TAB R76.2|TAB R106|TAB R83.2|TAB M813G|TAB I721|GCTA722|TAB I70|TAB I71|TAB S73|TAB R73|TAB R74|TAB R93|TAB R75|TAB R76.1|TAB A73|TAB A93|TAB A93.2|TAB T72|TAB R83|TAB R974|TAB R973|TAB A101|TAB A103|TAB A104|TAB A104.2|R105BK|M713G|A972BK|TAB A971|TAB R974.2|TAB R104|TAB R83.3|TAB A1042",ModecomTablet:"FreeTAB 9000|FreeTAB 7.4|FreeTAB 7004|FreeTAB 7800|FreeTAB 2096|FreeTAB 7.5|FreeTAB 1014|FreeTAB 1001 |FreeTAB 8001|FreeTAB 9706|FreeTAB 9702|FreeTAB 7003|FreeTAB 7002|FreeTAB 1002|FreeTAB 7801|FreeTAB 1331|FreeTAB 1004|FreeTAB 8002|FreeTAB 8014|FreeTAB 9704|FreeTAB 1003",VoninoTablet:"\\\\b(Argus\[ \_\]?S|Diamond\[ \_\]?79HD|Emerald\[ \_\]?78E|Luna\[ \_\]?70C|Onyx\[ \_\]?S|Onyx\[ \_\]?Z|Orin\[ \_\]?HD|Orin\[ \_\]?S|Otis\[ \_\]?S|SpeedStar\[ \_\]?S|Magnet\[ \_\]?M9|Primus\[ \_\]?94\[ \_\]?3G|Primus\[ \_\]?94HD|Primus\[ \_\]?QS|Android.\*\\\\bQ8\\\\b|Sirius\[ \_\]?EVO\[ \_\]?QS|Sirius\[ \_\]?QS|Spirit\[ \_\]?S)\\\\b",ECSTablet:"V07OT2|TM105A|S10OT1|TR10CS1",StorexTablet:"eZee\[\_'\]?(Tab|Go)\[0-9\]+|TabLC7|Looney Tunes Tab",VodafoneTablet:"SmartTab(\[ \]+)?\[0-9\]+|SmartTabII10|SmartTabII7|VF-1497|VFD 1400",EssentielBTablet:"Smart\[ '\]?TAB\[ \]+?\[0-9\]+|Family\[ '\]?TAB2",RossMoorTablet:"RM-790|RM-997|RMD-878G|RMD-974R|RMT-705A|RMT-701|RME-601|RMT-501|RMT-711",iMobileTablet:"i-mobile i-note",TolinoTablet:"tolino tab \[0-9.\]+|tolino shine",AudioSonicTablet:"\\\\bC-22Q|T7-QC|T-17B|T-17P\\\\b",AMPETablet:"Android.\* A78 ",SkkTablet:"Android.\* (SKYPAD|PHOENIX|CYCLOPS)",TecnoTablet:"TECNO P9|TECNO DP8D",JXDTablet:"Android.\* \\\\b(F3000|A3300|JXD5000|JXD3000|JXD2000|JXD300B|JXD300|S5800|S7800|S602b|S5110b|S7300|S5300|S602|S603|S5100|S5110|S601|S7100a|P3000F|P3000s|P101|P200s|P1000m|P200m|P9100|P1000s|S6600b|S908|P1000|P300|S18|S6600|S9100)\\\\b",iJoyTablet:"Tablet (Spirit 7|Essentia|Galatea|Fusion|Onix 7|Landa|Titan|Scooby|Deox|Stella|Themis|Argon|Unique 7|Sygnus|Hexen|Finity 7|Cream|Cream X2|Jade|Neon 7|Neron 7|Kandy|Scape|Saphyr 7|Rebel|Biox|Rebel|Rebel 8GB|Myst|Draco 7|Myst|Tab7-004|Myst|Tadeo Jones|Tablet Boing|Arrow|Draco Dual Cam|Aurix|Mint|Amity|Revolution|Finity 9|Neon 9|T9w|Amity 4GB Dual Cam|Stone 4GB|Stone 8GB|Andromeda|Silken|X2|Andromeda II|Halley|Flame|Saphyr 9,7|Touch 8|Planet|Triton|Unique 10|Hexen 10|Memphis 4GB|Memphis 8GB|Onix 10)",FX2Tablet:"FX2 PAD7|FX2 PAD10",XoroTablet:"KidsPAD 701|PAD\[ \]?712|PAD\[ \]?714|PAD\[ \]?716|PAD\[ \]?717|PAD\[ \]?718|PAD\[ \]?720|PAD\[ \]?721|PAD\[ \]?722|PAD\[ \]?790|PAD\[ \]?792|PAD\[ \]?900|PAD\[ \]?9715D|PAD\[ \]?9716DR|PAD\[ \]?9718DR|PAD\[ \]?9719QR|PAD\[ \]?9720QR|TelePAD1030|Telepad1032|TelePAD730|TelePAD731|TelePAD732|TelePAD735Q|TelePAD830|TelePAD9730|TelePAD795|MegaPAD 1331|MegaPAD 1851|MegaPAD 2151",ViewsonicTablet:"ViewPad 10pi|ViewPad 10e|ViewPad 10s|ViewPad E72|ViewPad7|ViewPad E100|ViewPad 7e|ViewSonic VB733|VB100a",VerizonTablet:"QTAQZ3|QTAIR7|QTAQTZ3|QTASUN1|QTASUN2|QTAXIA1",OdysTablet:"LOOX|XENO10|ODYS\[ -\](Space|EVO|Xpress|NOON)|\\\\bXELIO\\\\b|Xelio10Pro|XELIO7PHONETAB|XELIO10EXTREME|XELIOPT2|NEO\_QUAD10",CaptivaTablet:"CAPTIVA PAD",IconbitTablet:"NetTAB|NT-3702|NT-3702S|NT-3702S|NT-3603P|NT-3603P|NT-0704S|NT-0704S|NT-3805C|NT-3805C|NT-0806C|NT-0806C|NT-0909T|NT-0909T|NT-0907S|NT-0907S|NT-0902S|NT-0902S",TeclastTablet:"T98 4G|\\\\bP80\\\\b|\\\\bX90HD\\\\b|X98 Air|X98 Air 3G|\\\\bX89\\\\b|P80 3G|\\\\bX80h\\\\b|P98 Air|\\\\bX89HD\\\\b|P98 3G|\\\\bP90HD\\\\b|P89 3G|X98 3G|\\\\bP70h\\\\b|P79HD 3G|G18d 3G|\\\\bP79HD\\\\b|\\\\bP89s\\\\b|\\\\bA88\\\\b|\\\\bP10HD\\\\b|\\\\bP19HD\\\\b|G18 3G|\\\\bP78HD\\\\b|\\\\bA78\\\\b|\\\\bP75\\\\b|G17s 3G|G17h 3G|\\\\bP85t\\\\b|\\\\bP90\\\\b|\\\\bP11\\\\b|\\\\bP98t\\\\b|\\\\bP98HD\\\\b|\\\\bG18d\\\\b|\\\\bP85s\\\\b|\\\\bP11HD\\\\b|\\\\bP88s\\\\b|\\\\bA80HD\\\\b|\\\\bA80se\\\\b|\\\\bA10h\\\\b|\\\\bP89\\\\b|\\\\bP78s\\\\b|\\\\bG18\\\\b|\\\\bP85\\\\b|\\\\bA70h\\\\b|\\\\bA70\\\\b|\\\\bG17\\\\b|\\\\bP18\\\\b|\\\\bA80s\\\\b|\\\\bA11s\\\\b|\\\\bP88HD\\\\b|\\\\bA80h\\\\b|\\\\bP76s\\\\b|\\\\bP76h\\\\b|\\\\bP98\\\\b|\\\\bA10HD\\\\b|\\\\bP78\\\\b|\\\\bP88\\\\b|\\\\bA11\\\\b|\\\\bA10t\\\\b|\\\\bP76a\\\\b|\\\\bP76t\\\\b|\\\\bP76e\\\\b|\\\\bP85HD\\\\b|\\\\bP85a\\\\b|\\\\bP86\\\\b|\\\\bP75HD\\\\b|\\\\bP76v\\\\b|\\\\bA12\\\\b|\\\\bP75a\\\\b|\\\\bA15\\\\b|\\\\bP76Ti\\\\b|\\\\bP81HD\\\\b|\\\\bA10\\\\b|\\\\bT760VE\\\\b|\\\\bT720HD\\\\b|\\\\bP76\\\\b|\\\\bP73\\\\b|\\\\bP71\\\\b|\\\\bP72\\\\b|\\\\bT720SE\\\\b|\\\\bC520Ti\\\\b|\\\\bT760\\\\b|\\\\bT720VE\\\\b|T720-3GE|T720-WiFi",OndaTablet:"\\\\b(V975i|Vi30|VX530|V701|Vi60|V701s|Vi50|V801s|V719|Vx610w|VX610W|V819i|Vi10|VX580W|Vi10|V711s|V813|V811|V820w|V820|Vi20|V711|VI30W|V712|V891w|V972|V819w|V820w|Vi60|V820w|V711|V813s|V801|V819|V975s|V801|V819|V819|V818|V811|V712|V975m|V101w|V961w|V812|V818|V971|V971s|V919|V989|V116w|V102w|V973|Vi40)\\\\b\[\\\\s\]+|V10 \\\\b4G\\\\b",JaytechTablet:"TPC-PA762",BlaupunktTablet:"Endeavour 800NG|Endeavour 1010",DigmaTablet:"\\\\b(iDx10|iDx9|iDx8|iDx7|iDxD7|iDxD8|iDsQ8|iDsQ7|iDsQ8|iDsD10|iDnD7|3TS804H|iDsQ11|iDj7|iDs10)\\\\b",EvolioTablet:"ARIA\_Mini\_wifi|Aria\[ \_\]Mini|Evolio X10|Evolio X7|Evolio X8|\\\\bEvotab\\\\b|\\\\bNeura\\\\b",LavaTablet:"QPAD E704|\\\\bIvoryS\\\\b|E-TAB IVORY|\\\\bE-TAB\\\\b",AocTablet:"MW0811|MW0812|MW0922|MTK8382|MW1031|MW0831|MW0821|MW0931|MW0712",MpmanTablet:"MP11 OCTA|MP10 OCTA|MPQC1114|MPQC1004|MPQC994|MPQC974|MPQC973|MPQC804|MPQC784|MPQC780|\\\\bMPG7\\\\b|MPDCG75|MPDCG71|MPDC1006|MP101DC|MPDC9000|MPDC905|MPDC706HD|MPDC706|MPDC705|MPDC110|MPDC100|MPDC99|MPDC97|MPDC88|MPDC8|MPDC77|MP709|MID701|MID711|MID170|MPDC703|MPQC1010",CelkonTablet:"CT695|CT888|CT\[\\\\s\]?910|CT7 Tab|CT9 Tab|CT3 Tab|CT2 Tab|CT1 Tab|C820|C720|\\\\bCT-1\\\\b",WolderTablet:"miTab \\\\b(DIAMOND|SPACE|BROOKLYN|NEO|FLY|MANHATTAN|FUNK|EVOLUTION|SKY|GOCAR|IRON|GENIUS|POP|MINT|EPSILON|BROADWAY|JUMP|HOP|LEGEND|NEW AGE|LINE|ADVANCE|FEEL|FOLLOW|LIKE|LINK|LIVE|THINK|FREEDOM|CHICAGO|CLEVELAND|BALTIMORE-GH|IOWA|BOSTON|SEATTLE|PHOENIX|DALLAS|IN 101|MasterChef)\\\\b",MediacomTablet:"M-MPI10C3G|M-SP10EG|M-SP10EGP|M-SP10HXAH|M-SP7HXAH|M-SP10HXBH|M-SP8HXAH|M-SP8MXA",MiTablet:"\\\\bMI PAD\\\\b|\\\\bHM NOTE 1W\\\\b",NibiruTablet:"Nibiru M1|Nibiru Jupiter One",NexoTablet:"NEXO NOVA|NEXO 10|NEXO AVIO|NEXO FREE|NEXO GO|NEXO EVO|NEXO 3G|NEXO SMART|NEXO KIDDO|NEXO MOBI",LeaderTablet:"TBLT10Q|TBLT10I|TBL-10WDKB|TBL-10WDKBO2013|TBL-W230V2|TBL-W450|TBL-W500|SV572|TBLT7I|TBA-AC7-8G|TBLT79|TBL-8W16|TBL-10W32|TBL-10WKB|TBL-W100",UbislateTablet:"UbiSlate\[\\\\s\]?7C",PocketBookTablet:"Pocketbook",KocasoTablet:"\\\\b(TB-1207)\\\\b",HisenseTablet:"\\\\b(F5281|E2371)\\\\b",Hudl:"Hudl HT7S3|Hudl 2",TelstraTablet:"T-Hub2",GenericTablet:"Android.\*\\\\b97D\\\\b|Tablet(?!.\*PC)|BNTV250A|MID-WCDMA|LogicPD Zoom2|\\\\bA7EB\\\\b|CatNova8|A1\_07|CT704|CT1002|\\\\bM721\\\\b|rk30sdk|\\\\bEVOTAB\\\\b|M758A|ET904|ALUMIUM10|Smartfren Tab|Endeavour 1010|Tablet-PC-4|Tagi Tab|\\\\bM6pro\\\\b|CT1020W|arc 10HD|\\\\bTP750\\\\b|\\\\bQTAQZ3\\\\b|WVT101|TM1088|KT107"},oss:{AndroidOS:"Android",BlackBerryOS:"blackberry|\\\\bBB10\\\\b|rim tablet os",PalmOS:"PalmOS|avantgo|blazer|elaine|hiptop|palm|plucker|xiino",SymbianOS:"Symbian|SymbOS|Series60|Series40|SYB-\[0-9\]+|\\\\bS60\\\\b",WindowsMobileOS:"Windows CE.\*(PPC|Smartphone|Mobile|\[0-9\]{3}x\[0-9\]{3})|Windows Mobile|Windows Phone \[0-9.\]+|WCE;",WindowsPhoneOS:"Windows Phone 10.0|Windows Phone 8.1|Windows Phone 8.0|Windows Phone OS|XBLWP7|ZuneWP7|Windows NT 6.\[23\]; ARM;",iOS:"\\\\biPhone.\*Mobile|\\\\biPod|\\\\biPad|AppleCoreMedia",iPadOS:"CPU OS 13",SailfishOS:"Sailfish",MeeGoOS:"MeeGo",MaemoOS:"Maemo",JavaOS:"J2ME/|\\\\bMIDP\\\\b|\\\\bCLDC\\\\b",webOS:"webOS|hpwOS",badaOS:"\\\\bBada\\\\b",BREWOS:"BREW"},uas:{Chrome:"\\\\bCrMo\\\\b|CriOS|Android.\*Chrome/\[.0-9\]\* (Mobile)?",Dolfin:"\\\\bDolfin\\\\b",Opera:"Opera.\*Mini|Opera.\*Mobi|Android.\*Opera|Mobile.\*OPR/\[0-9.\]+$|Coast/\[0-9.\]+",Skyfire:"Skyfire",Edge:"\\\\bEdgiOS\\\\b|Mobile Safari/\[.0-9\]\* Edge",IE:"IEMobile|MSIEMobile",Firefox:"fennec|firefox.\*maemo|(Mobile|Tablet).\*Firefox|Firefox.\*Mobile|FxiOS",Bolt:"bolt",TeaShark:"teashark",Blazer:"Blazer",Safari:"Version((?!\\\\bEdgiOS\\\\b).)\*Mobile.\*Safari|Safari.\*Mobile|MobileSafari",WeChat:"\\\\bMicroMessenger\\\\b",UCBrowser:"UC.\*Browser|UCWEB",baiduboxapp:"baiduboxapp",baidubrowser:"baidubrowser",DiigoBrowser:"DiigoBrowser",Mercury:"\\\\bMercury\\\\b",ObigoBrowser:"Obigo",NetFront:"NF-Browser",GenericBrowser:"NokiaBrowser|OviBrowser|OneBrowser|TwonkyBeamBrowser|SEMC.\*Browser|FlyFlow|Minimo|NetFront|Novarra-Vision|MQQBrowser|MicroMessenger",PaleMoon:"Android.\*PaleMoon|Mobile.\*PaleMoon"},props:{Mobile:"Mobile/\[VER\]",Build:"Build/\[VER\]",Version:"Version/\[VER\]",VendorID:"VendorID/\[VER\]",iPad:"iPad.\*CPU\[a-z \]+\[VER\]",iPhone:"iPhone.\*CPU\[a-z \]+\[VER\]",iPod:"iPod.\*CPU\[a-z \]+\[VER\]",Kindle:"Kindle/\[VER\]",Chrome:\["Chrome/\[VER\]","CriOS/\[VER\]","CrMo/\[VER\]"\],Coast:\["Coast/\[VER\]"\],Dolfin:"Dolfin/\[VER\]",Firefox:\["Firefox/\[VER\]","FxiOS/\[VER\]"\],Fennec:"Fennec/\[VER\]",Edge:"Edge/\[VER\]",IE:\["IEMobile/\[VER\];","IEMobile \[VER\]","MSIE \[VER\];","Trident/\[0-9.\]+;.\*rv:\[VER\]"\],NetFront:"NetFront/\[VER\]",NokiaBrowser:"NokiaBrowser/\[VER\]",Opera:\[" OPR/\[VER\]","Opera Mini/\[VER\]","Version/\[VER\]"\],"Opera Mini":"Opera Mini/\[VER\]","Opera Mobi":"Version/\[VER\]",UCBrowser:\["UCWEB\[VER\]","UC.\*Browser/\[VER\]"\],MQQBrowser:"MQQBrowser/\[VER\]",MicroMessenger:"MicroMessenger/\[VER\]",baiduboxapp:"baiduboxapp/\[VER\]",baidubrowser:"baidubrowser/\[VER\]",SamsungBrowser:"SamsungBrowser/\[VER\]",Iron:"Iron/\[VER\]",Safari:\["Version/\[VER\]","Safari/\[VER\]"\],Skyfire:"Skyfire/\[VER\]",Tizen:"Tizen/\[VER\]",Webkit:"webkit\[ /\]\[VER\]",PaleMoon:"PaleMoon/\[VER\]",SailfishBrowser:"SailfishBrowser/\[VER\]",Gecko:"Gecko/\[VER\]",Trident:"Trident/\[VER\]",Presto:"Presto/\[VER\]",Goanna:"Goanna/\[VER\]",iOS:" \\\\bi?OS\\\\b \[VER\]\[ ;\]{1}",Android:"Android \[VER\]",Sailfish:"Sailfish \[VER\]",BlackBerry:\["BlackBerry\[\\\\w\]+/\[VER\]","BlackBerry.\*Version/\[VER\]","Version/\[VER\]"\],BREW:"BREW \[VER\]",Java:"Java/\[VER\]","Windows Phone OS":\["Windows Phone OS \[VER\]","Windows Phone \[VER\]"\],"Windows Phone":"Windows Phone \[VER\]","Windows CE":"Windows CE/\[VER\]","Windows NT":"Windows NT \[VER\]",Symbian:\["SymbianOS/\[VER\]","Symbian/\[VER\]"\],webOS:\["webOS/\[VER\]","hpwOS/\[VER\];"\]},utils:{Bot:"Googlebot|facebookexternalhit|Google-AMPHTML|s~amp-validator|AdsBot-Google|Google Keyword Suggestion|Facebot|YandexBot|YandexMobileBot|bingbot|ia\_archiver|AhrefsBot|Ezooms|GSLFbot|WBSearchBot|Twitterbot|TweetmemeBot|Twikle|PaperLiBot|Wotbox|UnwindFetchor|Exabot|MJ12bot|YandexImages|TurnitinBot|Pingdom|contentkingapp|AspiegelBot",MobileBot:"Googlebot-Mobile|AdsBot-Google-Mobile|YahooSeeker/M1A1-R2D2",DesktopMode:"WPDesktop",TV:"SonyDTV|HbbTV",WebKit:"(webkit)\[ /\](\[\\\\w.\]+)",Console:"\\\\b(Nintendo|Nintendo WiiU|Nintendo 3DS|Nintendo Switch|PLAYSTATION|Xbox)\\\\b",Watch:"SM-V700"}},g.detectMobileBrowsers={fullPattern:/(android|bb\\d+|meego).+mobile|avantgo|bada\\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\\.(browser|link)|vodafone|wap|windows ce|xda|xiino/i, shortPattern:/1207|6310|6590|3gso|4thp|50\[1-6\]i|770s|802s|a wa|abac|ac(er|oo|s\\-)|ai(ko|rn)|al(av|ca|co)|amoi|an(ex|ny|yw)|aptu|ar(ch|go)|as(te|us)|attw|au(di|\\-m|r |s )|avan|be(ck|ll|nq)|bi(lb|rd)|bl(ac|az)|br(e|v)w|bumb|bw\\-(n|u)|c55\\/|capi|ccwa|cdm\\-|cell|chtm|cldc|cmd\\-|co(mp|nd)|craw|da(it|ll|ng)|dbte|dc\\-s|devi|dica|dmob|do(c|p)o|ds(12|\\-d)|el(49|ai)|em(l2|ul)|er(ic|k0)|esl8|ez(\[4-7\]0|os|wa|ze)|fetc|fly(\\-|\_)|g1 u|g560|gene|gf\\-5|g\\-mo|go(\\.w|od)|gr(ad|un)|haie|hcit|hd\\-(m|p|t)|hei\\-|hi(pt|ta)|hp( i|ip)|hs\\-c|ht(c(\\-| |\_|a|g|p|s|t)|tp)|hu(aw|tc)|i\\-(20|go|ma)|i230|iac( |\\-|\\/)|ibro|idea|ig01|ikom|im1k|inno|ipaq|iris|ja(t|v)a|jbro|jemu|jigs|kddi|keji|kgt( |\\/)|klon|kpt |kwc\\-|kyo(c|k)|le(no|xi)|lg( g|\\/(k|l|u)|50|54|\\-\[a-w\])|libw|lynx|m1\\-w|m3ga|m50\\/|ma(te|ui|xo)|mc(01|21|ca)|m\\-cr|me(rc|ri)|mi(o8|oa|ts)|mmef|mo(01|02|bi|de|do|t(\\-| |o|v)|zz)|mt(50|p1|v )|mwbp|mywa|n10\[0-2\]|n20\[2-3\]|n30(0|2)|n50(0|2|5)|n7(0(0|1)|10)|ne((c|m)\\-|on|tf|wf|wg|wt)|nok(6|i)|nzph|o2im|op(ti|wv)|oran|owg1|p800|pan(a|d|t)|pdxg|pg(13|\\-(\[1-8\]|c))|phil|pire|pl(ay|uc)|pn\\-2|po(ck|rt|se)|prox|psio|pt\\-g|qa\\-a|qc(07|12|21|32|60|\\-\[2-7\]|i\\-)|qtek|r380|r600|raks|rim9|ro(ve|zo)|s55\\/|sa(ge|ma|mm|ms|ny|va)|sc(01|h\\-|oo|p\\-)|sdk\\/|se(c(\\-|0|1)|47|mc|nd|ri)|sgh\\-|shar|sie(\\-|m)|sk\\-0|sl(45|id)|sm(al|ar|b3|it|t5)|so(ft|ny)|sp(01|h\\-|v\\-|v )|sy(01|mb)|t2(18|50)|t6(00|10|18)|ta(gt|lk)|tcl\\-|tdg\\-|tel(i|m)|tim\\-|t\\-mo|to(pl|sh)|ts(70|m\\-|m3|m5)|tx\\-9|up(\\.b|g1|si)|utst|v400|v750|veri|vi(rg|te)|vk(40|5\[0-3\]|\\-v)|vm40|voda|vulc|vx(52|53|60|61|70|80|81|83|85|98)|w3c(\\-| )|webc|whit|wi(g |nc|nw)|wmlb|wonu|x700|yas\\-|your|zeto|zte\\-/i,tabletPattern:/android|ipad|playbook|silk/i};var h,i=Object.prototype.hasOwnProperty;return g.FALLBACK\_PHONE="UnknownPhone",g.FALLBACK\_TABLET="UnknownTablet",g.FALLBACK\_MOBILE="UnknownMobile",h="isArray"in Array?Array.isArray:function(a){return"\[object Array\]"===Object.prototype.toString.call(a)},function(){var a,b,c,e,f,j,k=g.mobileDetectRules;for(a in k.props)if(i.call(k.props,a)){for(b=k.props\[a\],h(b)||(b=\[b\]),f=b.length,e=0;e<f;++e)c=b\[e\],j=c.indexOf("\[VER\]"),j>=0&&(c=c.substring(0,j)+"(\[\\\\w.\_\\\\+\]+)"+c.substring(j+5)),b\[e\]=new RegExp(c,"i");k.props\[a\]=b}d(k.oss),d(k.phones),d(k.tablets),d(k.uas),d(k.utils),k.oss0={WindowsPhoneOS:k.oss.WindowsPhoneOS,WindowsMobileOS:k.oss.WindowsMobileOS}}(),g.findMatch=function(a,b){for(var c in a)if(i.call(a,c)&&a\[c\].test(b))return c;return null},g.findMatches=function(a,b){var c=\[\];for(var d in a)i.call(a,d)&&a\[d\].test(b)&&c.push(d);return c},g.getVersionStr=function(a,b){var c,d,e,f,h=g.mobileDetectRules.props;if(i.call(h,a))for(c=h\[a\],e=c.length,d=0;d<e;++d)if(f=c\[d\].exec(b),null!==f)return f\[1\];return null},g.getVersion=function(a,b){var c=g.getVersionStr(a,b);return c?g.prepareVersionNo(c):NaN},g.prepareVersionNo=function(a){var b;return b=a.split(/\[a-z.\_ \\/\\-\]/i),1===b.length&&(a=b\[0\]),b.length>1&&(a=b\[0\]+".",b.shift(),a+=b.join("")),Number(a)},g.isMobileFallback=function(a){return g.detectMobileBrowsers.fullPattern.test(a)||g.detectMobileBrowsers.shortPattern.test(a.substr(0,4))},g.isTabletFallback=function(a){return g.detectMobileBrowsers.tabletPattern.test(a)},g.prepareDetectionCache=function(a,c,d){if(a.mobile===b){var e,h,i;return(h=g.findMatch(g.mobileDetectRules.tablets,c))?(a.mobile=a.tablet=h,void(a.phone=null)):(e=g.findMatch(g.mobileDetectRules.phones,c))?(a.mobile=a.phone=e,void(a.tablet=null)):void(g.isMobileFallback(c)?(i=f.isPhoneSized(d),i===b?(a.mobile=g.FALLBACK\_MOBILE,a.tablet=a.phone=null):i?(a.mobile=a.phone=g.FALLBACK\_PHONE,a.tablet=null):(a.mobile=a.tablet=g.FALLBACK\_TABLET,a.phone=null)):g.isTabletFallback(c)?(a.mobile=a.tablet=g.FALLBACK\_TABLET,a.phone=null):a.mobile=a.tablet=a.phone=null)}},g.mobileGrade=function(a){var b=null!==a.mobile();return a.os("iOS")&&a.version("iPad")>=4.3||a.os("iOS")&&a.version("iPhone")>=3.1||a.os("iOS")&&a.version("iPod")>=3.1||a.version("Android")>2.1&&a.is("Webkit")||a.version("Windows Phone OS")>=7||a.is("BlackBerry")&&a.version("BlackBerry")>=6||a.match("Playbook.\*Tablet")||a.version("webOS")>=1.4&&a.match("Palm|Pre|Pixi")||a.match("hp.\*TouchPad")||a.is("Firefox")&&a.version("Firefox")>=12||a.is("Chrome")&&a.is("AndroidOS")&&a.version("Android")>=4||a.is("Skyfire")&&a.version("Skyfire")>=4.1&&a.is("AndroidOS")&&a.version("Android")>=2.3||a.is("Opera")&&a.version("Opera Mobi")>11&&a.is("AndroidOS")||a.is("MeeGoOS")||a.is("Tizen")||a.is("Dolfin")&&a.version("Bada")>=2||(a.is("UC Browser")||a.is("Dolfin"))&&a.version("Android")>=2.3||a.match("Kindle Fire")||a.is("Kindle")&&a.version("Kindle")>=3||a.is("AndroidOS")&&a.is("NookTablet")||a.version("Chrome")>=11&&!b||a.version("Safari")>=5&&!b||a.version("Firefox")>=4&&!b||a.version("MSIE")>=7&&!b||a.version("Opera")>=10&&!b?"A":a.os("iOS")&&a.version("iPad")<4.3||a.os("iOS")&&a.version("iPhone")<3.1||a.os("iOS")&&a.version("iPod")<3.1||a.is("Blackberry")&&a.version("BlackBerry")>=5&&a.version("BlackBerry")<6||a.version("Opera Mini")>=5&&a.version("Opera Mini")<=6.5&&(a.version("Android")>=2.3||a.is("iOS"))||a.match("NokiaN8|NokiaC7|N97.\*Series60|Symbian/3")||a.version("Opera Mobi")>=11&&a.is("SymbianOS")?"B":(a.version("BlackBerry")<5||a.match("MSIEMobile|Windows CE.\*Mobile")||a.version("Windows Mobile")<=5.2,"C")},g.detectOS=function(a){return g.findMatch(g.mobileDetectRules.oss0,a)||g.findMatch(g.mobileDetectRules.oss,a)},g.getDeviceSmallerSide=function(){return window.screen.width<window.screen.height?window.screen.width:window.screen.height},f.prototype={constructor:f,mobile:function(){return g.prepareDetectionCache(this.\_cache,this.ua,this.maxPhoneWidth),this.\_cache.mobile},phone:function(){return g.prepareDetectionCache(this.\_cache,this.ua,this.maxPhoneWidth),this.\_cache.phone},tablet:function(){return g.prepareDetectionCache(this.\_cache,this.ua,this.maxPhoneWidth),this.\_cache.tablet},userAgent:function(){return this.\_cache.userAgent===b&&(this.\_cache.userAgent=g.findMatch(g.mobileDetectRules.uas,this.ua)),this.\_cache.userAgent},userAgents:function(){return this.\_cache.userAgents===b&&(this.\_cache.userAgents=g.findMatches(g.mobileDetectRules.uas,this.ua)),this.\_cache.userAgents},os:function(){return this.\_cache.os===b&&(this.\_cache.os=g.detectOS(this.ua)),this.\_cache.os},version:function(a){return g.getVersion(a,this.ua)},versionStr:function(a){return g.getVersionStr(a,this.ua)},is:function(b){return c(this.userAgents(),b)||a(b,this.os())||a(b,this.phone())||a(b,this.tablet())||c(g.findMatches(g.mobileDetectRules.utils,this.ua),b)},match:function(a){return a instanceof RegExp||(a=new RegExp(a,"i")),a.test(this.ua)},isPhoneSized:function(a){return f.isPhoneSized(a||this.maxPhoneWidth)},mobileGrade:function(){return this.\_cache.grade===b&&(this.\_cache.grade=g.mobileGrade(this)),this.\_cache.grade}},"undefined"!=typeof window&&window.screen?f.isPhoneSized=function(a){return a<0?b:g.getDeviceSmallerSide()<=a}:f.isPhoneSized=function(){},f.\_impl=g,f.version="1.4.5 2021-03-13",f})}(function(a){if("undefined"!=typeof module&&module.exports)return function(a){module.exports=a()};if("function"==typeof define&&define.amd)return define;if("undefined"!=typeof window)return function(a){window.MobileDetect=a()};throw new Error("unknown environment")}());var ai\_lists=!0,ai\_block\_class\_def="code-block"; jQuery(function(a){function B(c){c=c.match(aa);return null!=c&&1<c.length&&"string"===typeof c\[1\]&&0<c\[1\].length?c\[1\].toLowerCase():null}function E(c){return c.includes(":")?(c=c.split(":"),1E3\*(3600\*parseInt(c\[0\])+60\*parseInt(c\[1\])+parseInt(c\[2\]))):null}function v(c){try{var k=Date.parse(c);isNaN(k)&&(k=null)}catch(G){k=null}if(null==k&&c.includes(" ")){c=c.split(" ");try{k=Date.parse(c\[0\]),k+=E(c\[1\]),isNaN(k)&&(k=null)}catch(G){k=null}}return k}function H(){(jQuery("#ai-iab-tcf-bar").length||jQuery(".ai-list-manual").length)&& "function"==typeof \_\_tcfapi&&"function"==typeof ai\_load\_blocks&&"undefined"==typeof ai\_iab\_tcf\_callback\_installed&&(\_\_tcfapi("addEventListener",2,function(c,k){k&&"useractioncomplete"===c.eventStatus&&(ai\_tcData=c,ai\_load\_blocks(),jQuery("#ai-iab-tcf-status").text("IAB TCF 2.0 DATA LOADED"),jQuery("#ai-iab-tcf-bar").addClass("status-ok").removeClass("status-error"))}),ai\_iab\_tcf\_callback\_installed=!0)}function w(c){c=\`; ${document.cookie}\`.split(\`; ${c}=\`);if(2===c.length)return c.pop().split(";").shift()} function h(c){if(w(c)){var k=window.location.hostname;w(c)&&(document.cookie=c+"=;path=/"+(k?";domain="+k:"")+";expires=Thu, 01 Jan 1970 00:00:01 GMT");document.cookie=c+"=; Path=/; Expires=Thu, 01 Jan 1970 00:00:01 GMT;"}}Array.prototype.includes||(Array.prototype.includes=function(c){return!!~this.indexOf(c)});var aa=RegExp(":\\\\/\\\\/(.\[^/:\]+)","i");ai\_process\_lists=function(c){function k(l,e,d){if(0==l.length){if("!@!"==d)return!0;e!=d&&("true"==d.toLowerCase()?d=!0:"false"==d.toLowerCase()&&(d= !1));return e==d}if("object"!=typeof e&&"array"!=typeof e)return!1;var n=l\[0\];l=l.slice(1);if("\*"==n)for(let \[,m\]of Object.entries(e)){if(k(l,m,d))return!0}else if(n in e)return k(l,e\[n\],d);return!1}function G(l,e,d){if("object"!=typeof l||-1==e.indexOf("\["))return!1;e=e.replace(/\]| /gi,"").split("\[");return k(e,l,d)}function ba(){"function"==typeof \_\_tcfapi&&(a("#ai-iab-tcf-status").text("IAB TCF 2.0 DETECTED"),\_\_tcfapi("getTCData",2,function(l,e){e?(a("#ai-iab-tcf-bar").addClass("status-ok"),"tcloaded"== l.eventStatus||"useractioncomplete"==l.eventStatus?(ai\_tcData=l,l.gdprApplies?a("#ai-iab-tcf-status").text("IAB TCF 2.0 DATA LOADED"):jQuery("#ai-iab-tcf-status").text("IAB TCF 2.0 GDPR DOES NOT APPLY"),a("#ai-iab-tcf-bar").addClass("status-ok").removeClass("status-error"),setTimeout(function(){ai\_process\_lists()},10)):"cmpuishown"==l.eventStatus&&(ai\_cmpuishown=!0,a("#ai-iab-tcf-status").text("IAB TCF 2.0 CMP UI SHOWN"),a("#ai-iab-tcf-bar").addClass("status-ok").removeClass("status-error"))):(a("#ai-iab-tcf-status").text("IAB TCF 2.0 \_\_tcfapi getTCData failed"), a("#ai-iab-tcf-bar").removeClass("status-ok").addClass("status-error"))}))}function K(l){"function"==typeof \_\_tcfapi?("undefined"==typeof ai\_iab\_tcf\_callback\_installed&&H(),"undefined"==typeof ai\_tcData\_requested&&(ai\_tcData\_requested=!0,ba(),cookies\_need\_tcData=!0)):l&&(a("#ai-iab-tcf-bar").addClass("status-error").removeClass("status-ok"),a("#ai-iab-tcf-status").text("IAB TCF 2.0 MISSING: \_\_tcfapi function not found"))}c=null==c?a("div.ai-list-data, meta.ai-list-data"):a(c).filter(".ai-list-data"); if(c.length){c.removeClass("ai-list-data");var U=getAllUrlParams(window.location.search);if(null!=U.referrer)var y=U.referrer;else y=document.referrer,""!=y&&(y=B(y));var Q=window.navigator.userAgent,R=Q.toLowerCase(),V=navigator.language,L=V.toLowerCase();if("undefined"!==typeof MobileDetect)var W=new MobileDetect(Q);c.each(function(){var l=document.cookie.split(";");l.forEach(function(u,g){l\[g\]=u.trim()});var e=a(this).closest("div.code-block"),d=!0,n=a(this).attr("referer-list"); if("undefined"!=typeof n){n=b64d(n).split(",");var m=a(this).attr("referer-list-type"),I=!1;a.each(n,function(u,g){g=g.trim();if(""==g)return!0;if("\*"==g.charAt(0))if("\*"==g.charAt(g.length-1)){if(g=g.substr(1,g.length-2),-1!=y.indexOf(g))return I=!0,!1}else{if(g=g.substr(1),y.substr(-g.length)==g)return I=!0,!1}else if("\*"==g.charAt(g.length-1)){if(g=g.substr(0,g.length-1),0==y.indexOf(g))return I=!0,!1}else if("#"==g){if(""==y)return I=!0,!1}else if(g==y)return I=!0,!1});var p=I;switch(m){case "B":p&& (d=!1);break;case "W":p||(d=!1)}}if(d&&(n=a(this).attr("client-list"),"undefined"!=typeof n&&"undefined"!==typeof W))switch(n=b64d(n).split(","),m=a(this).attr("client-list-type"),p=!1,a.each(n,function(u,g){if(""==g.trim())return!0;u=g.split("&&");a.each(u,function(r,b){r=!0;var t=!1;for(b=b.trim();"!!"==b.substring(0,2);)r=!r,b=b.substring(2);"language:"==b.substring(0,9)&&(t=!0,b=b.substring(9).toLowerCase());var q=!1;t?"\*"==b.charAt(0)?"\*"==b.charAt(b.length-1)?(b=b.substr(1,b.length-2).toLowerCase(), -1!=L.indexOf(b)&&(q=!0)):(b=b.substr(1).toLowerCase(),L.substr(-b.length)==b&&(q=!0)):"\*"==b.charAt(b.length-1)?(b=b.substr(0,b.length-1).toLowerCase(),0==L.indexOf(b)&&(q=!0)):b==L&&(q=!0):"\*"==b.charAt(0)?"\*"==b.charAt(b.length-1)?(b=b.substr(1,b.length-2).toLowerCase(),-1!=R.indexOf(b)&&(q=!0)):(b=b.substr(1).toLowerCase(),R.substr(-b.length)==b&&(q=!0)):"\*"==b.charAt(b.length-1)?(b=b.substr(0,b.length-1).toLowerCase(),0==R.indexOf(b)&&(q=!0)):W.is(b)&&(q=!0);p=q?r:!r;if(!p)return!1});if(p)return!1}), m){case "B":p&&(d=!1);break;case "W":p||(d=!1)}var M=n=!1;for(m=1;2>=m;m++)if(d){switch(m){case 1:var f=a(this).attr("cookie-list");break;case 2:f=a(this).attr("parameter-list")}if("undefined"!=typeof f){f=b64d(f);switch(m){case 1:var A=a(this).attr("cookie-list-type");break;case 2:A=a(this).attr("parameter-list-type")}f=f.replace("tcf-gdpr","tcf-v2\[gdprApplies\]=true");f=f.replace("tcf-no-gdpr","tcf-v2\[gdprApplies\]=false");f=f.replace("tcf-google","tcf-v2\[vendor\]\[consents\]\[755\]=true && tcf-v2\[purpose\]\[consents\]\[1\]=true"); f=f.replace("tcf-no-google","!!tcf-v2\[vendor\]\[consents\]\[755\]");f=f.replace("tcf-media.net","tcf-v2\[vendor\]\[consents\]\[142\]=true && tcf-v2\[purpose\]\[consents\]\[1\]=true");f=f.replace("tcf-no-media.net","!!tcf-v2\[vendor\]\[consents\]\[142\]");f=f.replace("tcf-amazon","tcf-v2\[vendor\]\[consents\]\[793\]=true && tcf-v2\[purpose\]\[consents\]\[1\]=true");f=f.replace("tcf-no-amazon","!!tcf-v2\[vendor\]\[consents\]\[793\]");f=f.replace("tcf-ezoic","tcf-v2\[vendor\]\[consents\]\[347\]=true && tcf-v2\[purpose\]\[consents\]\[1\]=true");f=f.replace("tcf-no-ezoic", "!!tcf-v2\[vendor\]\[consents\]\[347\]");var D=f.split(","),X=\[\];l.forEach(function(u){u=u.split("=");try{var g=JSON.parse(decodeURIComponent(u\[1\]))}catch(r){g=decodeURIComponent(u\[1\])}X\[u\[0\]\]=g});p=!1;var N=a(this);a.each(D,function(u,g){u=g.split("&&");a.each(u,function(r,b){r=!0;for(b=b.trim();"!!"==b.substring(0,2);)r=!r,b=b.substring(2);var t=b,q="!@!",Y=-1!=b.indexOf("\["),Z=(0==b.indexOf("tcf-v2")||0==b.indexOf("euconsent-v2"))&&-1!=b.indexOf("\[");-1!=b.indexOf("=")&&(q=b.split("="),t=q\[0\],q=q\[1\], Y=-1!=t.indexOf("\["),Z=(0==t.indexOf("tcf-v2")||0==t.indexOf("euconsent-v2"))&&-1!=t.indexOf("\["));if(Z)a("#ai-iab-tcf-bar").show(),"object"==typeof ai\_tcData?(a("#ai-iab-tcf-bar").addClass("status-ok"),t=t.replace(/\]| /gi,"").split("\["),t.shift(),p=(t=k(t,ai\_tcData,q))?r:!r):(N.addClass("ai-list-data"),M=!0,"function"==typeof \_\_tcfapi?K(!1):"undefined"==typeof ai\_tcData\_retrying&&(ai\_tcData\_retrying=!0,setTimeout(function(){"function"==typeof \_\_tcfapi?K(!1):setTimeout(function(){"function"==typeof \_\_tcfapi? K(!1):setTimeout(function(){K(!0)},3E3)},1E3)},600)));else if(Y)p=(t=G(X,t,q))?r:!r;else{var S=!1;"!@!"==q?l.every(function(ca){return ca.split("=")\[0\]==b?(S=!0,!1):!0}):S=-1!=l.indexOf(b);p=S?r:!r}if(!p)return!1});if(p)return!1});p&&(M=!1);switch(A){case "B":p&&(d=!1);break;case "W":p||(d=!1)}}}a(this).hasClass("ai-list-manual")&&(d?(N.removeClass("ai-list-data"),N.removeClass("ai-list-manual")):(n=!0,N.addClass("ai-list-data")));if(d||!n&&!M)if(f=a(this).data("debug-info"),"undefined"!=typeof f&& (f=a("."+f),0!=f.length)){var x=f.parent();x.hasClass("ai-debug-info")&&x.remove()}x=a(this).prevAll(".ai-debug-bar.ai-debug-lists");f=""==y?"#":y;x.find(".ai-debug-name.ai-list-info").text(f).attr("title",Q+"\\n"+V);x.find(".ai-debug-name.ai-list-status").text(d?ai\_front.visible:ai\_front.hidden);f=!1;if(d&&(m=a(this).attr("scheduling-start"),A=a(this).attr("scheduling-end"),D=a(this).attr("scheduling-days"),"undefined"!=typeof m&&"undefined"!=typeof A&&"undefined"!=typeof D)){f=!0;var z=b64d(m),O= b64d(A),T=parseInt(a(this).attr("scheduling-fallback")),P=parseInt(a(this).attr("gmt"));z.includes("-")||O.includes("-")?(A=v(z)+P,m=v(O)+P):(A=E(z),m=E(O));D=b64d(D).split(",");x=a(this).attr("scheduling-type");var C=(new Date).getTime()+P,F=new Date(C),J=F.getDay();z.includes("-")||O.includes("-")||(z=(new Date(F.getFullYear(),F.getMonth(),F.getDate())).getTime()+P,C-=z,0>C&&(C+=864E5));0==J?J=6:J--;z=C>=A&&C<m&&D.includes(J.toString());switch(x){case "B":z=!z}z||(d=!1);F=F.toISOString().split(".")\[0\].replace("T", " ");x=a(this).prevAll(".ai-debug-bar.ai-debug-scheduling");x.find(".ai-debug-name.ai-scheduling-info").text(F+" "+J+" current\_time:"+Math.floor(C.toString()/1E3)+" start\_date:"+Math.floor(A/1E3).toString()+" ="+(C>=A).toString()+" end\_date:"+Math.floor(m/1E3).toString()+" =:"+(C<m).toString()+" days:"+D.toString()+" =:"+D.includes(J.toString()).toString());x.find(".ai-debug-name.ai-scheduling-status").text(d?ai\_front.visible:ai\_front.hidden);d||0==T||(x.removeClass("ai-debug-scheduling").addClass("ai-debug-fallback"), x.find(".ai-debug-name.ai-scheduling-status").text(ai\_front.fallback+" = "+T))}if(n||!d&&M)return!0;a(this).css({visibility:"",position:"",width:"",height:"","z-index":""});d?(e.css({visibility:""}),e.hasClass("ai-remove-position")&&e.css({position:""}),"undefined"!=typeof a(this).data("code")&&(d=b64d(a(this).data("code")),0!=a(this).closest("head").length?(a(this).after(d),a(this).remove()):a(this).append(d),ai\_process\_element\_lists(this))):f&&!z&&0!=T?(e.css({visibility:""}),e.hasClass("ai-remove-position")&& e.css({position:""}),a(this).next(".ai-fallback").removeClass("ai-fallback"),"undefined"!=typeof a(this).data("fallback-code")?(d=b64d(a(this).data("fallback-code")),a(this).append(d),ai\_process\_element\_lists(this)):(a(this).hide(),!e.find(".ai-debug-block").length&&e\[0\].hasAttribute("style")&&-1==e.attr("style").indexOf("height:")&&e.hide()),d=e.attr("data-ai"),"undefined"!==typeof d&&!1!==d&&(d=a(this).attr("fallback-tracking"),"undefined"!==typeof d&&!1!==d&&e.attr("data-ai-"+a(this).attr("fallback\_level"), d))):(a(this).hide(),e.length&&(e.removeAttr("data-ai").removeClass("ai-track"),e.find(".ai-debug-block").length?(e.css({visibility:""}).removeClass("ai-close"),e.hasClass("ai-remove-position")&&e.css({position:""})):e\[0\].hasAttribute("style")&&-1==e.attr("style").indexOf("height:")&&e.hide()));a(this).attr("data-code","");a(this).attr("data-fallback-code","");e.removeClass("ai-list-block")})}};a(document).ready(function(c){setTimeout(function(){ai\_process\_lists();setTimeout(function(){H();if("function"== typeof ai\_load\_blocks){jQuery(document).on("cmplzEnableScripts",k);jQuery(document).on("cmplz\_event\_marketing",k);function k(G){"cmplzEnableScripts"!=G.type&&"all"!==G.consentLevel||ai\_load\_blocks()}}},50);jQuery(".ai-debug-page-type").dblclick(function(){jQuery("#ai-iab-tcf-status").text("CONSENT COOKIES");jQuery("#ai-iab-tcf-bar").show()});jQuery("#ai-iab-tcf-bar").click(function(){h("euconsent-v2");h("\_\_lxG\_\_consent\_\_v2");h("\_\_lxG\_\_consent\_\_v2\_daisybit");h("\_\_lxG\_\_consent\_\_v2\_gdaisybit");h("CookieLawInfoConsent"); h("cookielawinfo-checkbox-advertisement");h("cookielawinfo-checkbox-analytics");h("cookielawinfo-checkbox-necessary");h("complianz\_policy\_id");h("complianz\_consent\_status");h("cmplz\_marketing");h("cmplz\_consent\_status");h("cmplz\_preferences");h("cmplz\_statistics-anonymous");h("cmplz\_choice");h("cmplz\_banner-status");h("cmplz\_functional");h("cmplz\_policy\_id");h("cmplz\_statistics");h("moove\_gdpr\_popup");h("real\_cookie\_banner-blog:1-tcf");h("real\_cookie\_banner-blog:1");jQuery("#ai-iab-tcf-status").text("CONSENT COOKIES DELETED")})}, 5)})}); function ai\_process\_element\_lists(a){setTimeout(function(){"function"==typeof ai\_process\_rotations\_in\_element&&ai\_process\_rotations\_in\_element(a);"function"==typeof ai\_process\_lists&&ai\_process\_lists(jQuery(".ai-list-data",a));"function"==typeof ai\_process\_ip\_addresses&&ai\_process\_ip\_addresses(jQuery(".ai-ip-data",a));"function"==typeof ai\_process\_filter\_hooks&&ai\_process\_filter\_hooks(jQuery(".ai-filter-check",a));"function"==typeof ai\_adb\_process\_blocks&&ai\_adb\_process\_blocks(a);"function"==typeof ai\_process\_impressions&& 1==ai\_tracking\_finished&&ai\_process\_impressions();"function"==typeof ai\_install\_click\_trackers&&1==ai\_tracking\_finished&&ai\_install\_click\_trackers();"function"==typeof ai\_install\_close\_buttons&&ai\_install\_close\_buttons(document)},5)} function getAllUrlParams(a){var B=a?a.split("?")\[1\]:window.location.search.slice(1);a={};if(B){B=B.split("#")\[0\];B=B.split("&");for(var E=0;E<B.length;E++){var v=B\[E\].split("="),H=void 0,w=v\[0\].replace(/\\\[\\d\*\\\]/,function(h){H=h.slice(1,-1);return""});v="undefined"===typeof v\[1\]?"":v\[1\];w=w.toLowerCase();v=v.toLowerCase();a\[w\]?("string"===typeof a\[w\]&&(a\[w\]=\[a\[w\]\]),"undefined"===typeof H?a\[w\].push(v):a\[w\]\[H\]=v):a\[w\]=v}}return a}; ai\_run\_719796126872 = function(){ ai\_document\_write=document.write;document.write=function(a){"interactive"==document.readyState?(console.error("document.write called after page load: ",a),"undefined"!=typeof ai\_js\_errors&&ai\_js\_errors.push(\["document.write called after page load",a,0\])):ai\_document\_write.call(document,a)}; ai\_insert\_viewport\_code ('ai-insert-5-39455075'); }; if (document.readyState === 'complete' || (document.readyState !== 'loading' && !document.documentElement.doScroll)) ai\_run\_719796126872 (); else document.addEventListener ('DOMContentLoaded', ai\_run\_719796126872); ai\_js\_code = true;} function ai\_wait\_for\_jquery(){function b(f,c){var a=document.createElement("script");a.src=f;var d=document.getElementsByTagName("head")\[0\],e=!1;a.onload=a.onreadystatechange=function(){e||this.readyState&&"loaded"!=this.readyState&&"complete"!=this.readyState||(e=!0,c&&c(),a.onload=a.onreadystatechange=null,d.removeChild(a))};d.appendChild(a)}window.jQuery&&window.jQuery.fn?ai\_run\_scripts():(ai\_jquery\_waiting\_counter++,4==ai\_jquery\_waiting\_counter&&b("https://phoenixnap.com/kb/wp-includes/js/jquery/jquery.min.js?ver=3.6.0",function(){b("https://phoenixnap.com/kb/wp-includes/js/jquery/jquery-migrate.min.js?ver=6.0", null)}),30>ai\_jquery\_waiting\_counter&&setTimeout(function(){ai\_wait\_for\_jquery()},50))}ai\_jquery\_waiting\_counter=0;ai\_wait\_for\_jquery(); window.lazyLoadOptions=\[{elements\_selector:"img\[data-lazy-src\],.rocket-lazyload",data\_src:"lazy-src",data\_srcset:"lazy-srcset",data\_sizes:"lazy-sizes",class\_loading:"lazyloading",class\_loaded:"lazyloaded",threshold:300,callback\_loaded:function(element){if(element.tagName==="IFRAME"&&element.dataset.rocketLazyload=="fitvidscompatible"){if(element.classList.contains("lazyloaded")){if(typeof window.jQuery!="undefined"){if(jQuery.fn.fitVids){jQuery(element).parent().fitVids()}}}}}},{elements\_selector:".rocket-lazyload",data\_src:"lazy-src",data\_srcset:"lazy-srcset",data\_sizes:"lazy-sizes",class\_loading:"lazyloading",class\_loaded:"lazyloaded",threshold:300,}\];window.addEventListener('LazyLoad::Initialized',function(e){var lazyLoadInstance=e.detail.instance;if(window.MutationObserver){var observer=new MutationObserver(function(mutations){var image\_count=0;var iframe\_count=0;var rocketlazy\_count=0;mutations.forEach(function(mutation){for(var i=0;i<mutation.addedNodes.length;i++){if(typeof mutation.addedNodes\[i\].getElementsByTagName!=='function'){continue} if(typeof mutation.addedNodes\[i\].getElementsByClassName!=='function'){continue} images=mutation.addedNodes\[i\].getElementsByTagName('img');is\_image=mutation.addedNodes\[i\].tagName=="IMG";iframes=mutation.addedNodes\[i\].getElementsByTagName('iframe');is\_iframe=mutation.addedNodes\[i\].tagName=="IFRAME";rocket\_lazy=mutation.addedNodes\[i\].getElementsByClassName('rocket-lazyload');image\_count+=images.length;iframe\_count+=iframes.length;rocketlazy\_count+=rocket\_lazy.length;if(is\_image){image\_count+=1} if(is\_iframe){iframe\_count+=1}}});if(image\_count>0||iframe\_count>0||rocketlazy\_count>0){lazyLoadInstance.update()}});var b=document.getElementsByTagName("body")\[0\];var config={childList:!0,subtree:!0};observer.observe(b,config)}},!1) "use strict";function wprRemoveCPCSS(){var preload\_stylesheets=document.querySelectorAll('link\[data-rocket-async="style"\]\[rel="preload"\]');if(preload\_stylesheets&&0<preload\_stylesheets.length)for(var stylesheet\_index=0;stylesheet\_index<preload\_stylesheets.length;stylesheet\_index++){var media=preload\_stylesheets\[stylesheet\_index\].getAttribute("media")||"all";if(window.matchMedia(media).matches)return void setTimeout(wprRemoveCPCSS,200)}var elem=document.getElementById("rocket-critical-css");elem&&"remove"in elem&&elem.remove()}window.addEventListener?window.addEventListener("load",wprRemoveCPCSS):window.attachEvent&&window.attachEvent("onload",wprRemoveCPCSS);