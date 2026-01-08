<script lang="ts">
    import { page } from '$app/state';
    let { children } = $props();
    export const prerender = true;
</script>
<header id="eprase-header">
	<i id="burger" class="fa fa-bars w3-xlarge w3-button w3-theme burger"></i>
</header>

<nav class="navbar">
	<a href="https://eprase.nhs.uk" class="go2button" title="ePRaSE tool">Sign up now</a>
	<a href="/" aria-current={page.url.pathname === '/' } class="mynav">Home</a>
	<a href="/about" aria-current={page.url.pathname === '/about' } class="mynav">About</a>
	<a href="/using" aria-current={page.url.pathname === '/using' } class="mynav">Using ePRaSE</a>
	<a href="/results" aria-current={page.url.pathname === '/results' } class="mynav">Results</a>
	<a href="/news" aria-current={page.url.pathname === '/news' } class="mynav">News</a>
	<a href="/lab" aria-current={page.url.pathname === '/lab' } class="mynav">Learning Lab</a>
	<a href="/faq" aria-current={page.url.pathname === '/faq' } class="mynav">FAQ</a>
</nav>

<main>
    {@render children()}
</main>

<footer class="row w3-center footer">
	<div class='col'><img class='floatleft' src='/img/ncl_logo.png' alt='Newcastle University'></div>
	<div class='col'>
  		<p class="eprase-contact"><a href="mailto:nuth.eprase@nhs.net">Contact</a></p>
  	</div>
  	<div class='col floatright'><img src='/img/nhs_logo.png' alt='NHS England'></div>
</footer>

<style>
    :global(body) {margin: 0; font-family:Arial, Helvetica, sans-serif; line-height: 1.5;}
    :global(h1,h2,h3,h4,h5,h6){font-family:"Segoe UI",Arial,sans-serif;font-weight:400;margin:10px 0;}
    :global(.accordion-text) {width: 60%; margin: auto; font-size: 1.2em; line-height: 1.6; margin-bottom: 30px;}
    :global(.eprase-image) {width: 40%; float: right; margin: 0 0 10px 10px; border: 2px solid #1e2a71;}
    :global(.eprase-h1) {font-size: 2.5em; color: #1e2a71; margin-left: 5%; position:relative;animation:animateleft 0.4s}@keyframes animateleft{from{left:-300px;opacity:0} to{left:0;opacity:1}}
    :global(.eprase-h2) {font-size: 1.8em; color: #3e53cc; font-style: italic; margin-left: 15%}
    .mynav:hover, a[aria-current="true"] {color: black; background-color: #9eb4e6;}
    .row {width: 100%; display: table; text-align: center;}
    .col {display: table-cell; width: 33.33%; float: left;}
    .w3-button{border:none;display:inline-block;padding:8px 16px;vertical-align:middle;overflow:hidden;text-decoration:none;color:inherit;background-color:inherit;text-align:center;cursor:pointer;white-space:nowrap; margin-bottom: 4px;}
    .w3-button{-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}   
    .w3-button:hover {color:#000!important;background-color:#ccc!important}
    .w3-xlarge{font-size:24px!important}
    .w3-theme {color:#fff !important; background-color:#0D6D62 !important}
    .navbar {padding: 0; display:inline-block; width: 100%;color:#fff !important; background-image:linear-gradient(#3e53cc,#151E51) !important;}
    .w3-center {text-align: center!important;}
    .footer {
        padding: 16px;
        color:#fff !important; 
        background-image:linear-gradient(#bfc6ee, #3e53cc) !important;
    }
    .floatright{float:right!important;}
    .floatleft {float:left!important;}
    #burger {display: none;}
    #eprase-header {
        background-image: url(/img/banner.jpg);
        background-size: cover;
        background-position: center;
        position: relative;
        width: 100%;
        padding-top: 20%; /* aspect ratio 5:2 */
        color: navy;
    }

    .eprase-contact a:hover {
        color: #5e70d4;
    }
    .burger {position: fixed; top: 10px; left: 10px; z-index: 99;}
    .mynav {
        padding: 16px;
        width:auto;
        border:none;
        height: 100%;
        margin: 0;
        display:inline-block;
        outline:0;
        vertical-align:middle;
        overflow:hidden;
        text-decoration:none;
        color:inherit;
        background-color:inherit;
        text-align:center;
        cursor:pointer;
        white-space:nowrap;
        -webkit-touch-callout:none;
        -webkit-user-select:none;
        -khtml-user-select:none;
        -moz-user-select:none;
        -ms-user-select:none;
        user-select:none;
    }

    @media (max-width:800px){.eprase-video iframe {width: 426px; height:240px;}}
    @media (min-width:801px){.eprase-video iframe {width: 854px; height: 480px;}}
    @media (max-width:600px){
        #burger {display: block;}
        nav.w3-bar {display: none;}
        #eprase-header {padding-top: 50%;}
        :global(.accordion-text) {width: 90%;}
        :global(.eprase-image) {width: 80%; float: none; display: block; margin: 10px auto; border: 2px solid #1e2a71;}
        :global(.col) {width: 100%; display: block; float: none;}
        .floatright{float:none!important;}
    }
    .go2button {
        float: right; 
        margin: 10px; 
        background-color: #bfc6ee;
        padding: 8px;
        border-radius: 12px;
        cursor: pointer;
        text-decoration: none;
    }
    .go2button:hover {
        background-color: #5e70d4;
        color: #bfc6ee;
    }

</style>