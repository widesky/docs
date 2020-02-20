---
title: "Interactive view"
linkTitle: "Interactive view"
weight: 4
type: docs
title_disable: true
lastmod_disable: true
toc_disable: true
breadcrumb_disable: true
md_nowrap: true

description: Representaion of the WideSky GraphQL API as an interactive graph
---

<html>
<head>
    <style>
        body {
            margin: 0;
            height: 100vh;
            overflow: auto;
        }
        #voyager {
            height: 85vh;
        }
        #mobile-warning {
      		display: none;
    	}
    	#mobile-warning.hidden {
      		display: none;
    	}
    	#mobile-warning small {
        	font-size: 1em;
      	}
      	#mobile-warning a {
        	display: block;
        	text-decoration: none;
        	margin: 1em 0;
        	font-weight: bold;
        	font-size: 1.4em;
        	color: #42a0dd;
      	}
      	@media screen and (max-width: 782px) {
	      #mobile-warning {
	        display: block;
	        position: absolute;
	        left: 0;
	        right: 0;
	        top: 0;
	        bottom: 0;
	        background: rgba(255, 255, 255, 0.9);
	        color: #0b2840;
	        z-index: 100;
	        padding: 20px;
	        text-align: center;
	        display: flex;
	        flex-direction: column;
	        justify-content: center;
	      }
	     }
    </style>
    <script src="https://cdn.jsdelivr.net/es6-promise/4.0.5/es6-promise.auto.min.js"></script>
    <script src="https://cdn.jsdelivr.net/fetch/0.9.0/fetch.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/react@16/umd/react.production.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/react-dom@16/umd/react-dom.production.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/graphql-voyager/dist/voyager.css" />
    <script src="https://cdn.jsdelivr.net/npm/graphql-voyager/dist/voyager.min.js"></script>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js">
    </script>
</head>
<body>
  <div style="border: 1px solid gray;">
    <div id="voyager">Loading...</div>
    <script>
        function introspectionProvider(introspectionQuery) {
            return $.getJSON('../widesky-graphql-introspection.json', function(responseBody) {
                return responseBody;
            });
        }
        var options =
        GraphQLVoyager.init(document.getElementById('voyager'), {
            introspection: introspectionProvider,
            hideSettings: true
        });
    </script>
      <div id="mobile-warning">
    <h1> Best served on bigger screen sizes </h1>
    <small> This tool presents complex graphs. Use it on bigger screen size for better experience </small>
    <a id="skip_warning" href="#"> GOT IT </a>
  </div>
  <script>
    var skipBtn = document.getElementById('skip_warning');
    var warning = document.getElementById('mobile-warning');
    if (document.cookie.indexOf('skip_mobile_warning1=true') > -1) {
      warning.classList.add('hidden');
    } else {
      var handler = function() {
        warning.classList.add('hidden');
        document.cookie = "skip_mobile_warning=true; expires=Fri, 31 Dec 9999 23:59:59 GMT";
      }
      skipBtn.addEventListener('touchstart', handler, false);
      skipBtn.addEventListener('click', handler, false);
    }
  </script>
</div>
</body>
</html>
