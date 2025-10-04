{% version "3.x" %}
> [!info]  
>
> Please note this page is a work in progress. Content is likely to change as Amelia V3 evolves and more in-depth documentation becomes available.

In addition to optimizing how Amelia converses with people, IPsoft works with customers to develop and launch Amelia projects. This page describes some of the development process and tools used.
# QA
Multiple IPsoft departments in the Cognitive and Research and Development groups collaborate to provide QA for Amelia systems. Testing includes Amelia Core UI and code, Language Packs, conversation QA, and automated end to end implementation testing.
The QA process includes a number of steps:
1.  During the full release cycle, JIRA project boards track all software development and release notes.
2.  Prior to release of new or updated software a meeting between Research and Development and the Project Management Office is called to analyze all bugs and new features, assign manual testers, and other release-related tasks.
3.  Unit and integration testing is then done by Research and Development.
4.  The new code is released into development environments.
5.  Research and Development does regression testing of software in a development environment.
6.  Conversational regression testing is done on the latest relevant conversations.
7.  InfoSec testing tests all major releases once a release is announced publicly.
8.  In parallel with Core UI and Conversational testing, Research and Development also performs manual testing
9.  Once a release passes development environment and other tests, the release is made available on the Amelia Core Releases page.
# Implementation Tooling
A variety of tools are used to design, build, launch, and maintain an Amelia instance. For more information about these and other tools, visit the implementation tools link at the bottom of this page.
**Project Management**
-   Clarizen
**Programming Languages**
-   Java
-   Groovy
**Code Editors**
-   IntelliJ
-   VisualStudio
-   Atom
**BPMN Editors**
-   Camundo
**Source Control**
-   Bitbucket
-   SourceTree
**Data Viewers/Manipulators**
-   CodeBeautify
{% /version %}
