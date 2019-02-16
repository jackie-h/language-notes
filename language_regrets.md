

# Node.js - 10 regrets - Ryan Dahl, creator of Node - 2018
https://tinyclouds.org/jsconf2018.pdf
https://www.youtube.com/watch?v=M3BM9TB-8yA
Javascript still the best dynamic language
Regrets:
1) Should have stuck with Promises - better async
2) Security - V8/web-browser secure, but node allowed things to be bound to everything - any system call. Sandboxing
3) Build System - GYP bindings, terrible, CHrome used to use it then abandoned it
4) Package - package.json - https://youtu.be/M3BM9TB-8yA?t=639. 
Need package.json to know which version, need a lot of systems NPM.
Introduced the idea of modules being files in a directory - tied to filesystem - not good
Resolving module names is now wildly complex - regrettable
Regret require() without the .js - you now need to probe the filesystem for unnecessary stuff
5) Index.js - unnecessary, cute - don't do it




# Deno - a secure typescript runtime
1) Utilize the fact that javascript is a secure sandbox - should run without network IO or file write access by default
2) Do not allow arbitrary native functions to be bound in - all should be message passing - protobuf based, 
Exactly two native functions send and recv - 
3) Modules - simple - just specify the URL or relative path, will download the files the first time - constantly reproducable
4) Use typescript - typescript allows code to grow from quick hacks to large typed systems. 
Should use V8 snapshots to optimize the compiler faster. 
5) Ship a single executable - download and run it easily, minimal linkage - use Parcel - single bundled Parcel file. 
Just use Http from underlying lib - Go/Rust/C - just use good native code
6) Die immediately if promises fail
7) Keep browser compatibility



