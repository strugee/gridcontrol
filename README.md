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
 - The only exception to this is if you are landing v1 roadmap items - in this case, feel free to land directly on master if you have the rights.

### roadmap ###

#### v1 ####
- nodejs HTTP server (httpd)
- nodejs service backend server (gridcontrold)
- preliminary, usable Service Broker API (SBAPI)
 - must fully support API feature detection

#### v2 ####
- SBAPI work
 - API expansions, possible redesign
 - future backwards compatibility guaranteed
- nodejs SPDY server (spdyd)
 - includes HTTPS (by specification)
 - minimal implementation, no optional features used - for example, no resource hinting
 - support for multiple locales

#### v3 ####
- full SPDY implementation - all optional features used, where appropriate
- plugins system (to modify the interface and functionality)


[1]: http://ramblingsfromalex.blogspot.com/2012/06/introducing-grid-control.html
[2]: http://gridcontrol.alexj.jumpingcrab.com/
[3]: http://scottchacon.com/2011/08/31/github-flow.html
[4]: http://ifttt.com/
