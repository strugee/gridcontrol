gridcontrol
===========

## about ##

See [my blog post][1] to learn more about gridcontrol. Everything not in that post will be covered below.

### instances ###

Anyone can install gridcontrol on their own computer, or possibly on cloud services. These installations are called gridcontrol instances. Because anyone can run a gridcontrol instance, you can take complete
control of all the account data that you enter into gridcontrol, by either running your own installation or choosing to use an installation of someone who you trust. gridcontrol will provide a way to brand a particular
gridcontrol instance with its own name and assets (like logo, favicon, etc.)

I - Alex Jordan - will run an "official" instance of gridcontrol on my server, which will eventually be live at [gridcontrol.alexj.jumpingcrab.com][2]. This instance will be called and branded as Grid Control, and it will
run vanilla gridcontrol - that is, source will never be modified beyond branding, and it will only make available the core service brokers (those that are official and come bundled with gridcontrol). So gridcontrol is the
software that powers Grid Control, and they are two distinct concepts. Anyone can run gridcontrol, and there can be any number of gridcontrol instances, but there will probably only ever be one Grid Control.

### Service Brokers ###

Service Brokers are JavaScript files that are designed to run under node.js. In a nutshell, they must implement an API specification - the SBAPI - in order to expose the functionality of a particular service that they
interface with. In order to get gridcontrol to use a particular Service Broker, you download the JavaScript file and then drop it into a directory.

For example, if you want to make your gridcontrol instance work with Google Talk, you'd download a JS file for Google Talk, then drop it into a specific directory in your gridcontrol installation directory. If you wanted
to implement a Google Talk Service Broker, you'd write said JS file to expose part of or all of the SBAPI, and the rest of your JS file would be dedicated to interfacing with Google Talk. gridcontrol doesn't care about the
internals of how you talk to other services - it only cares if you expose a valid SBAPI.

For more information on writing Service Brokers, consult the Service Broker API section of this README.

### how to write the name ###

Grid Control is always capitalized and in two words. gridcontrol is never capitalized (even at the beginning of a sentence) and is always one word.

GridControl, Gridcontrol, gridControl, grid control, Grid control, and grid Control are all wrong - even at the beginning of a sentence.

---

## APIs ##

### Web API (WAPI) ###

The purpose of the Web API (WAPI) is to enable other applications, sites, and services to interact with gridcontrol. For example, [ifttt][4] could have a gridcontrol channel, and take the user off the grid or delete him
or her from the grid when sent a command. The WAPI will eventually also power native mobile client applications.

Websites using the WAPI should generally assume that a user has an account at Grid Control, but should provide a way to use a different URL for a custom gridcontrol instance.

When a website first asks for access to a gridcontrol instance, a verification screen will appear to the user. The user can then either deny or accept the request. If they accept the request, they have to make two choices:

 - Can the site actually delete them from the grid, or just take them off it? This question exists because deleting someone from the grid is a permanent action, and users should be able to decide whether sites are allowed
   to do permanent things.

 - Should gridcontrol perform the action immediately, or wait for confirmation from the user? Confirmation could come in the form of an email, phone call, text message, instant message, etc. Basically, gridcontrol would
   automatically contact the user and make sure they wanted the change to happen.

### Service Broker API (SBAPI) ###

Still a fluid design. So far, Service Brokers will basically expose methods to gridcontrold to perform the two gridcontrol actions, and gridcontrol will then call those actions. Not sure how Service Brokers will understand
different identities/accounts yet.

### Plugin/Extension API (EAPI) ###

The plugin system (due to land by milestone 3) will consist of two parts, heavily inspired by Firefox's plugin interface.

The first will consist of APIs (collectively the Extention API, or EAPI) built into gridcontrol to modify the functionality or looks. To install a plugin of this type, you'll drop a JS file into a certain directory. gridcontrol will run it,
modify the interface or functionality according to the API calls in the JS file, and be done.

The second will be a system in which a plugin author can specify custom content to replace part of the gridcontrol interface. Every single part of the interface will be broken up using `<div>`s, and a developer will be able
to choose to insert his or her custom HTML after a `<div>`, or totally replace the `<div>`. He or she will be able to specify custom CSS, which will always get loaded after the main gridcontrol CSS, to allow for overwriting CSS
selectors. Finally, he or she will be allowed to load custom JS files into the gridcontrol page. This type of extension will be packaged as a directory, which you'll drop into the same directory as the first plugin type to install.
The plugin author will also be allowed to make EAPI calls in this type of extenstion by way of special JS files, effectively embedding a type one extention in a type two extention.

gridcontrol will also include support for user-specific extensions, in which users will be able to upload their own extensions and gridcontrol will build custom pages for them, keeping the experience the same for all other users.

All of this basically adds up to mean that gridcontrol will have the most robust and badass extension system of all web applications.

---

## developing gridcontrol ##

### development model ###
gridcontrol follows the [GitHub flow][3] development model.

Note that in accordance with the GitHub flow, if you get stuck or want feedback, you can and should open a Pull Request, even if your code isn't ready for prime-time yet.

When developing, try to follow the roadmap and only work on the current milestone's items as best as you can. That being said, if you can't make yourself useful on the current milestone, but you can on a future one,
feel free to work on future roadmap items.

### development requirements ###

1. You must have at least rudimentary knowledge of node.js.
 - A nessesary prerequisite to this is knowledge of JavaScript.
2. You'll also obviously need a working git client and a GitHub account.
3. You'll have to understand the GitHub flow and be willing to follow it.
 - The only exception to this is if you are landing m1 roadmap items - in this case, feel free to land directly on master if you have the rights.

### roadmap ###

#### m1 ####
- nodejs HTTP server (httpd)
- nodejs service backend server (gridcontrold)
- preliminary, usable Service Broker API (SBAPI)
 - must fully support API feature detection

#### m2 ####
- SBAPI work
 - API expansions, possible redesign
 - future backwards compatibility guaranteed, except in major API revisions
  - API revisions will be announced well in advance, and both the old APIs and the new APIs will be available for use (even at the same time, so you could transition part of your codebase - even individual API calls - without
    doing the entire thing)
- preliminary, usable Web API (WAPI)
 - data liberation
- nodejs SPDY server (spdyd)
 - includes HTTPS (by specification)
 - minimal implementation, no optional features used - for example, no resource hinting
- support for multiple locales
 - not having the actual strings, just support for adding them

#### m3 ####
- WAPI work
 - API expansions, possible redesign
 - future backwards compatibility guaranteed, except in major API revisions
  - API revisions will be announced well in advance, and both the old APIs and the new APIs will be available for use (even at the same time, so you could transition part of your codebase - even individual API calls - without
    doing the entire thing)
- full SPDY implementation - all optional features used, where appropriate
- plugins system (to modify the interface and functionality)


[1]: http://ramblingsfromalex.blogspot.com/2012/06/introducing-grid-control.html
[2]: http://gridcontrol.alexj.jumpingcrab.com/
[3]: http://scottchacon.com/2011/08/31/github-flow.html
[4]: http://ifttt.com/
