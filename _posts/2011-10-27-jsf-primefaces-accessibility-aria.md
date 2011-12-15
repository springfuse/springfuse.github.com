---
layout: english
title: Generate Accessible Rich Internet Application using JSF2 and PrimeFaces
comments: true
---

# Generate Accessible Rich Internet Application using JSF2 and PrimeFaces

We are trying to make the web applications generated by SpringFuse as accessible as possible.

## Online code checker
Our first goal was to pass online code checkers such as <a href="http://achecker.ca/">achecker</a>. 

All the generated pages pass the  WCAG 2.0 (Level AAA) with <strong>0 known problems</strong> and <strong>0 likely problems</strong>.

<a href="/images/blog/2011-10-27/achecker.png" class="screen" title="achecker result" rel="group"><img src="/images/blog/2011-10-27/achecker-min.png" /></a>

Achieving it is not really complicated, the key is to use standard HTML components. 

Hopefully, PrimeFaces, the JSF 2 component library that we use is pretty clean in that respect.

## keyboard

Our next focus was to unplug the mouse to ensure that the generated application is entirely usable with the keyboad.

The result is pretty good with all major browsers except with IE8 which randomly select the default submit button when the user presses enter.

If you have any hints on how we could fix it, please drop us a line.
(Note: SpringFuse v. 3.0.66 resolves this issue).

## Screen readers and Aria

Then we started to leverage ARIA and specially ARIA live region.

For the screencast, we use Mac OSX Lion, which includes a new version of VoiceOver (a screen reader) with a nice French voice (sorry for the accent :-)

The generated app uses live regions for two main purposes:

* to announce the number of items found on each search pages [<a href="/images/blog/2011-10-27/search-aria-live-region-voiceover.png" class="screen" title="achecker result" rel="group">photo</a>
 | <a href="http://www.facebook.com/photo.php?v=10150355167495905&set=vb.307765762572284&type=2&theater" target="_jaxio_on_fb" >screencast</a>]
* to announce the error detected after a form submission [<a href="/images/blog/2011-10-27/form-error-aria-live-region-voiceover.png" class="screen" title="achecker result" rel="group">photo</a>
 | <a href="http://www.facebook.com/photo.php?v=10150355172465905&set=vb.307765762572284&type=2&theater" target="_jaxio_on_fb">screencast</a>]


Issue with numbers:

* You probably noticed that it does not read 2 digits numbers properly. When it encounters '48', instead of saying 'quarante-huit' (forty eight), it says 'quatre' (four) then 'huit' (eight). If you know how to fix that, we are interested. 


## More tests...

We encourage you to <a href="http://www.springfuse.com/">generate a webapp</a> and try it for yourself.
Your feedbacks, specially test results using screen readers would be greatly appreciated.

## Resources

* <a href="http://www.w3.org/TR/WCAG20/">Web Content Accessibility Guidelines (WCAG) 2.0</a>
* <a href="http://www.w3.org/WAI/intro/aria">ARIA Overview</a>
* <a href="http://achecker.ca">Web Accessibility Checker</a>
* <a href="http://http://www.primefaces.org/">Primefaces components library</a>