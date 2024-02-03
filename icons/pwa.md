PWA
We can buil mobile installbe applications on the web.
Though PWA do require browsers to run.


Things intrestig to look into
1. WebRTC
2. Web Assembly
3. Indexdb
4. Local Storage.

With PWA we can have 
a) Offlie access.
b) Installed Icon
c) OS Integration.
d) Performace and UX


Things to consider
a) IOS dosen't support push notifications on pWA
and also batching.
b) so when we are talking about shipping app to app store than we would need to 
add some native code to support push notifications and batching. etc.
c)As this is running on browser, if you kill the browser process then the pwa will also
get destrye.
d) Video calls are supported by platforms but  native complex camera features are not supported on ios.
 
e) firefox and opera do not support pwa installation on desktopp but they do support on mobile
f) apple watch and apple os MAcos does not upport pwa on ipad.



Three main components of a PWA
a) Web App
b) Web app manifest
c) Service Worker.

How do we know if it's a PWA
solution: Lighthouse



1st step to create an pwa

1. Make a manifest file.
one manifest for one pwa project
ideally the manifest file should be in the root folder of the pwa project

**Note: We should have somekind of fallback if, some of our properties are in manifest file is not supported.
in the meta tag in html we can have
<meta name="theme-color" content="#ffc252" media>
with this we can set content to dynamic value as well as media attribute for light and dark mode of the user ass well

landscape mode is not available on iphone so we can use a fallback concept on the 
in manifest files we should stick with the rgb and name colors.
no gradients
rgba


if you want to change the icons on desktop and ios they will not change
the user will need to re install the app.
on andriod it will change, but on other platform it will change.

start_url should be :- one and specified.
it should be the same origin as the webmanifest itself.
if we are passing this to someother extenal url then the starturl property will be completly ignored

the themeColor that we have in the manifest is actually a fallback.
it's a good idea to have the theme color in both places. The webmanifest and meta tag

    "start_url": "./?utm_source=pwa",
with this we can differentiate if our users are coming from pwa or from the website


  "display":"standalone"
if the display value if set to broser then the pwa will show as a bookmark in the app and
not as pwa
minimal-ui for display property means

ios: does not support mininal ui
so if you set that in ios it will open in the browser and not in the pwa
display : 'fullscreen" only suitable for andriod. it user the full status bar.
full screen is suitable for games and immersive experience.
Full screen is not suitable on desktop and ios


icons on the manifest are not used by saffari, 
they are used by andriod and desktop

icons on Andriod

shortcut

1) Creates a shorcut in the browser launcher
2) Browser's badge(Andriod 8+)
3) It's installed only at the home screen.
No icon in the launcher
does not appear in the applist


WebApk

Only if PWA Criteria passes
It's a full Andriod native package
It contains only app's name, icon and Url
Apk is installed silently
icons got to home screen and launcher
Google chrome with play services.
Samsung Internet on Samsung devices.

only chrome and samsung internet can actually create this webapk packages


Icons for the App manifest

Format: PNG, cOLOR SPACE sRGb

Used on Andriod and desktop OS
if There is no exact ico available it will pick the closest one.

Recmmended sizes:
 at lest: 192x192, 512 x 512
 - 384 x 384, 1024 x 1024
 depcriacted size: 72x72, 152x152
 -simpler versions: 96x96, 144 x 144
 
 
also for  limiting selecting text and icons in our pwa
we will use this css for not enabling our user to select button, text and icons.

    user-select: none;
    -webkit-user-select: none;
    
    
We can also add css specifically for the standalone mode too.

@media (display-mode: standalone)
{
    body>#toolbar {
        padding: env(safe-area-inset-top)
        env(safe-area-inset-right)
        env(safe-area-inset-bottom, 5px)
        env(safe-area-inset-left) !important;
        
    }
}

this is the css example for it.
so that anything may not get hidden on the bottom, espacially for ios,

Service Workers;

You downloaded HTML
The HTML REGISTERS A SERIVE WORKER
THE SERVICE WORKER INSTALLS SOME RESOURSEES.
THE BROWSER download resouceso on demand.
they can be served from  the SW or the server

The app can consume web services.
offline works!



A javascript file running in its own thread that will  act as a 
middleware offering a local installed web server or web proxy 
for your pwa, including resources and api calls.

A service worker is a webserver that can serve files. it is installed on the client side.
Some points regarding that:

1) Runs client-side in broswer's engine
2) Https required;
3) Installed by a web page
4) Own thread and lifecycle.
5) Acts as a network proxy or local  web server in the name of the real server.
6) Abilities to run in the background.
7) No need for user's permission.

Scope
An origin (host and port) and a path.
the service worker can be installed in the whole domain or in a subdomain.


It manages all pages within broswer and within installed app from scope.
it's insalled by any page in the scope.
after installed, it can serve all files requested from the scope.

only one service worker is allowed in one scope. 
only one service worker will be working even if mulitple instances of pwa  are open

when we create a service worker, we have the option to run the funcitonality in main ui thread or 
the service worker thread.

After some moments of activity, the thread will die off.

service worker is not the right place to put content or logic in.


Caching 
Resources:

Service worker has a local cache
We can cache all or some resources.
javascript promse: async await
prefetch on installation
Cache on request.
App Shellp pattern.


The service worker will respond for every request the pwa makes
It can serve from the cache.
It can forward the request to the network.
It can synthesize a response.
Any mixed algorithm is possible. 
We are using the service worker as a middleware.


Note*: We can cache a croos domain resource . our Service worker can cache assets from the whole web.

Cache Serving Strategies

1) Cache first
2) Network first
3) State while revalidate.

Updating Resources.

Files are saved in the client.
UPdating files in the server won't trigger any automatic change in the client

We need to define  and code and update alogorithm

It will need a process within your build system for hashing or versioning files.

Note: We can also cache api response. synthesie api responses.

When you install a app to your phone, we use a Web APk Mint server

for installation, the install dialog box appearing on andriod  this event never happens in saffari..

enterprise solution
Enterprise

 















