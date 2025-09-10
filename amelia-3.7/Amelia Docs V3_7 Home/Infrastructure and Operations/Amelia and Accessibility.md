People with disabilities need access to the same technology as everyone else. Web accessibility ensures that people with physical and non-physical disabilities have equal access to the web.
# How much is Amelia accessible?
IPsoft follows Web Content Accessibility Guidelines in terms of accessibility.  For developer convenience, W3 created a [checklist](https://www.w3.org/TR/2006/WD-WCAG20-20060427/appendixB.html) of success criteria which IPsoft used during implementation accessibility. Operating systems such as Windows, iOS, and Android come equipped with accessibility modules that can easily be built into applications, while the W3C's [Accessible Rich Internet Applications Suite](http://www.w3.org/WAI/intro/aria) (ARIA) defines how applications written in Ajax, HTML, JavaScript, and similar scripting languages should provide information on user interaction to assistive technologies.
# Testing
To check the Amelia application for accessibility, IPsoft used [aXe](https://www.deque.com/axe/) library. It’s automated accessibility testing library which has set out on the road to bring accessibility testing into mainstream web development. It’s always possible to use any other tools which run all important accessibility test. [Web Accessibility Evaluation Tool List](https://www.w3.org/WAI/ER/tools/) contains a long list of tools which can be used for testing.
# Screen Reader
Screen readers convert digital text into synthesized speech. Users hear content and navigate with the keyboard. The technology helps people who are blind or who have low vision to use information technology with the same level of independence and privacy as anyone else. Screen readers are also used by people with certain cognitive or learning disabilities, or users who simply prefer audio content over text. 
All operation systems and browsers have their own product for providing screen reading. To activate a screen reader, you have to Install needed application and follow their particular instructions for activation. IPsoft used the ChromeVox extension for Chrome as a basic tool for testing compatibility of the Amelia application with a screen reader.  
Here the list of popular screen readers for different systems:
1.  NVDA (Windows)
2.  Serotek System Access (Windows)
3.  Apply VoiceOver (OS X)
4.  ORCA (Linux)
5.  BRLTTY (Linux)
6.  Emacspeak (Linux)
7.  WebAnywhere (All OSs, Web browsers) 
8.  Spoken Web (IE)
9.  ChromeVox (Google Chrome)
10. ChromeVis (Google Chrome)
# Keyboard accessibility 
Keyboard accessibility is one of the most important aspects of web accessibility. Many users with motor disabilities rely on a keyboard. Blind users also typically use a keyboard for navigation. Some people have tremors which don't allow for fine muscle control. Others have little or no use of their hands. Some people simply do not have hands. In addition to traditional keyboards, some users may use modified keyboards or other hardware that mimics the functionality of a keyboard.
Amelia's Custom UI application provides keyboard accessibility for all elements users can interact with. Amelia provides support of more popular key combinations used in web applications: 
-   Tab - navigate forward 
-   Shift + Tab - navigate backward
-   Enter - replacement for ‘click’ mouse event
-   Esc - close dialog, close menu, cancel some actions
-   Arrow keys - navigate between elements (links, options etc)
Before trying this out, check that keyboard accessibility is turned on in your browser. To check it, try to press “Tab” key for a few times and see if you get a focus indicator which should look like a blur around border of an elements. If a blur around the border of an element doesn't appear, find instructions to turn on keyboard access in the browser.
Your browser does not support the HTML5 video element
# Development Aspects
### Focusable elements
All Amelia links and form elements are focusable by default and "Tab" / "Shift + Tab" keys move focus between them. To make some other selector be able to receive focus, 'tabIndex="0"' attribute can be added to a selector. In some cases you need to disable or enable focusability of an element. In this case, tabIndex value can be switched from 0 to -1 and vice versa. It's very common situation to not see a focus indicator. It's usually happens because an element doesn't have any margin and the parent selector has rule "overflow: hidden";
### Clicking elements
When a specific behavior for click event is defined, define the 'onKeyPress' event as well to get the same behavior by pressing Enter.
### ARIA
ARIA is a set of special accessibility attributes which can be added to any markup, but is especially suited to HTML. All ARIA attributes are described in [ARIA documentation](https://www.w3.org/TR/wai-aria/), as well as other attributes used for accessibility implementation.
-   aria-hidden="false"
-   aria-label=""
-   aria-live="polite";  aria-live="assertive"
-   aria-atomic="true/false"
-   aria-relevant="additions"
-   aria-checked="true/false"
-   aria-selected="true/false"
-   aria-invalid="false"
-   aria-required="true"
-   aria-labelledby="loginEmailInput"
### Roles
All interacting elements and important application units should be reviewed in terms of used roles, role attribute with some value. All roles are described in [ARIA documentation](https://www.w3.org/TR/wai-aria/), as well as other attributes used for accessibility implementation.
There is a list of roles we used in Amelia:
-   role="main"
-   role="navigation"
-   role="banner"
-   role="complementary"
-   role="presentation"
-   role="searchbox"
-   role="button"
-   role="status"
-   role="form"
-   role="alert", role="alertdialog"
-   role="radiogroup", role="radio"
-   role="listbox", role="option"
-   role="combobox"
### Screen reader messages
In a web application, it's a common practice to add some additional information which is hidden from vision but still visible for screen readers. For this purpose, we use the \`.screen-reader-only\` class which hide this sort of information in a specific way defined with CSS.
## Attachments:
![](images/icons/bullet_blue.gif) [IPsoft-Amelia-Accessibility.mp4](attachments/11940489/11940490.mp4) (video/mp4)  
