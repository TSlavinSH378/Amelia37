# How much of the Custom UI is accessible?
We follow Web Content Accessibility Guidelines in terms of accessibility.  For developer convenience, W3 created a [checklist](https://www.w3.org/TR/2006/WD-WCAG20-20060427/appendixB.html) of success criterias  
which we used during implementation accessibility. Operating systems such as Windows, iOS, and Android come equipped with accessibility modules  
that you can easily build into your application, while the W3C's [Accessible Rich Internet Applications Suite](http://www.w3.org/WAI/intro/aria) (ARIA) defines how applications written  
in Ajax, HTML, JavaScript, and similar scripting languages should provide information on user interaction to assistive technologies.
# Testing
To check our the application for accessibility, we used [aXe](https://www.deque.com/axe/) library. It’s automated accessibility testing library which has set out on the road  
to bring accessibility testing into mainstream web development. It’s always possible to use any other tools which run all important accessibility test.  
[Web Accessibility Evaluation Tool List](https://www.w3.org/WAI/ER/tools/) contains a long list of tools which can be used for testing.
# Screen Reader
Screen readers convert digital text into synthesized speech. They empower users to hear content and navigate with the keyboard.  
The technology helps people who are blind or who have low vision to use information technology with the same level of independence and privacy as anyone else.  
Screen readers are also used by people with certain cognitive or learning disabilities, or users who simply prefer audio content over text. 
All operation systems and browsers have their own product for providing screen reading. To activate a screen reader, you have to Install needed application  
and follow their particular instructions for activation. We used *ChromeVox (*extension for Chrome) as a basic tool for testing compatibility of out application with a screen reader.  
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
The following document describes additional messages we used to be pronounced by a screen readers: [ScreenReader-messages.html](../28476444/Accessibility)
# Keyboard accessibility 
Keyboard accessibility is one of the most important aspects of web accessibility. Many users with motor disabilities rely on a keyboard.  
Blind users also typically use a keyboard for navigation. Some people have tremors which don't allow for fine muscle control.  
Others have little or no use of their hands. Some people simply do not have hands, whether due to a birth defect, an accident, or amputation.  
In addition to traditional keyboards, some users may use modified keyboards or other hardware that mimics the functionality of a keyboard.
Amelia Custom UI application provides keyboard accessibility for all element which users can interact with.  
We provide support of more popular set of key combinations used in a web application: 
-   Tab - navigate forward 
-   Shift + Tab - navigate backward
-   Enter - replacement for ‘click’ mouse event
-   Esc - close dialog, close menu, cancel some actions
-   Arrow keys - navigate between elements (links, options etc)
Before trying this out, you should be sure keyboard accessibility is turn on in your browser. To check it, try to press “Tab” key for a few times   
and see if you get a focus indicator which should look like a blur around border of an elements. If you don't see it,  
find an instruction for turning keyboard access on in your particular browser.
Accessibility.mp4
# Development aspects
## Focusable elements
All links and form elements are focusable by default and you can use "Tab" / "Shift + Tab" keys to move focus between them.    
To make some other selector be able to receive focus, 'tabIndex="0"' attribute can be added to a selector. In some cases you need to disable/enable focusability of an element.  
In this case, tabIndex value can be switched from 0 to -1 and vice versa. It's very common situation when you don't see a focus indicator.  
It's usually happens because an element doesn't have any margin and the parent selector has rule "overflow: hidden";
## Clicking elements
When you define some specific behavior for click event, be sure you define 'onKeyPress' event as well to be able to get the same behavior by pressing Enter.
## ARIA
ARIA is a set of special accessibility attributes which can be added to any markup, but is especially suited to HTML. All ARIA attributes described in [ARIA documentation](https://www.w3.org/TR/wai-aria/) as well as other attributes used for accessibility implementation.
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
## Roles
All interacting elements and important application units should be review in terms of used roles (role attribute with some value).  
All roles described in [ARIA documentation](https://www.w3.org/TR/wai-aria/) as well as other attributes used for accessibility implementation.
There is a list of roles we used in the application:
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
## Screen reader messages
In a web application, it's a common practice to add some additional information which is hidden from vision but still visible for screen readers.  
For this purpose we use \`.screen-reader-only\` class which hide this sort of information in a specific way defined with CSS.
## Blue Focus Rings
> [!warning]  
>
> The accessibility blue focus ring in the chat input area is turned off by default. To add it back, please refer to the [Add Blue Focus Ring in Chat Input section](https://docs.ipsoft.com/display/AmeliaDocsV37/Customize+UI+with+config.json#CustomizeUIwithconfig.json-AddBlueFocusRinginChatInput) on the [Customize UI with config.json](https://docs.amelia.com/display/AmeliaDocsV37/Customize+UI+with+config.json) page.
