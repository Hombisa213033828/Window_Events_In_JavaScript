# Window_Events_In_JavaScript.
 Week1
Popups and window methods. 
A popup window is one of the oldest methods to show additional document to user.
Popups exist from ancient times.
The initial idea was to show another content without closing the main window.
Popups are tricky on mobile devise, that don’t show multiple windows simultaneously.
1.	A popup is a separate window which has its own independent JavaScript environment. 
2.	It is very easy to open a popup.
3.	A popup can navigate(change URL) and send messages to the opener window.
Popup blocking.
A popup blocker is any program that prohibits a popup at some point in time.
 This may consist of multiple internet windows, or actual pop-ups caused by coding on a webpage. 
Generally, pop-ups blockers are installed to avoid pop-up ads from webpages.
Window.open
Window.open() method is used to open a new tab or window with the specified URL and name.
It supports various parameters that can be used to specify the type and URL location of the window to be opened.
Syntax:
 Window.open(url, windowName, windowFeatures)

Parameters: 
It has following parameters as mentioned above and described below:
1.	URL: It accepts URL that will be open in the new window.
2.	 If an empty string is provided then it will open a blank new tab. 
3.	WindowName: It can be used to provide the name of the window. 
4.	This is not associated with the title of the window in any manner.
5.	It can accept values like  _blank,_self,_parent.

windowFeatures:
It is used to provide features to the window that will open, e.g,  the dimension and position of the window.

A Minimalistic window
A minimalistic window is a type of window design characterized by its simplicity, functionality, and lack of unnecessary ornamentation.
It emphasizes clean lines, uncluttered surfaces, and a focus on essential elements. 
In architecture and interior design, a minimalistic window typically exhibits the following characteristics:
1.	Clean lines: Minimalistic windows feature straight, unadorned lines without intricate detailing.
2.	Simple Frames: The frames around the window are typically streamlined and unobtrusive.
3.	They may be made of materials like metal or wood, designed to blend seamlessly with the overall aesthetic.
Efficient Use of Space:
These windows are designed to make the most of available space without adding unnecessary bulk or visual clutter.
 
Window features:
o	menubar (yes/no) – shows or hides the browser menu on the new window.
o	toolbar (yes/no) – shows or hides the browser navigation bar (back, forward, reload etc) on the new window.
o	location (yes/no) – shows or hides the URL field in the new window. FF and IE don’t allow to hide it by default.
o	status (yes/no) – shows or hides the status bar. Again, most browsers force it to show.
o	resizable (yes/no) – allows to disable the resize for the new window. Not recommended.
o	scrollbars (yes/no) – allows to disable the scrollbars for the new window. Not recommended.
Accessing popup from window.
To access a popup window from the parent window in JavaScript, you can use the window.opener property. 
This property allows you to interact with the parent window from the popup window and vice versa.
A popup can be opened by the open(url, name, params) call. It returns the reference to the newly opened window. 
Browsers block open calls from the code outside of user actions. Usually a notification appears, so that a user may allow them.

A popup may access the “opener” window as well using window.opener reference. It is null for all windows except popups.
Closing a popup window.

To close a popup window in HTML, you typically need to use JavaScript, as HTML alone doesn't provide a built-in mechanism for closing popup windows. 
Usually, it's good practice to let the user close a popup window themselves, either by providing a close button or by allowing them to use the browser's built-in window controls (like the close button in the top-right corner of the window).

Scrolling and resizing.
There are methods to move/resize a window:
win.moveBy(x,y)
Move the window relative to current position x pixels to the right and y pixels down. Negative values are allowed (to move left/up).
win.moveTo(x,y)
Move the window to coordinates (x,y) on the screen.
win.resizeBy(width,height)
Resize the window by given width/height relative to the current size. Negative values are allowed.
win.resizeTo(width,height)
Resize the window to the given size.
There’s also window.onresize event.
Only popups
To prevent abuse, the browser usually blocks these methods. They only work reliably on popups that we opened, that have no additional tabs.
No minification/maximization
JavaScript has no way to minify or maximize a window. These OS-level functions are hidden from Frontend-developers.
Scrolling a window.

There’s also window.onscroll event.

Focus/Blur on a window.
Theoretically, there are window.focus() and window.blur() methods to focus/unfocus on a window.
Also there are focus/blur events that allow to focus a window and catch the moment when the visitor switches elsewhere.
In the past evil pages abused those. For instance, look at this code:
window.onblur = () => window.focus();
When a user attempts to switch out of the window (blur), it brings it back to focus. The intention is to “lock” the user within the window.
So, there are limitations that forbid the code like that. There are many limitations to protect the user from ads and evils pages. They depend on the browser.
For instance, a mobile browser usually ignores that call completely. Also focusing doesn’t work when a popup opens in a separate tab rather than a new window.

Coding popups.

A modal popup is a dialog box that appears on top of the current page and requires user interaction before continuing.
An alert box is a simple popup used to display a message to the user.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modal Popup Example</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <button id="openModal">Open Modal</button>

    <div id="modal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <p>This is a modal popup.</p>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>


Day 2.
Week 1

The "same origin policy" is a security feature implemented by web browsers. 
It's a crucial concept in web security that prevents a web page from making requests to a different domain than the one the page came from. 
This policy helps protect users from malicious scripts and potential attacks.
The origin is a globally unique identifier assigned when the Document is created.
 If a Document or image was generated from a javascript: URL. 
The origin is equal to the origin of the script of that javascript: URL.
What is the origin of a URL?
"Origin" is a combination of a scheme (also known as the protocol, for example HTTP or HTTPS), hostname, and port (if specified).
 The origin property returns the protocol, hostname and port number of the href attribute value. Note: If the port number is not specified in the URL (or if it is the scheme's default port - like 80, or 443), some browsers will not display the port number.

IN ACTION: IFRAME

An <iframe> tag hosts a separate embedded window, with its own separate document and window objects.

We can access them using properties:

iframe.contentWindow to get the window inside the <iframe>.
iframe.contentDocument to get the document inside the <iframe>, короткий аналог iframe.contentWindow.document.
When we access something inside the embedded
 window, the browser checks if the iframe has the same origin. If that’s not so then the access is denied (writing to location is an exception, it’s still permitted).

The code above shows errors for any operations except:

Getting the reference to the inner window iframe.contentWindow – that’s allowed.
Writing to location.

iframe.onload vsiframe.contentWindow.onload
The iframe.onload event (on the <iframe>tag) is essentially the same as iframe.contentWindow.onload (on the embedded window object). It triggers when the embedded window fully loads with all resources.
…But we can’t access iframe.contentWindow.onload for an iframe from another origin, so using iframe.onload.

Windows on subdomains: document.domain.

By definition, two URLs with different domains have different origins.
But if windows share the same second-level domain, for instance, john.site.com, peter.site.com, and site.com (so that their common second-level domain is site.com), we can make the browser ignore that difference, so that they can be treated as coming from the “same origin” for the purposes of cross-window communication.
To make it work, each such window should run the code:
document.domain = 'site.com';
The document. domain setter is deprecated. It undermines the security protections provided by the same origin policy, and complicates the origin model in browsers, leading to interoperability problems and security bugs.
So, by default two URLs that have different domains have different origins. But, when windows have the same second-level domain, it is possible to make the browser ignore the difference.
IFRAME: WRONG DOCUMENT PITFALL.
f the iframe is from the same origin with a possibility of accessing its document, then there exists a pitfall. It is an essential thing to know but doesn’t relate to cross-origin requests.
Setting any event handlers on it will be ignored. The right document is where iframe.onload occurs. However, it occurs only when the total iframe with all the resources is loaded.
Collection: windows iframe

An iframe may have other iframes inside. The corresponding window objects form a hierarchy.
Navigation links are:
window.frames – the collection of “children” windows (for nested frames).
window.parent – the reference to the “parent” (outer) window.
window.top – the reference to the topmost parent window.



The “SANDBOX” IFRAME ATTRIBUTE.

The sandbox attribute allows for the exclusion of certain actions inside an <iframe> in order to prevent it from executing untrusted code. It “sandboxes” the iframe by treating it as coming from another origin and/or applying other limitations.
There’s a “default set” of restrictions applied for <iframe sandbox src="...">. But it can be relaxed if we provide a space-separated list of restrictions that should not be applied as a value of the attribute, like this: <iframe sandbox="allow-forms allow-popups">.
In other words, an empty "sandbox" attribute puts the strictest limitations possible, but we can put a space-delimited list of those that we want to lift.
Here’s a list of limitations:
allow-same-origin
By default "sandbox" forces the “different origin” policy for the iframe. In other words, it makes the browser to treat the iframe as coming from another origin, even if its src points to the same site. With all implied restrictions for scripts. This option removes that feature.
allow-top-navigation
Allows the iframe to change parent.location.
allow-forms
Allows to submit forms from iframe.
allow-scripts
Allows to run scripts from the iframe.
allow-popups
Allows to window.open popups from the iframe
You can access the manual for more.

CROSS WINDOW MESSAGING.

The postMessage interface allows windows to talk to each other no matter which origin they are from.

So, it’s a way around the “Same Origin” policy. It allows a window from john-smith.com to talk to gmail.comand exchange information, but only if they both agree and call corresponding JavaScript functions. That makes it safe for users.

The interface has two parts.

postMessage
The window that wants to send a message calls postMessage method of the receiving window. 
In other words, if we want to send the message to win, we should call win.postMessage(data, targetOrigin).

Arguments:

data
The data to send. Can be any object, the data is cloned using the “structured cloning algorithm”.
IE supports only strings, so we should JSON.stringify complex objects to support that browser.

targetOrigin
Specifies the origin for the target window, so that only a window from the given origin will get the message.

The targetOrigin is a safety measure. Remember, if the target window comes from another origin, we can’t read it’s location in the sender window.
So we can’t be sure which site is open in the intended window right now: the user could navigate away, and the sender window has no idea about it.

Specifying targetOrigin ensures that the window only receives the data if it’s still at the right site. Important when the data is sensitive.


DAY3 WEEK1

Clickjacking.

Clickjacking, also known as UI redress attack or user-interface redress attack, is a malicious technique used by attackers to trick users into interacting with web content unintentionally or without their knowledge. 
It involves overlaying or embedding a legitimate website or web application with a deceptive element.

Here's how it works:

Creating a Deceptive Layer: The attacker creates a transparent or invisible layer on top of a legitimate website or web application.
This layer can contain malicious elements, such as buttons, forms, or links.
User Interaction: When the user interacts with the visible elements on the page, they are actually interacting with the deceptive layer, not the legitimate content underneath.
Hidden Actions: The attacker can then perform actions on the user's behalf, potentially leading to unintended consequences like making unauthorized purchases, changing settings, or posting content without the user's consent.

How to Prevent Clickjacking:

X-Frame-Options Header: Websites can use the X-Frame-Options HTTP header to indicate whether a browser should be allowed to render a page in a frame or iframe. 
Setting it to DENY or SAMEORIGIN can help prevent clickjacking.
Frame-Busting Scripts: Developers can include scripts in their web pages that prevent the page from being loaded within an iframe.
Old school defenes.
The oldest defense is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”).
That looks like this:
if (top != window) {
  top.location = window.location;
}
That is: if the window finds out that it’s not on top, then it automatically makes itself the top.
This is not a reliable defense, because there are many ways to hack around it. Let’s cover a few.
Blocking top-navigation
We can block the transition caused by changing top.location in beforeunload event handler.
The top page (enclosing one, belonging to the hacker) sets a preventing handler to it, like this:
window.onbeforeunload = function() {
  return false;
};
When the iframe tries to change top.location, the visitor gets a message asking them whether they want to leave.
In most cases the visitor would answer negatively because they don’t know about the iframe – all they can see is the top page, there’s no reason to leave. So top.location won’t change!
Sandbox attribute
One of the things restricted by the sandbox attribute is navigation. A sandboxed iframe may not change top.location.
So we can add the iframe with sandbox="allow-scripts allow-forms". That would relax the restrictions, permitting scripts and forms. But we omit allow-top-navigation so that changing top.location is forbidden.
Here’s the code:
<iframe sandbox="allow-scripts allow-forms" src="facebook.html"></iframe>


X-FRAME-Options

The server-side header X-Frame-Options can permit or forbid displaying the page inside a frame.
It must be sent exactly as HTTP-header: the browser will ignore it if found in HTML <meta> tag. So, <meta http-equiv="X-Frame-Options"...> won’t do anything.
The header may have 3 values:
1. DENY
    Never ever show the page inside a frame.
2. SAMEORIGIN
    Allow inside a frame if the parent document comes from the same origin.
3. ALLOW-FROM domain
   Allow inside a frame if the parent document is from the given domain.
   
For instance, Twitter uses X-Frame-Options: SAMEORIGIN.
Samesite cookie Atribute
The samesite cookie attribute can also prevent clickjacking attacks.
A cookie with such attribute is only sent to a website if it’s opened directly, not via a frame, or otherwise.
More information can be accessed using this link Cookies, document.cookie.
If the site, such as Facebook, had samesite attribute on its authentication cookie, like this:
Set-Cookie: authorization=secret; samesite
Then such cookie wouldn’t be sent when Facebook is open in iframe from another site. So the attack would fail.
The samesite cookie attribute will not have an effect when cookies are not used.
 This may allow other websites to easily show our public, unauthenticated pages in iframes.
