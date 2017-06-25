<html lang="en"><head>
<title>SBCL 1.3.18 User Manual</title>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta name="description" content="SBCL 1.3.18 User Manual">
<meta name="generator" content="makeinfo 4.13">
<link title="Top" rel="top" href="#Top">
<link href="http://www.gnu.org/software/texinfo/" rel="generator-home" title="Texinfo Homepage">
<!--

     This manual is part of the SBCL software system. See the `README'
     file for more information.

     This manual is largely derived from the manual for the CMUCL
     system, which was produced at Carnegie Mellon University and later
     released into the public domain. This manual is in the public
     domain and is provided with absolutely no warranty. See the
     `COPYING' and `CREDITS' files for more information.
   -->
<meta http-equiv="Content-Style-Type" content="text/css">
<style type="text/css"><!--
  pre.display { font-family:inherit }
  pre.format  { font-family:inherit }
  pre.smalldisplay { font-family:inherit; font-size:smaller }
  pre.smallformat  { font-family:inherit; font-size:smaller }
  pre.smallexample { font-size:smaller }
  pre.smalllisp    { font-size:smaller }
  span.sc    { font-variant:small-caps }
  span.roman { font-family:serif; font-weight:normal; } 
  span.sansserif { font-family:sans-serif; font-weight:normal; } 
.node { visibility:hidden; height: 0px; }
  .menu { visibility:hidden; height: 0px; }
  .chapter { background-color:#d0e4fe; }
  .section { background-color:#d0e4fe; }
  .subsection { background-color:#d0e4fe; }
  .settitle { background-color:#d0e4fe; }
  .contents { border: 2px solid black;
              margin: 1cm 1cm 1cm 1cm; 
              padding-left: 3mm; }
  body { padding-left: 3mm; }--></style>
</head>
<body>
<h1 class="settitle">SBCL 1.3.18 User Manual</h1>
   <div class="contents">
<h2>Table of Contents</h2>
<ul>
<li><a name="toc_Top" href="#Top">sbcl</a>
</li><li><a name="toc_Getting-Support-and-Reporting-Bugs" href="#Getting-Support-and-Reporting-Bugs">1 Getting Support and Reporting Bugs</a>
<ul>
<li><a href="#Volunteer-Support">1.1 Volunteer Support</a>
</li><li><a href="#Commercial-Support">1.2 Commercial Support</a>
</li><li><a href="#Reporting-Bugs">1.3 Reporting Bugs</a>
<ul>
<li><a href="#Reporting-Bugs">1.3.1 How to Report Bugs Effectively</a>
</li><li><a href="#Reporting-Bugs">1.3.2 Signal Related Bugs</a>
</li></ul>
</li></ul>
</li><li><a name="toc_Introduction" href="#Introduction">2 Introduction</a>
<ul>
<li><a href="#ANSI-Conformance">2.1 ANSI Conformance</a>
</li><li><a href="#Extensions">2.2 Extensions</a>
</li><li><a href="#Idiosyncrasies">2.3 Idiosyncrasies</a>
<ul>
<li><a href="#Declarations">2.3.1 Declarations</a>
</li><li><a href="#FASL-Format">2.3.2 FASL Format</a>
</li><li><a href="#Compiler_002donly-Implementation">2.3.3 Compiler-only Implementation</a>
</li><li><a href="#Defining-Constants">2.3.4 Defining Constants</a>
</li><li><a href="#Style-Warnings">2.3.5 Style Warnings</a>
</li></ul>
</li><li><a href="#Development-Tools">2.4 Development Tools</a>
<ul>
<li><a href="#Editor-Integration">2.4.1 Editor Integration</a>
</li><li><a href="#Language-Reference">2.4.2 Language Reference</a>
</li><li><a href="#Generating-Executables">2.4.3 Generating Executables</a>
</li></ul>
</li><li><a href="#More-SBCL-Information">2.5 More SBCL Information</a>
<ul>
<li><a href="#SBCL-Homepage">2.5.1 SBCL Homepage</a>
</li><li><a href="#Online-Documentation">2.5.2 Online Documentation</a>
</li><li><a href="#Additional-Documentation-Files">2.5.3 Additional Documentation Files</a>
</li><li><a href="#Internals-Documentation">2.5.4 Internals Documentation</a>
</li></ul>
</li><li><a href="#More-Common-Lisp-Information">2.6 More Common Lisp Information</a>
<ul>
<li><a href="#Internet-Community">2.6.1 Internet Community</a>
</li><li><a href="#Third_002dparty-Libraries">2.6.2 Third-party Libraries</a>
</li><li><a href="#Common-Lisp-Books">2.6.3 Common Lisp Books</a>
</li></ul>
</li><li><a href="#History-and-Implementation-of-SBCL">2.7 History and Implementation of SBCL</a>
</li></ul>
</li><li><a name="toc_Starting-and-Stopping" href="#Starting-and-Stopping">3 Starting and Stopping</a>
<ul>
<li><a href="#Starting-SBCL">3.1 Starting SBCL</a>
<ul>
<li><a href="#Running-from-Shell">3.1.1 From Shell to Lisp</a>
</li><li><a href="#Running-from-Emacs">3.1.2 Running from Emacs</a>
</li><li><a href="#Shebang-Scripts">3.1.3 Shebang Scripts</a>
</li></ul>
</li><li><a href="#Stopping-SBCL">3.2 Stopping SBCL</a>
<ul>
<li><a href="#Exit">3.2.1 Exit</a>
</li><li><a href="#End-of-File">3.2.2 End of File</a>
</li><li><a href="#Saving-a-Core-Image">3.2.3 Saving a Core Image</a>
</li><li><a href="#Exit-on-Errors">3.2.4 Exit on Errors</a>
</li></ul>
</li><li><a href="#Command-Line-Options">3.3 Command Line Options</a>
<ul>
<li><a href="#Runtime-Options">3.3.1 Runtime Options</a>
</li><li><a href="#Toplevel-Options">3.3.2 Toplevel Options</a>
</li></ul>
</li><li><a href="#Initialization-Files">3.4 Initialization Files</a>
</li><li><a href="#Initialization-and-Exit-Hooks">3.5 Initialization and Exit Hooks</a>
</li></ul>
</li><li><a name="toc_Compiler" href="#Compiler">4 Compiler</a>
<ul>
<li><a href="#Diagnostic-Messages">4.1 Diagnostic Messages</a>
<ul>
<li><a href="#Controlling-Verbosity">4.1.1 Controlling Verbosity</a>
</li><li><a href="#Diagnostic-Severity">4.1.2 Diagnostic Severity</a>
</li><li><a href="#Understanding-Compiler-Diagnostics">4.1.3 Understanding Compile Diagnostics</a>
<ul>
<li><a href="#The-Parts-of-a-Compiler-Diagnostic">4.1.3.1 The Parts of a Compiler Diagnostic</a>
</li><li><a href="#The-Original-and-Actual-Source">4.1.3.2 The Original and Actual Source</a>
</li><li><a href="#The-Processing-Path">4.1.3.3 The Processing Path</a>
</li></ul>
</li></ul>
</li><li><a href="#Handling-of-Types">4.2 Handling of Types</a>
<ul>
<li><a href="#Declarations-as-Assertions">4.2.1 Declarations as Assertions</a>
</li><li><a href="#Precise-Type-Checking">4.2.2 Precise Type Checking</a>
</li><li><a href="#Getting-Existing-Programs-to-Run">4.2.3 Getting Existing Programs to Run</a>
</li><li><a href="#Implementation-Limitations">4.2.4 Implementation Limitations</a>
</li></ul>
</li><li><a href="#Compiler-Policy">4.3 Compiler Policy</a>
</li><li><a href="#Compiler-Errors">4.4 Compiler Errors</a>
<ul>
<li><a href="#Type-Errors-at-Compile-Time">4.4.1 Type Errors at Compile Time</a>
</li><li><a href="#Errors-During-Macroexpansion">4.4.2 Errors During Macroexpansion</a>
</li><li><a href="#Read-Errors">4.4.3 Read Errors</a>
</li></ul>
</li><li><a href="#Open-Coding-and-Inline-Expansion">4.5 Open Coding and Inline Expansion</a>
</li><li><a href="#Interpreter">4.6 Interpreter</a>
</li></ul>
</li><li><a name="toc_Debugger" href="#Debugger">5 Debugger</a>
<ul>
<li><a href="#Debugger-Entry">5.1 Debugger Entry</a>
<ul>
<li><a href="#Debugger-Banner">5.1.1 Debugger Banner</a>
</li><li><a href="#Debugger-Invocation">5.1.2 Debugger Invocation</a>
</li></ul>
</li><li><a href="#Debugger-Command-Loop">5.2 Debugger Command Loop</a>
</li><li><a href="#Stack-Frames">5.3 Stack Frames</a>
<ul>
<li><a href="#Stack-Motion">5.3.1 Stack Motion</a>
</li><li><a href="#How-Arguments-are-Printed">5.3.2 How Arguments are Printed</a>
</li><li><a href="#Function-Names">5.3.3 Function Names</a>
<ul>
<li><a href="#Entry-Point-Details">5.3.3.1 Entry Point Details</a>
</li></ul>
</li><li><a href="#Debug-Tail-Recursion">5.3.4 Debug Tail Recursion</a>
</li><li><a href="#Unknown-Locations-and-Interrupts">5.3.5 Unknown Locations and Interrupts</a>
</li></ul>
</li><li><a href="#Variable-Access">5.4 Variable Access</a>
<ul>
<li><a href="#Variable-Value-Availability">5.4.1 Variable Value Availability</a>
</li><li><a href="#Note-On-Lexical-Variable-Access">5.4.2 Note On Lexical Variable Access</a>
</li></ul>
</li><li><a href="#Source-Location-Printing">5.5 Source Location Printing</a>
<ul>
<li><a href="#How-the-Source-is-Found">5.5.1 How the Source is Found</a>
</li><li><a href="#Source-Location-Availability">5.5.2 Source Location Availability</a>
</li></ul>
</li><li><a href="#Debugger-Policy-Control">5.6 Debugger Policy Control</a>
</li><li><a href="#Exiting-Commands">5.7 Exiting Commands</a>
</li><li><a href="#Information-Commands">5.8 Information Commands</a>
</li><li><a href="#Function-Tracing">5.9 Function Tracing</a>
</li><li><a href="#Single-Stepping">5.10 Single Stepping</a>
</li><li><a href="#Enabling-and-Disabling-the-Debugger">5.11 Enabling and Disabling the Debugger</a>
</li></ul>
</li><li><a name="toc_Efficiency" href="#Efficiency">6 Efficiency</a>
<ul>
<li><a href="#Slot-access">6.1 Slot access</a>
<ul>
<li><a href="#Slot-access">6.1.1 Structure object slot access</a>
</li><li><a href="#Slot-access">6.1.2 Standard object slot access</a>
</li></ul>
</li><li><a href="#Dynamic_002dextent-allocation">6.2 Dynamic-extent allocation</a>
</li><li><a href="#Modular-arithmetic">6.3 Modular arithmetic</a>
</li><li><a href="#Global-and-Always_002dBound-variables">6.4 Global and Always-Bound variables</a>
</li><li><a href="#Miscellaneous-Efficiency-Issues">6.5 Miscellaneous Efficiency Issues</a>
</li></ul>
</li><li><a name="toc_Beyond-the-ANSI-Standard" href="#Beyond-the-ANSI-Standard">7 Beyond the ANSI Standard</a>
<ul>
<li><a href="#Reader-Extensions">7.1 Reader Extensions</a>
</li><li><a href="#Package_002dLocal-Nicknames">7.2 Package-Local Nicknames</a>
</li><li><a href="#Package-Variance">7.3 Package Variance</a>
</li><li><a href="#Garbage-Collection">7.4 Garbage Collection</a>
<ul>
<li><a href="#Garbage-Collection">7.4.1 Finalization</a>
</li><li><a href="#Garbage-Collection">7.4.2 Weak Pointers</a>
</li><li><a href="#Garbage-Collection">7.4.3 Introspection and Tuning</a>
</li></ul>
</li><li><a href="#Metaobject-Protocol">7.5 Metaobject Protocol</a>
<ul>
<li><a href="#Metaobject-Protocol">7.5.1 AMOP Compatibility of Metaobject Protocol</a>
</li><li><a href="#Metaobject-Protocol">7.5.2 Metaobject Protocol Extensions</a>
</li></ul>
</li><li><a href="#Extensible-Sequences">7.6 Extensible Sequences</a>
<ul>
<li><a href="#Iterator-Protocol">7.6.1 Iterator Protocol</a>
</li><li><a href="#Simple-Iterator-Protocol">7.6.2 Simple Iterator Protocol</a>
</li></ul>
</li><li><a href="#Support-For-Unix">7.7 Support For Unix</a>
<ul>
<li><a href="#Command_002dline-arguments">7.7.1 Command-line arguments</a>
</li><li><a href="#Querying-the-process-environment">7.7.2 Querying the process environment</a>
</li><li><a href="#Running-external-programs">7.7.3 Running external programs</a>
</li></ul>
</li><li><a href="#Unicode-Support">7.8 Unicode Support</a>
<ul>
<li><a href="#Unicode-Support">7.8.1 Unicode property access</a>
</li><li><a href="#Unicode-Support">7.8.2 String operations</a>
</li><li><a href="#Unicode-Support">7.8.3 Breaking strings</a>
</li></ul>
</li><li><a href="#Customization-Hooks-for-Users">7.9 Customization Hooks for Users</a>
</li><li><a href="#Tools-To-Help-Developers">7.10 Tools To Help Developers</a>
</li><li><a href="#Resolution-of-Name-Conflicts">7.11 Resolution of Name Conflicts</a>
</li><li><a href="#Hash-Table-Extensions">7.12 Hash Table Extensions</a>
</li><li><a href="#Random-Number-Generation">7.13 Random Number Generation</a>
</li><li><a href="#Miscellaneous-Extensions">7.14 Miscellaneous Extensions</a>
</li><li><a href="#Stale-Extensions">7.15 Stale Extensions</a>
</li><li><a href="#Efficiency-Hacks">7.16 Efficiency Hacks</a>
</li></ul>
</li><li><a name="toc_Foreign-Function-Interface" href="#Foreign-Function-Interface">8 Foreign Function Interface</a>
<ul>
<li><a href="#Introduction-to-the-Foreign-Function-Interface">8.1 Introduction to the Foreign Function Interface</a>
</li><li><a href="#Foreign-Types">8.2 Foreign Types</a>
<ul>
<li><a href="#Defining-Foreign-Types">8.2.1 Defining Foreign Types</a>
</li><li><a href="#Foreign-Types-and-Lisp-Types">8.2.2 Foreign Types and Lisp Types</a>
</li><li><a href="#Foreign-Type-Specifiers">8.2.3 Foreign Type Specifiers</a>
</li></ul>
</li><li><a href="#Operations-On-Foreign-Values">8.3 Operations On Foreign Values</a>
<ul>
<li><a href="#Accessing-Foreign-Values">8.3.1 Accessing Foreign Values</a>
<ul>
<li><a href="#Accessing-Foreign-Values">8.3.1.1 Untyped memory</a>
</li></ul>
</li><li><a href="#Coercing-Foreign-Values">8.3.2 Coercing Foreign Values</a>
</li><li><a href="#Foreign-Dynamic-Allocation">8.3.3 Foreign Dynamic Allocation</a>
</li></ul>
</li><li><a href="#Foreign-Variables">8.4 Foreign Variables</a>
<ul>
<li><a href="#Local-Foreign-Variables">8.4.1 Local Foreign Variables</a>
</li><li><a href="#External-Foreign-Variables">8.4.2 External Foreign Variables</a>
</li></ul>
</li><li><a href="#Foreign-Data-Structure-Examples">8.5 Foreign Data Structure Examples</a>
</li><li><a href="#Loading-Shared-Object-Files">8.6 Loading Shared Object Files</a>
</li><li><a href="#Foreign-Function-Calls">8.7 Foreign Function Calls</a>
<ul>
<li><a href="#The-alien_002dfuncall-Primitive">8.7.1 The <code>alien-funcall</code> Primitive</a>
</li><li><a href="#The-define_002dalien_002droutine-Macro">8.7.2 The <code>define-alien-routine</code> Macro</a>
</li><li><a href="#define_002dalien_002droutine-Example">8.7.3 <code>define-alien-routine</code> Example</a>
</li><li><a href="#Calling-Lisp-From-C">8.7.4 Calling Lisp From C</a>
</li></ul>
</li><li><a href="#Step_002dBy_002dStep-Example-of-the-Foreign-Function-Interface">8.8 Step-By-Step Example of the Foreign Function Interface</a>
</li></ul>
</li><li><a name="toc_Pathnames" href="#Pathnames">9 Pathnames</a>
<ul>
<li><a href="#Lisp-Pathnames">9.1 Lisp Pathnames</a>
<ul>
<li><a href="#Lisp-Pathnames">9.1.1 Home Directory Specifiers</a>
</li><li><a href="#Lisp-Pathnames">9.1.2 The SYS Logical Pathname Host</a>
</li></ul>
</li><li><a href="#Native-Filenames">9.2 Native Filenames</a>
</li></ul>
</li><li><a name="toc_Streams" href="#Streams">10 Streams</a>
<ul>
<li><a href="#External-Formats">10.1 External Formats</a>
</li><li><a href="#Bivalent-Streams">10.2 Bivalent Streams</a>
</li><li><a href="#Gray-Streams">10.3 Gray Streams</a>
<ul>
<li><a href="#Gray-Streams-classes">10.3.1 Gray Streams classes</a>
</li><li><a href="#Methods-common-to-all-streams">10.3.2 Methods common to all streams</a>
</li><li><a href="#Input-stream-methods">10.3.3 Input stream methods</a>
</li><li><a href="#Character-input-stream-methods">10.3.4 Character input stream methods</a>
</li><li><a href="#Output-stream-methods">10.3.5 Output stream methods</a>
</li><li><a href="#Character-output-stream-methods">10.3.6 Character output stream methods</a>
</li><li><a href="#Binary-stream-methods">10.3.7 Binary stream methods</a>
</li><li><a href="#Gray-Streams-examples">10.3.8 Gray Streams examples</a>
<ul>
<li><a href="#Character-counting-input-stream">10.3.8.1 Character counting input stream</a>
</li><li><a href="#Output-prefixing-character-stream">10.3.8.2 Output prefixing character stream</a>
</li></ul>
</li></ul>
</li><li><a href="#Simple-Streams">10.4 Simple Streams</a>
</li></ul>
</li><li><a name="toc_Package-Locks" href="#Package-Locks">11 Package Locks</a>
<ul>
<li><a href="#Package-Lock-Concepts">11.1 Package Lock Concepts</a>
<ul>
<li><a href="#Package-Lock-Overview">11.1.1 Package Locking Overview</a>
</li><li><a href="#Implementation-Packages">11.1.2 Implementation Packages</a>
</li><li><a href="#Package-Lock-Violations">11.1.3 Package Lock Violations</a>
<ul>
<li><a href="#Package-Lock-Violations">11.1.3.1 Lexical Bindings and Declarations</a>
</li><li><a href="#Package-Lock-Violations">11.1.3.2 Other Operations</a>
</li></ul>
</li><li><a href="#Package-Locks-in-Compiled-Code">11.1.4 Package Locks in Compiled Code</a>
<ul>
<li><a href="#Package-Locks-in-Compiled-Code">11.1.4.1 Interned Symbols</a>
</li><li><a href="#Package-Locks-in-Compiled-Code">11.1.4.2 Other Limitations on Compiled Code</a>
</li></ul>
</li><li><a href="#Operations-Violating-Package-Locks">11.1.5 Operations Violating Package Locks</a>
<ul>
<li><a href="#Operations-Violating-Package-Locks">11.1.5.1 Operations on Packages</a>
</li><li><a href="#Operations-Violating-Package-Locks">11.1.5.2 Operations on Symbols</a>
</li></ul>
</li></ul>
</li><li><a href="#Package-Lock-Dictionary">11.2 Package Lock Dictionary</a>
</li></ul>
</li><li><a name="toc_Threading" href="#Threading">12 Threading</a>
<ul>
<li><a href="#Threading-basics">12.1 Threading basics</a>
<ul>
<li><a href="#Threading-basics">12.1.1 Thread Objects</a>
</li><li><a href="#Threading-basics">12.1.2 Making, Returning From, Joining, and Yielding Threads</a>
</li><li><a href="#Threading-basics">12.1.3 Asynchronous Operations</a>
</li><li><a href="#Threading-basics">12.1.4 Miscellaneous Operations</a>
</li><li><a href="#Threading-basics">12.1.5 Error Conditions</a>
</li></ul>
</li><li><a href="#Special-Variables">12.2 Special Variables</a>
</li><li><a href="#Atomic-Operations">12.3 Atomic Operations</a>
<ul>
<li><a href="#Atomic-Operations">CAS Protocol</a>
</li></ul>
</li><li><a href="#Mutex-Support">12.4 Mutex Support</a>
</li><li><a href="#Semaphores">12.5 Semaphores</a>
</li><li><a href="#Waitqueue_002fcondition-variables">12.6 Waitqueue/condition variables</a>
</li><li><a href="#Barriers">12.7 Barriers</a>
</li><li><a href="#Sessions_002fDebugging">12.8 Sessions/Debugging</a>
</li><li><a href="#Foreign-threads">12.9 Foreign threads</a>
</li><li><a href="#Implementation-_0028Linux-x86_002fx86_002d64_0029">12.10 Implementation (Linux x86/x86-64)</a>
</li></ul>
</li><li><a name="toc_Timers" href="#Timers">13 Timers</a>
<ul>
<li><a href="#Timers">13.1 Timer Dictionary</a>
</li></ul>
</li><li><a name="toc_Networking" href="#Networking">14 Networking</a>
<ul>
<li><a href="#Sockets-Overview">14.1 Sockets Overview</a>
</li><li><a href="#General-Sockets">14.2 General Sockets</a>
</li><li><a href="#Socket-Options">14.3 Socket Options</a>
</li><li><a href="#INET-Domain-Sockets">14.4 INET Domain Sockets</a>
</li><li><a href="#Local-_0028Unix_0029-Domain-Sockets">14.5 Local (Unix) Domain Sockets</a>
</li><li><a href="#Name-Service">14.6 Name Service</a>
</li></ul>
</li><li><a name="toc_Profiling" href="#Profiling">15 Profiling</a>
<ul>
<li><a href="#Deterministic-Profiler">15.1 Deterministic Profiler</a>
</li><li><a href="#Statistical-Profiler">15.2 Statistical Profiler</a>
<ul>
<li><a href="#Statistical-Profiler">15.2.1 Example Usage</a>
</li><li><a href="#Statistical-Profiler">15.2.2 Output</a>
</li><li><a href="#Statistical-Profiler">15.2.3 Platform support</a>
</li><li><a href="#Statistical-Profiler">15.2.4 Macros</a>
</li><li><a href="#Statistical-Profiler">15.2.5 Functions</a>
</li><li><a href="#Statistical-Profiler">15.2.6 Variables</a>
</li><li><a href="#Statistical-Profiler">15.2.7 Credits</a>
</li></ul>
</li></ul>
</li><li><a name="toc_Contributed-Modules" href="#Contributed-Modules">16 Contributed Modules</a>
<ul>
<li><a href="#sb_002daclrepl">16.1 sb-aclrepl</a>
<ul>
<li><a href="#sb_002daclrepl">16.1.1 Usage</a>
</li><li><a href="#sb_002daclrepl">16.1.2 Example Initialization</a>
</li><li><a href="#sb_002daclrepl">16.1.3 Credits</a>
</li></ul>
</li><li><a href="#sb_002dconcurrency">16.2 sb-concurrency</a>
<ul>
<li><a href="#sb_002dconcurrency">16.2.1 Queue</a>
</li><li><a href="#sb_002dconcurrency">16.2.2 Mailbox (lock-free)</a>
</li><li><a href="#sb_002dconcurrency">16.2.3 Gates</a>
</li><li><a href="#sb_002dconcurrency">16.2.4 Frlocks, aka Fast Read Locks</a>
</li></ul>
</li><li><a href="#sb_002dcover">16.3 sb-cover</a>
<ul>
<li><a href="#sb_002dcover">16.3.1 Example Usage</a>
</li><li><a href="#sb_002dcover">16.3.2 Functions</a>
</li></ul>
</li><li><a href="#sb_002dgrovel">16.4 sb-grovel</a>
<ul>
<li><a href="#sb_002dgrovel">16.4.1 Using sb-grovel in your own ASDF system</a>
</li><li><a href="#sb_002dgrovel">16.4.2 Contents of a grovel-constants-file</a>
</li><li><a href="#sb_002dgrovel">16.4.3 Programming with sb-grovel's structure types</a>
<ul>
<li><a href="#sb_002dgrovel">16.4.3.1 Traps and Pitfalls</a>
</li></ul>
</li></ul>
</li><li><a href="#sb_002dmd5">16.5 sb-md5</a>
<ul>
<li><a href="#sb_002dmd5">16.5.1 Credits</a>
</li></ul>
</li><li><a href="#sb_002dposix">16.6 sb-posix</a>
<ul>
<li><a href="#Lisp-names-for-C-names">16.6.1 Lisp names for C names</a>
</li><li><a href="#Types">16.6.2 Types</a>
<ul>
<li><a href="#File_002ddescriptors">16.6.2.1 File-descriptors</a>
</li><li><a href="#Filenames">16.6.2.2 Filenames</a>
</li></ul>
</li><li><a href="#Function-Parameters">16.6.3 Function Parameters</a>
</li><li><a href="#Function-Return-Values">16.6.4 Function Return Values</a>
</li><li><a href="#Lisp-objects-and-C-structures">16.6.5 Lisp objects and C structures</a>
</li><li><a href="#Functions-with-idiosyncratic-bindings">16.6.6 Functions with idiosyncratic bindings</a>
</li></ul>
</li><li><a href="#sb_002dqueue">16.7 sb-queue</a>
</li><li><a href="#sb_002drotate_002dbyte">16.8 sb-rotate-byte</a>
</li></ul>
</li><li><a name="toc_Deprecation" href="#Deprecation">17 Deprecation</a>
<ul>
<li><a href="#Why-Deprecate_003f">17.1 Why Deprecate?</a>
</li><li><a href="#The-Deprecation-Pipeline">17.2 The Deprecation Pipeline</a>
</li><li><a href="#Deprecation-Conditions">17.3 Deprecation Conditions</a>
</li><li><a href="#Introspecting-Deprecation-Information">17.4 Introspecting Deprecation Information</a>
</li><li><a href="#Deprecation-Declaration">17.5 Deprecation Declaration</a>
</li><li><a href="#Deprecation-Examples">17.6 Deprecation Examples</a>
</li><li><a href="#Deprecated-Interfaces-in-SBCL">17.7 Deprecated Interfaces in SBCL</a>
<ul>
<li><a href="#Deprecated-Interfaces-in-SBCL">17.7.1 List of Deprecated Interfaces</a>
<ul>
<li><a href="#Deprecated-Interfaces-in-SBCL">17.7.1.1 Early Deprecation</a>
</li><li><a href="#Deprecated-Interfaces-in-SBCL">17.7.1.2 Late Deprecation</a>
</li><li><a href="#Deprecated-Interfaces-in-SBCL">17.7.1.3 Final Deprecation</a>
</li></ul>
</li><li><a href="#Deprecated-Interfaces-in-SBCL">17.7.2 Historical Interfaces</a>
</li></ul>
</li></ul>
</li><li><a name="toc_Concept-Index" href="#Concept-Index">Appendix A Concept Index</a>
</li><li><a name="toc_Function-Index" href="#Function-Index">Appendix B Function Index</a>
</li><li><a name="toc_Variable-Index" href="#Variable-Index">Appendix C Variable Index</a>
</li><li><a name="toc_Type-Index" href="#Type-Index">Appendix D Type Index</a>
</li><li><a name="toc_Colophon" href="#Colophon">Colophon</a>
</li></ul>
</div>



<!-- We use @andkey, etc to escape & from TeX in lambda lists - -->
<!-- so we need to define them for info as well. -->
<div class="node">
<a name="Top"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Getting-Support-and-Reporting-Bugs">Getting Support and Reporting Bugs</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#dir">(dir)</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="unnumbered">sbcl</h2>

<blockquote>
This manual is part of the SBCL software system. See the
<samp><span class="file">README</span></samp> file for more information.

   <p>This manual is largely derived from the manual for the CMUCL system,
which was produced at Carnegie Mellon University and later released
into the public domain. This manual is in the public domain and is
provided with absolutely no warranty. See the <samp><span class="file">COPYING</span></samp> and
<samp><span class="file">CREDITS</span></samp> files for more information. 
</p></blockquote>

<ul class="menu">
<li><a accesskey="1" href="#Getting-Support-and-Reporting-Bugs">Getting Support and Reporting Bugs</a>
</li><li><a accesskey="2" href="#Introduction">Introduction</a>
</li><li><a accesskey="3" href="#Starting-and-Stopping">Starting and Stopping</a>
</li><li><a accesskey="4" href="#Compiler">Compiler</a>
</li><li><a accesskey="5" href="#Debugger">Debugger</a>
</li><li><a accesskey="6" href="#Efficiency">Efficiency</a>
</li><li><a accesskey="7" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>
</li><li><a accesskey="8" href="#Foreign-Function-Interface">Foreign Function Interface</a>
</li><li><a accesskey="9" href="#Pathnames">Pathnames</a>
</li><li><a href="#Streams">Streams</a>
</li><li><a href="#Package-Locks">Package Locks</a>
</li><li><a href="#Threading">Threading</a>
</li><li><a href="#Timers">Timers</a>
</li><li><a href="#Networking">Networking</a>
</li><li><a href="#Profiling">Profiling</a>
</li><li><a href="#Contributed-Modules">Contributed Modules</a>
</li><li><a href="#Deprecation">Deprecation</a>
</li><li><a href="#Concept-Index">Concept Index</a>
</li><li><a href="#Function-Index">Function Index</a>
</li><li><a href="#Variable-Index">Variable Index</a>
</li><li><a href="#Type-Index">Type Index</a>
</li><li><a href="#Colophon">Colophon</a>
</li></ul>

<div class="node">
<a name="Getting-Support-and-Reporting-Bugs"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Introduction">Introduction</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Top">Top</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">1 Getting Support and Reporting Bugs</h2>

<ul class="menu">
<li><a accesskey="1" href="#Volunteer-Support">Volunteer Support</a>
</li><li><a accesskey="2" href="#Commercial-Support">Commercial Support</a>
</li><li><a accesskey="3" href="#Reporting-Bugs">Reporting Bugs</a>
</li></ul>

<div class="node">
<a name="Volunteer-Support"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Commercial-Support">Commercial Support</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Getting-Support-and-Reporting-Bugs">Getting Support and Reporting Bugs</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">1.1 Volunteer Support</h3>

<p>Your primary source of SBCL support should probably be the mailing
list <strong>sbcl-help</strong>: in addition to other users SBCL developers
monitor this list and are available for advice. As an anti-spam
measure subscription is required for posting:

   </p><p>&nbsp;<!-- /@w --> &nbsp;<!-- /@w --> <a href="https://lists.sourceforge.net/lists/listinfo/sbcl-help">https://lists.sourceforge.net/lists/listinfo/sbcl-help</a>

   </p><p>Remember that the people answering your question are volunteers, so
you stand a much better chance of getting a good answer if you ask a
good question.

   </p><p>Before sending mail, check the list archives at either

   </p><p>&nbsp;<!-- /@w --> &nbsp;<!-- /@w --> <a href="http://sourceforge.net/mailarchive/forum.php?forum_name=sbcl-help">http://sourceforge.net/mailarchive/forum.php?forum_name=sbcl-help</a>

   </p><p>or

   </p><p>&nbsp;<!-- /@w --> &nbsp;<!-- /@w --> <a href="http://news.gmane.org/gmane.lisp.steel-bank.general">http://news.gmane.org/gmane.lisp.steel-bank.general</a>

   </p><p>to see if your question has been answered already. Checking the bug
database is also worth it See <a href="#Reporting-Bugs">Reporting Bugs</a>, to see if the issue
is already known.

   </p><p>For general advice on asking good questions, see

   </p><p>&nbsp;<!-- /@w --> &nbsp;<!-- /@w --> <a href="http://www.catb.org/%7Eesr/faqs/smart-questions.html">http://www.catb.org/~esr/faqs/smart-questions.html</a>.

</p><div class="node">
<a name="Commercial-Support"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Reporting-Bugs">Reporting Bugs</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Volunteer-Support">Volunteer Support</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Getting-Support-and-Reporting-Bugs">Getting Support and Reporting Bugs</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">1.2 Commercial Support</h3>

<p>There is no formal organization developing SBCL, but if you need a
paid support arrangement or custom SBCL development, we maintain the
list of companies and consultants below. Use it to identify service
providers with appropriate skills and interests, and contact them
directly.

   </p><p>The SBCL project cannot verify the accuracy of the information or the
competence of the people listed, and they have provided their own
blurbs below: you must make your own judgement of suitability from the
available information - refer to the links they provide, the CREDITS
file, mailing list archives, CVS commit messages, and so on. Please
feel free to ask for advice on the sbcl-help list.

   </p><p>(At present, no companies or consultants wish to advertise paid support
or custom SBCL development in this manual).

</p><div class="node">
<a name="Reporting-Bugs"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Commercial-Support">Commercial Support</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Getting-Support-and-Reporting-Bugs">Getting Support and Reporting Bugs</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">1.3 Reporting Bugs</h3>

<p>SBCL uses Launchpad to track bugs. The bug database is available at

   </p><p>&nbsp;<!-- /@w --> &nbsp;<!-- /@w --> <a href="https://bugs.launchpad.net/sbcl">https://bugs.launchpad.net/sbcl</a>

   </p><p>Reporting bugs there requires registering at Launchpad. However, bugs
can also be reported on the mailing list <strong>sbcl-bugs</strong>, which is
moderated but does <em>not</em> require subscribing.

   </p><p>Simply send email to <a href="mailto:sbcl-bugs@lists.sourceforge.net">sbcl-bugs@lists.sourceforge.net</a> and the
bug will be checked and added to Launchpad by SBCL maintainers.

</p><h4 class="subsection">1.3.1 How to Report Bugs Effectively</h4>

<p>Please include enough information in a bug report that someone reading
it can reproduce the problem, i.e. don't write

</p><pre class="example">     Subject: apparent bug in PRINT-OBJECT (or *PRINT-LENGTH*?)
     PRINT-OBJECT doesn't seem to work with *PRINT-LENGTH*. Is this a bug?
</pre>
   <p>but instead

</p><pre class="example">     Subject: apparent bug in PRINT-OBJECT (or *PRINT-LENGTH*?)
     In sbcl-1.2.3 running under OpenBSD 4.5 on my Alpha box, when
     I compile and load the file
        (DEFSTRUCT (FOO (:PRINT-OBJECT (LAMBDA (X Y)
                                         (LET ((*PRINT-LENGTH* 4))
                                           (PRINT X Y)))))
          X Y)
     then at the command line type
        (MAKE-FOO)
     the program loops endlessly instead of printing the object.
</pre>
   <p>A more in-depth discussion on reporting bugs effectively can be found
at

   </p><p>&nbsp;<!-- /@w --> &nbsp;<!-- /@w --> <a href="http://www.chiark.greenend.org.uk/%7Esgtatham/bugs.html">http://www.chiark.greenend.org.uk/~sgtatham/bugs.html</a>.

</p><h4 class="subsection">1.3.2 Signal Related Bugs</h4>

<p>If you run into a signal related bug, you are getting fatal errors
such as <code>signal N is [un]blocked</code> or just hangs, and you want to
send a useful bug report then:

     </p><ol start="1" type="1">

     <li><a name="index-ldb-1"></a>Compile SBCL with ldb support (feature <code>:sb-ldb</code>, see
<samp><span class="file">base-target-features.lisp-expr</span></samp>) and change <code>#define QSHOW_SIGNAL 0</code> to
<code>#define QSHOW_SIGNAL 1</code> in <samp><span class="file">src/runtime/runtime.h</span></samp>.

     </li><li>Isolate a smallish test case, run it.

     </li><li>If it just hangs kill it with sigabrt: <code>kill -ABRT &lt;pidof sbcl&gt;</code>.

     </li><li>Print the backtrace from ldb by typing <code>ba</code>.

     </li><li>Attach gdb: <code>gdb -p &lt;pidof sbcl&gt;</code> and get backtraces for all threads:
<code>thread apply all ba</code>.

     </li><li>If multiple threads are in play then still in gdb, try to get Lisp
backtrace for all threads: <code>thread apply all call
backtrace_from_fp($ebp, 100)</code>. Substitute <code>$ebp</code> with <code>$rbp</code>
on x86-64. The backtraces will appear in the stdout of the SBCL
process.

     </li><li>Send a report with the backtraces and the output (both stdout and
stderr) produced by SBCL.

     </li><li>Don't forget to include OS and SBCL version.

     </li><li>If available, include information on outcome of the same test with
other versions of SBCL, OS, ...
        </li></ol>

<div class="node">
<a name="Introduction"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Starting-and-Stopping">Starting and Stopping</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Getting-Support-and-Reporting-Bugs">Getting Support and Reporting Bugs</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">2 Introduction</h2>

<p>SBCL is a mostly-conforming implementation of the ANSI Common Lisp
standard. This manual focuses on behavior which is specific to SBCL,
not on behavior which is common to all implementations of ANSI Common
Lisp.

</p><ul class="menu">
<li><a accesskey="1" href="#ANSI-Conformance">ANSI Conformance</a>
</li><li><a accesskey="2" href="#Extensions">Extensions</a>
</li><li><a accesskey="3" href="#Idiosyncrasies">Idiosyncrasies</a>
</li><li><a accesskey="4" href="#Development-Tools">Development Tools</a>
</li><li><a accesskey="5" href="#More-SBCL-Information">More SBCL Information</a>
</li><li><a accesskey="6" href="#More-Common-Lisp-Information">More Common Lisp Information</a>
</li><li><a accesskey="7" href="#History-and-Implementation-of-SBCL">History and Implementation of SBCL</a>
</li></ul>

<div class="node">
<a name="ANSI-Conformance"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Extensions">Extensions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.1 ANSI Conformance</h3>

<p>Essentially every type of non-conformance is considered a bug. (The
exceptions involve internal inconsistencies in the standard.) 
See <a href="#Reporting-Bugs">Reporting Bugs</a>.

</p><div class="node">
<a name="Extensions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Idiosyncrasies">Idiosyncrasies</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#ANSI-Conformance">ANSI Conformance</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.2 Extensions</h3>

<p>SBCL comes with numerous extensions, some in core and some in modules
loadable with <code>require</code>. Unfortunately, not all of these
extensions have proper documentation yet.

<!-- FIXME: Once bits and pieces referred to here get real documentation -->
<!-- add xrefs there. -->
     </p><dl>
<dt><strong>System Definition Tool</strong></dt><dd><code>asdf</code> is a flexible and popular protocol-oriented system
definition tool by Daniel Barlow. see <a href="http://sbcl.org/manual/asdf.html#Top">the asdf manual</a>, for
more information.

     <br></dd><dt><strong>Foreign Function Interface</strong></dt><dd><code>sb-alien</code> package allows interfacing with C-code, loading shared
object files, etc. See <a href="#Foreign-Function-Interface">Foreign Function Interface</a>.

     <p><code>sb-grovel</code> can be used to partially automate generation of
foreign function interface definitions. See <a href="#sb_002dgrovel">sb-grovel</a>.

     <br></p></dd><dt><strong>Recursive Event Loop</strong></dt><dd>SBCL provides a recursive event loop (<code>serve-event</code>) for doing
non-blocking IO on multiple streams without using threads.

     <br></dd><dt><strong>Metaobject Protocol</strong></dt><dd><code>sb-mop</code> package provides a metaobject protocol for the Common
Lisp Object System as described in <cite>Art of Metaobject Protocol</cite>.

     <br></dd><dt><strong>Extensible Sequences</strong></dt><dd>SBCL allows users to define subclasses of the <code>sequence</code>
class. See <a href="#Extensible-Sequences">Extensible Sequences</a>.

     <br></dd><dt><strong>Native Threads</strong></dt><dd>SBCL has native threads on x86/Linux, capable of taking advantage
of SMP on multiprocessor machines. See <a href="#Threading">Threading</a>.

     <br></dd><dt><strong>Network Interface</strong></dt><dd><code>sb-bsd-sockets</code> is a low-level networking interface, providing
both TCP and UDP sockets. See <a href="#Networking">Networking</a>.

     <br></dd><dt><strong>Introspective Facilities</strong></dt><dd><code>sb-introspect</code> module offers numerous introspective extensions,
including access to function lambda-lists and a cross referencing
facility.

     <br></dd><dt><strong>Operating System Interface</strong></dt><dd><code>sb-ext</code> contains a number of functions for running external
processes, accessing environment variables, etc.

     <p><code>sb-posix</code> module provides a lispy interface to standard POSIX
facilities.

     <br></p></dd><dt><strong>Extensible Streams</strong></dt><dd><code>sb-gray</code> is an implementation of <em>Gray Streams</em>. See <a href="#Gray-Streams">Gray Streams</a>.

     <p><code>sb-simple-streams</code> is an implementation of the <em>simple
streams</em> API proposed by Franz Inc. See <a href="#Simple-Streams">Simple Streams</a>.

     <br></p></dd><dt><strong>Profiling</strong></dt><dd><code>sb-profile</code> is a exact per-function profiler. See <a href="#Deterministic-Profiler">Deterministic Profiler</a>.

     <p><code>sb-sprof</code> is a statistical profiler, capable of call-graph
generation and instruction level profiling, which also supports
allocation profiling. See <a href="#Statistical-Profiler">Statistical Profiler</a>.

     <br></p></dd><dt><strong>Customization Hooks</strong></dt><dd>SBCL contains a number of extra-standard customization hooks that
can be used to tweak the behaviour of the system. See <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a>.

     <p><code>sb-aclrepl</code> provides an Allegro CL -style toplevel for SBCL,
as an alternative to the classic CMUCL-style one. See <a href="#sb_002daclrepl">sb-aclrepl</a>.

     <br></p></dd><dt><strong>CLTL2 Compatibility Layer</strong></dt><dd><code>sb-cltl2</code> module provides <code>compiler-let</code> and environment
access functionality described in <cite>Common Lisp The Language, 2nd
Edition</cite> which were removed from the language during the ANSI
standardization process.

     <br></dd><dt><strong>Executable Delivery</strong></dt><dd>The <code>:executable</code> argument to <a href="#Function-sb_002dext_003asave_002dlisp_002dand_002ddie">Function sb-ext:save-lisp-and-die</a> can produce a `standalone' executable
containing both an image of the current Lisp session and an SBCL
runtime.

     <br></dd><dt><strong>Bitwise Rotation</strong></dt><dd><code>sb-rotate-byte</code> provides an efficient primitive for bitwise
rotation of integers, an operation required by e.g. numerous
cryptographic algorithms, but not available as a primitive in ANSI
Common Lisp. See <a href="#sb_002drotate_002dbyte">sb-rotate-byte</a>.

     <br></dd><dt><strong>Test Harness</strong></dt><dd><code>sb-rt</code> module is a simple yet attractive regression and
unit-test framework.

     <br></dd><dt><strong>MD5 Sums</strong></dt><dd><code>sb-md5</code> is an implementation of the MD5 message digest algorithm
for Common Lisp, using the modular arithmetic optimizations provided
by SBCL. See <a href="#sb_002dmd5">sb-md5</a>.

   </dd></dl>

<div class="node">
<a name="Idiosyncrasies"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Development-Tools">Development Tools</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Extensions">Extensions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.3 Idiosyncrasies</h3>

<p>The information in this section describes some of the ways that SBCL
deals with choices that the ANSI standard leaves to the
implementation.

</p><ul class="menu">
<li><a accesskey="1" href="#Declarations">Declarations</a>
</li><li><a accesskey="2" href="#FASL-Format">FASL Format</a>
</li><li><a accesskey="3" href="#Compiler_002donly-Implementation">Compiler-only Implementation</a>
</li><li><a accesskey="4" href="#Defining-Constants">Defining Constants</a>
</li><li><a accesskey="5" href="#Style-Warnings">Style Warnings</a>
</li></ul>

<div class="node">
<a name="Declarations"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#FASL-Format">FASL Format</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Idiosyncrasies">Idiosyncrasies</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.3.1 Declarations</h4>

<p>Declarations are generally treated as assertions. This general
principle, and its implications, and the bugs which still keep the
compiler from quite satisfying this principle, are discussed in
<a href="#Declarations-as-Assertions">Declarations as Assertions</a>.

</p><div class="node">
<a name="FASL-Format"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Compiler_002donly-Implementation">Compiler-only Implementation</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Declarations">Declarations</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Idiosyncrasies">Idiosyncrasies</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.3.2 FASL Format</h4>

<p>SBCL fasl-format is binary compatible only with the exact SBCL version
it was generated with. While this is obviously suboptimal, it has
proven more robust than trying to maintain fasl compatibility across
versions: accidentally breaking things is far too easy, and can lead
to hard to diagnose bugs.

   </p><p>The following snippet handles fasl recompilation automatically for
ASDF-based systems, and makes a good candidate for inclusion in
the user or system initialization file (see <a href="#Initialization-Files">Initialization Files</a>.)

</p><pre class="lisp">     (require :asdf)
     
     ;;; If a fasl was stale, try to recompile and load (once).
     (defmethod asdf:perform :around ((o asdf:load-op)
                                      (c asdf:cl-source-file))
        (handler-case (call-next-method o c)
           ;; If a fasl was stale, try to recompile and load (once).
           (sb-ext:invalid-fasl ()
              (asdf:perform (make-instance 'asdf:compile-op) c)
              (call-next-method))))
</pre>
   <div class="node">
<a name="Compiler-only-Implementation"></a>
<a name="Compiler_002donly-Implementation"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Defining-Constants">Defining Constants</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#FASL-Format">FASL Format</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Idiosyncrasies">Idiosyncrasies</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.3.3 Compiler-only Implementation</h4>

<p>SBCL is essentially a compiler-only implementation of Common Lisp. 
That is, for all but a few special cases, <code>eval</code> creates a lambda
expression, calls <code>compile</code> on the lambda expression to create a
compiled function, and then calls <code>funcall</code> on the resulting
function object. A more traditional interpreter is also available on
default builds; it is usually only called internally.  This is
explicitly allowed by the ANSI standard, but leads to some oddities;
e.g. at default settings, <code>functionp</code> and
<code>compiled-function-p</code> are equivalent, and they collapse into the
same function when SBCL is built without the interpreter.

</p><div class="node">
<a name="Defining-Constants"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Style-Warnings">Style Warnings</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Compiler_002donly-Implementation">Compiler-only Implementation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Idiosyncrasies">Idiosyncrasies</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.3.4 Defining Constants</h4>

<p><a name="index-g_t_0040cl_007bdefconstant_007d-2"></a>
SBCL is quite strict about ANSI's definition of <code>defconstant</code>. 
ANSI says that doing <code>defconstant</code> of the same symbol more than
once is undefined unless the new value is <code>eql</code> to the old value. 
Conforming to this specification is a nuisance when the “constant”
value is only constant under some weaker test like <code>string=</code> or
<code>equal</code>.

   </p><p>It's especially annoying because, in SBCL, <code>defconstant</code> takes
effect not only at load time but also at compile time, so that just
compiling and loading reasonable code like
</p><pre class="lisp">     (defconstant +foobyte+ '(1 4))
</pre>
   <p>runs into this undefined behavior. Many implementations of Common Lisp
try to help the programmer around this annoyance by silently accepting
the undefined code and trying to do what the programmer probably
meant.

   </p><p>SBCL instead treats the undefined behavior as an error. Often such
code can be rewritten in portable ANSI Common Lisp which has the
desired behavior. E.g., the code above can be given an exactly defined
meaning by replacing <code>defconstant</code> either with
<code>defparameter</code> or with a customized macro which does the right
thing, e.g.
</p><pre class="lisp">     (defmacro define-constant (name value &amp;optional doc)
       `(defconstant ,name (if (boundp ',name) (symbol-value ',name) ,value)
                           ,@(when doc (list doc))))
</pre>
   <p>or possibly along the lines of the <code>defconstant-eqx</code> macro used
internally in the implementation of SBCL itself. In circumstances
where this is not appropriate, the programmer can handle the condition
type <code>sb-ext:defconstant-uneql</code>, and choose either the
<samp><span class="command">continue</span></samp> or <samp><span class="command">abort</span></samp> restart as appropriate.

</p><div class="node">
<a name="Style-Warnings"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Defining-Constants">Defining Constants</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Idiosyncrasies">Idiosyncrasies</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.3.5 Style Warnings</h4>

<p>SBCL gives style warnings about various kinds of perfectly legal code,
e.g.

     </p><ul>
<li><code>defmethod</code> without a preceding <code>defgeneric</code>;

     </li><li>multiple <code>defun</code>s of the same symbol in different units;

     </li><li>special variables not named in the conventional <code>*foo*</code> style,
and lexical variables unconventionally named in the <code>*foo*</code> style

   </li></ul>

   <p>This causes friction with people who point out that other ways of
organizing code (especially avoiding the use of <code>defgeneric</code>) are
just as aesthetically stylish.  However, these warnings should be read
not as “warning, bad aesthetics detected, you have no style” but
“warning, this style keeps the compiler from understanding the code
as well as you might like.” That is, unless the compiler warns about
such conditions, there's no way for the compiler to warn about some
programming errors which would otherwise be easy to overlook. (Related
bug: The warning about multiple <code>defun</code>s is pointlessly annoying
when you compile and then load a function containing <code>defun</code>
wrapped in <code>eval-when</code>, and ideally should be suppressed in that
case, but still isn't as of SBCL 0.7.6.)

</p><div class="node">
<a name="Development-Tools"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#More-SBCL-Information">More SBCL Information</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Idiosyncrasies">Idiosyncrasies</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.4 Development Tools</h3>

<ul class="menu">
<li><a accesskey="1" href="#Editor-Integration">Editor Integration</a>
</li><li><a accesskey="2" href="#Language-Reference">Language Reference</a>
</li><li><a accesskey="3" href="#Generating-Executables">Generating Executables</a>
</li></ul>

<div class="node">
<a name="Editor-Integration"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Language-Reference">Language Reference</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Development-Tools">Development Tools</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.4.1 Editor Integration</h4>

<p>Though SBCL can be used running “bare”, the recommended mode of
development is with an editor connected to SBCL, supporting not
only basic lisp editing (paren-matching, etc), but providing among
other features an integrated debugger, interactive compilation, and
automated documentation lookup.

   </p><p>Currently <dfn>SLIME</dfn><a rel="footnote" href="#fn-1" name="fnd-1"><sup>1</sup></a> (Superior Lisp Interaction
Mode for Emacs) together with Emacs is recommended for use with
SBCL, though other options exist as well.

   </p><p>SLIME can be downloaded from
<a href="http://www.common-lisp.net/project/slime/">http://www.common-lisp.net/project/slime/</a>.

</p><div class="node">
<a name="Language-Reference"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Generating-Executables">Generating Executables</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Editor-Integration">Editor Integration</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Development-Tools">Development Tools</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.4.2 Language Reference</h4>

<p><dfn>CLHS</dfn> (Common Lisp Hyperspec) is a hypertext version of the ANSI
standard, made freely available by <em>LispWorks</em> – an invaluable
reference.

   </p><p>See: <a href="http://www.lispworks.com/reference/HyperSpec/index.html">http://www.lispworks.com/reference/HyperSpec/index.html</a>

</p><div class="node">
<a name="Generating-Executables"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Language-Reference">Language Reference</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Development-Tools">Development Tools</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.4.3 Generating Executables</h4>

<p>SBCL can generate stand-alone executables.  The generated executables
include the SBCL runtime itself, so no restrictions are placed on
program functionality.  For example, a deployed program can call
<code>compile</code> and <code>load</code>, which requires the compiler to be present
in the executable.  For further information, See <a href="#Function-sb_002dext_003asave_002dlisp_002dand_002ddie">Function sb-ext:save-lisp-and-die</a>.

</p><div class="node">
<a name="More-SBCL-Information"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#More-Common-Lisp-Information">More Common Lisp Information</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Development-Tools">Development Tools</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.5 More SBCL Information</h3>

<ul class="menu">
<li><a accesskey="1" href="#SBCL-Homepage">SBCL Homepage</a>
</li><li><a accesskey="2" href="#Online-Documentation">Online Documentation</a>
</li><li><a accesskey="3" href="#Additional-Documentation-Files">Additional Documentation Files</a>
</li><li><a accesskey="4" href="#Internals-Documentation">Internals Documentation</a>
</li></ul>

<div class="node">
<a name="SBCL-Homepage"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Online-Documentation">Online Documentation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-SBCL-Information">More SBCL Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.5.1 SBCL Homepage</h4>

<p>The SBCL website at <a href="http://www.sbcl.org/">http://www.sbcl.org/</a> has some general
information, plus links to mailing lists devoted to SBCL, and to
archives of these mailing lists. Subscribing to the mailing lists
<cite>sbcl-help</cite> and <cite>sbcl-announce</cite> is recommended: both are
fairly low-volume, and help you keep abreast with SBCL development.

</p><div class="node">
<a name="Online-Documentation"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Additional-Documentation-Files">Additional Documentation Files</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#SBCL-Homepage">SBCL Homepage</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-SBCL-Information">More SBCL Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.5.2 Online Documentation</h4>

<p>Documentation for non-ANSI extensions for various commands is
available online from the SBCL executable itself. The extensions
for functions which have their own command prompts (e.g. the debugger,
and <code>inspect</code>) are documented in text available by typing
<samp><span class="command">help</span></samp> at their command prompts. The extensions for functions
which don't have their own command prompt (such as <code>trace</code>) are
described in their documentation strings, unless your SBCL was
compiled with an option not to include documentation strings, in which
case the documentation strings are only readable in the source code.

</p><div class="node">
<a name="Additional-Documentation-Files"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Internals-Documentation">Internals Documentation</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Online-Documentation">Online Documentation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-SBCL-Information">More SBCL Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.5.3 Additional Documentation Files</h4>

<p>Besides this user manual both SBCL source and binary distributions
include some other SBCL-specific documentation files, which should be
installed along with this manual on your system, e.g. in
<samp><span class="file">/usr/local/share/doc/sbcl/</span></samp>.

     </p><dl>
<dt><samp><span class="file">COPYING</span></samp></dt><dd>Licence and copyright summary.

     <br></dd><dt><samp><span class="file">CREDITS</span></samp></dt><dd>Authorship information on various parts of SBCL.

     <br></dd><dt><samp><span class="file">INSTALL</span></samp></dt><dd>Covers installing SBCL from both source and binary distributions on
your system, and also has some installation related troubleshooting
information.

     <br></dd><dt><samp><span class="file">NEWS</span></samp></dt><dd>Summarizes changes between various SBCL versions.

   </dd></dl>

<div class="node">
<a name="Internals-Documentation"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Additional-Documentation-Files">Additional Documentation Files</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-SBCL-Information">More SBCL Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.5.4 Internals Documentation</h4>

<p>If you're interested in the development of the SBCL system itself,
then subscribing to <cite>sbcl-devel</cite> is a good idea.

   </p><p>SBCL internals documentation – besides comments in the source – is
currently maintained as a <em>wiki-like</em> website:
<a href="http://sbcl-internals.cliki.net/">http://sbcl-internals.cliki.net/</a>.

   </p><p>Some low-level information describing the programming details of the
conversion from CMUCL to SBCL is available in the
<samp><span class="file">doc/FOR-CMUCL-DEVELOPERS</span></samp> file in the SBCL distribution, though
it is not installed by default.

</p><div class="node">
<a name="More-Common-Lisp-Information"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#History-and-Implementation-of-SBCL">History and Implementation of SBCL</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#More-SBCL-Information">More SBCL Information</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.6 More Common Lisp Information</h3>

<ul class="menu">
<li><a accesskey="1" href="#Internet-Community">Internet Community</a>
</li><li><a accesskey="2" href="#Third_002dparty-Libraries">Third-party Libraries</a>
</li><li><a accesskey="3" href="#Common-Lisp-Books">Common Lisp Books</a>
</li></ul>

<div class="node">
<a name="Internet-Community"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Third_002dparty-Libraries">Third-party Libraries</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-Common-Lisp-Information">More Common Lisp Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.6.1 Internet Community</h4>

<!-- FIXME: Say something smart here -->
<p>The Common Lisp internet community is fairly diverse:
<a href="news://comp.lang.lisp">news://comp.lang.lisp</a> is fairly high volume newsgroup, but has
a rather poor signal/noise ratio. Various special interest mailing
lists and IRC tend to provide more content and less flames. 
<a href="http://www.lisp.org/">http://www.lisp.org</a> and <a href="http://www.cliki.net/">http://www.cliki.net</a> contain
numerous pointers places in the net where lispers talks shop.

</p><div class="node">
<a name="Third-party-Libraries"></a>
<a name="Third_002dparty-Libraries"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Common-Lisp-Books">Common Lisp Books</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Internet-Community">Internet Community</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-Common-Lisp-Information">More Common Lisp Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.6.2 Third-party Libraries</h4>

<p>For a wealth of information about free Common Lisp libraries and tools
we recommend checking out <em>CLiki</em>: <a href="http://www.cliki.net/">http://www.cliki.net/</a>.

</p><div class="node">
<a name="Common-Lisp-Books"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Third_002dparty-Libraries">Third-party Libraries</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#More-Common-Lisp-Information">More Common Lisp Information</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">2.6.3 Common Lisp Books</h4>

<p>If you're not a programmer and you're trying to learn, many
introductory Lisp books are available. However, we don't have any
standout favorites. If you can't decide, try checking the Usenet
<a href="news://comp.lang.lisp">news://comp.lang.lisp</a> FAQ for recent recommendations.

<!-- FIXME: This non-stance is silly. Maybe we could recommend SICP, -->
<!-- Touretzky, or something at least. -->
   </p><p>If you are an experienced programmer in other languages but need to
learn about Common Lisp, some books stand out:

     </p><dl>
<dt><cite>Practical Common Lisp, by Peter Seibel</cite></dt><dd>An excellent introduction to the language, covering both the basics
and “advanced topics” like macros, CLOS, and packages. Available
both in print format and on the web: <a href="http://www.gigamonkeys.com/book/">http://www.gigamonkeys.com/book/</a>.

     <br></dd><dt><cite>Paradigms Of Artificial Intelligence Programming, by Peter Norvig</cite></dt><dd>Good information on general Common Lisp programming, and many
nontrivial examples. Whether or not your work is AI, it's a very good
book to look at.

     <br></dd><dt><cite>On Lisp, by Paul Graham</cite></dt><dd>An in-depth treatment of macros, but not recommended as a first Common
Lisp book, since it is slightly pre-ANSI so you need to be on your
guard against non-standard usages, and since it doesn't really even
try to cover the language as a whole, focusing solely on macros. 
Downloadable from <a href="http://www.paulgraham.com/onlisp.html">http://www.paulgraham.com/onlisp.html</a>.

     <br></dd><dt><cite>Object-Oriented Programming In Common Lisp, by Sonya Keene</cite></dt><dd>With the exception of <cite>Practical Common Lisp</cite> most introductory
books don't emphasize CLOS. This one does. Even if you're very
knowledgeable about object oriented programming in the abstract, it's
worth looking at this book if you want to do any OO in Common Lisp. 
Some abstractions in CLOS (especially multiple dispatch) go beyond
anything you'll see in most OO systems, and there are a number of
lesser differences as well. This book tends to help with the culture
shock.

     <br></dd><dt><cite>Art Of Metaobject Programming, by Gregor Kiczales et al.</cite></dt><dd>Currently the prime source of information on the Common Lisp Metaobject
Protocol, which is supported by SBCL. Section 2 (Chapters 5 and 6) are
freely available at <a href="http://www.lisp.org/mop/">http://www.lisp.org/mop/</a>.

   </dd></dl>

<div class="node">
<a name="History-and-Implementation-of-SBCL"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#More-Common-Lisp-Information">More Common Lisp Information</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Introduction">Introduction</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">2.7 History and Implementation of SBCL</h3>

<p>You can work productively with SBCL without knowing or
understanding anything about where it came from, how it is
implemented, or how it extends the ANSI Common Lisp standard. However,
a little knowledge can be helpful in order to understand error
messages, to troubleshoot problems, to understand why some parts of
the system are better debugged than others, and to anticipate which
known bugs, known performance problems, and missing extensions are
likely to be fixed, tuned, or added.

   </p><p>SBCL is descended from CMUCL, which is itself descended from Spice
Lisp, including early implementations for the Mach operating system on
the IBM RT, back in the 1980s. Some design decisions from that time are
still reflected in the current implementation:

     </p><ul>
<li>The system expects to be loaded into a fixed-at-compile-time location
in virtual memory, and also expects the location of all of its heap
storage to be specified at compile time.

     </li><li>The system overcommits memory, allocating large amounts of address
space from the system (often more than the amount of virtual memory
available) and then failing if ends up using too much of the allocated
storage.

     </li><li>The system is implemented as a C program which is responsible for
supplying low-level services and loading a Lisp <samp><span class="file">.core</span></samp>
file.

   </li></ul>

   <p><a name="index-Garbage-Collection_002c-generational-3"></a>SBCL also inherited some newer architectural features from CMUCL. The
most important is that on some architectures it has a generational
garbage collector (“GC”), which has various implications (mostly
good) for performance. These are discussed in another chapter,
<a href="#Efficiency">Efficiency</a>.

   </p><p>SBCL has diverged from CMUCL in that SBCL is now essentially a
“compiler-only implementation” of Common Lisp. This is a change in
implementation strategy, taking advantage of the freedom “any of these
facilities might share the same execution strategy” guaranteed in the
ANSI specification section 3.1 (“Evaluation”). It does not mean SBCL
can't be used interactively, and in fact the change is largely invisible
to the casual user, since SBCL still can and does execute code
interactively by compiling it on the fly. (It is visible if you know how
to look, like using <code>compiled-function-p</code>; and it is visible in the
way that SBCL doesn't have many bugs which behave differently in
interpreted code than in compiled code.) What it means is that in SBCL,
the <code>eval</code> function only truly “interprets” a few easy kinds of
forms, such as symbols which are <code>boundp</code>. More complicated forms
are evaluated by calling <code>compile</code> and then calling <code>funcall</code>
on the returned result.

   </p><p>The direct ancestor of SBCL is the x86 port of CMUCL. This port was in
some ways the most cobbled-together of all the CMUCL ports, since a
number of strange changes had to be made to support the register-poor
x86 architecture. Some things (like tracing and debugging) do not work
particularly well there. SBCL should be able to improve in these areas
(and has already improved in some other areas), but it takes a while.

   </p><p><a name="index-Garbage-Collection_002c-conservative-4"></a>On the x86 SBCL – like the x86 port of CMUCL – uses a
<em>conservative</em> GC. This means that it doesn't maintain a strict
separation between tagged and untagged data, instead treating some
untagged data (e.g. raw floating point numbers) as possibly-tagged
data and so not collecting any Lisp objects that they point to. This
has some negative consequences for average time efficiency (though
possibly no worse than the negative consequences of trying to
implement an exact GC on a processor architecture as register-poor as
the X86) and also has potentially unlimited consequences for
worst-case memory efficiency. In practice, conservative garbage
collectors work reasonably well, not getting anywhere near the worst
case. But they can occasionally cause odd patterns of memory usage.

   </p><p>The fork from CMUCL was based on a major rewrite of the system
bootstrap process. CMUCL has for many years tolerated a very unusual
“build” procedure which doesn't actually build the complete system
from scratch, but instead progressively overwrites parts of a running
system with new versions. This quasi-build procedure can cause various
bizarre bootstrapping hangups, especially when a major change is made
to the system. It also makes the connection between the current source
code and the current executable more tenuous than in other software
systems – it's easy to accidentally “build” a CMUCL system
containing characteristics not reflected in the current version of the
source code.

   </p><p>Other major changes since the fork from CMUCL include

     </p><ul>
<li>SBCL has removed many CMUCL extensions, (e.g. IP networking,
remote procedure call, Unix system interface, and X11 interface) from
the core system. Most of these are available as contributed modules
(distributed with SBCL) or third-party modules instead.

     </li><li>SBCL has deleted or deprecated some nonstandard features and code
complexity which helped efficiency at the price of
maintainability. For example, the SBCL compiler no longer implements
memory pooling internally (and so is simpler and more maintainable,
but generates more garbage and runs more slowly), and various
block-compilation efficiency-increasing extensions to the language
have been deleted or are no longer used in the implementation of SBCL
itself.

   </li></ul>

<div class="node">
<a name="Starting-and-Stopping"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Compiler">Compiler</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Introduction">Introduction</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">3 Starting and Stopping</h2>

<ul class="menu">
<li><a accesskey="1" href="#Starting-SBCL">Starting SBCL</a>
</li><li><a accesskey="2" href="#Stopping-SBCL">Stopping SBCL</a>
</li><li><a accesskey="3" href="#Command-Line-Options">Command Line Options</a>
</li><li><a accesskey="4" href="#Initialization-Files">Initialization Files</a>
</li><li><a accesskey="5" href="#Initialization-and-Exit-Hooks">Initialization and Exit Hooks</a>
</li></ul>

<div class="node">
<a name="Starting-SBCL"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Stopping-SBCL">Stopping SBCL</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-and-Stopping">Starting and Stopping</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">3.1 Starting SBCL</h3>

<ul class="menu">
<li><a accesskey="1" href="#Running-from-Shell">Running from Shell</a>
</li><li><a accesskey="2" href="#Running-from-Emacs">Running from Emacs</a>
</li><li><a accesskey="3" href="#Shebang-Scripts">Shebang Scripts</a>
</li></ul>

<div class="node">
<a name="Running-from-Shell"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Running-from-Emacs">Running from Emacs</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-SBCL">Starting SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.1.1 From Shell to Lisp</h4>

<p>To run SBCL type <samp><span class="command">sbcl</span></samp> at the command line.

   </p><p>You should end up in the toplevel <dfn>REPL</dfn> (read, eval, print
-loop), where you can interact with SBCL by typing expressions.

</p><pre class="smallexample">     $ sbcl
     This is SBCL 0.8.13.60, an implementation of ANSI Common Lisp.
     More information about SBCL is available at &lt;http://www.sbcl.org/&gt;.
     
     SBCL is free software, provided as is, with absolutely no warranty.
     It is mostly in the public domain; some portions are provided under
     BSD-style licenses.  See the CREDITS and COPYING files in the
     distribution for more information.
     * (+ 2 2)
     
     4
     * (exit)
     $
</pre>
   <p>See also <a href="#Command-Line-Options">Command Line Options</a> and <a href="#Stopping-SBCL">Stopping SBCL</a>.

</p><div class="node">
<a name="Running-from-Emacs"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Shebang-Scripts">Shebang Scripts</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Running-from-Shell">Running from Shell</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-SBCL">Starting SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.1.2 Running from Emacs</h4>

<p>To run SBCL as an inferior-lisp from Emacs in your <samp><span class="file">.emacs</span></samp> do
something like:

</p><pre class="lisp">     ;;; The SBCL binary and command-line arguments
     (setq inferior-lisp-program "/usr/local/bin/sbcl --noinform")
</pre>
   <p>For more information on using SBCL with Emacs, see <a href="#Editor-Integration">Editor Integration</a>.

</p><div class="node">
<a name="Shebang-Scripts"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Running-from-Emacs">Running from Emacs</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-SBCL">Starting SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.1.3 Shebang Scripts</h4>

<p><a name="index-g_t_0040sbext_007b_0040earmuffs_007bposix_002dargv_007d_007d-5"></a>
Standard Unix tools that are interpreters follow a common command line
protocol that is necessary to work with “shebang scripts”. SBCL supports
this via the <code>--script</code> command line option.

   </p><p>Example file (<samp><span class="file">hello.lisp</span></samp>):

</p><pre class="lisp">     #!/usr/local/bin/sbcl --script
     (write-line "Hello, World!")
</pre>
   <p>Usage examples:

</p><pre class="smallexample">     $ ./hello.lisp
     Hello, World!
</pre>
   <pre class="smallexample">     $ sbcl --script hello.lisp
     Hello, World!
</pre>
   <div class="node">
<a name="Stopping-SBCL"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Command-Line-Options">Command Line Options</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Starting-SBCL">Starting SBCL</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-and-Stopping">Starting and Stopping</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">3.2 Stopping SBCL</h3>

<ul class="menu">
<li><a accesskey="1" href="#Exit">Exit</a>
</li><li><a accesskey="2" href="#End-of-File">End of File</a>
</li><li><a accesskey="3" href="#Saving-a-Core-Image">Saving a Core Image</a>
</li><li><a accesskey="4" href="#Exit-on-Errors">Exit on Errors</a>
</li></ul>

<div class="node">
<a name="Exit"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#End-of-File">End of File</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stopping-SBCL">Stopping SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.2.1 Exit</h4>

<p>SBCL can be stopped at any time by calling <code>sb-ext:exit</code>,
optionally returning a specified numeric value to the calling process. 
See <a href="#Threading">Threading</a> for information about terminating individual threads.

   </p><p><a name="Function-sb_002dext_003aexit"></a>

</p><div class="defun">
— Function: <b>exit [sb-ext]</b><var> &amp;key code abort timeout<a name="index-g_t_0040sbext_007bexit_007d-6"></a></var><br>
<blockquote><p>Terminates the process, causing <code>sbcl</code> to exit with <code>code</code>. <code>code</code>
defaults to 0 when <code>abort</code> is false, and 1 when it is true.

        </p><p>When <code>abort</code> is false (the default), current thread is first unwound,
<code>*exit-hooks*</code> are run, other threads are terminated, and standard
output streams are flushed before <code>sbcl</code> calls exit(3) <code>--</code> at which point
atexit(3) functions will run. If multiple threads call <code>exit</code> with <code>abort</code>
being false, the first one to call it will complete the protocol.

        </p><p>When <code>abort</code> is true, <code>sbcl</code> exits immediately by calling _exit(2) without
unwinding stack, or calling exit hooks. Note that _exit(2) does not
call atexit(3) functions unlike exit(3).

        </p><p>Recursive calls to <code>exit</code> cause <code>exit</code> to behave as it <code>abort</code> was true.

        </p><p><code>timeout</code> controls waiting for other threads to terminate when <code>abort</code> is
<code>nil</code>. Once current thread has been unwound and <code>*exit-hooks*</code> have been
run, spawning new threads is prevented and all other threads are
terminated by calling <code>terminate-thread</code> on them. The system then waits
for them to finish using <code>join-thread</code>, waiting at most a total <code>timeout</code>
seconds for all threads to join. Those threads that do not finish
in time are simply ignored while the exit protocol continues. <code>timeout</code>
defaults to <code>*exit-timeout*</code>, which in turn defaults to 60. <code>timeout</code> <code>nil</code>
means to wait indefinitely.

        </p><p>Note that <code>timeout</code> applies only to <code>join-thread</code>, not <code>*exit-hooks*</code>. Since
<code>terminate-thread</code> is asynchronous, getting multithreaded application
termination with complex cleanups right using it can be tricky. To
perform an orderly synchronous shutdown use an exit hook instead of
relying on implicit thread termination.

        </p><p>Consequences are unspecified if serious conditions occur during <code>exit</code>
excepting errors from <code>*exit-hooks*</code>, which cause warnings and stop
execution of the hook that signaled, but otherwise allow the exit
process to continue normally. 
</p></blockquote></div>

<div class="node">
<a name="End-of-File"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Saving-a-Core-Image">Saving a Core Image</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Exit">Exit</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stopping-SBCL">Stopping SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.2.2 End of File</h4>

<p>By default SBCL also exits on end of input, caused either by user
pressing <kbd>Control-D</kbd> on an attached terminal, or end of input when
using SBCL as part of a shell pipeline.

</p><div class="node">
<a name="Saving-a-Core-Image"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Exit-on-Errors">Exit on Errors</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#End-of-File">End of File</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stopping-SBCL">Stopping SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.2.3 Saving a Core Image</h4>

<p>SBCL has the ability to save its state as a file for later
execution. This functionality is important for its bootstrapping
process, and is also provided as an extension to the user.

   </p><p><a name="Function-sb_002dext_003asave_002dlisp_002dand_002ddie"></a>

</p><div class="defun">
— Function: <b>save-lisp-and-die [sb-ext]</b><var> core-file-name &amp;key toplevel executable save-runtime-options purify root-structures environment-name compression<a name="index-g_t_0040sbext_007bsave_002dlisp_002dand_002ddie_007d-7"></a></var><br>
<blockquote><p>Save a "core image", i.e. enough information to restart a Lisp
process later in the same state, in the file of the specified name. 
Only global state is preserved: the stack is unwound in the process.

        </p><p>The following <code>&amp;key</code> arguments are defined:

          </p><dl>
<dt><code>:toplevel</code></dt><dd>     The function to run when the created core file is resumed. The
     default function handles command line toplevel option processing
     and runs the top level read-eval-print loop. This function returning
     is equivalent to <code>(sb-ext:exit :code 0) </code>being called.

          <p><code>toplevel</code> functions should always provide an <code>abort</code> restart: otherwise
     code they call will run without one.

          <br></p></dd><dt><code>:executable</code></dt><dd>     If true, arrange to combine the <code>sbcl</code> runtime and the core image
     to create a standalone executable.  If false (the default), the
     core image will not be executable on its own. Executable images
     always behave as if they were passed the –noinform runtime option.

          <br></dd><dt><code>:save-runtime-options</code></dt><dd>     If true, values of runtime options –dynamic-space-size and
     –control-stack-size that were used to start <code>sbcl</code> are stored in
     the standalone executable, and restored when the executable is
     run. This also inhibits normal runtime option processing, causing
     all command line arguments to be passed to the toplevel. 
     Meaningless if <code>:executable</code> is <code>nil</code>.

          <br></dd><dt><code>:purify</code></dt><dd>     If true (the default on cheneygc), do a purifying <code>gc</code> which moves all
     dynamically allocated objects into static space. This takes
     somewhat longer than the normal <code>gc</code> which is otherwise done, but
     it's only done once, and subsequent GC's will be done less often
     and will take less time in the resulting core file. See the <code>purify</code>
     function. This parameter has no effect on platforms using the
     generational garbage collector.

          <br></dd><dt><code>:root-structures</code></dt><dd>     This should be a list of the main entry points in any newly loaded
     systems. This need not be supplied, but locality and/or <code>gc</code> performance
     may be better if they are. This has two different but related meanings:
     If <code>:purify</code> is true <code>-</code> and only for cheneygc <code>-</code> the root structures
     are those which anchor the set of objects moved into static space. 
     On gencgc <code>-</code> and only on platforms supporting immobile code <code>-</code> these are
     the functions and/or function-names which commence a depth-first scan
     of code when reordering based on the statically observable call chain. 
     The complete set of reachable objects is not affected per se. 
     This argument is meaningless if neither enabling precondition holds.

          <br></dd><dt><code>:environment-name</code></dt><dd>     This has no purpose; it is accepted only for legacy compatibility.

          <br></dd><dt><code>:compression</code></dt><dd>     This is only meaningful if the runtime was built with the <code>:sb-core-compression</code>
     feature enabled. If <code>nil</code> (the default), saves to uncompressed core files. If
     <code>:sb-core-compression</code> was enabled at build-time, the argument may also be
     an integer from -1 to 9, corresponding to zlib compression levels, or <code>t</code>
     (which is equivalent to the default compression level, -1).

          <br></dd><dt><code>:application-type</code></dt><dd>     Present only on Windows and is meaningful only with <code>:executable</code> <code>t</code>. 
     Specifies the subsystem of the executable, <code>:console</code> or <code>:gui</code>. 
     The notable difference is that <code>:gui</code> doesn't automatically create a console
     window. The default is <code>:console</code>.

        </dd></dl>

        <p>The save/load process changes the values of some global variables:

          </p><dl>
<dt><code>*standard-output*</code><em>, </em><code>*debug-io*</code><em>, etc.</em></dt><dd>    Everything related to open streams is necessarily changed, since
    the <code>os</code> won't let us preserve a stream across save and load.

          <br></dd><dt><code>*default-pathname-defaults*</code></dt><dd>    This is reinitialized to reflect the working directory where the
    saved core is loaded.

        </dd></dl>

        <p><code>save-lisp-and-die</code> interacts with <code>sb-alien:load-shared-object:</code> see its
documentation for details.

        </p><p>On threaded platforms only a single thread may remain running after
<code>sb-ext:*save-hooks*</code> have run. Applications using multiple threads can
be <code>save-lisp-and-die</code> friendly by registering a save-hook that quits
any additional threads, and an init-hook that restarts them.

        </p><p>This implementation is not as polished and painless as you might like:
          </p><ul>
<li>It corrupts the current Lisp image enough that the current process
    needs to be killed afterwards. This can be worked around by forking
    another process that saves the core. 
</li><li>There is absolutely no binary compatibility of core images between
    different runtime support programs. Even runtimes built from the same
    sources at different times are treated as incompatible for this
    purpose. 
</li></ul>
        This isn't because we like it this way, but just because there don't
seem to be good quick fixes for either limitation and no one has been
sufficiently motivated to do lengthy fixes. 
<p></p></blockquote></div>

   <p><a name="Variable-sb_002dext_003a_002asave_002dhooks_002a"></a>

</p><div class="defun">
— Variable: <b>*save-hooks* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bsave_002dhooks_007d_007d-8"></a></var><br>
<blockquote><p>A list of function designators which are called in an unspecified
order before creating a saved core image.

        </p><p>Unused by <code>sbcl</code> itself: reserved for user and applications. 
</p></blockquote></div>

   <p>In cases where the standard initialization files have already been loaded
into the saved core, and alternative ones should be used (or none at all),
SBCL allows customizing the initfile pathname computation.

   </p><p><a name="Variable-sb_002dext_003a_002asysinit_002dpathname_002dfunction_002a"></a>

</p><div class="defun">
— Variable: <b>*sysinit-pathname-function* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bsysinit_002dpathname_002dfunction_007d_007d-9"></a></var><br>
<blockquote><p>Designator for a function of zero arguments called to obtain a
pathname designator for the default sysinit file, or <code>nil</code>. If the
function returns <code>nil</code>, no sysinit file is used unless one has been
specified on the command-line. 
</p></blockquote></div>

   <p><a name="Variable-sb_002dext_003a_002auserinit_002dpathname_002dfunction_002a"></a>

</p><div class="defun">
— Variable: <b>*userinit-pathname-function* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007buserinit_002dpathname_002dfunction_007d_007d-10"></a></var><br>
<blockquote><p>Designator for a function of zero arguments called to obtain a
pathname designator or a stream for the default userinit file, or <code>nil</code>. 
If the function returns <code>nil</code>, no userinit file is used unless one has
been specified on the command-line. 
</p></blockquote></div>

   <p>To facilitate distribution of SBCL applications using external
resources, the filesystem location of the SBCL core file being used is
available from Lisp.

   </p><p><a name="Variable-sb_002dext_003a_002acore_002dpathname_002a"></a>

</p><div class="defun">
— Variable: <b>*core-pathname* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bcore_002dpathname_007d_007d-11"></a></var><br>
<blockquote><p>The absolute pathname of the running <code>sbcl</code> core. 
</p></blockquote></div>

<div class="node">
<a name="Exit-on-Errors"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Saving-a-Core-Image">Saving a Core Image</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stopping-SBCL">Stopping SBCL</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.2.4 Exit on Errors</h4>

<p>SBCL can also be configured to exit if an unhandled error occurs,
which is mainly useful for acting as part of a shell pipeline; doing
so under most other circumstances would mean giving up large parts of
the flexibility and robustness of Common Lisp. See <a href="#Debugger-Entry">Debugger Entry</a>.

</p><div class="node">
<a name="Command-Line-Options"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Initialization-Files">Initialization Files</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Stopping-SBCL">Stopping SBCL</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-and-Stopping">Starting and Stopping</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">3.3 Command Line Options</h3>

<!-- FIXME: This is essentially cut-and-paste from the manpage -->
<!-- What should probably be done is generate both this and the -->
<!-- man-page from ``sbcl -help'' output. -->
<p>Command line options can be considered an advanced topic; for ordinary
interactive use, no command line arguments should be necessary.

   </p><p>In order to understand the command line argument syntax for SBCL, it
is helpful to understand that the SBCL system is implemented as two
components, a low-level runtime environment written in C and a
higher-level system written in Common Lisp itself. Some command line
arguments are processed during the initialization of the low-level
runtime environment, some command line arguments are processed during
the initialization of the Common Lisp system, and any remaining
command line arguments are passed on to user code.

   </p><p>The full, unambiguous syntax for invoking SBCL at the command line is:

   </p><p><samp><span class="command">sbcl</span></samp> <var>runtime-option</var>* <code>--end-runtime-options</code> <var>toplevel-option</var>* <code>--end-toplevel-options</code> <var>user-options</var>*

   </p><p>For convenience, the <code>--end-runtime-options</code> and
<code>--end-toplevel-options</code> elements can be omitted. Omitting these
elements can be convenient when you are running the program
interactively, and you can see that no ambiguities are possible with
the option values you are using. Omitting these elements is probably a
bad idea for any batch file where any of the options are under user
control, since it makes it impossible for SBCL to detect erroneous
command line input, so that erroneous command line arguments will be
passed on to the user program even if they was intended for the
runtime system or the Lisp system.

</p><ul class="menu">
<li><a accesskey="1" href="#Runtime-Options">Runtime Options</a>
</li><li><a accesskey="2" href="#Toplevel-Options">Toplevel Options</a>
</li></ul>

<div class="node">
<a name="Runtime-Options"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Toplevel-Options">Toplevel Options</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Command-Line-Options">Command Line Options</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.3.1 Runtime Options</h4>

     <dl>
<dt><code>--core </code><var>corefilename</var></dt><dd>Run the specified Lisp core file instead of the default. Note that if
the Lisp core file is a user-created core file, it may run a
nonstandard toplevel which does not recognize the standard toplevel
options.

     <br></dd><dt><code>--dynamic-space-size </code><var>megabytes</var></dt><dd>Size of the dynamic space reserved on startup in megabytes. Default
value is platform dependent.

     <br></dd><dt><code>--control-stack-size </code><var>megabytes</var></dt><dd>Size of control stack reserved for each thread in megabytes. Default
value is 2.

     <br></dd><dt><code>--noinform</code></dt><dd>Suppress the printing of any banner or other informational message at
startup. This makes it easier to write Lisp programs which work
cleanly in Unix pipelines. See also the <code>--noprint</code> and
<code>--disable-debugger</code> options.

     <br></dd><dt><code>--disable-ldb</code></dt><dd><a name="index-ldb-12"></a><a name="index-ldb_002c-disabling-13"></a><a name="index-disabling-ldb-14"></a>Disable the low-level debugger. Only effective if SBCL is compiled
with LDB.

     <br></dd><dt><code>--lose-on-corruption</code></dt><dd><a name="index-ldb-15"></a>There are some dangerous low level errors (for instance, control stack
exhausted, memory fault) that (or whose handlers) can corrupt the
image. By default SBCL prints a warning, then tries to continue and
handle the error in Lisp, but this will not always work and SBCL may
malfunction or even hang. With this option, upon encountering such an
error SBCL will invoke ldb (if present and enabled) or else exit.

     <br></dd><dt><code>--script </code><var>filename</var></dt><dd>As a runtime option this is equivalent to <code>--noinform</code>
<code>--disable-ldb</code> <code>--lose-on-corruption</code>
<code>--end-runtime-options</code> <code>--script</code> <var>filename</var>. See the
description of <code>--script</code> as a toplevel option below. If there
are no other command line arguments following <code>--script</code>, the
filename argument can be omitted.

     <br></dd><dt><code>--merge-core-pages</code></dt><dd>When platform support is present, provide hints to the operating system
that identical pages may be shared between processes until they are
written to.  This can be useful to reduce the memory usage on systems
with multiple SBCL processes started from similar but differently-named
core files, or from compressed cores.  Without platform support, do
nothing.

     <br></dd><dt><code>--no-merge-core-pages</code></dt><dd>Ensures that no sharing hint is provided to the operating system.

     <br></dd><dt><code>--default-merge-core-pages</code></dt><dd>Reverts the sharing hint policy to the default: only compressed cores
trigger hinting.  Uncompressed cores are mapped directly from the core
file, which is usually enough to ensure sharing.

     <br></dd><dt><code>--help</code></dt><dd>Print some basic information about SBCL, then exit.

     <br></dd><dt><code>--version</code></dt><dd>Print SBCL's version information, then exit.

</dd></dl>

   <p>In the future, runtime options may be added to control behaviour such
as lazy allocation of memory.

   </p><p>Runtime options, including any –end-runtime-options option, are
stripped out of the command line before the Lisp toplevel logic gets a
chance to see it.

</p><div class="node">
<a name="Toplevel-Options"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Runtime-Options">Runtime Options</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Command-Line-Options">Command Line Options</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">3.3.2 Toplevel Options</h4>

     <dl>
<dt><code>--sysinit </code><var>filename</var></dt><dd>Load filename instead of the default system initialization file
(see <a href="#Initialization-Files">Initialization Files</a>.)

     <br></dd><dt><code>--no-sysinit</code></dt><dd>Don't load a system-wide initialization file.  If this option is given,
the <code>--sysinit</code> option is ignored.

     <br></dd><dt><code>--userinit </code><var>filename</var></dt><dd>Load filename instead of the default user initialization file
(see <a href="#Initialization-Files">Initialization Files</a>.)

     <br></dd><dt><code>--no-userinit</code></dt><dd>Don't load a user initialization file.  If this option is given,
the <code>--userinit</code> option is ignored.

     <br></dd><dt><code>--eval </code><var>command</var></dt><dd>After executing any initialization file, but before starting the
read-eval-print loop on standard input, read and evaluate the command
given. More than one <code>--eval</code> option can be used, and all will be
read and executed, in the order they appear on the command line.

     <br></dd><dt><code>--load </code><var>filename</var></dt><dd>This is equivalent to <code>--eval '(load "</code><var>filename</var><code>")'</code>. The
special syntax is intended to reduce quoting headaches when invoking
SBCL from shell scripts.

     <br></dd><dt><code>--noprint</code></dt><dd>When ordinarily the toplevel "read-eval-print loop" would be executed,
execute a "read-eval loop" instead, i.e. don't print a prompt and
don't echo results. Combined with the <code>--noinform</code> runtime
option, this makes it easier to write Lisp "scripts" which work
cleanly in Unix pipelines.

     <br></dd><dt><code>--disable-debugger</code></dt><dd>By default when SBCL encounters an error, it enters the builtin
debugger, allowing interactive diagnosis and possible intercession. 
This option disables the debugger, causing errors to print a backtrace
and exit with status 1 instead. When given, this option takes effect
before loading of initialization files or processing <code>--eval</code> and
<code>--load</code> options. See <code>sb-ext:disable-debugger</code> for details. 
See <a href="#Debugger-Entry">Debugger Entry</a>.

     <br></dd><dt><code>--script </code><var>filename</var></dt><dd>Implies <code>--no-userinit</code> <code>--no-sysinit</code>
<code>--disable-debugger</code> <code>--end-toplevel-options</code>.

     <p>Causes the system to load the specified file instead of entering the
read-eval-print-loop, and exit afterwards. If the file begins with a
shebang line, it is ignored.

     </p><p>If there are no other command line arguments following, the filename
can be omitted: this causes the script to be loaded from standard
input instead. Shebang lines in standard input script are currently
<em>not</em> ignored.

     </p><p>In either case, if there is an unhandled error (e.g. end of file, or a
broken pipe) on either standard input, standard output, or standard
error, the script silently exits with code 0. This allows e.g. safely
piping output from SBCL to <code>head -n1</code> or similar.

</p></dd></dl>

<div class="node">
<a name="Initialization-Files"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Initialization-and-Exit-Hooks">Initialization and Exit Hooks</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Command-Line-Options">Command Line Options</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-and-Stopping">Starting and Stopping</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">3.4 Initialization Files</h3>

<p>SBCL processes initialization files with <code>read</code> and <code>eval</code>,
not <code>load</code>; hence initialization files can be used to set startup
<code>*package*</code> and <code>*readtable*</code>, and for proclaiming a global
optimization policy.

     </p><ul>
<li><strong>System Initialization File</strong>

     <p>Defaults to <samp><samp><span class="env">$SBCL_HOME</span></samp><span class="file">/sbclrc</span></samp>, or if that doesn't exist to
<samp><span class="file">/etc/sbclrc</span></samp>. Can be overridden with the command line option
<code>--sysinit</code> or <code>--no-sysinit</code>.

     </p><p>The system initialization file is intended for system administrators
and software packagers to configure locations of installed third party
modules, etc.

     </p></li><li><strong>User Initialization File</strong>

     <p>Defaults to <samp><samp><span class="env">$HOME</span></samp><span class="file">/.sbclrc</span></samp>. Can be overridden with the
command line option <code>--userinit</code> or <code>--no-userinit</code>.

     </p><p>The user initialization file is intended for personal customizations,
such as loading certain modules at startup, defining convenience
functions to use in the REPL, handling automatic recompilation
of FASLs (see <a href="#FASL-Format">FASL Format</a>), etc.

   </p></li></ul>

   <p>Neither initialization file is required.

</p><div class="node">
<a name="Initialization-and-Exit-Hooks"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Initialization-Files">Initialization Files</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Starting-and-Stopping">Starting and Stopping</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">3.5 Initialization and Exit Hooks</h3>

<p>SBCL provides hooks into the system initialization and exit.

   </p><p><a name="Variable-sb_002dext_003a_002ainit_002dhooks_002a"></a>

</p><div class="defun">
— Variable: <b>*init-hooks* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007binit_002dhooks_007d_007d-16"></a></var><br>
<blockquote><p>A list of function designators which are called in an unspecified
order when a saved core image starts up, after the system itself has
been initialized.

        </p><p>Unused by <code>sbcl</code> itself: reserved for user and applications. 
</p></blockquote></div>

   <p><a name="Variable-sb_002dext_003a_002aexit_002dhooks_002a"></a>

</p><div class="defun">
— Variable: <b>*exit-hooks* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bexit_002dhooks_007d_007d-17"></a></var><br>
<blockquote><p>A list of function designators which are called in an unspecified
order when <code>sbcl</code> process exits.

        </p><p>Unused by <code>sbcl</code> itself: reserved for user and applications.

        </p><p>Using <code>(sb-ext:exit :abort t)</code>, or calling exit(3) directly circumvents
these hooks. 
</p></blockquote></div>

<div class="node">
<a name="Compiler"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Debugger">Debugger</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Starting-and-Stopping">Starting and Stopping</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">4 Compiler</h2>

<p>This chapter will discuss most compiler issues other than efficiency,
including compiler error messages, the SBCL compiler's unusual
approach to type safety in the presence of type declarations, the
effects of various compiler optimization policies, and the way that
inlining and open coding may cause optimized code to differ from a
naive translation. Efficiency issues are sufficiently varied and
separate that they have their own chapter, <a href="#Efficiency">Efficiency</a>.

</p><ul class="menu">
<li><a accesskey="1" href="#Diagnostic-Messages">Diagnostic Messages</a>
</li><li><a accesskey="2" href="#Handling-of-Types">Handling of Types</a>
</li><li><a accesskey="3" href="#Compiler-Policy">Compiler Policy</a>
</li><li><a accesskey="4" href="#Compiler-Errors">Compiler Errors</a>
</li><li><a accesskey="5" href="#Open-Coding-and-Inline-Expansion">Open Coding and Inline Expansion</a>
</li><li><a accesskey="6" href="#Interpreter">Interpreter</a>
</li></ul>

<div class="node">
<a name="Diagnostic-Messages"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Handling-of-Types">Handling of Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler">Compiler</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">4.1 Diagnostic Messages</h3>

<p><a name="index-Messages_002c-Compiler-18"></a><a name="index-Compiler-messages-19"></a>

</p><ul class="menu">
<li><a accesskey="1" href="#Controlling-Verbosity">Controlling Verbosity</a>
</li><li><a accesskey="2" href="#Diagnostic-Severity">Diagnostic Severity</a>
</li><li><a accesskey="3" href="#Understanding-Compiler-Diagnostics">Understanding Compiler Diagnostics</a>
</li></ul>

<div class="node">
<a name="Controlling-Verbosity"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Diagnostic-Severity">Diagnostic Severity</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Diagnostic-Messages">Diagnostic Messages</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.1.1 Controlling Verbosity</h4>

<p>The compiler can be quite verbose in its diagnostic reporting, rather
more then some users would prefer – the amount of noise emitted can
be controlled, however.

   </p><p>To control emission of compiler diagnostics (of any severity other
than <code>error</code>: see <a href="#Diagnostic-Severity">Diagnostic Severity</a>) use the
<code>sb-ext:muffle-conditions</code> and <code>sb-ext:unmuffle-conditions</code>
declarations, specifying the type of condition that is to be muffled
(the muffling is done using an associated <code>muffle-warning</code> restart).

   </p><p>Global control:
</p><pre class="lisp">     ;;; Muffle compiler-notes globally
     (declaim (sb-ext:muffle-conditions sb-ext:compiler-note))
</pre>
   <p>Local control:
</p><pre class="lisp">     ;;; Muffle compiler-notes based on lexical scope
     (defun foo (x)
       (declare (optimize speed) (fixnum x)
                (sb-ext:muffle-conditions sb-ext:compiler-note))
       (values (* x 5) ; no compiler note from this
         (locally
           (declare (sb-ext:unmuffle-conditions sb-ext:compiler-note))
           ;; this one gives a compiler note
           (* x -5))))
</pre>
   <div class="defun">
— Declaration: <b>muffle-conditions [sb-ext]</b><var><a name="index-g_t_0040sbext_007bmuffle_002dconditions_007d-20"></a></var><br>
<blockquote><p>Syntax: type*

        </p><p>Muffles the diagnostic messages that would be caused by compile-time
signals of given types. 
</p></blockquote></div>

<div class="defun">
— Declaration: <b>unmuffle-conditions [sb-ext]</b><var><a name="index-g_t_0040sbext_007bunmuffle_002dconditions_007d-21"></a></var><br>
<blockquote><p>Syntax: type*

        </p><p>Cancels the effect of a previous <code>sb-ext:muffle-conditions</code>
declaration. 
</p></blockquote></div>

   <p>Various details of <em>how</em> the compiler messages are printed can be
controlled via the alist
<code>sb-ext:*compiler-print-variable-alist*</code>.

   </p><p><a name="Variable-sb_002dext_003a_002acompiler_002dprint_002dvariable_002dalist_002a"></a>

</p><div class="defun">
— Variable: <b>*compiler-print-variable-alist* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bcompiler_002dprint_002dvariable_002dalist_007d_007d-22"></a></var><br>
<blockquote><p>an association list describing new bindings for special variables
to be used by the compiler for error-reporting, etc. Eg.

     </p><pre class="lisp">           ((*PRINT-LENGTH* . 10) (*PRINT-LEVEL* . 6) (*PRINT-PRETTY* . NIL))
</pre>
        <p>The variables in the <code>car</code> positions are bound to the values in the <code>cdr</code>
during the execution of some debug commands. When evaluating arbitrary
expressions in the debugger, the normal values of the printer control
variables are in effect.

        </p><p>Initially empty, <code>*compiler-print-variable-alist*</code> is Typically used to
specify bindings for printer control variables. 
</p></blockquote></div>

   <p>For information about muffling warnings signaled outside of the
compiler, see <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a>.

<!-- <!- FIXME: How much control over error messages is in SBCL? -->
<!-- _     How much should be? How much of this documentation should -->
<!-- _     we save or adapt? -->
<!-- _ -->
<!-- _ %%\node Error Message Parameterization,  , Read Errors, Interpreting Error Messages -->
<!-- _ \subsection{Error Message Parameterization} -->
<!-- _ \cpsubindex{error messages}{verbosity} -->
<!-- _ \cpsubindex{verbosity}{of error messages} -->
<!-- _ -->
<!-- _ There is some control over the verbosity of error messages.  See also -->
<!-- _ \varref{undefined-warning-limit}, \code{*efficiency-note-limit*} and -->
<!-- _ \varref{efficiency-note-cost-threshold}. -->
<!-- _ -->
<!-- _ \begin{defvar}{}{enclosing-source-cutoff} -->
<!-- _ -->
<!-- _   This variable specifies the number of enclosing actual source forms -->
<!-- _   that are printed in full, rather than in the abbreviated processing -->
<!-- _   path format.  Increasing the value from its default of \code{1} -->
<!-- _   allows you to see more of the guts of the macroexpanded source, -->
<!-- _   which is useful when debugging macros. -->
<!-- _ \end{defvar} -->
<!-- _ -->
<!-- _ \begin{defmac}{extensions:}{define-source-context}{% -->
<!-- _     \args{\var{name} \var{lambda-list} \mstar{form}}} -->
<!-- _ -->
<!-- _   This macro defines how to extract an abbreviated source context from -->
<!-- _   the \var{name}d form when it appears in the compiler input. -->
<!-- _   \var{lambda-list} is a \code{defmacro} style lambda-list used to -->
<!-- _   parse the arguments.  The \var{body} should return a list of -->
<!-- _   subforms that can be printed on about one line.  There are -->
<!-- _   predefined methods for \code{defstruct}, \code{defmethod}, etc.  If -->
<!-- _   no method is defined, then the first two subforms are returned. -->
<!-- _   Note that this facility implicitly determines the string name -->
<!-- _   associated with anonymous functions. -->
<!-- _ \end{defmac} -->
<!-- _ -->
<!-- _ -> -->
</p><div class="node">
<a name="Diagnostic-Severity"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Understanding-Compiler-Diagnostics">Understanding Compiler Diagnostics</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Controlling-Verbosity">Controlling Verbosity</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Diagnostic-Messages">Diagnostic Messages</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.1.2 Diagnostic Severity</h4>

<p><a name="index-Severity-of-compiler-messages-23"></a><a name="index-Compiler-Diagnostic-Severity-24"></a><a name="index-g_t_0040cl_007berror_007d-25"></a><a name="index-g_t_0040cl_007bwarning_007d-26"></a><a name="index-g_t_0040cl_007bstyle_002dwarning_007d-27"></a><a name="index-g_t_0040sbext_007bcompiler_002dnote_007d-28"></a><a name="index-g_t_0040sbext_007bcode_002ddeletion_002dnote_007d-29"></a>
There are four levels of compiler diagnostic severity:

     </p><ol start="1" type="1">
<li>error
</li><li>warning
</li><li>style warning
</li><li>note
        </li></ol>

   <p>The first three levels correspond to condition classes which are
defined in the ANSI standard for Common Lisp and which have special
significance to the <code>compile</code> and <code>compile-file</code> functions. 
These levels of compiler error severity occur when the compiler
handles conditions of these classes.

   </p><p>The fourth level of compiler error severity, <em>note</em>, corresponds
to the <code>sb-ext:compiler-note</code>, and is used for problems which are
too mild for the standard condition classes, typically hints about how
efficiency might be improved. The <code>sb-ext:code-deletion-note</code>, a
subtype of <code>compiler-note</code>, is signalled when the compiler
deletes user-supplied code after proving that the code in question is
unreachable.

   </p><p>Future work for SBCL includes expanding this hierarchy of types to
allow more fine-grained control over emission of diagnostic messages.

   </p><p><a name="Condition-sb_002dext_003acompiler_002dnote"></a>

</p><div class="defun">
— Condition: <b>compiler-note [sb-ext]</b><var><a name="index-g_t_0040sbext_007bcompiler_002dnote_007d-30"></a></var><br>
<blockquote><p>Class precedence list: <code>compiler-note, condition, t</code>

        </p><p>Root of the hierarchy of conditions representing information discovered
by the compiler that the user might wish to know, but which does not merit
a <code>style-warning</code> (or any more serious condition). 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003acode_002ddeletion_002dnote"></a>

</p><div class="defun">
— Condition: <b>code-deletion-note [sb-ext]</b><var><a name="index-g_t_0040sbext_007bcode_002ddeletion_002dnote_007d-31"></a></var><br>
<blockquote><p>Class precedence list: <code>code-deletion-note, compiler-note, condition, t</code>

        </p><p>A condition type signalled when the compiler deletes code that the user
has written, having proved that it is unreachable. 
</p></blockquote></div>

<div class="node">
<a name="Understanding-Compiler-Diagnostics"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Diagnostic-Severity">Diagnostic Severity</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Diagnostic-Messages">Diagnostic Messages</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.1.3 Understanding Compile Diagnostics</h4>

<p>The messages emitted by the compiler contain a lot of detail in a
terse format, so they may be confusing at first. The messages will be
illustrated using this example program:

</p><pre class="lisp">     (defmacro zoq (x)
       `(roq (ploq (+ ,x 3))))
     
     (defun foo (y)
       (declare (symbol y))
       (zoq y))
</pre>
   <p>The main problem with this program is that it is trying to add
<code>3</code> to a symbol. Note also that the functions <code>roq</code> and
<code>ploq</code> aren't defined anywhere.

</p><ul class="menu">
<li><a accesskey="1" href="#The-Parts-of-a-Compiler-Diagnostic">The Parts of a Compiler Diagnostic</a>
</li><li><a accesskey="2" href="#The-Original-and-Actual-Source">The Original and Actual Source</a>
</li><li><a accesskey="3" href="#The-Processing-Path">The Processing Path</a>
</li></ul>

<div class="node">
<a name="The-Parts-of-a-Compiler-Diagnostic"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#The-Original-and-Actual-Source">The Original and Actual Source</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Understanding-Compiler-Diagnostics">Understanding Compiler Diagnostics</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h5 class="subsubsection">4.1.3.1 The Parts of a Compiler Diagnostic</h5>

<p>When processing this program, the compiler will produce this warning:

</p><pre class="example">     ; file: /tmp/foo.lisp
     ; in: DEFUN FOO
     ;     (ZOQ Y)
     ; --&gt; ROQ PLOQ
     ; ==&gt;
     ;   (+ Y 3)
     ;
     ; caught WARNING:
     ;   Asserted type NUMBER conflicts with derived type (VALUES SYMBOL &amp;OPTIONAL).
</pre>
   <p>In this example we see each of the six possible parts of a compiler
diagnostic:

     </p><ol start="1" type="1">

     <li><a name="index-g_t_0040cl_007bwith_002dcompilation_002dunit_007d-32"></a>‘<samp><span class="samp">file: /tmp/foo.lisp</span></samp>’ This is the name of the file that the
compiler read the relevant code from.  The file name is displayed
because it may not be immediately obvious when there is an error
during compilation of a large system, especially when
<code>with-compilation-unit</code> is used to delay undefined warnings.

     </li><li>‘<samp><span class="samp">in: DEFUN FOO</span></samp>’ This is the definition top level form responsible
for the diagnostic. It is obtained by taking the first two elements of
the enclosing form whose first element is a symbol beginning with
“‘<samp><span class="samp">def</span></samp>’”. If there is no such enclosing “‘<samp><span class="samp">def</span></samp>’” form,
then the outermost form is used. If there are multiple ‘<samp><span class="samp">def</span></samp>’
forms, then they are all printed from the outside in, separated by
‘<samp><span class="samp">=&gt;</span></samp>’'s. In this example, the problem was in the <code>defun</code> for
<code>foo</code>.

     </li><li><a name="index-Original-Source-33"></a>‘<samp><span class="samp">(ZOQ Y)</span></samp>’ This is the <dfn>original source</dfn> form responsible for
the diagnostic. Original source means that the form directly appeared
in the original input to the compiler, i.e. in the lambda passed to
<code>compile</code> or in the top level form read from the source file. In
this example, the expansion of the <code>zoq</code> macro was responsible
for the message.

     </li><li><a name="index-Processing-Path-34"></a>‘<samp><span class="samp">--&gt; ROQ PLOQ</span></samp>’ This is the <dfn>processing path</dfn> that the
compiler used to produce the code that caused the message to be
emitted. The processing path is a representation of the evaluated
forms enclosing the actual source that the compiler encountered when
processing the original source. The path is the first element of each
form, or the form itself if the form is not a list. These forms result
from the expansion of macros or source-to-source transformation done
by the compiler. In this example, the enclosing evaluated forms are
the calls to <code>roq</code> and <code>ploq</code>. These calls resulted from the
expansion of the <code>zoq</code> macro.

     </li><li><a name="index-Actual-Source-35"></a>‘<samp><span class="samp">==&gt; (+ Y 3)</span></samp>’ This is the <dfn>actual source</dfn> responsible for the
diagnostic. If the actual source appears in the explanation, then we
print the next enclosing evaluated form, instead of printing the
actual source twice. (This is the form that would otherwise have been
the last form of the processing path.) In this example, the problem is
with the evaluation of the reference to the variable <code>y</code>.

     </li><li>‘<samp><span class="samp">caught WARNING: Asserted type NUMBER conflicts with derived type
(VALUES SYMBOL &amp;OPTIONAL).</span></samp>’  This is the <dfn>explanation</dfn> of the
problem. In this example, the problem is that, while the call to
<code>+</code> requires that its arguments are all of type <code>number</code>,
the compiler has derived that <code>y</code> will evaluate to a
<code>symbol</code>.  Note that ‘<samp><span class="samp">(VALUES SYMBOL &amp;OPTIONAL)</span></samp>’ expresses
that <code>y</code> evaluates to precisely one value.

        </li></ol>

   <p>Note that each part of the message is distinctively marked:

     </p><ul>
<li> ‘<samp><span class="samp">file:</span></samp>’ and ‘<samp><span class="samp">in:</span></samp>’ mark the file and definition,
respectively.

     </li><li>The original source is an indented form with no prefix.

     </li><li>Each line of the processing path is prefixed with ‘<samp><span class="samp">--&gt;</span></samp>’

     </li><li>The actual source form is indented like the original source, but is
marked by a preceding ‘<samp><span class="samp">==&gt;</span></samp>’ line. 
<!-- no it isn't. -->

     </li><li>The explanation is prefixed with the diagnostic severity, which can be
‘<samp><span class="samp">caught ERROR:</span></samp>’, ‘<samp><span class="samp">caught WARNING:</span></samp>’, ‘<samp><span class="samp">caught
STYLE-WARNING:</span></samp>’, or ‘<samp><span class="samp">note:</span></samp>’.

   </li></ul>

   <p>Each part of the message is more specific than the preceding one. If
consecutive messages are for nearby locations, then the front part of
the messages would be the same. In this case, the compiler omits as
much of the second message as in common with the first. For example:

</p><pre class="example">     ; file: /tmp/foo.lisp
     ; in: DEFUN FOO
     ;     (ZOQ Y)
     ; --&gt; ROQ
     ; ==&gt;
     ;   (PLOQ (+ Y 3))
     ;
     ; caught STYLE-WARNING:
     ;   undefined function: PLOQ
     
     ; ==&gt;
     ;   (ROQ (PLOQ (+ Y 3)))
     ;
     ; caught STYLE-WARNING:
     ;   undefined function: ROQ
</pre>
   <!-- fixing that weird blank line might be good -->
   <p>In this example, the file, definition and original source are
identical for the two messages, so the compiler omits them in the
second message. If consecutive messages are entirely identical, then
the compiler prints only the first message, followed by: ‘<samp><span class="samp">[Last
message occurs </span><var>repeats</var><span class="samp"> times]</span></samp>’ where <var>repeats</var> is the number
of times the message was given.

   </p><p>If the source was not from a file, then no file line is printed. If
the actual source is the same as the original source, then the
processing path and actual source will be omitted. If no forms
intervene between the original source and the actual source, then the
processing path will also be omitted.

</p><div class="node">
<a name="The-Original-and-Actual-Source"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#The-Processing-Path">The Processing Path</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#The-Parts-of-a-Compiler-Diagnostic">The Parts of a Compiler Diagnostic</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Understanding-Compiler-Diagnostics">Understanding Compiler Diagnostics</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h5 class="subsubsection">4.1.3.2 The Original and Actual Source</h5>

<p><a name="index-Original-Source-36"></a><a name="index-Actual-Source-37"></a>
The <em>original source</em> displayed will almost always be a list. If
the actual source for an message is a symbol, the original source will
be the immediately enclosing evaluated list form. So even if the
offending symbol does appear in the original source, the compiler will
print the enclosing list and then print the symbol as the actual
source (as though the symbol were introduced by a macro.)

   </p><p>When the <em>actual source</em> is displayed (and is not a symbol), it
will always be code that resulted from the expansion of a macro or a
source-to-source compiler optimization. This is code that did not
appear in the original source program; it was introduced by the
compiler.

   </p><p>Keep in mind that when the compiler displays a source form in an
diagnostic message, it always displays the most specific (innermost)
responsible form. For example, compiling this function

</p><pre class="lisp">     (defun bar (x)
       (let (a)
         (declare (fixnum a))
         (setq a (foo x))
         a))
</pre>
   <p>gives this error message

</p><pre class="example">     ; file: /tmp/foo.lisp
     ; in: DEFUN BAR
     ;     (LET (A)
     ;     (DECLARE (FIXNUM A))
     ;     (SETQ A (FOO X))
     ;     A)
     ;
     ; caught WARNING:
     ;   Asserted type FIXNUM conflicts with derived type (VALUES NULL &amp;OPTIONAL).
</pre>
   <p>This message is not saying “there is a problem somewhere in this
<code>let</code>” – it is saying that there is a problem with the
<code>let</code> itself. In this example, the problem is that <code>a</code>'s
<code>nil</code> initial value is not a <code>fixnum</code>.

</p><div class="node">
<a name="The-Processing-Path"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#The-Original-and-Actual-Source">The Original and Actual Source</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Understanding-Compiler-Diagnostics">Understanding Compiler Diagnostics</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h5 class="subsubsection">4.1.3.3 The Processing Path</h5>

<p><a name="index-Processing-Path-38"></a><a name="index-Macroexpansion-39"></a><a name="index-Source_002dto_002dsource-transformation-40"></a>
The processing path is mainly useful for debugging macros, so if you
don't write macros, you can probably ignore it. Consider this example:

</p><pre class="lisp">     (defun foo (n)
       (dotimes (i n *undefined*)))
</pre>
   <p>Compiling results in this error message:

</p><pre class="example">     ; in: DEFUN FOO
     ;     (DOTIMES (I N *UNDEFINED*))
     ; --&gt; DO BLOCK LET TAGBODY RETURN-FROM
     ; ==&gt;
     ;   (PROGN *UNDEFINED*)
     ;
     ; caught WARNING:
     ;   undefined variable: *UNDEFINED*
</pre>
   <p>Note that <code>do</code> appears in the processing path. This is because
<code>dotimes</code> expands into:

</p><pre class="lisp">     (do ((i 0 (1+ i)) (#:g1 n))
         ((&gt;= i #:g1) *undefined*)
       (declare (type unsigned-byte i)))
</pre>
   <p>The rest of the processing path results from the expansion of
<code>do</code>:

</p><pre class="lisp">     (block nil
       (let ((i 0) (#:g1 n))
         (declare (type unsigned-byte i))
         (tagbody (go #:g3)
           #:g2    (psetq i (1+ i))
           #:g3    (unless (&gt;= i #:g1) (go #:g2))
           (return-from nil (progn *undefined*)))))
</pre>
   <p>In this example, the compiler descended into the <code>block</code>,
<code>let</code>, <code>tagbody</code> and <code>return-from</code> to reach the
<code>progn</code> printed as the actual source. This is a place where the
“actual source appears in explanation” rule was applied. The
innermost actual source form was the symbol <code>*undefined*</code> itself,
but that also appeared in the explanation, so the compiler backed out
one level.

</p><div class="node">
<a name="Handling-of-Types"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Compiler-Policy">Compiler Policy</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Diagnostic-Messages">Diagnostic Messages</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler">Compiler</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">4.2 Handling of Types</h3>

<p>One of the most important features of the SBCL compiler (similar to
the original CMUCL compiler, also known as <dfn>Python</dfn>) is its fairly
sophisticated understanding of the Common Lisp type system and its
conservative approach to the implementation of type declarations.

   </p><p>These two features reward the use of type declarations throughout
development, even when high performance is not a concern. Also, as
discussed in the chapter on performance (see <a href="#Efficiency">Efficiency</a>), the use
of appropriate type declarations can be very important for performance
as well.

   </p><p><a name="index-g_t_0040cl_007bsatisfies_007d-41"></a>The SBCL compiler also has a greater knowledge of the Common Lisp
type system than other compilers. Support is incomplete only for types
involving the <code>satisfies</code> type specifier.

<!-- <!- FIXME: See also sections \ref{advanced-type-stuff} -->
<!-- and \ref{type-inference}, once we snarf them from the -->
<!-- CMU CL manual. -> -->
<!-- Also see my paper on improving Baker, when I get round to it. -->
<!-- Whose paper? -->
</p><ul class="menu">
<li><a accesskey="1" href="#Declarations-as-Assertions">Declarations as Assertions</a>
</li><li><a accesskey="2" href="#Precise-Type-Checking">Precise Type Checking</a>
</li><li><a accesskey="3" href="#Getting-Existing-Programs-to-Run">Getting Existing Programs to Run</a>
</li><li><a accesskey="4" href="#Implementation-Limitations">Implementation Limitations</a>
</li></ul>

<div class="node">
<a name="Declarations-as-Assertions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Precise-Type-Checking">Precise Type Checking</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Handling-of-Types">Handling of Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.2.1 Declarations as Assertions</h4>

<p><a name="index-Safety-optimization-quality-42"></a>
The SBCL compiler treats type declarations differently from most other
Lisp compilers. Under default compilation policy the compiler doesn't
blindly believe type declarations, but considers them assertions about
the program that should be checked: all type declarations that have
not been proven to always hold are asserted at runtime.

   </p><blockquote>
<em>Remaining bugs in the compiler's handling of types unfortunately
provide some exceptions to this rule, see <a href="#Implementation-Limitations">Implementation Limitations</a>.</em>
</blockquote>

   <p>CLOS slot types form a notable exception. Types declared using the
<code>:type</code> slot option in <code>defclass</code> are asserted if and only
if the class was defined in <em>safe code</em> and the slot access
location is in <em>safe code</em> as well. This laxness does not pose
any internal consistency issues, as the CLOS slot types are not
available for the type inferencer, nor do CLOS slot types provide any
efficiency benefits.

   </p><p>There are three type checking policies available in SBCL, selectable
via <code>optimize</code> declarations.

     </p><dl>
<!-- FIXME: This should be properly integrated with general policy -->
<!-- stuff, once that gets cleaned up. -->

     <dt><strong>Full Type Checks</strong></dt><dd>All declarations are considered assertions to be checked at runtime,
and all type checks are precise. The default compilation policy
provides full type checks.

     <p>Used when <code>(or (&gt;= safety 2) (&gt;= safety speed 1))</code>.

     <br></p></dd><dt><strong>Weak Type Checks</strong></dt><dd>Declared types may be simplified into faster to check supertypes: for
example, <code>(or (integer -17 -7) (integer 7 17))</code> is simplified
into <code>(integer -17 17)</code>.

     <p><strong>Note</strong>: it is relatively easy to corrupt the heap when weak
type checks are used if the program contains type-errors.

     </p><p>Used when <code>(and (&lt; safety 2) (&lt; safety speed))</code>

     <br></p></dd><dt><strong>No Type Checks</strong></dt><dd>All declarations are believed without assertions. Also disables
argument count and array bounds checking.

     <p><strong>Note</strong>: any type errors in code where type checks are not
performed are liable to corrupt the heap.

     </p><p>Used when <code>(= safety 0)</code>.

   </p></dd></dl>

<div class="node">
<a name="Precise-Type-Checking"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Getting-Existing-Programs-to-Run">Getting Existing Programs to Run</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Declarations-as-Assertions">Declarations as Assertions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Handling-of-Types">Handling of Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.2.2 Precise Type Checking</h4>

<p><a name="index-Precise-type-checking-43"></a><a name="index-Type-checking_002c-precise-44"></a>
Precise checking means that the check is done as though <code>typep</code>
had been called with the exact type specifier that appeared in the
declaration.

   </p><p>If a variable is declared to be <code>(integer 3 17)</code> then its value
must always be an integer between <code>3</code> and <code>17</code>. If multiple
type declarations apply to a single variable, then all the
declarations must be correct; it is as though all the types were
intersected producing a single <code>and</code> type specifier.

   </p><p>To gain maximum benefit from the compiler's type checking, you should
always declare the types of function arguments and structure slots as
precisely as possible. This often involves the use of <code>or</code>,
<code>member</code>, and other list-style type specifiers.

</p><div class="node">
<a name="Getting-Existing-Programs-to-Run"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Implementation-Limitations">Implementation Limitations</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Precise-Type-Checking">Precise Type Checking</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Handling-of-Types">Handling of Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.2.3 Getting Existing Programs to Run</h4>

<p><a name="index-Existing-programs_002c-to-run-45"></a><a name="index-Types_002c-portability-46"></a><a name="index-Compatibility-with-other-Lisps-47"></a><!-- (should also have an entry in the non-ANSI-isms section)-> -->

   </p><p>Since SBCL's compiler does much more comprehensive type checking than
most Lisp compilers, SBCL may detect type errors in programs that have
been debugged using other compilers. These errors are mostly incorrect
declarations, although compile-time type errors can find actual bugs
if parts of the program have never been tested.

   </p><p>Some incorrect declarations can only be detected by run-time type
checking. It is very important to initially compile a program with
full type checks (high <code>safety</code> optimization) and then test this
safe version. After the checking version has been tested, then you can
consider weakening or eliminating type checks.  <em>This applies
even to previously debugged programs,</em> because the SBCL compiler does
much more type inference than other Common Lisp compilers, so an
incorrect declaration can do more damage.

   </p><p>The most common problem is with variables whose constant initial value
doesn't match the type declaration. Incorrect constant initial values
will always be flagged by a compile-time type error, and they are
simple to fix once located. Consider this code fragment:

</p><pre class="lisp">     (prog (foo)
       (declare (fixnum foo))
       (setq foo ...)
       ...)
</pre>
   <p>Here <code>foo</code> is given an initial value of <code>nil</code>, but is
declared to be a <code>fixnum</code>.  Even if it is never read, the initial
value of a variable must match the declared type.  There are two ways
to fix this problem. Change the declaration

</p><pre class="lisp">     (prog (foo)
       (declare (type (or fixnum null) foo))
       (setq foo ...)
       ...)
</pre>
   <p>or change the initial value

</p><pre class="lisp">     (prog ((foo 0))
       (declare (fixnum foo))
       (setq foo ...)
       ...)
</pre>
   <p>It is generally preferable to change to a legal initial value rather
than to weaken the declaration, but sometimes it is simpler to weaken
the declaration than to try to make an initial value of the
appropriate type.

   </p><p>Another declaration problem occasionally encountered is incorrect
declarations on <code>defmacro</code> arguments. This can happen when a
function is converted into a macro. Consider this macro:

</p><pre class="lisp">     (defmacro my-1+ (x)
       (declare (fixnum x))
       `(the fixnum (1+ ,x)))
</pre>
   <p>Although legal and well-defined Common Lisp code, this meaning of this
definition is almost certainly not what the writer intended. For
example, this call is illegal:

</p><pre class="lisp">     (my-1+ (+ 4 5))
</pre>
   <p>This call is illegal because the argument to the macro is <code>(+ 4
5)</code>, which is a <code>list</code>, not a <code>fixnum</code>.  Because of macro
semantics, it is hardly ever useful to declare the types of macro
arguments.  If you really want to assert something about the type of
the result of evaluating a macro argument, then put a <code>the</code> in
the expansion:

</p><pre class="lisp">     (defmacro my-1+ (x)
       `(the fixnum (1+ (the fixnum ,x))))
</pre>
   <p>In this case, it would be stylistically preferable to change this
macro back to a function and declare it inline. 
<!-- <!-FIXME: <xref>inline-expansion, once we crib the -->
<!-- relevant text from the CMU CL manual.-> -->

   </p><p>Some more subtle problems are caused by incorrect declarations that
can't be detected at compile time.  Consider this code:

</p><pre class="lisp">     (do ((pos 0 (position #\a string :start (1+ pos))))
       ((null pos))
       (declare (fixnum pos))
       ...)
</pre>
   <p>Although <code>pos</code> is almost always a <code>fixnum</code>, it is <code>nil</code>
at the end of the loop. If this example is compiled with full type
checks (the default), then running it will signal a type error at the
end of the loop. If compiled without type checks, the program will go
into an infinite loop (or perhaps <code>position</code> will complain
because <code>(1+ nil)</code> isn't a sensible start.) Why? Because if you
compile without type checks, the compiler just quietly believes the
type declaration. Since the compiler believes that <code>pos</code> is
always a <code>fixnum</code>, it believes that <code>pos</code> is never
<code>nil</code>, so <code>(null pos)</code> is never true, and the loop exit test
is optimized away. Such errors are sometimes flagged by unreachable
code notes, but it is still important to initially compile and test
any system with full type checks, even if the system works fine when
compiled using other compilers.

   </p><p>In this case, the fix is to weaken the type declaration to <code>(or
fixnum null)</code> <a rel="footnote" href="#fn-2" name="fnd-2"><sup>2</sup></a>.

   </p><p>Note that there is usually little performance penalty for weakening a
declaration in this way. Any numeric operations in the body can still
assume that the variable is a <code>fixnum</code>, since <code>nil</code> is not a
legal numeric argument. Another possible fix would be to say:

</p><pre class="lisp">     (do ((pos 0 (position #\a string :start (1+ pos))))
         ((null pos))
       (let ((pos pos))
         (declare (fixnum pos))
         ...))
</pre>
   <p>This would be preferable in some circumstances, since it would allow a
non-standard representation to be used for the local <code>pos</code>
variable in the loop body. 
<!-- <!- FIXME: <xref>ND-variables, once we crib the text from the -->
<!-- CMU CL manual. -> -->

</p><div class="node">
<a name="Implementation-Limitations"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Getting-Existing-Programs-to-Run">Getting Existing Programs to Run</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Handling-of-Types">Handling of Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.2.4 Implementation Limitations</h4>

<p>Ideally, the compiler would consider <em>all</em> type declarations to
be assertions, so that adding type declarations to a program, no
matter how incorrect they might be, would <em>never</em> cause undefined
behavior. However, the compiler is known to fall short of this goal in
two areas:

     </p><ul>
<li><em>Proclaimed</em> constraints on argument and result types of a
function are supposed to be checked by the function. If the function
type is proclaimed before function definition, type checks are
inserted by the compiler, but the standard allows the reversed order,
in which case the compiler will trust the declaration.

     </li><li>The compiler cannot check types of an unknown number of values; if the
number of generated values is unknown, but the number of consumed is
known, only consumed values are checked.

     <p>For example,

     </p><pre class="lisp">          (defun foo (x)
            (the integer (bar x)))
</pre>
     <p>causes the following compiler diagnostic to be emitted:

     </p><pre class="example">          ; note: type assertion too complex to check:
          ;  (VALUES INTEGER &amp;REST T).
</pre>
     <p>A partial workaround is instead write:

     </p><pre class="lisp">          (defun foo (x)
            (the (values integer &amp;optional) (bar x)))
</pre>
     </li></ul>

   <p>These are important issues, but are not necessarily easy to fix, so
they may, alas, remain in the system for a while.

</p><div class="node">
<a name="Compiler-Policy"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Compiler-Errors">Compiler Errors</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Handling-of-Types">Handling of Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler">Compiler</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">4.3 Compiler Policy</h3>

<p>Compiler policy is controlled by the <code>optimize</code> declaration,
supporting all ANSI optimization qualities (<code>debug</code>,
<code>safety</code>, <code>space</code>, and <code>speed</code>).<a rel="footnote" href="#fn-3" name="fnd-3"><sup>3</sup></a>

   </p><p>For effects of various optimization qualities on type-safety and
debuggability see <a href="#Declarations-as-Assertions">Declarations as Assertions</a> and <a href="#Debugger-Policy-Control">Debugger Policy Control</a>.

   </p><p>Ordinarily, when the <code>speed</code> quality is high, the compiler emits
notes to notify the programmer about its inability to apply various
optimizations. For selective muffling of these notes See <a href="#Controlling-Verbosity">Controlling Verbosity</a>.

   </p><p>The value of <code>space</code> mostly influences the compiler's decision
whether to inline operations, which tend to increase the size of
programs. Use the value <code>0</code> with caution, since it can cause the
compiler to inline operations so indiscriminately that the net effect
is to slow the program by causing cache misses or even swapping.

<!-- <!- FIXME: old CMU CL compiler policy, should perhaps be adapted -->
<!-- _    for SBCL. (Unfortunately, the CMU CL docs are out of sync with the -->
<!-- _    CMU CL code, so adapting this requires not only reformatting -->
<!-- _    the documentation, but rooting out code rot.) -->
<!-- _ -->
<!-- _<sect2 id="compiler-policy"><title>Compiler Policy</1000 -->
<!-- _  INDEX {policy}{compiler} -->
<!-- _  INDEX compiler policy -->
<!-- _ -->
<!-- _<para>The policy is what tells the compiler <emphasis>how</emphasis> to -->
<!-- _compile a program. This is logically (and often textually) distinct -->
<!-- _from the program itself. Broad control of policy is provided by the -->
<!-- _<parameter>optimize</parameter> declaration; other declarations and variables -->
<!-- _control more specific aspects of compilation. -->
<!-- _ -->
<!-- _\begin{comment} -->
<!-- _* The Optimize Declaration:: -->
<!-- _* The Optimize-Interface Declaration:: -->
<!-- _\end{comment} -->
<!-- _ -->
<!-- _%%\node The Optimize Declaration, The Optimize-Interface Declaration, Compiler Policy, Compiler Policy -->
<!-- _\subsection{The Optimize Declaration} -->
<!-- _\label{optimize-declaration} -->
<!-- _\cindex{optimize declaration} -->
<!-- _\cpsubindex{declarations}{\code{optimize}} -->
<!-- _ -->
<!-- _The \code{optimize} declaration recognizes six different -->
<!-- _\var{qualities}.  The qualities are conceptually independent aspects -->
<!-- _of program performance.  In reality, increasing one quality tends to -->
<!-- _have adverse effects on other qualities.  The compiler compares the -->
<!-- _relative values of qualities when it needs to make a trade-off; i.e., -->
<!-- _if \code{speed} is greater than \code{safety}, then improve speed at -->
<!-- _the cost of safety. -->
<!-- _ -->
<!-- _The default for all qualities (except \code{debug}) is \code{1}. -->
<!-- _Whenever qualities are equal, ties are broken according to a broad -->
<!-- _idea of what a good default environment is supposed to be.  Generally -->
<!-- _this downplays \code{speed}, \code{compile-speed} and \code{space} in -->
<!-- _favor of \code{safety} and \code{debug}.  Novice and casual users -->
<!-- _should stick to the default policy.  Advanced users often want to -->
<!-- _improve speed and memory usage at the cost of safety and -->
<!-- _debuggability. -->
<!-- _ -->
<!-- _If the value for a quality is \code{0} or \code{3}, then it may have a -->
<!-- _special interpretation.  A value of \code{0} means ``totally -->
<!-- _unimportant'', and a \code{3} means ``ultimately important.''  These -->
<!-- _extreme optimization values enable ``heroic'' compilation strategies -->
<!-- _that are not always desirable and sometimes self-defeating. -->
<!-- _Specifying more than one quality as \code{3} is not desirable, since -->
<!-- _it doesn't tell the compiler which quality is most important. -->
<!-- _ -->
<!-- _ -->
<!-- _These are the optimization qualities: -->
<!-- _\begin{Lentry} -->
<!-- _ -->
<!-- _\item[\code{speed}] \cindex{speed optimization quality}How fast the -->
<!-- _  program should is run.  \code{speed 3} enables some optimizations -->
<!-- _  that hurt debuggability. -->
<!-- _ -->
<!-- _\item[\code{compilation-speed}] \cindex{compilation-speed optimization -->
<!-- _    quality}How fast the compiler should run.  Note that increasing -->
<!-- _  this above \code{safety} weakens type checking. -->
<!-- _ -->
<!-- _\item[\code{space}] \cindex{space optimization quality}How much space -->
<!-- _  the compiled code should take up.  Inline expansion is mostly -->
<!-- _  inhibited when \code{space} is greater than \code{speed}.  A value -->
<!-- _  of \code{0} enables indiscriminate inline expansion.  Wide use of a -->
<!-- _  \code{0} value is not recommended, as it may waste so much space -->
<!-- _  that run time is slowed.  \xlref{inline-expansion} for a discussion -->
<!-- _  of inline expansion. -->
<!-- _ -->
<!-- _\item[\code{debug}] \cindex{debug optimization quality}How debuggable -->
<!-- _  the program should be.  The quality is treated differently from the -->
<!-- _  other qualities: each value indicates a particular level of debugger -->
<!-- _  information; it is not compared with the other qualities. -->
<!-- _  \xlref{debugger-policy} for more details. -->
<!-- _ -->
<!-- _\item[\code{safety}] \cindex{safety optimization quality}How much -->
<!-- _  error checking should be done.  If \code{speed}, \code{space} or -->
<!-- _  \code{compilation-speed} is more important than \code{safety}, then -->
<!-- _  type checking is weakened (\pxlref{weakened-type-checks}).  If -->
<!-- _  \code{safety} if \code{0}, then no run time error checking is done. -->
<!-- _  In addition to suppressing type checks, \code{0} also suppresses -->
<!-- _  argument count checking, unbound-symbol checking and array bounds -->
<!-- _  checks. -->
<!-- _  ... and checking of tag existence in RETURN-FROM and GO. -->
<!-- _ -->
<!-- _\item[\code{extensions:inhibit-warnings}] \cindex{inhibit-warnings -->
<!-- _    optimization quality}This is a CMU extension that determines how -->
<!-- _  little (or how much) diagnostic output should be printed during -->
<!-- _  compilation.  This quality is compared to other qualities to -->
<!-- _  determine whether to print style notes and warnings concerning those -->
<!-- _  qualities.  If \code{speed} is greater than \code{inhibit-warnings}, -->
<!-- _  then notes about how to improve speed will be printed, etc.  The -->
<!-- _  default value is \code{1}, so raising the value for any standard -->
<!-- _  quality above its default enables notes for that quality.  If -->
<!-- _  \code{inhibit-warnings} is \code{3}, then all notes and most -->
<!-- _  non-serious warnings are inhibited.  This is useful with -->
<!-- _  \code{declare} to suppress warnings about unavoidable problems. -->
<!-- _\end{Lentry} -->
<!-- _ -->
<!-- _%%\node The Optimize-Interface Declaration,  , The Optimize Declaration, Compiler Policy -->
<!-- _\subsection{The Optimize-Interface Declaration} -->
<!-- _\label{optimize-interface-declaration} -->
<!-- _\cindex{optimize-interface declaration} -->
<!-- _\cpsubindex{declarations}{\code{optimize-interface}} -->
<!-- _ -->
<!-- _The \code{extensions:optimize-interface} declaration is identical in -->
<!-- _syntax to the \code{optimize} declaration, but it specifies the policy -->
<!-- _used during compilation of code the compiler automatically generates -->
<!-- _to check the number and type of arguments supplied to a function.  It -->
<!-- _is useful to specify this policy separately, since even thoroughly -->
<!-- _debugged functions are vulnerable to being passed the wrong arguments. -->
<!-- _The \code{optimize-interface} declaration can specify that arguments -->
<!-- _should be checked even when the general \code{optimize} policy is -->
<!-- _unsafe. -->
<!-- _ -->
<!-- _Note that this argument checking is the checking of user-supplied -->
<!-- _arguments to any functions defined within the scope of the -->
<!-- _declaration, \code{not} the checking of arguments to \llisp{} -->
<!-- _primitives that appear in those definitions. -->
<!-- _ -->
<!-- _The idea behind this declaration is that it allows the definition of -->
<!-- _functions that appear fully safe to other callers, but that do no -->
<!-- _internal error checking.  Of course, it is possible that arguments may -->
<!-- _be invalid in ways other than having incorrect type.  Functions -->
<!-- _compiled unsafely must still protect themselves against things like -->
<!-- _user-supplied array indices that are out of bounds and improper lists. -->
<!-- _See also the \kwd{context-declarations} option to -->
<!-- _\macref{with-compilation-unit}. -->
<!-- _ -->
<!-- _(end of section on compiler policy) -->
<!-- _-> -->
   </p><p><a name="Function-sb_002dext_003adescribe_002dcompiler_002dpolicy"></a>

</p><div class="defun">
— Function: <b>describe-compiler-policy [sb-ext]</b><var> &amp;optional spec<a name="index-g_t_0040sbext_007bdescribe_002dcompiler_002dpolicy_007d-48"></a></var><br>
<blockquote><p>Print all global optimization settings, augmented by <code>spec</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003arestrict_002dcompiler_002dpolicy"></a>

</p><div class="defun">
— Function: <b>restrict-compiler-policy [sb-ext]</b><var> &amp;optional quality min max<a name="index-g_t_0040sbext_007brestrict_002dcompiler_002dpolicy_007d-49"></a></var><br>
<blockquote><p>Assign a minimum value to an optimization quality. <code>quality</code> is the name of
the optimization quality to restrict, <code>min</code> (defaulting to zero) is the
minimum allowed value, and <code>max</code> (defaults to 3) is the maximum.

        </p><p>Returns the alist describing the current policy restrictions.

        </p><p>If <code>quality</code> is <code>nil</code> or not given, nothing is done.

        </p><p>Otherwise, if <code>min</code> is zero or <code>max</code> is 3 or neither are given, any
existing restrictions of <code>quality</code> are removed.

        </p><p>See also <code>:policy</code> option in <code>with-compilation-unit</code>. 
</p></blockquote></div>

   <p><a name="Macro-common_002dlisp_003awith_002dcompilation_002dunit"></a>

</p><div class="defun">
— Macro: <b>with-compilation-unit [cl]</b><var> options &amp;body body<a name="index-g_t_0040cl_007bwith_002dcompilation_002dunit_007d-50"></a></var><br>
<blockquote><p>Affects compilations that take place within its dynamic extent. It is
intended to be eg. wrapped around the compilation of all files in the same system.

        </p><p>Following options are defined:

          </p><dl>
<dt><code>:override</code><em> Boolean-Form</em></dt><dd>      One of the effects of this form is to delay undefined warnings until the
      end of the form, instead of giving them at the end of each compilation. 
      If <code>override</code> is <code>nil</code> (the default), then the outermost
      <code>with-compilation-unit</code> form grabs the undefined warnings. Specifying
      <code>override</code> true causes that form to grab any enclosed warnings, even if it
      is enclosed by another <code>with-compilation-unit</code>.

          <br></dd><dt><code>:policy</code><em> Optimize-Declaration-Form</em></dt><dd>      Provides dynamic scoping for global compiler optimization qualities and
      restrictions, limiting effects of subsequent <code>optimize</code> proclamations and
      calls to <code>sb-ext:restrict-compiler-policy</code> to the dynamic scope of <code>body</code>.

          <p>If <code>override</code> is false, specified <code>policy</code> is merged with current global
      policy. If <code>override</code> is true, current global policy, including any
      restrictions, is discarded in favor of the specified <code>policy</code>.

          </p><p>Supplying <code>policy</code> <code>nil</code> is equivalent to the option not being supplied at
      all, ie. dynamic scoping of policy does not take place.

          </p><p>This option is an SBCL-specific experimental extension: Interface
      subject to change.

          <br></p></dd><dt><code>:source-namestring</code><em> Namestring-Form</em></dt><dd>      Attaches the value returned by the Namestring-Form to the internal
      debug-source information as the namestring of the source file. Normally
      the namestring of the input-file for <code>compile-file</code> is used: this option
      can be used to provide source-file information for functions compiled
      using <code>compile</code>, or to override the input-file of <code>compile-file</code>.

          <p>If both an outer and an inner <code>with-compilation-unit</code> provide a
      <code>source-namestring</code>, the inner one takes precedence. Unaffected
      by <code>:override</code>.

          </p><p>This is an SBCL-specific extension.

          <br></p></dd><dt><code>:source-plist</code><em> Plist-Form</em></dt><dd>      Attaches the value returned by the Plist-Form to internal debug-source
      information of functions compiled in within the dynamic extent of <code>body</code>.

          <p>Primarily for use by development environments, in order to eg. associate
      function definitions with editor-buffers. Can be accessed using
      <code>sb-introspect:definition-source-plist</code>.

          </p><p>If an outer <code>with-compilation-unit</code> form also provide a <code>source-plist</code>, it
      is appended to the end of the provided <code>source-plist</code>. Unaffected
      by <code>:override</code>.

          </p><p>This is an SBCL-specific extension.

        </p></dd></dl>

        <p>Examples:

     </p><pre class="lisp">            ;; Prevent proclamations from the file leaking, and restrict
            ;; SAFETY to 3 -- otherwise uses the current global policy.
            (with-compilation-unit (:policy '(optimize))
              (restrict-compiler-policy 'safety 3)
              (load "foo.lisp"))
          
            ;; Using default policy instead of the current global one,
            ;; except for DEBUG 3.
            (with-compilation-unit (:policy '(optimize debug)
                                    :override t)
              (load "foo.lisp"))
          
            ;; Same as if :POLICY had not been specified at all: SAFETY 3
            ;; proclamation leaks out from WITH-COMPILATION-UNIT.
            (with-compilation-unit (:policy nil)
              (declaim (optimize safety))
              (load "foo.lisp"))
</pre>
        </blockquote></div>

<div class="node">
<a name="Compiler-Errors"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Open-Coding-and-Inline-Expansion">Open Coding and Inline Expansion</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Compiler-Policy">Compiler Policy</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler">Compiler</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">4.4 Compiler Errors</h3>

<ul class="menu">
<li><a accesskey="1" href="#Type-Errors-at-Compile-Time">Type Errors at Compile Time</a>
</li><li><a accesskey="2" href="#Errors-During-Macroexpansion">Errors During Macroexpansion</a>
</li><li><a accesskey="3" href="#Read-Errors">Read Errors</a>
</li></ul>

<div class="node">
<a name="Type-Errors-at-Compile-Time"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Errors-During-Macroexpansion">Errors During Macroexpansion</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler-Errors">Compiler Errors</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.4.1 Type Errors at Compile Time</h4>

<p><a name="index-Compile-time-type-errors-51"></a><a name="index-Type-checking_002c-at-compile-time-52"></a>
If the compiler can prove at compile time that some portion of the
program cannot be executed without a type error, then it will give a
warning at compile time.

   </p><p>It is possible that the offending code would never actually be
executed at run-time due to some higher level consistency constraint
unknown to the compiler, so a type warning doesn't always indicate an
incorrect program.

   </p><p>For example, consider this code fragment:

</p><pre class="lisp">     (defun raz (foo)
       (let ((x (case foo
                   (:this 13)
                   (:that 9)
                   (:the-other 42))))
         (declare (fixnum x))
         (foo x)))
</pre>
   <p>Compilation produces this warning:

</p><pre class="example">     ; in: DEFUN RAZ
     ;     (CASE FOO (:THIS 13) (:THAT 9) (:THE-OTHER 42))
     ; --&gt; LET COND IF COND IF COND IF
     ; ==&gt;
     ;   (COND)
     ;
     ; caught WARNING:
     ;   This is not a FIXNUM:
     ;   NIL
</pre>
   <p>In this case, the warning means that if <code>foo</code> isn't any of
<code>:this</code>, <code>:that</code> or <code>:the-other</code>, then <code>x</code> will be
initialized to <code>nil</code>, which the <code>fixnum</code> declaration makes
illegal. The warning will go away if <code>ecase</code> is used instead of
<code>case</code>, or if <code>:the-other</code> is changed to <code>t</code>.

   </p><p>This sort of spurious type warning happens moderately often in the
expansion of complex macros and in inline functions. In such cases,
there may be dead code that is impossible to correctly execute. The
compiler can't always prove this code is dead (could never be
executed), so it compiles the erroneous code (which will always signal
an error if it is executed) and gives a warning.

</p><div class="node">
<a name="Errors-During-Macroexpansion"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Read-Errors">Read Errors</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Type-Errors-at-Compile-Time">Type Errors at Compile Time</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler-Errors">Compiler Errors</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.4.2 Errors During Macroexpansion</h4>

<p><a name="index-Macroexpansion_002c-errors-during-53"></a>
The compiler handles errors that happen during macroexpansion, turning
them into compiler errors. If you want to debug the error (to debug a
macro), you can set <code>*break-on-signals*</code> to <code>error</code>. For
example, this definition:

</p><pre class="lisp">     (defun foo (e l)
       (do ((current l (cdr current))
            ((atom current) nil))
           (when (eq (car current) e) (return current))))
</pre>
   <p>gives this error:

</p><pre class="example">     ; in: DEFUN FOO
     ;     (DO ((CURRENT L (CDR CURRENT))
     ;        ((ATOM CURRENT) NIL))
     ;       (WHEN (EQ (CAR CURRENT) E) (RETURN CURRENT)))
     ;
     ; caught ERROR:
     ;   (in macroexpansion of (DO # #))
     ;   (hint: For more precise location, try *BREAK-ON-SIGNALS*.)
     ;   DO step variable is not a symbol: (ATOM CURRENT)
</pre>
   <div class="node">
<a name="Read-Errors"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Errors-During-Macroexpansion">Errors During Macroexpansion</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler-Errors">Compiler Errors</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">4.4.3 Read Errors</h4>

<p><a name="index-Read-errors_002c-compiler-54"></a>
SBCL's compiler does not attempt to recover from read errors when
reading a source file, but instead just reports the offending
character position and gives up on the entire source file.

</p><div class="node">
<a name="Open-Coding-and-Inline-Expansion"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Interpreter">Interpreter</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Compiler-Errors">Compiler Errors</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler">Compiler</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">4.5 Open Coding and Inline Expansion</h3>

<p><a name="index-Open_002dcoding-55"></a><a name="index-Inline-expansion-56"></a><a name="index-Static-functions-57"></a>
Since Common Lisp forbids the redefinition of standard functions, the
compiler can have special knowledge of these standard functions
embedded in it. This special knowledge is used in various ways (open
coding, inline expansion, source transformation), but the implications
to the user are basically the same:

     </p><ul>
<li>Attempts to redefine standard functions may be frustrated, since the
function may never be called. Although it is technically illegal to
redefine standard functions, users sometimes want to implicitly
redefine these functions when they are debugging using the
<code>trace</code> macro.  Special-casing of standard functions can be
inhibited using the <code>notinline</code> declaration, but even then some
phases of analysis such as type inferencing are applied by the
compiler.

     </li><li>The compiler can have multiple alternate implementations of standard
functions that implement different trade-offs of speed, space and
safety.  This selection is based on the compiler policy, <a href="#Compiler-Policy">Compiler Policy</a>.

   </li></ul>

   <p>When a function call is <em>open coded</em>, inline code whose effect is
equivalent to the function call is substituted for that function
call. When a function call is <em>closed coded</em>, it is usually left
as is, although it might be turned into a call to a different function
with different arguments. As an example, if <code>nthcdr</code> were to be
open coded, then

</p><pre class="lisp">     (nthcdr 4 foobar)
</pre>
   <p>might turn into

</p><pre class="lisp">     (cdr (cdr (cdr (cdr foobar))))
</pre>
   <p>or even

</p><pre class="lisp">     (do ((i 0 (1+ i))
       (list foobar (cdr foobar)))
       ((= i 4) list))
</pre>
   <p>If <code>nth</code> is closed coded, then

</p><pre class="lisp">     (nth x l)
</pre>
   <p>might stay the same, or turn into something like

</p><pre class="lisp">     (car (nthcdr x l))
</pre>
   <p>In general, open coding sacrifices space for speed, but some functions
(such as <code>car</code>) are so simple that they are always
open-coded. Even when not open-coded, a call to a standard function
may be transformed into a different function call (as in the last
example) or compiled as <em>static call</em>. Static function call uses
a more efficient calling convention that forbids redefinition.

</p><div class="node">
<a name="Interpreter"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Open-Coding-and-Inline-Expansion">Open Coding and Inline Expansion</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Compiler">Compiler</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">4.6 Interpreter</h3>

<p><a name="index-Interpreter-58"></a><a name="index-g_t_0040cl_007beval_007d-59"></a><a name="index-g_t_0040sbext_007b_0040earmuffs_007bevaluator_002dmode_007d_007d-60"></a>
By default SBCL implements <code>eval</code> by calling the native code
compiler.

   </p><p>SBCL also includes an interpreter for use in special cases where using
the compiler is undesirable, for example due to compilation overhead. 
Unlike in some other Lisp implementations, in SBCL interpreted code is
not safer or more debuggable than compiled code.

   </p><p><a name="Variable-sb_002dext_003a_002aevaluator_002dmode_002a"></a>

</p><div class="defun">
— Variable: <b>*evaluator-mode* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bevaluator_002dmode_007d_007d-61"></a></var><br>
<blockquote><p>Toggle between different evaluator implementations. If set to <code>:compile</code>,
an implementation of <code>eval</code> that calls the compiler will be used. If set
to <code>:interpret</code>, an interpreter will be used. 
</p></blockquote></div>

<div class="node">
<a name="Debugger"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Efficiency">Efficiency</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Compiler">Compiler</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">5 Debugger</h2>

<p><a name="index-Debugger-62"></a>
This chapter documents the debugging facilities of SBCL, including
the debugger, single-stepper and <code>trace</code>, and the effect of
<code>(optimize debug)</code> declarations.

</p><ul class="menu">
<li><a accesskey="1" href="#Debugger-Entry">Debugger Entry</a>
</li><li><a accesskey="2" href="#Debugger-Command-Loop">Debugger Command Loop</a>
</li><li><a accesskey="3" href="#Stack-Frames">Stack Frames</a>
</li><li><a accesskey="4" href="#Variable-Access">Variable Access</a>
</li><li><a accesskey="5" href="#Source-Location-Printing">Source Location Printing</a>
</li><li><a accesskey="6" href="#Debugger-Policy-Control">Debugger Policy Control</a>
</li><li><a accesskey="7" href="#Exiting-Commands">Exiting Commands</a>
</li><li><a accesskey="8" href="#Information-Commands">Information Commands</a>
</li><li><a accesskey="9" href="#Function-Tracing">Function Tracing</a>
</li><li><a href="#Single-Stepping">Single Stepping</a>
</li><li><a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a>
</li></ul>

<div class="node">
<a name="Debugger-Entry"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Debugger-Command-Loop">Debugger Command Loop</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.1 Debugger Entry</h3>

<ul class="menu">
<li><a accesskey="1" href="#Debugger-Banner">Debugger Banner</a>
</li><li><a accesskey="2" href="#Debugger-Invocation">Debugger Invocation</a>
</li></ul>

<div class="node">
<a name="Debugger-Banner"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Debugger-Invocation">Debugger Invocation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger-Entry">Debugger Entry</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.1.1 Debugger Banner</h4>

<p>When you enter the debugger, it looks something like this:

</p><pre class="example">     debugger invoked on a TYPE-ERROR in thread 11184:
       The value 3 is not of type LIST.
     
     You can type HELP for debugger help, or (SB-EXT:QUIT) to exit from SBCL.
     
     restarts (invokable by number or by possibly-abbreviated name):
       0: [ABORT   ] Reduce debugger level (leaving debugger, returning to toplevel).
       1: [TOPLEVEL] Restart at toplevel READ/EVAL/PRINT loop.
     (CAR 1 3)
     0]
</pre>
   <p>The first group of lines describe what the error was that put us in
the debugger.  In this case <code>car</code> was called on <code>3</code>, causing
a <code>type-error</code>.

   </p><p>This is followed by the “beginner help line”, which appears only if
<code>sb-debug:*debug-beginner-help-p*</code> is true (default).

   </p><p>Next comes a listing of the active restart names, along with their
descriptions – the ways we can restart execution after this error. In
this case, both options return to top-level. Restarts can be selected
by entering the corresponding number or name.

   </p><p>The current frame appears right underneath the restarts, immediately
followed by the debugger prompt.

</p><div class="node">
<a name="Debugger-Invocation"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Debugger-Banner">Debugger Banner</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger-Entry">Debugger Entry</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.1.2 Debugger Invocation</h4>

<p>The debugger is invoked when:

     </p><ul>
<li><code>error</code> is called, and the condition it signals is not handled.

     </li><li><code>break</code> is called, or <code>signal</code> is called with a condition
that matches the current <code>*break-on-signals*</code>.

     </li><li>the debugger is explicitly entered with the <code>invoke-debugger</code>
function.

   </li></ul>

   <p>When the debugger is invoked by a condition, ANSI mandates that the
value of <code>*debugger-hook*</code>, if any, be called with two arguments:
the condition that caused the debugger to be invoked and the previous
value of <code>*debugger-hook*</code>. When this happens,
<code>*debugger-hook*</code> is bound to NIL to prevent recursive errors. 
However, ANSI also mandates that <code>*debugger-hook*</code> not be invoked
when the debugger is to be entered by the <code>break</code> function. For
users who wish to provide an alternate debugger interface (and thus
catch <code>break</code> entries into the debugger), SBCL provides
<code>sb-ext:*invoke-debugger-hook*</code>, which is invoked during any
entry into the debugger.

   </p><p><a name="Variable-sb_002dext_003a_002ainvoke_002ddebugger_002dhook_002a"></a>

</p><div class="defun">
— Variable: <b>*invoke-debugger-hook* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007binvoke_002ddebugger_002dhook_007d_007d-63"></a></var><br>
<blockquote><p>This is either <code>nil</code> or a designator for a function of two arguments,
   to be run when the debugger is about to be entered.  The function is
   run with <code>*invoke-debugger-hook*</code> bound to <code>nil</code> to minimize recursive
   errors, and receives as arguments the condition that triggered
   debugger entry and the previous value of <code>*invoke-debugger-hook*</code>

        </p><p>This mechanism is an <code>sbcl</code> extension similar to the standard <code>*debugger-hook*</code>. 
   In contrast to <code>*debugger-hook*</code>, it is observed by <code>invoke-debugger</code> even when
   called by <code>break</code>. 
</p></blockquote></div>

<div class="node">
<a name="Debugger-Command-Loop"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Stack-Frames">Stack Frames</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Debugger-Entry">Debugger Entry</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.2 Debugger Command Loop</h3>

<p>The debugger is an interactive read-eval-print loop much like the
normal top level, but some symbols are interpreted as debugger
commands instead of being evaluated. A debugger command starts with
the symbol name of the command, possibly followed by some arguments on
the same line. Some commands prompt for additional input. Debugger
commands can be abbreviated by any unambiguous prefix: <samp><span class="command">help</span></samp>
can be typed as ‘<samp><span class="samp">h</span></samp>’, ‘<samp><span class="samp">he</span></samp>’, etc.

   </p><p>The package is not significant in debugger commands; any symbol with
the name of a debugger command will work. If you want to show the
value of a variable that happens also to be the name of a debugger
command you can wrap the variable in a <code>progn</code> to hide it from
the command loop.

   </p><p>The debugger prompt is “<var>frame</var><code>]</code>”, where <var>frame</var> is
the number of the current frame.  Frames are numbered starting from
zero at the top (most recent call), increasing down to the bottom. 
The current frame is the frame that commands refer to.

   </p><p>It is possible to override the normal printing behaviour in the
debugger by using the <code>sb-ext:*debug-print-variable-alist*</code>.

   </p><p><a name="Variable-sb_002dext_003a_002adebug_002dprint_002dvariable_002dalist_002a"></a>

</p><div class="defun">
— Variable: <b>*debug-print-variable-alist* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bdebug_002dprint_002dvariable_002dalist_007d_007d-64"></a></var><br>
<blockquote><p>an association list describing new bindings for special variables
to be used within the debugger. Eg.

     </p><pre class="lisp">           ((*PRINT-LENGTH* . 10) (*PRINT-LEVEL* . 6) (*PRINT-PRETTY* . NIL))
</pre>
        <p>The variables in the <code>car</code> positions are bound to the values in the <code>cdr</code>
during the execution of some debug commands. When evaluating arbitrary
expressions in the debugger, the normal values of the printer control
variables are in effect.

        </p><p>Initially empty, <code>*debug-print-variable-alist*</code> is typically used to
provide bindings for printer control variables. 
</p></blockquote></div>

<div class="node">
<a name="Stack-Frames"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Variable-Access">Variable Access</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Debugger-Command-Loop">Debugger Command Loop</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.3 Stack Frames</h3>

<p><a name="index-Stack-frames-65"></a>
A <dfn>stack frame</dfn> is the run-time representation of a call to a
function; the frame stores the state that a function needs to remember
what it is doing.  Frames have:

     </p><ul>
<li><dfn>variables</dfn> (see <a href="#Variable-Access">Variable Access</a>), which are the values being operated
on.

     </li><li><dfn>arguments</dfn> to the call (which are really just particularly
interesting variables).

     </li><li>a current source location (see <a href="#Source-Location-Printing">Source Location Printing</a>), which is
the place in the program where the function was running when it
stopped to call another function, or because of an interrupt or error.

   </li></ul>

<ul class="menu">
<li><a accesskey="1" href="#Stack-Motion">Stack Motion</a>
</li><li><a accesskey="2" href="#How-Arguments-are-Printed">How Arguments are Printed</a>
</li><li><a accesskey="3" href="#Function-Names">Function Names</a>
</li><li><a accesskey="4" href="#Debug-Tail-Recursion">Debug Tail Recursion</a>
</li><li><a accesskey="5" href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a>
</li></ul>

<div class="node">
<a name="Stack-Motion"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#How-Arguments-are-Printed">How Arguments are Printed</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stack-Frames">Stack Frames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.3.1 Stack Motion</h4>

<p>These commands move to a new stack frame and print the name of the
function and the values of its arguments in the style of a Lisp
function call:

</p><div class="defun">
— Debugger Command: <b>up</b><var><a name="index-g_t_0040nopkg_007bup_007d-66"></a></var><br>
<blockquote><p>Move up to the next higher frame.  More recent function calls are
considered to be higher on the stack. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>down</b><var><a name="index-g_t_0040nopkg_007bdown_007d-67"></a></var><br>
<blockquote><p>Move down to the next lower frame. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>top</b><var><a name="index-g_t_0040nopkg_007btop_007d-68"></a></var><br>
<blockquote><p>Move to the highest frame, that is, the frame where the debugger was
entered. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>bottom</b><var><a name="index-g_t_0040nopkg_007bbottom_007d-69"></a></var><br>
<blockquote><p>Move to the lowest frame. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>frame</b> [<var>n</var>]<var><a name="index-g_t_0040nopkg_007bframe_007d-70"></a></var><br>
<blockquote><p>Move to the frame with the specified number.  Prompts for the number if not
supplied.  The frame with number 0 is the frame where the debugger
was entered. 
</p></blockquote></div>

<div class="node">
<a name="How-Arguments-are-Printed"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Function-Names">Function Names</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Stack-Motion">Stack Motion</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stack-Frames">Stack Frames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.3.2 How Arguments are Printed</h4>

<p>A frame is printed to look like a function call, but with the actual
argument values in the argument positions.  So the frame for this call
in the source:

</p><pre class="lisp">     (myfun (+ 3 4) 'a)
</pre>
   <p>would look like this:

</p><pre class="example">     (MYFUN 7 A)
</pre>
   <p>All keyword and optional arguments are displayed with their actual
values; if the corresponding argument was not supplied, the value will
be the default.  So this call:

</p><pre class="lisp">     (subseq "foo" 1)
</pre>
   <p>would look like this:

</p><pre class="example">     (SUBSEQ "foo" 1 3)
</pre>
   <p>And this call:

</p><pre class="lisp">     (string-upcase "test case")
</pre>
   <p>would look like this:

</p><pre class="example">     (STRING-UPCASE "test case" :START 0 :END NIL)
</pre>
   <p>The arguments to a function call are displayed by accessing the
argument variables.  Although those variables are initialized to the
actual argument values, they can be set inside the function; in this
case the new value will be displayed.

   </p><p><code>&amp;rest</code> arguments are handled somewhat differently.  The value of
the rest argument variable is displayed as the spread-out arguments to
the call, so:

</p><pre class="lisp">     (format t "~A is a ~A." "This" 'test)
</pre>
   <p>would look like this:

</p><pre class="example">     (FORMAT T "~A is a ~A." "This" 'TEST)
</pre>
   <p>Rest arguments cause an exception to the normal display of keyword
arguments in functions that have both <code>&amp;rest</code> and <code>&amp;key</code>
arguments.  In this case, the keyword argument variables are not
displayed at all; the rest arg is displayed instead.  So for these
functions, only the keywords actually supplied will be shown, and the
values displayed will be the argument values, not values of the
(possibly modified) variables.

   </p><p>If the variable for an argument is never referenced by the function,
it will be deleted.  The variable value is then unavailable, so the
debugger prints ‘<samp><span class="samp">#&lt;unused-arg&gt;</span></samp>’ instead of the value.  Similarly,
if for any of a number of reasons the value of the variable is
unavailable or not known to be available (see <a href="#Variable-Access">Variable Access</a>),
then ‘<samp><span class="samp">#&lt;unavailable-arg&gt;</span></samp>’ will be printed instead of the argument
value.

   </p><p>Note that inline expansion and open-coding affect what frames
are present in the debugger, see <a href="#Debugger-Policy-Control">Debugger Policy Control</a>. 
<!-- FIXME: link here to section about open coding once it exists. -->
<!-- @ref{open-coding} -->

</p><div class="node">
<a name="Function-Names"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Debug-Tail-Recursion">Debug Tail Recursion</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#How-Arguments-are-Printed">How Arguments are Printed</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stack-Frames">Stack Frames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.3.3 Function Names</h4>

<p>If a function is defined by <code>defun</code> it will appear in backtrace
by that name. Functions defined by <code>labels</code> and <code>flet</code> will
appear as <code>(FLET </code><var>name</var><code>)</code> and <code>(LABELS </code><var>name</var><code>)</code> respectively. 
Anonymous lambdas will appear as <code>(LAMDBA </code><var>lambda-list</var><code>)</code>.

</p><ul class="menu">
<li><a accesskey="1" href="#Entry-Point-Details">Entry Point Details</a>
</li></ul>

<div class="node">
<a name="Entry-Point-Details"></a>
<p></p><hr>
Up:&nbsp;<a rel="up" accesskey="u" href="#Function-Names">Function Names</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h5 class="subsubsection">5.3.3.1 Entry Point Details</h5>

<p><a name="index-External-entry-points-71"></a><a name="index-Entry-points_002c-external-72"></a><a name="index-Block-compilation_002c-debugger-implications-73"></a><a name="index-External_002c-stack-frame-kind-74"></a><a name="index-Optional_002c-stack-frame-kind-75"></a><a name="index-Cleanup_002c-stack-frame-kind-76"></a>
Sometimes the compiler introduces new functions that are used to
implement a user function, but are not directly specified in the
source. This is mostly done for argument type and count checking.

<!-- FIXME: the following bits talked about block-compilation, but -->
<!-- we don't currently support it... -->
<!-- With recursive -->
<!-- or block compiled -->
<!-- functions, an additional @code{:EXTERNAL} frame -->
<!-- may appear before the frame representing the first call to the -->
<!-- recursive function -->
<!-- or entry to the compiled block. -->
<!-- This is a -->
<!-- consequence of the way the compiler works: there is -->
<!-- nothing odd with your program. You will also see @code{:CLEANUP} -->
<!-- frames during the execution of @code{unwind-protect} cleanup -->
<!-- code. -->
   </p><p>With recursive functions, an additional <code>external</code> frame may
appear before the frame representing the first call to the recursive
function. This is a consequence of the way the compiler works: there
is nothing odd with your program. You may also see <code>cleanup</code>
frames during the execution of <code>unwind-protect</code> cleanup code, and
<code>optional</code> for variable argument entry points.

</p><div class="node">
<a name="Debug-Tail-Recursion"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Function-Names">Function Names</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stack-Frames">Stack Frames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.3.4 Debug Tail Recursion</h4>

<p><a name="index-Tail-recursion-77"></a><a name="index-Recursion_002c-tail-78"></a>
The compiler is “properly tail recursive.” If a function call is in
a tail-recursive position, the stack frame will be deallocated
<em>at the time of the call</em>, rather than after the call returns. 
Consider this backtrace:

</p><pre class="example">     (BAR ...)
     (FOO ...)
</pre>
   <p>Because of tail recursion, it is not necessarily the case that
<code>FOO</code> directly called <code>BAR</code>.  It may be that <code>FOO</code>
called some other function <code>FOO2</code> which then called <code>BAR</code>
tail-recursively, as in this example:

</p><pre class="lisp">     (defun foo ()
       ...
       (foo2 ...)
       ...)
     
     (defun foo2 (...)
       ...
       (bar ...))
     
     (defun bar (...)
       ...)
</pre>
   <p>Usually the elimination of tail-recursive frames makes debugging more
pleasant, since these frames are mostly uninformative.  If there is any
doubt about how one function called another, it can usually be
eliminated by finding the source location in the calling frame. 
See <a href="#Source-Location-Printing">Source Location Printing</a>.

   </p><p>The elimination of tail-recursive frames can be prevented by disabling
tail-recursion optimization, which happens when the <code>debug</code>
optimization quality is greater than <code>2</code>. 
See <a href="#Debugger-Policy-Control">Debugger Policy Control</a>.

<!-- FIXME: reinstate this link once the chapter is in the manual. -->
<!-- For a more thorough discussion of tail recursion, @ref{tail-recursion}. -->
</p><div class="node">
<a name="Unknown-Locations-and-Interrupts"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Debug-Tail-Recursion">Debug Tail Recursion</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Stack-Frames">Stack Frames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.3.5 Unknown Locations and Interrupts</h4>

<p><a name="index-Unknown-code-locations-79"></a><a name="index-Locations_002c-unknown-80"></a><a name="index-Interrupts-81"></a><a name="index-Errors_002c-run_002dtime-82"></a>
The debugger operates using special debugging information attached to
the compiled code.  This debug information tells the debugger what it
needs to know about the locations in the code where the debugger can
be invoked.  If the debugger somehow encounters a location not
described in the debug information, then it is said to be
<dfn>unknown</dfn>.  If the code location for a frame is unknown, then some
variables may be inaccessible, and the source location cannot be
precisely displayed.

   </p><p>There are three reasons why a code location could be unknown:

     </p><ul>
<li>There is inadequate debug information due to the value of the <code>debug</code>
optimization quality.  See <a href="#Debugger-Policy-Control">Debugger Policy Control</a>.

     </li><li>The debugger was entered because of an interrupt such as &lt;C-c&gt;.

     </li><li>A hardware error such as “‘<samp><span class="samp">bus error</span></samp>’” occurred in code that was
compiled unsafely due to the value of the <code>safety</code> optimization
quality. 
<!-- FIXME: reinstate link when section on optimize qualities exists. -->
<!-- @xref{optimize-declaration}. -->

   </li></ul>

   <p>In the last two cases, the values of argument variables are
accessible, but may be incorrect.  For more details on when variable
values are accessible, <a href="#Variable-Value-Availability">Variable Value Availability</a>.

   </p><p>It is possible for an interrupt to happen when a function call or
return is in progress.  The debugger may then flame out with some
obscure error or insist that the bottom of the stack has been reached,
when the real problem is that the current stack frame can't be
located.  If this happens, return from the interrupt and try again.

</p><div class="node">
<a name="Variable-Access"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Source-Location-Printing">Source Location Printing</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Stack-Frames">Stack Frames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.4 Variable Access</h3>

<p><a name="index-Debug-variables-83"></a><a name="index-Variables_002c-debugger-access-84"></a>
There are two ways to access the current frame's local variables in
the debugger: <samp><span class="command">list-locals</span></samp> and <code>sb-debug:var</code>.

   </p><p>The debugger doesn't really understand lexical scoping; it has just
one namespace for all the variables in the current stack frame.  If a
symbol is the name of multiple variables in the same function, then
the reference appears ambiguous, even though lexical scoping specifies
which value is visible at any given source location.  If the scopes of
the two variables are not nested, then the debugger can resolve the
ambiguity by observing that only one variable is accessible.

   </p><p>When there are ambiguous variables, the evaluator assigns each one a
small integer identifier.  The <code>sb-debug:var</code> function uses this
identifier to distinguish between ambiguous variables.  The
<samp><span class="command">list-locals</span></samp> command prints the identifier.  In the
following example, there are two variables named <code>X</code>.  The first
one has identifier 0 (which is not printed), the second one has
identifier 1.

</p><pre class="example">     X  =  1
     X#1  =  2
</pre>
   <div class="defun">
— Debugger Command: <b>list-locals</b> [<var>prefix</var>]<var><a name="index-g_t_0040nopkg_007blist_002dlocals_007d-85"></a></var><br>
<blockquote><p>This command prints the name and value of all variables in the current
frame whose name has the specified <var>prefix</var>.  <var>prefix</var> may be
a string or a symbol.  If no <var>prefix</var> is given, then all available
variables are printed.  If a variable has a potentially ambiguous
name, then the name is printed with a “<code>#</code><var>identifier</var>”
suffix, where <var>identifier</var> is the small integer used to make the
name unique. 
</p></blockquote></div>

<div class="defun">
— Function: <b>var [sb-debug]</b><var> name &amp;optional identifier<a name="index-g_t_0040sbdebug_007bvar_007d-86"></a></var><br>
<blockquote><p>This function returns the value of the variable in the current frame
with the specified <var>name</var>.  If supplied, <var>identifier</var>
determines which value to return when there are ambiguous variables.

        </p><p>When <var>name</var> is a symbol, it is interpreted as the symbol name of
the variable, i.e. the package is significant.  If <var>name</var> is an
uninterned symbol (gensym), then return the value of the uninterned
variable with the same name.  If <var>name</var> is a string,
<code>sb-debug:var</code> interprets it as the prefix of a variable name
that must unambiguously complete to the name of a valid variable.

        </p><p><var>identifier</var> is used to disambiguate the variable name; use
<samp><span class="command">list-locals</span></samp> to find out the identifiers. 
</p></blockquote></div>

<ul class="menu">
<li><a accesskey="1" href="#Variable-Value-Availability">Variable Value Availability</a>
</li><li><a accesskey="2" href="#Note-On-Lexical-Variable-Access">Note On Lexical Variable Access</a>
</li></ul>

<div class="node">
<a name="Variable-Value-Availability"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Note-On-Lexical-Variable-Access">Note On Lexical Variable Access</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Variable-Access">Variable Access</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.4.1 Variable Value Availability</h4>

<p><a name="index-Availability-of-debug-variables-87"></a><a name="index-Validity-of-debug-variables-88"></a><a name="index-Debug-optimization-quality-89"></a>
The value of a variable may be unavailable to the debugger in portions
of the program where Lisp says that the variable is defined.  If a
variable value is not available, the debugger will not let you read or
write that variable.  With one exception, the debugger will never
display an incorrect value for a variable.  Rather than displaying
incorrect values, the debugger tells you the value is unavailable.

   </p><p>The one exception is this: if you interrupt (e.g., with &lt;C-c&gt;) or
if there is an unexpected hardware error such as “‘<samp><span class="samp">bus error</span></samp>’”
(which should only happen in unsafe code), then the values displayed
for arguments to the interrupted frame might be
incorrect.<a rel="footnote" href="#fn-4" name="fnd-4"><sup>4</sup></a>  This exception applies only to the
interrupted frame: any frame farther down the stack will be fine.

   </p><p>The value of a variable may be unavailable for these reasons:

     </p><ul>
<li>The value of the <code>debug</code> optimization quality may have omitted debug
information needed to determine whether the variable is available. 
Unless a variable is an argument, its value will only be available when
<code>debug</code> is at least <code>2</code>.

     </li><li>The compiler did lifetime analysis and determined that the value was no longer
needed, even though its scope had not been exited.  Lifetime analysis is
inhibited when the <code>debug</code> optimization quality is <code>3</code>.

     </li><li>The variable's name is an uninterned symbol (gensym).  To save space, the
compiler only dumps debug information about uninterned variables when the
<code>debug</code> optimization quality is <code>3</code>.

     </li><li>The frame's location is unknown (see <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a>) because the debugger was entered due to an interrupt or
unexpected hardware error.  Under these conditions the values of
arguments will be available, but might be incorrect.  This is the
exception mentioned above.

     </li><li>The variable (or the code referencing it) was optimized out
of existence.  Variables with no reads are always optimized away.  The
degree to which the compiler deletes variables will depend on the
value of the <code>compilation-speed</code> optimization quality, but most
source-level optimizations are done under all compilation policies.

     </li><li>The variable is never set and its definition looks like
     <pre class="lisp">          (LET ((var1 var2))
             ...)
</pre>
     <p>In this case, <code>var1</code> is substituted with <code>var2</code>.

     </p></li><li>The variable is never set and is referenced exactly once.  In this
case, the reference is substituted with the variable initial value.

   </li></ul>

   <p>Since it is especially useful to be able to get the arguments to a
function, argument variables are treated specially when the
<code>speed</code> optimization quality is less than <code>3</code> and the
<code>debug</code> quality is at least <code>1</code>.  With this compilation
policy, the values of argument variables are almost always available
everywhere in the function, even at unknown locations.  For
non-argument variables, <code>debug</code> must be at least <code>2</code> for
values to be available, and even then, values are only available at
known locations.

</p><div class="node">
<a name="Note-On-Lexical-Variable-Access"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Variable-Value-Availability">Variable Value Availability</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Variable-Access">Variable Access</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.4.2 Note On Lexical Variable Access</h4>

<p>When the debugger command loop establishes variable bindings for
available variables, these variable bindings have lexical scope and
dynamic extent.<a rel="footnote" href="#fn-5" name="fnd-5"><sup>5</sup></a>  You can close
over them, but such closures can't be used as upward function arguments.

   </p><p>You can also set local variables using <code>setq</code>, but if the
variable was closed over in the original source and never set, then
setting the variable in the debugger may not change the value in all
the functions the variable is defined in.  Another risk of setting
variables is that you may assign a value of a type that the compiler
proved the variable could never take on.  This may result in bad
things happening.

</p><div class="node">
<a name="Source-Location-Printing"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Debugger-Policy-Control">Debugger Policy Control</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Variable-Access">Variable Access</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.5 Source Location Printing</h3>

<p><a name="index-Source-location-printing_002c-debugger-90"></a>
One of the debugger's capabilities is source level debugging of
compiled code.  These commands display the source location for the
current frame:

</p><div class="defun">
— Debugger Command: <b>source</b> [<var>context</var>]<var><a name="index-g_t_0040nopkg_007bsource_007d-91"></a></var><br>
<blockquote><p>This command displays the file that the current frame's function was
defined from (if it was defined from a file), and then the source form
responsible for generating the code that the current frame was
executing.  If <var>context</var> is specified, then it is an integer
specifying the number of enclosing levels of list structure to print. 
</p></blockquote></div>

   <p>The source form for a location in the code is the innermost list present
in the original source that encloses the form responsible for generating
that code.  If the actual source form is not a list, then some enclosing
list will be printed.  For example, if the source form was a reference
to the variable <code>*some-random-special*</code>, then the innermost
enclosing evaluated form will be printed.  Here are some possible
enclosing forms:

</p><pre class="lisp">     (let ((a *some-random-special*))
       ...)
     
     (+ *some-random-special* ...)
</pre>
   <p>If the code at a location was generated from the expansion of a macro
or a source-level compiler optimization, then the form in the original
source that expanded into that code will be printed.  Suppose the file
<samp><span class="file">/usr/me/mystuff.lisp</span></samp> looked like this:

</p><pre class="lisp">     (defmacro mymac ()
       '(myfun))
     
     (defun foo ()
       (mymac)
       ...)
</pre>
   <p>If <code>foo</code> has called <code>myfun</code>, and is waiting for it to
return, then the <samp><span class="command">source</span></samp> command would print:

</p><pre class="example">     ; File: /usr/me/mystuff.lisp
     
     (MYMAC)
</pre>
   <p>Note that the macro use was printed, not the actual function call form,
<code>(myfun)</code>.

   </p><p>If enclosing source is printed by giving an argument to
<samp><span class="command">source</span></samp> or <samp><span class="command">vsource</span></samp>, then the actual source form is
marked by wrapping it in a list whose first element is
‘<samp><span class="samp">#:***HERE***</span></samp>’.  In the previous example, <code>source 1</code> would
print:

</p><pre class="example">     ; File: /usr/me/mystuff.lisp
     
     (DEFUN FOO ()
       (#:***HERE***
        (MYMAC))
       ...)
</pre>
   <ul class="menu">
<li><a accesskey="1" href="#How-the-Source-is-Found">How the Source is Found</a>
</li><li><a accesskey="2" href="#Source-Location-Availability">Source Location Availability</a>
</li></ul>

<div class="node">
<a name="How-the-Source-is-Found"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Source-Location-Availability">Source Location Availability</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Source-Location-Printing">Source Location Printing</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.5.1 How the Source is Found</h4>

<p>If the code was defined from Lisp by <code>compile</code> or
<code>eval</code>, then the source can always be reliably located.  If the
code was defined from a <samp><span class="file">fasl</span></samp> file created by
<code>compile-file</code>, then the debugger gets the source forms it
prints by reading them from the original source file.  This is a
potential problem, since the source file might have moved or changed
since the time it was compiled.

   </p><p>The source file is opened using the <code>truename</code> of the source file
pathname originally given to the compiler.  This is an absolute pathname
with all logical names and symbolic links expanded.  If the file can't
be located using this name, then the debugger gives up and signals an
error.

   </p><p>If the source file can be found, but has been modified since the time it was
compiled, the debugger prints this warning:

</p><pre class="example">     ; File has been modified since compilation:
     ;   <var>filename</var>
     ; Using form offset instead of character position.
</pre>
   <p>where <var>filename</var> is the name of the source file.  It then proceeds
using a robust but not foolproof heuristic for locating the source. 
This heuristic works if:

     </p><ul>
<li>No top-level forms before the top-level form containing the source
have been added or deleted, and

     </li><li>The top-level form containing the source has not been modified much. 
(More precisely, none of the list forms beginning before the source
form have been added or deleted.)

   </li></ul>

   <p>If the heuristic doesn't work, the displayed source will be wrong, but will
probably be near the actual source.  If the “shape” of the top-level form in
the source file is too different from the original form, then an error will be
signaled.  When the heuristic is used, the source location commands are
noticeably slowed.

   </p><p>Source location printing can also be confused if (after the source was
compiled) a read-macro you used in the code was redefined to expand
into something different, or if a read-macro ever returns the same
<code>eq</code> list twice.  If you don't define read macros and don't use
<code>##</code> in perverted ways, you don't need to worry about this.

</p><div class="node">
<a name="Source-Location-Availability"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#How-the-Source-is-Found">How the Source is Found</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Source-Location-Printing">Source Location Printing</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">5.5.2 Source Location Availability</h4>

<p><a name="index-Debug-optimization-quality-92"></a><a name="index-Block_002c-basic-93"></a><a name="index-Block_002c-start-location-94"></a>
Source location information is only available when the <code>debug</code>
optimization quality is at least <code>2</code>.  If source location
information is unavailable, the source commands will give an error
message.

   </p><p>If source location information is available, but the source location
is unknown because of an interrupt or unexpected hardware error
(see <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a>), then the command will
print:

</p><pre class="example">     Unknown location: using block start.
</pre>
   <p>and then proceed to print the source location for the start of the
<em>basic block</em> enclosing the code location.  It's a bit
complicated to explain exactly what a basic block is, but here are
some properties of the block start location:

     </p><ul>
<li>The block start location may be the same as the true location.

     </li><li>The block start location will never be later in the
program's flow of control than the true location.

     </li><li>No conditional control structures (such as <code>if</code>,
<code>cond</code>, <code>or</code>) will intervene between the block start and the
true location (but note that some conditionals present in the original
source could be optimized away.)  Function calls <em>do not</em> end
basic blocks.

     </li><li>The head of a loop will be the start of a block.

     </li><li>The programming language concept of “block structure” and the
Lisp <code>block</code> special form are totally unrelated to the compiler's
basic block.

   </li></ul>

   <p>In other words, the true location lies between the printed location and the
next conditional (but watch out because the compiler may have changed the
program on you.)

</p><div class="node">
<a name="Debugger-Policy-Control"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Exiting-Commands">Exiting Commands</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Source-Location-Printing">Source Location Printing</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.6 Debugger Policy Control</h3>

<p><a name="index-Policy_002c-debugger-95"></a><a name="index-Debug-optimization-quality-96"></a><a name="index-Optimize-declaration-97"></a><a name="index-Inline-expansion-98"></a><a name="index-Semi_002dinline-expansion-99"></a>
The compilation policy specified by <code>optimize</code> declarations
affects the behavior seen in the debugger.  The <code>debug</code> quality
directly affects the debugger by controlling the amount of debugger
information dumped.  Other optimization qualities have indirect but
observable effects due to changes in the way compilation is done.

   </p><p>Unlike the other optimization qualities (which are compared in relative value
to evaluate tradeoffs), the <code>debug</code> optimization quality is directly
translated to a level of debug information.  This absolute interpretation
allows the user to count on a particular amount of debug information being
available even when the values of the other qualities are changed during
compilation.  These are the levels of debug information that correspond to the
values of the <code>debug</code> quality:

     </p><dl>
<dt><code>0</code></dt><dd>Only the function name and enough information to allow the stack to
be parsed.

     <br></dd><dt><code>&gt; 0</code></dt><dd>Any level greater than <code>0</code> gives level <code>0</code> plus all argument
variables.  Values will only be accessible if the argument variable is
never set and <code>speed</code> is not <code>3</code>.  SBCL allows any real
value for optimization qualities.  It may be useful to specify
<code>0.5</code> to get backtrace argument display without argument
documentation.

     <br></dd><dt><code>1</code></dt><dd>Level <code>1</code> provides argument documentation (printed argument lists) and
derived argument/result type information.  This makes <code>describe</code>
more informative, and allows the compiler to do compile-time argument
count and type checking for any calls compiled at run-time.  This is
the default.

     <br></dd><dt><code>2</code></dt><dd>Level <code>1</code> plus all interned local variables, source location
information, and lifetime information that tells the debugger when
arguments are available (even when <code>speed</code> is <code>3</code> or the
argument is set).

     <br></dd><dt><code>&gt; 2</code></dt><dd>Any level greater than <code>2</code> gives level <code>2</code> and in addition
disables tail-call optimization, so that the backtrace will contain
frames for all invoked functions, even those in tail positions.

     <br></dd><dt><code>3</code></dt><dd>Level <code>2</code> plus all uninterned variables.  In addition, lifetime
analysis is disabled (even when <code>speed</code> is <code>3</code>), ensuring
that all variable values are available at any known location within
the scope of the binding.  This has a speed penalty in addition to the
obvious space penalty.

     <br></dd><dt><code>&gt; (max speed space)</code></dt><dd>If <code>debug</code> is greater than both <code>speed</code> and <code>space</code>,
the command <samp><span class="command">return</span></samp> can be used to continue execution by
returning a value from the current stack frame.

     <br></dd><dt><code>&gt; (max speed space compilation-speed)</code></dt><dd>If <code>debug</code> is greater than all of <code>speed</code>, <code>space</code> and
<code>compilation-speed</code> the code will be steppable (see <a href="#Single-Stepping">Single Stepping</a>).

   </dd></dl>

   <p>As you can see, if the <code>speed</code> quality is <code>3</code>, debugger performance is
degraded.  This effect comes from the elimination of argument variable
special-casing (see <a href="#Variable-Value-Availability">Variable Value Availability</a>).  Some degree of
speed/debuggability tradeoff is unavoidable, but the effect is not too drastic
when <code>debug</code> is at least <code>2</code>.

   </p><p>In addition to <code>inline</code> and <code>notinline</code> declarations, the
relative values of the <code>speed</code> and <code>space</code> qualities also
change whether functions are inline expanded. 
<!-- FIXME: link to section about inline expansion when it exists -->
<!-- (\pxlref{inline-expansion}.) -->
If a function is inline expanded, then
there will be no frame to represent the call, and the arguments will
be treated like any other local variable.  Functions may also be
“semi-inline”, in which case there is a frame to represent the call,
but the call is to an optimized local version of the function, not to
the original function.

</p><div class="node">
<a name="Exiting-Commands"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Information-Commands">Information Commands</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Debugger-Policy-Control">Debugger Policy Control</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.7 Exiting Commands</h3>

<p>These commands get you out of the debugger.

</p><div class="defun">
— Debugger Command: <b>toplevel</b><var><a name="index-g_t_0040nopkg_007btoplevel_007d-100"></a></var><br>
<blockquote><p>Throw to top level. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>restart</b> [<var>n</var>]<var><a name="index-g_t_0040nopkg_007brestart_007d-101"></a></var><br>
<blockquote><p>Invokes the <var>n</var>th restart case as displayed by the <code>error</code>
command.  If <var>n</var> is not specified, the available restart cases are
reported. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>continue</b><var><a name="index-g_t_0040nopkg_007bcontinue_007d-102"></a></var><br>
<blockquote><p>Calls <code>continue</code> on the condition given to <code>debug</code>.  If there is no
restart case named <var>continue</var>, then an error is signaled. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>abort</b><var><a name="index-g_t_0040nopkg_007babort_007d-103"></a></var><br>
<blockquote><p>Calls <code>abort</code> on the condition given to <code>debug</code>.  This is
useful for popping debug command loop levels or aborting to top level,
as the case may be. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>return</b><var> value<a name="index-g_t_0040nopkg_007breturn_007d-104"></a></var><br>
<blockquote><p>Returns <var>value</var> from the current stack frame.  This command is
available when the <code>debug</code> optimization quality is greater than
both <code>speed</code> and <code>space</code>.  Care must be taken that the value
is of the same type as SBCL expects the stack frame to return. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>restart-frame</b><var><a name="index-g_t_0040nopkg_007brestart_002dframe_007d-105"></a></var><br>
<blockquote><p>Restarts execution of the current stack frame. This command is
available when the <code>debug</code> optimization quality is greater than
both <code>speed</code> and <code>space</code> and when the frame is for is a global
function. If the function is redefined in the debugger before the frame
is restarted, the new function will be used. 
</p></blockquote></div>

<div class="node">
<a name="Information-Commands"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Function-Tracing">Function Tracing</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Exiting-Commands">Exiting Commands</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.8 Information Commands</h3>

<p>Most of these commands print information about the current frame or
function, but a few show general information.

</p><div class="defun">
— Debugger Command: <b>help</b><var><a name="index-g_t_0040nopkg_007bhelp_007d-106"></a></var><br>
— Debugger Command: <b>?</b><var><a name="index-g_t_0040nopkg_007b_003f_007d-107"></a></var><br>
<blockquote><p>Displays a synopsis of debugger commands. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>describe</b><var><a name="index-g_t_0040nopkg_007bdescribe_007d-108"></a></var><br>
<blockquote><p>Calls <code>describe</code> on the current function and displays the number of
local variables. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>print</b><var><a name="index-g_t_0040nopkg_007bprint_007d-109"></a></var><br>
<blockquote><p>Displays the current function call as it would be displayed by moving to
this frame. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>error</b><var><a name="index-g_t_0040nopkg_007berror_007d-110"></a></var><br>
<blockquote><p>Prints the condition given to <code>invoke-debugger</code> and the active
proceed cases. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>backtrace</b> [<var>n</var>]<var><a name="index-g_t_0040nopkg_007bbacktrace_007d-111"></a></var><br>
<blockquote><p>Displays all the frames from the current to the bottom. Only shows
<var>n</var> frames if specified. The printing is controlled by
<code>*debug-print-variable-alist*</code>. 
</p></blockquote></div>

<!-- The new instrumentation based single stepper doesn't support -->
<!-- the following commands, but BREAKPOINT at least should be -->
<!-- resurrectable via (TRACE FOO :BREAK T). -->
<!-- @cindex Breakpoints -->
<!-- SBCL supports setting of breakpoints inside compiled functions and -->
<!-- stepping of compiled code.  Breakpoints can only be set at known -->
<!-- locations (@pxref{Unknown Locations and Interrupts}), so these -->
<!-- commands are largely useless unless the @code{debug} optimize quality -->
<!-- is at least @code{2} (@pxref{Debugger Policy Control}).  These -->
<!-- commands manipulate breakpoints: -->
<!-- @deffn {Debugger Command} breakpoint @var{location} [@var{option} @var{value}]* -->
<!-- Set a breakpoint in some function.  @var{location} may be an integer -->
<!-- code location number (as displayed by @command{list-locations}) or a -->
<!-- keyword.  The keyword can be used to indicate setting a breakpoint at -->
<!-- the function start (@code{:start}, @code{:s}) or function end -->
<!-- (@code{:end}, @code{:e}).  The @command{breakpoint} command has -->
<!-- @code{:condition}, @code{:break}, @code{:print} and @code{:function} -->
<!-- options which work similarly to the @code{trace} options. -->
<!-- @end deffn -->
<!-- @deffn {Debugger Command} list-locations [@var{function}] -->
<!-- @deffnx {Debugger Command} ll  [@var{function}] -->
<!-- List all the code locations in the current frame's function, or in -->
<!-- @var{function} if it is supplied.  The display format is the code -->
<!-- location number, a colon and then the source form for that location: -->
<!-- @example -->
<!-- 3: (1- N) -->
<!-- @end example -->
<!-- If consecutive locations have the same source, then a numeric range -->
<!-- like @code{3-5:} will be printed.  For example, a default function -->
<!-- call has a known location both immediately before and after the call, -->
<!-- which would result in two code locations with the same source.  The -->
<!-- listed function becomes the new default function for breakpoint -->
<!-- setting (via the @command{breakpoint}) command. -->
<!-- @end deffn -->
<!-- @deffn {Debugger Command} list-breakpoints -->
<!-- @deffnx {Debugger Command} lb -->
<!-- List all currently active breakpoints with their breakpoint number. -->
<!-- @end deffn -->
<!-- @deffn {Debugger Command} delete-breakpoint [@var{number}] -->
<!-- @deffnx {Debugger Command} db  [@var{number}] -->
<!-- Delete a breakpoint specified by its breakpoint number.  If no number -->
<!-- is specified, delete all breakpoints. -->
<!-- @end deffn -->
<!-- @menu -->
<!-- * Breakpoint Example:: -->
<!-- @end menu -->
<!-- @node  Breakpoint Example,  , Breakpoint Commands, Breakpoint Commands -->
<!-- @comment  node-name,  next,  previous,  up -->
<!-- @subsection Breakpoint Example -->
<!-- Consider this definition of the factorial function: -->
<!-- @lisp -->
<!-- (defun ! (n) -->
<!-- (if (zerop n) -->
<!-- 1 -->
<!-- (* n (! (1- n))))) -->
<!-- @end lisp -->
<!-- This debugger session demonstrates the use of breakpoints: -->
<!-- @example -->
<!-- * (break)  ; invoke debugger -->
<!-- debugger invoked on a SIMPLE-CONDITION in thread 11184: break -->
<!-- restarts (invokable by number or by possibly-abbreviated name): -->
<!-- 0: [CONTINUE] Return from BREAK. -->
<!-- 1: [ABORT   ] Reduce debugger level (leaving debugger, returning to toplevel). -->
<!-- 2: [TOPLEVEL] Restart at toplevel READ/EVAL/PRINT loop. -->
<!-- ("varargs entry for top level local call BREAK" "break") -->
<!-- 0] ll #'! -->
<!-- 0-1: (SB-INT:NAMED-LAMBDA ! (N) (BLOCK ! (IF (ZEROP N) 1 (* N (! #))))) -->
<!-- 2: (BLOCK ! (IF (ZEROP N) 1 (* N (! (1- N))))) -->
<!-- 3: (ZEROP N) -->
<!-- 4: (* N (! (1- N))) -->
<!-- 5: (1- N) -->
<!-- 6: (! (1- N)) -->
<!-- 7-8: (* N (! (1- N))) -->
<!-- 9-10: (IF (ZEROP N) 1 (* N (! (1- N)))) -->
<!-- 0] br 4 -->
<!-- (* N (! (1- N))) -->
<!-- 1: 4 in ! -->
<!-- added -->
<!-- 0] toplevel -->
<!-- FIXME: SBCL errored out, and not in the expected way ... Copying the -->
<!-- output verbatim from the CMUCL manual for now. -->
<!-- common-lisp-user> (! 10) ; Call the function -->
<!-- *Breakpoint hit* -->
<!-- Restarts: -->
<!-- 0: [CONTINUE] Return from BREAK. -->
<!-- 1: [ABORT   ] Return to Top-Level. -->
<!-- Debug  (type H for help) -->
<!-- (! 10) ; We are now in first call (arg 10) before the multiply -->
<!-- Source: (* N (! (1- N))) -->
<!-- 3] st -->
<!-- *Step* -->
<!-- (! 10) ; We have finished evaluation of (1- n) -->
<!-- Source: (1- N) -->
<!-- 3] st -->
<!-- *Breakpoint hit* -->
<!-- Restarts: -->
<!-- 0: [CONTINUE] Return from BREAK. -->
<!-- 1: [ABORT   ] Return to Top-Level. -->
<!-- Debug  (type H for help) -->
<!-- (! 9) ; We hit the breakpoint in the recursive call -->
<!-- Source: (* N (! (1- N))) -->
<!-- 3] -->
<!-- @end example -->
<div class="node">
<a name="Function-Tracing"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Single-Stepping">Single Stepping</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Information-Commands">Information Commands</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.9 Function Tracing</h3>

<p><a name="index-Tracing-112"></a><a name="index-Function_002c-tracing-113"></a>
The tracer causes selected functions to print their arguments and
their results whenever they are called.  Options allow conditional
printing of the trace information and conditional breakpoints on
function entry or exit.

   </p><p><a name="Macro-common_002dlisp_003atrace"></a>

</p><div class="defun">
— Macro: <b>trace [cl]</b><var> &amp;rest specs<a name="index-g_t_0040cl_007btrace_007d-114"></a></var><br>
<blockquote><p><code>trace</code> {Option Global-Value}* {Name {Option Value}*}*

        </p><p><code>trace</code> is a debugging tool that provides information when specified
functions are called. In its simplest form:

     </p><pre class="lisp">                 (TRACE NAME-1 NAME-2 ...)
</pre>
        <p>The NAMEs are not evaluated. Each may be a symbol, denoting an
individual function, or a string, denoting all functions fbound to
symbols whose home package is the package with the given name.

        </p><p>Options allow modification of the default behavior. Each option is a
pair of an option keyword and a value form. Global options are
specified before the first name, and affect all functions traced by a
given use of <code>trace</code>. Options may also be interspersed with function
names, in which case they act as local options, only affecting tracing
of the immediately preceding function name. Local options override
global options.

        </p><p>By default, <code>trace</code> causes a printout on <code>*trace-output*</code> each time that
one of the named functions is entered or returns. (This is the basic,
<code>ansi</code> Common Lisp behavior of <code>trace</code>.)

        </p><p>The following options are defined:

          </p><dl>
<dt><code>:report</code><em> Report-Type</em></dt><dd>       If Report-Type is <code>trace</code> (the default) then information is
       reported by printing immediately. If Report-Type is <code>nil</code>, then
       the only effect of the trace is to execute other
       options (e.g. <code>print</code> or BREAK).

          <br></dd><dt><code>:condition</code><em> Form</em></dt><dt><code>:condition-after</code><em> Form</em></dt><dt><code>:condition-all</code><em> Form</em></dt><dd>       If <code>:condition</code> is specified, then <code>trace</code> does nothing unless Form
       evaluates to true at the time of the call. <code>:condition-after</code> is
       similar, but suppresses the initial printout, and is tested when the
       function returns. <code>:condition-all</code> tries both before and after.

          <br></dd><dt><code>:break</code><em> Form</em></dt><dt><code>:break-after</code><em> Form</em></dt><dt><code>:break-all</code><em> Form</em></dt><dd>       If specified, and Form evaluates to true, then the debugger is invoked
       at the start of the function, at the end of the function, or both,
       according to the respective option.

          <br></dd><dt><code>:print</code><em> Form</em></dt><dt><code>:print-after</code><em> Form</em></dt><dt><code>:print-all</code><em> Form</em></dt><dd>       In addition to the usual printout, the result of evaluating Form is
       printed at the start of the function, at the end of the function, or
       both, according to the respective option. Multiple print options cause
       multiple values to be printed.

          <br></dd><dt><code>:wherein</code><em> Names</em></dt><dd>       If specified, Names is a function name or list of names. <code>trace</code> does
       nothing unless a call to one of those functions encloses the call to
       this function (i.e. it would appear in a backtrace.)  Anonymous
       functions have string names like "DEFUN FOO".

          <br></dd><dt><code>:encapsulate</code><em> {:DEFAULT | </em><code>t</code><em> | NIL}</em></dt><dd>       If <code>t</code>, the tracing is done via encapsulation (redefining the function
       name) rather than by modifying the function. <code>:default</code> is the default,
       and means to use encapsulation for interpreted functions and funcallable
       instances, breakpoints otherwise. When encapsulation is used, forms are
       *not* evaluated in the function's lexical environment, but <code>sb-debug:arg</code>
       can still be used.

          <br></dd><dt><code>:methods</code><em> {T | NIL}</em></dt><dd>       If <code>t</code>, any function argument naming a generic function will have its
       methods traced in addition to the generic function itself.

          <br></dd><dt><code>:function</code><em> Function-Form</em></dt><dd>       This is a not really an option, but rather another way of specifying
       what function to trace. The Function-Form is evaluated immediately,
       and the resulting function is traced.

        </dd></dl>

        <p><code>:condition</code>, <code>:break</code> and <code>:print</code> forms are evaluated in a context which
mocks up the lexical environment of the called function, so that
<code>sb-debug:var</code> and <code>sb-debug:arg</code> can be used. 
The <code>-after</code> and <code>-all</code> forms can use <code>sb-debug:arg</code>. 
</p></blockquote></div>

   <p><a name="Macro-common_002dlisp_003auntrace"></a>

</p><div class="defun">
— Macro: <b>untrace [cl]</b><var> &amp;rest specs<a name="index-g_t_0040cl_007buntrace_007d-115"></a></var><br>
<blockquote><p>Remove tracing from the specified functions. Untraces all
functions when called with no arguments. 
</p></blockquote></div>

   <p><a name="Variable-sb_002ddebug_003a_002atrace_002dindentation_002dstep_002a"></a>

</p><div class="defun">
— Variable: <b>*trace-indentation-step* [sb-debug]</b><var><a name="index-g_t_0040sbdebug_007b_0040earmuffs_007btrace_002dindentation_002dstep_007d_007d-116"></a></var><br>
<blockquote><p>the increase in trace indentation at each call level
</p></blockquote></div>

   <p><a name="Variable-sb_002ddebug_003a_002amax_002dtrace_002dindentation_002a"></a>

</p><div class="defun">
— Variable: <b>*max-trace-indentation* [sb-debug]</b><var><a name="index-g_t_0040sbdebug_007b_0040earmuffs_007bmax_002dtrace_002dindentation_007d_007d-117"></a></var><br>
<blockquote><p>If the trace indentation exceeds this value, then indentation restarts at
   0. 
</p></blockquote></div>

   <p><a name="Variable-sb_002ddebug_003a_002atrace_002dencapsulate_002ddefault_002a"></a>

</p><div class="defun">
— Variable: <b>*trace-encapsulate-default* [sb-debug]</b><var><a name="index-g_t_0040sbdebug_007b_0040earmuffs_007btrace_002dencapsulate_002ddefault_007d_007d-118"></a></var><br>
<blockquote><p>the default value for the <code>:encapsulate</code> option to <code>trace</code>
</p></blockquote></div>

<!-- FIXME rudi 2004-03-26: encapsulate is (per TODO file as of -->
<!-- 0.8.9) in a state of flux.  When it's sorted out, revive the -->
<!-- cmucl documentation. -->
<div class="node">
<a name="Single-Stepping"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Function-Tracing">Function Tracing</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.10 Single Stepping</h3>

<p><a name="index-Stepper-119"></a><a name="index-Single-Stepping-120"></a>
SBCL includes an instrumentation based single-stepper for compiled
code, that can be invoked via the <code>step</code> macro, or from within
the debugger. See <a href="#Debugger-Policy-Control">Debugger Policy Control</a>, for details on enabling
stepping for compiled code.

   </p><p>The following debugger commands are used for controlling single stepping.

</p><div class="defun">
— Debugger Command: <b>start</b><var><a name="index-g_t_0040nopkg_007bstart_007d-121"></a></var><br>
<blockquote><p>Selects the <code>continue</code> restart if one exists and starts single stepping. 
None of the other single stepping commands can be used before stepping has
been started either by using <code>start</code> or by using the standard
<code>step</code> macro. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>step</b><var><a name="index-g_t_0040nopkg_007bstep_007d-122"></a></var><br>
<blockquote><p>Steps into the current form. Stepping will be resumed when the next
form that has been compiled with stepper instrumentation is evaluated. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>next</b><var><a name="index-g_t_0040nopkg_007bnext_007d-123"></a></var><br>
<blockquote><p>Steps over the current form. Stepping will be disabled until evaluation of
the form is complete. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>out</b><var><a name="index-g_t_0040nopkg_007bout_007d-124"></a></var><br>
<blockquote><p>Steps out of the current frame. Stepping will be disabled until the
topmost stack frame that had been stepped into returns. 
</p></blockquote></div>

<div class="defun">
— Debugger Command: <b>stop</b><var><a name="index-g_t_0040nopkg_007bstop_007d-125"></a></var><br>
<blockquote><p>Stops the single stepper and resumes normal execution. 
</p></blockquote></div>

   <p><a name="Macro-common_002dlisp_003astep"></a>

</p><div class="defun">
— Macro: <b>step [cl]</b><var> form<a name="index-g_t_0040cl_007bstep_007d-126"></a></var><br>
<blockquote><p>The form is evaluated with single stepping enabled. Function calls
outside the lexical scope of the form can be stepped into only if the
functions in question have been compiled with sufficient <code>debug</code> policy
to be at least partially steppable. 
</p></blockquote></div>

<div class="node">
<a name="Enabling-and-Disabling-the-Debugger"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Single-Stepping">Single Stepping</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Debugger">Debugger</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">5.11 Enabling and Disabling the Debugger</h3>

<p><a name="index-debugger_002c-enabling-127"></a><a name="index-debugger_002c-disabling-128"></a><a name="index-disabling-debugger-129"></a><a name="index-ldb_002c-enabling-130"></a><a name="index-ldb_002c-disabling-131"></a><a name="index-disabling-ldb-132"></a>
In certain contexts (e.g., non-interactive applications), it may be
desirable to turn off the SBCL debugger (and possibly re-enable it). 
The functions here control the debugger.

   </p><p><a name="Function-sb_002dext_003adisable_002ddebugger"></a>

</p><div class="defun">
— Function: <b>disable-debugger [sb-ext]</b><var><a name="index-g_t_0040sbext_007bdisable_002ddebugger_007d-133"></a></var><br>
<blockquote><p>When invoked, this function will turn off both the <code>sbcl</code> debugger
and <code>ldb</code> (the low-level debugger).  See also <code>enable-debugger</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aenable_002ddebugger"></a>

</p><div class="defun">
— Function: <b>enable-debugger [sb-ext]</b><var><a name="index-g_t_0040sbext_007benable_002ddebugger_007d-134"></a></var><br>
<blockquote><p>Restore the debugger if it has been turned off by <code>disable-debugger</code>. 
</p></blockquote></div>

<div class="node">
<a name="Efficiency"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Debugger">Debugger</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">6 Efficiency</h2>

<p><a name="index-Efficiency-135"></a>

</p><ul class="menu">
<li><a accesskey="1" href="#Slot-access">Slot access</a>
</li><li><a accesskey="2" href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a>
</li><li><a accesskey="3" href="#Modular-arithmetic">Modular arithmetic</a>
</li><li><a accesskey="4" href="#Global-and-Always_002dBound-variables">Global and Always-Bound variables</a>
</li><li><a accesskey="5" href="#Miscellaneous-Efficiency-Issues">Miscellaneous Efficiency Issues</a>
</li></ul>

<div class="node">
<a name="Slot-access"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Efficiency">Efficiency</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">6.1 Slot access</h3>

<p><a name="index-Slot-access-136"></a>

</p><h4 class="subsection">6.1.1 Structure object slot access</h4>

<p>Structure slot accessors are efficient only if the compiler is able to
open code them: compiling a call to a structure slot accessor before
the structure is defined, declaring one <code>notinline</code>, or passing
it as a functional argument to another function causes severe
performance degradation.

</p><h4 class="subsection">6.1.2 Standard object slot access</h4>

<p>The most efficient way to access a slot of a <code>standard-object</code> is
by using <code>slot-value</code> with a constant slot name argument inside a
<code>defmethod</code> body, where the variable holding the instance is a
specializer parameter of the method and is never assigned to. The cost
is roughly 1.6 times that of an open coded structure slot accessor.

   </p><p>Second most efficient way is to use a CLOS slot accessor, or
<code>slot-value</code> with a constant slot name argument, but in
circumstances other than specified above. This may be up to 3 times as
slow as the method described above.

   </p><p>Example:

</p><pre class="lisp">     (defclass foo () ((bar)))
     
     ;; Fast: specializer and never assigned to
     (defmethod quux ((foo foo) new)
       (let ((old (slot-value foo 'bar)))
         (setf (slot-value foo 'bar) new)
         old))
     
     ;; Slow: not a specializer
     (defmethod quux ((foo foo) new)
       (let* ((temp foo)
              (old (slot-value temp 'bar)))
         (setf (slot-value temp 'bar) new)
         old))
     
     ;; Slow: assignment to FOO
     (defmethod quux ((foo foo) new)
       (let ((old (slot-value foo 'bar)))
         (setf (slot-value foo 'bar) new)
         (setf foo new)
         old))
</pre>
   <p>Note that when profiling code such as this, the first few calls to the
generic function are not representative, as the dispatch mechanism is
lazily set up during those calls.

</p><div class="node">
<a name="Dynamic-extent-allocation"></a>
<a name="Dynamic_002dextent-allocation"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Modular-arithmetic">Modular arithmetic</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Slot-access">Slot access</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Efficiency">Efficiency</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">6.2 Dynamic-extent allocation</h3>

<p><a name="index-g_t_0040code_007bdynamic_002dextent_007d-declaration-137"></a><a name="index-declaration_002c-_0040code_007bdynamic_002dextent_007d-138"></a>
SBCL has fairly extensive support for performing allocation on the
stack when a variable is declared <code>dynamic-extent</code>. The
<code>dynamic-extent</code> declarations are not verified, but are simply
trusted as long as <code>sb-ext:*stack-allocate-dynamic-extent*</code> is
true.

   </p><p><a name="Variable-sb_002dext_003a_002astack_002dallocate_002ddynamic_002dextent_002a"></a>

</p><div class="defun">
— Variable: <b>*stack-allocate-dynamic-extent* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bstack_002dallocate_002ddynamic_002dextent_007d_007d-139"></a></var><br>
<blockquote><p>If true (the default), the compiler respects <code>dynamic-extent</code> declarations
and stack allocates otherwise inaccessible parts of the object whenever
possible. Potentially long (over one page in size) vectors are, however, not
stack allocated except in zero <code>safety</code> code, as such a vector could overflow
the stack without triggering overflow protection. 
</p></blockquote></div>

   <p>If dynamic extent constraints specified in the Common Lisp standard
are violated, the best that can happen is for the program to have
garbage in variables and return values; more commonly, the system will
crash.

   </p><p>In particular, it is important to realize that dynamic extend is
contagious:

</p><pre class="lisp">     (let* ((a (list 1 2 3))
            (b (cons a a)))
        (declare (dynamic-extent b))
        ;; Unless A is accessed elsewhere as well, SBCL will consider
        ;; it to be otherwise inaccessible -- it can only be accessed
        ;; through B, after all -- and stack allocate it as well.
        ;;
        ;; Hence returning (CAR B) here is unsafe.
        ...)
</pre>
   <p>This allows stack allocation of complex structures. As a notable
exception to this, SBCL does not as of 1.0.48.21 propagate
dynamic-extentness through <code>&amp;rest</code> arguments – but another
conforming implementation might, so portable code should not rely on
this.

</p><pre class="lisp">     (declaim (inline foo))
     (defun foo (fun &amp;rest arguments)
       (declare (dynamic-extent arguments))
       (apply fun arguments))
     
     (defun bar (a)
       ;; SBCL will heap allocate the result of (LIST A), and stack allocate
       ;; only the spine of the &amp;rest list -- so this is safe, but unportable.
       ;;
       ;; Another implementation, including earlier versions of SBCL might consider
       ;; (LIST A) to be otherwise inaccessible and stack-allocate it as well!
       (foo #'car (list a)))
</pre>
   <p>There are many cases when <code>dynamic-extent</code> declarations could be
useful. At present, SBCL implements stack allocation for

     </p><ul>
<li><code>&amp;rest</code> lists, when these are declared <code>dynamic-extent</code>.

     </li><li><a name="index-g_t_0040cl_007bcons_007d-140"></a><a name="index-g_t_0040cl_007blist_007d-141"></a><a name="index-g_t_0040cl_007blist_002a_007d-142"></a><a name="index-g_t_0040cl_007bvector_007d-143"></a><code>cons</code>, <code>list</code>, <code>list*</code>, and <code>vector</code> when the
result is bound to a variable declared <code>dynamic-extent</code>.

     </li><li><a name="index-g_t_0040cl_007bmake_002darray_007d-144"></a>simple forms of <code>make-array</code>, whose result is bound to a variable
declared <code>dynamic-extent</code>: stack allocation is possible only if
the resulting array is known to be both simple and one-dimensional,
and has a constant <code>:element-type</code>.

     <p><a name="index-Safety-optimization-quality-145"></a><strong>Note</strong>: stack space is limited, so allocation of a large vector
may cause stack overflow. For this reason potentially large vectors,
which might circumvent stack overflow detection, are stack allocated
only in zero <code>safety</code> policies.

     </p></li><li><a name="index-g_t_0040cl_007bflet_007d-146"></a><a name="index-g_t_0040cl_007blabels_007d-147"></a><a name="index-g_t_0040code_007bsafety_007d-optimization-quality-148"></a><a name="index-optimization-quality_002c-_0040code_007bsafety_007d-149"></a>closures defined with <code>flet</code> or <code>labels</code>, with a bound
<code>dynamic-extent</code> declaration. Blocks and tags are also allocated
on the heap, unless all non-local control transfers to them are
compiled with zero <code>safety</code>.

     </li><li>user-defined structures when the structure constructor defined using
<code>defstruct</code> has been declared <code>inline</code> and the result of the
call to the constructor is bound to a variable declared
<code>dynamic-extent</code>.

     <p><strong>Note</strong>: structures with “raw” slots can currently be
stack-allocated only on x86 and x86-64.

     </p></li><li>all of the above when they appear as initial parts of another
stack-allocated object.

   </li></ul>

   <p>Examples:

</p><pre class="lisp">     ;;; Declaiming a structure constructor inline before definition makes
     ;;; stack allocation possible.
     (declaim (inline make-thing))
     (defstruct thing obj next)
     
     ;;; Stack allocation of various objects bound to DYNAMIC-EXTENT
     ;;; variables.
     (let* ((list (list 1 2 3))
            (nested (cons (list 1 2) (list* 3 4 (list 5))))
            (vector (make-array 3 :element-type 'single-float))
            (thing (make-thing :obj list
                               :next (make-thing :obj (make-array 3)))))
       (declare (dynamic-extent list nested vector thing))
       ...)
     
     ;;; Stack allocation of arguments to a local function is equivalent
     ;;; to stack allocation of local variable values.
     (flet ((f (x)
              (declare (dynamic-extent x))
              ...))
       ...
       (f (list 1 2 3))
       (f (cons (cons 1 2) (cons 3 4)))
       ...)
     
     ;;; Stack allocation of &amp;REST lists
     (defun foo (&amp;rest args)
       (declare (dynamic-extent args))
       ...)
</pre>
   <p>Future plans include

     </p><ul>
<li>Automatic detection of the common idiom of calling quantifiers with a
closure, even when the closure is not declared <code>dynamic-extent</code>.

   </li></ul>

<div class="node">
<a name="Modular-arithmetic"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Global-and-Always_002dBound-variables">Global and Always-Bound variables</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Efficiency">Efficiency</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">6.3 Modular arithmetic</h3>

<p><a name="index-Modular-arithmetic-150"></a><a name="index-Arithmetic_002c-modular-151"></a><a name="index-Arithmetic_002c-hardware-152"></a><a name="index-g_t_0040cl_007blogand_007d-153"></a>Some numeric functions have a property: <var>N</var> lower bits of the
result depend only on <var>N</var> lower bits of (all or some)
arguments. If the compiler sees an expression of form <code>(logand
</code><var>exp</var> <var>mask</var><code>)</code>, where <var>exp</var> is a tree of such “good”
functions and <var>mask</var> is known to be of type <code>(unsigned-byte
</code><var>w</var><code>)</code>, where <var>w</var> is a “good” width, all intermediate results
will be cut to <var>w</var> bits (but it is not done for variables and
constants!). This often results in an ability to use simple machine
instructions for the functions.

   </p><p>Consider an example.

</p><pre class="lisp">     (defun i (x y)
       (declare (type (unsigned-byte 32) x y))
       (ldb (byte 32 0) (logxor x (lognot y))))
</pre>
   <p>The result of <code>(lognot y)</code> will be negative and of type
<code>(signed-byte 33)</code>, so a naive implementation on a 32-bit
platform is unable to use 32-bit arithmetic here. But modular
arithmetic optimizer is able to do it: because the result is cut down
to 32 bits, the compiler will replace <code>logxor</code> and <code>lognot</code>
with versions cutting results to 32 bits, and because terminals
(here—expressions <code>x</code> and <code>y</code>) are also of type
<code>(unsigned-byte 32)</code>, 32-bit machine arithmetic can be used.

   </p><p>As of SBCL 0.8.5 “good” functions are <code>+</code>, <code>-</code>;
<code>logand</code>, <code>logior</code>, <code>logxor</code>, <code>lognot</code> and their
combinations; and <code>ash</code> with the positive second
argument. “Good” widths are 32 on HPPA, MIPS, PPC, Sparc and x86 and
64 on Alpha.  While it is possible to support smaller widths as well,
currently this is not implemented.

</p><div class="node">
<a name="Global-and-Always-Bound-variables"></a>
<a name="Global-and-Always_002dBound-variables"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Miscellaneous-Efficiency-Issues">Miscellaneous Efficiency Issues</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Modular-arithmetic">Modular arithmetic</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Efficiency">Efficiency</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">6.4 Global and Always-Bound variables</h3>

<p><a name="Macro-sb_002dext_003adefglobal"></a>

</p><div class="defun">
— Macro: <b>defglobal [sb-ext]</b><var> name value &amp;optional doc<a name="index-g_t_0040sbext_007bdefglobal_007d-154"></a></var><br>
<blockquote><p>Defines <code>name</code> as a global variable that is always bound. <code>value</code> is evaluated
and assigned to <code>name</code> both at compile- and load-time, but only if <code>name</code> is not
already bound.

        </p><p>Global variables share their values between all threads, and cannot be
locally bound, declared special, defined as constants, and neither bound
nor defined as symbol macros.

        </p><p>See also the declarations <code>sb-ext:global</code> and <code>sb-ext:always-bound</code>. 
</p></blockquote></div>

<div class="defun">
— Declaration: <b>global [sb-ext]</b><var><a name="index-g_t_0040sbext_007bglobal_007d-155"></a></var><br>
<blockquote>
        <p>Syntax: <code>(sb-ext:global symbol*)</code>

        </p><p>Only valid as a global proclamation.

        </p><p>Specifies that the named symbols cannot be proclaimed or locally
declared <code>special</code>. Proclaiming an already special or constant
variable name as <code>global</code> signal an error. Allows more efficient
value lookup in threaded environments in addition to expressing
programmer intention. 
</p></blockquote></div>

<div class="defun">
— Declaration: <b>always-bound [sb-ext]</b><var><a name="index-g_t_0040sbext_007balways_002dbound_007d-156"></a></var><br>
<blockquote>
        <p>Syntax: <code>(sb-ext:always-bound symbol*)</code>

        </p><p>Only valid as a global proclamation.

        </p><p>Specifies that the named symbols are always bound. Inhibits
<code>makunbound</code> of the named symbols. Proclaiming an unbound symbol
as <code>always-bound</code> signals an error. Allows the compiler to elide
boundness checks from value lookups. 
</p></blockquote></div>

<div class="node">
<a name="Miscellaneous-Efficiency-Issues"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Global-and-Always_002dBound-variables">Global and Always-Bound variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Efficiency">Efficiency</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">6.5 Miscellaneous Efficiency Issues</h3>

<p>FIXME: The material in the CMUCL manual about getting good
performance from the compiler should be reviewed, reformatted in
Texinfo, lightly edited for SBCL, and substituted into this
manual. In the meantime, the original CMUCL manual is still 95+%
correct for the SBCL version of the Python compiler. See the
sections

     </p><ul>
<li>Advanced Compiler Use and Efficiency Hints
</li><li>Advanced Compiler Introduction
</li><li>More About Types in Python
</li><li>Type Inference
</li><li>Source Optimization
</li><li>Tail Recursion
</li><li>Local Call
</li><li>Block Compilation
</li><li>Inline Expansion
</li><li>Object Representation
</li><li>Numbers
</li><li>General Efficiency Hints
</li><li>Efficiency Notes
</li></ul>

   <p>Besides this information from the CMUCL manual, there are a few other
points to keep in mind.

     </p><ul>
<li><a name="index-g_t_0040cl_007blet_007d-157"></a><a name="index-g_t_0040cl_007blet_002a_007d-158"></a><a name="index-g_t_0040cl_007bsetq_007d-159"></a><a name="index-g_t_0040cl_007bsetf_007d-160"></a>The CMUCL manual doesn't seem to state it explicitly, but Python has a
mental block about type inference when assignment is involved. Python
is very aggressive and clever about inferring the types of values
bound with <code>let</code>, <code>let*</code>, inline function call, and so
forth. However, it's much more passive and dumb about inferring the
types of values assigned with <code>setq</code>, <code>setf</code>, and
friends. It would be nice to fix this, but in the meantime don't
expect that just because it's very smart about types in most respects
it will be smart about types involved in assignments.  (This doesn't
affect its ability to benefit from explicit type declarations
involving the assigned variables, only its ability to get by without
explicit type declarations.)

     <!-- <!- FIXME: Python dislikes assignments, but not in type -->
     <!-- inference. The real problems are loop induction, closed over -->
     <!-- variables and aliases. -> -->
     </li><li>Since the time the CMUCL manual was written, CMUCL (and thus SBCL) has
gotten a generational garbage collector. This means that there are
some efficiency implications of various patterns of memory usage which
aren't discussed in the CMUCL manual. (Some new material should be
written about this.)

     </li><li>SBCL has some important known efficiency problems.  Perhaps the most
important are

          <ul>
<li>The garbage collector is not particularly efficient, at least on
platforms without the generational collector (as of SBCL 0.8.9, all
except x86).

          </li><li>Various aspects of the PCL implementation of CLOS are more inefficient
than necessary.

     </li></ul>

   </li></ul>

   <p>Finally, note that Common Lisp defines many constructs which, in
the infamous phrase, “could be compiled efficiently by a
sufficiently smart compiler”. The phrase is infamous because
making a compiler which actually is sufficiently smart to find all
these optimizations systematically is well beyond the state of the art
of current compiler technology. Instead, they're optimized on a
case-by-case basis by hand-written code, or not optimized at all if
the appropriate case hasn't been hand-coded. Some cases where no such
hand-coding has been done as of SBCL version 0.6.3 include

     </p><ul>
<li><code>(reduce #'f x)</code> where the type of <code>x</code> is known at compile
time

     </li><li>various bit vector operations, e.g.  <code>(position 0
some-bit-vector)</code>

     </li><li>specialized sequence idioms, e.g.  <code>(remove item list :count 1)</code>

     </li><li>cases where local compilation policy does not require excessive type
checking, e.g.  <code>(locally (declare (safety 1)) (assoc item
list))</code> (which currently performs safe <code>endp</code> checking internal
to assoc).

   </li></ul>

   <p>If your system's performance is suffering because of some construct
which could in principle be compiled efficiently, but which the SBCL
compiler can't in practice compile efficiently, consider writing a
patch to the compiler and submitting it for inclusion in the main
sources. Such code is often reasonably straightforward to write;
search the sources for the string “<code>deftransform</code>” to find many
examples (some straightforward, some less so).

</p><div class="node">
<a name="Beyond-the-ANSI-Standard"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Function-Interface">Foreign Function Interface</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Efficiency">Efficiency</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">7 Beyond the ANSI Standard</h2>

<p>SBCL is derived from CMUCL, which implements many extensions to the
ANSI standard. SBCL doesn't support as many extensions as CMUCL, but
it still has quite a few.  See <a href="#Contributed-Modules">Contributed Modules</a>.

</p><ul class="menu">
<li><a accesskey="1" href="#Reader-Extensions">Reader Extensions</a>
</li><li><a accesskey="2" href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a>
</li><li><a accesskey="3" href="#Package-Variance">Package Variance</a>
</li><li><a accesskey="4" href="#Garbage-Collection">Garbage Collection</a>
</li><li><a accesskey="5" href="#Metaobject-Protocol">Metaobject Protocol</a>
</li><li><a accesskey="6" href="#Extensible-Sequences">Extensible Sequences</a>
</li><li><a accesskey="7" href="#Support-For-Unix">Support For Unix</a>
</li><li><a accesskey="8" href="#Unicode-Support">Unicode Support</a>
</li><li><a accesskey="9" href="#Customization-Hooks-for-Users">Customization Hooks for Users</a>
</li><li><a href="#Tools-To-Help-Developers">Tools To Help Developers</a>
</li><li><a href="#Resolution-of-Name-Conflicts">Resolution of Name Conflicts</a>
</li><li><a href="#Hash-Table-Extensions">Hash Table Extensions</a>
</li><li><a href="#Random-Number-Generation">Random Number Generation</a>
</li><li><a href="#Miscellaneous-Extensions">Miscellaneous Extensions</a>
</li><li><a href="#Stale-Extensions">Stale Extensions</a>
</li><li><a href="#Efficiency-Hacks">Efficiency Hacks</a>
</li></ul>

<div class="node">
<a name="Reader-Extensions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.1 Reader Extensions</h3>

<p><a name="index-Reader-Extensions-161"></a>
SBCL supports extended package prefix syntax, which allows specifying
an alternate package instead of <code>*package*</code> for the reader to use
as the default package for interning symbols:

</p><pre class="lisp">     <var>package-name</var>::<var>form-with-interning-into-package</var>
</pre>
   <p>Example:

</p><pre class="lisp">       'foo::(bar quux zot) == '(foo::bar foo::quux foo::zot)
</pre>
   <p>Doesn't alter <code>*package*</code>: if <code>foo::bar</code> would cause a
read-time package lock violation, so does <code>foo::(bar)</code>.

   </p><p>SBCL also extends the reader to normalize all symbols to Normalization
Form KC in builds with Unicode enabled. Whether symbols are normalized
is controlled by

   </p><p><a name="Function-sb_002dext_003areadtable_002dnormalization"></a>

</p><div class="defun">
— Function: <b>readtable-normalization [sb-ext]</b><var> readtable<a name="index-g_t_0040sbext_007breadtable_002dnormalization_007d-162"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>readtable</code> normalizes strings to <code>nfkc</code>, and <code>nil</code> otherwise. 
The <code>readtable-normalization</code> of the standard readtable is <code>t</code>. 
</p></blockquote></div>

   <p>Symbols created by
<a name="index-g_t_0040cl_007bintern_007d-163"></a><code>intern</code> and similar functions are not affected by this setting. If
<code>sb-ext:readtable-normalization</code> is <code>t</code>, symbols that are not
normalized are escaped during printing.

</p><div class="node">
<a name="Package-Local-Nicknames"></a>
<a name="Package_002dLocal-Nicknames"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Package-Variance">Package Variance</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Reader-Extensions">Reader Extensions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.2 Package-Local Nicknames</h3>

<p><a name="index-Package_002dLocal-Nicknames-164"></a>
SBCL allows giving packages local nicknames: they allow short and
easy-to-use names to be used without fear of name conflict associated
with normal nicknames.

   </p><p>A local nickname is valid only when inside the package for which it
has been specified. Different packages can use same local nickname for
different global names, or different local nickname for same global
name.

   </p><p>Symbol <code>:package-local-nicknames</code> in <code>*features*</code> denotes the
support for this feature.

   </p><p><a name="index-g_t_0040cl_007bdefpackage_007d-165"></a>

</p><div class="defun">
— Macro: <b>defpackage [cl]</b><var> name </var>[[<var>option</var>]]<var>* ⇒ package<a name="index-g_t_0040cl_007bdefpackage_007d-166"></a></var><br>
<blockquote>
        <p>Options are extended to include

          </p><ul>
<li><code>:local-nicknames (</code><var>local-nickname</var> <var>actual-package-name</var><code>)*</code>

          <p>The package has the specified local nicknames for the corresponding
actual packages. 
</p></li></ul>

        <p>Example:

     </p><pre class="lisp">          (defpackage :bar (:intern "X"))
          (defpackage :foo (:intern "X"))
          (defpackage :quux (:use :cl) (:local-nicknames (:bar :foo) (:foo :bar)))
          (find-symbol "X" :foo) ; =&gt; FOO::X
          (find-symbol "X" :bar) ; =&gt; BAR::X
          (let ((*package* (find-package :quux)))
            (find-symbol "X" :foo))               ; =&gt; BAR::X
          (let ((*package* (find-package :quux)))
            (find-symbol "X" :bar))               ; =&gt; FOO::X
</pre>
        </blockquote></div>

   <p><a name="Function-sb_002dext_003apackage_002dlocal_002dnicknames"></a>

</p><div class="defun">
— Function: <b>package-local-nicknames [sb-ext]</b><var> package-designator<a name="index-g_t_0040sbext_007bpackage_002dlocal_002dnicknames_007d-167"></a></var><br>
<blockquote><p>Returns an alist of (local-nickname . actual-package) describing the
nicknames local to the designated package.

        </p><p>When in the designated package, calls to <code>find-package</code> with the any of the
local-nicknames will return the corresponding actual-package instead. This
also affects all implied calls to <code>find-package</code>, including those performed by
the reader.

        </p><p>When printing a package prefix for a symbol with a package local nickname, the
local nickname is used instead of the real name in order to preserve
print-read consistency.

        </p><p>See also: <code>add-package-local-nickname</code>, <code>package-locally-nicknamed-by-list</code>,
<code>remove-package-local-nickname</code>, and the <code>defpackage</code> option <code>:local-nicknames</code>.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003apackage_002dlocally_002dnicknamed_002dby_002dlist"></a>

</p><div class="defun">
— Function: <b>package-locally-nicknamed-by-list [sb-ext]</b><var> package-designator<a name="index-g_t_0040sbext_007bpackage_002dlocally_002dnicknamed_002dby_002dlist_007d-168"></a></var><br>
<blockquote><p>Returns a list of packages which have a local nickname for the designated
package.

        </p><p>See also: <code>add-package-local-nickname</code>, <code>package-local-nicknames</code>,
<code>remove-package-local-nickname</code>, and the <code>defpackage</code> option <code>:local-nicknames</code>.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aadd_002dpackage_002dlocal_002dnickname"></a>

</p><div class="defun">
— Function: <b>add-package-local-nickname [sb-ext]</b><var> local-nickname actual-package &amp;optional package-designator<a name="index-g_t_0040sbext_007badd_002dpackage_002dlocal_002dnickname_007d-169"></a></var><br>
<blockquote><p>Adds <code>local-nickname</code> for <code>actual-package</code> in the designated package, defaulting
to current package. <code>local-nickname</code> must be a string designator, and
<code>actual-package</code> must be a package designator.

        </p><p>Returns the designated package.

        </p><p>Signals a continuable error if <code>local-nickname</code> is already a package local
nickname for a different package, or if <code>local-nickname</code> is one of "CL",
"COMMON-LISP", or, "KEYWORD", or if <code>local-nickname</code> is a global name or
nickname for the package to which the nickname would be added.

        </p><p>When in the designated package, calls to <code>find-package</code> with the <code>local-nickname</code>
will return the package the designated <code>actual-package</code> instead. This also
affects all implied calls to <code>find-package</code>, including those performed by the
reader.

        </p><p>When printing a package prefix for a symbol with a package local nickname,
local nickname is used instead of the real name in order to preserve
print-read consistency.

        </p><p>See also: <code>package-local-nicknames</code>, <code>package-locally-nicknamed-by-list</code>,
<code>remove-package-local-nickname</code>, and the <code>defpackage</code> option <code>:local-nicknames</code>.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aremove_002dpackage_002dlocal_002dnickname"></a>

</p><div class="defun">
— Function: <b>remove-package-local-nickname [sb-ext]</b><var> old-nickname &amp;optional package-designator<a name="index-g_t_0040sbext_007bremove_002dpackage_002dlocal_002dnickname_007d-170"></a></var><br>
<blockquote><p>If the designated package had <code>old-nickname</code> as a local nickname for
another package, it is removed. Returns true if the nickname existed and was
removed, and <code>nil</code> otherwise.

        </p><p>See also: <code>add-package-local-nickname</code>, <code>package-local-nicknames</code>,
<code>package-locally-nicknamed-by-list</code>, and the <code>defpackage</code> option <code>:local-nicknames</code>.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

<div class="node">
<a name="Package-Variance"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Garbage-Collection">Garbage Collection</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.3 Package Variance</h3>

<p>Common Lisp standard specifies that “If the new definition is at
variance with the current state of that package, the consequences are
undefined;” SBCL by default signals a full warning and retains as
much of the package state as possible.

   </p><p>This can be adjusted using <code>sb-ext:*on-package-variance*</code>:

   </p><p><a name="Variable-sb_002dext_003a_002aon_002dpackage_002dvariance_002a"></a>

</p><div class="defun">
— Variable: <b>*on-package-variance* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bon_002dpackage_002dvariance_007d_007d-171"></a></var><br>
<blockquote><p>Specifies behavior when redefining a package using <code>defpackage</code> and the
definition is in variance with the current state of the package.

        </p><p>The value should be of the form:

     </p><pre class="lisp">            (:WARN [T | packages-names] :ERROR [T | package-names])
</pre>
        <p>specifying which packages get which behaviour <code>--</code> with <code>t</code> signifying the default unless
otherwise specified. If default is not specified, <code>:warn</code> is used.

        </p><p><code>:warn</code> keeps as much state as possible and causes <code>sbcl</code> to signal a full warning.

        </p><p><code>:error</code> causes <code>sbcl</code> to signal an error when the variant <code>defpackage</code> form is executed,
with restarts provided for user to specify what action should be taken.

        </p><p>Example:

     </p><pre class="lisp">            (setf *on-package-variance* '(:warn (:swank :swank-backend) :error t))
</pre>
        <p>specifies to signal a warning if <code>swank</code> package is in variance, and an error otherwise. 
</p></blockquote></div>

<div class="node">
<a name="Garbage-Collection"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Metaobject-Protocol">Metaobject Protocol</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package-Variance">Package Variance</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.4 Garbage Collection</h3>

<p><a name="index-Garbage-collection-172"></a>
SBCL provides additional garbage collection functionality not
specified by ANSI.

   </p><p><a name="Variable-sb_002dext_003a_002aafter_002dgc_002dhooks_002a"></a>

</p><div class="defun">
— Variable: <b>*after-gc-hooks* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bafter_002dgc_002dhooks_007d_007d-173"></a></var><br>
<blockquote><p>Called after each garbage collection, except for garbage collections
triggered during thread exits. In a multithreaded environment these hooks may
run in any thread. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003agc"></a>

</p><div class="defun">
— Function: <b>gc [sb-ext]</b><var> &amp;key full gen &amp;allow-other-keys<a name="index-g_t_0040sbext_007bgc_007d-174"></a></var><br>
<blockquote><p>Initiate a garbage collection.

        </p><p>The default is to initiate a nursery collection, which may in turn
trigger a collection of one or more older generations as well. If <code>full</code>
is true, all generations are collected. If <code>gen</code> is provided, it can be
used to specify the oldest generation guaranteed to be collected.

        </p><p>On CheneyGC platforms arguments <code>full</code> and <code>gen</code> take no effect: a full
collection is always performed. 
</p></blockquote></div>

<h4 class="subsection">7.4.1 Finalization</h4>

<p><a name="index-Finalization-175"></a>
Finalization allows code to be executed after an object has been
garbage collected. This is useful for example for releasing foreign
memory associated with a Lisp object.

   </p><p><a name="Function-sb_002dext_003afinalize"></a>

</p><div class="defun">
— Function: <b>finalize [sb-ext]</b><var> object function &amp;key dont-save<a name="index-g_t_0040sbext_007bfinalize_007d-176"></a></var><br>
<blockquote><p>Arrange for the designated <code>function</code> to be called when there
are no more references to <code>object</code>, including references in
<code>function</code> itself.

        </p><p>If <code>dont-save</code> is true, the finalizer will be cancelled when
<code>save-lisp-and-die</code> is called: this is useful for finalizers
deallocating system memory, which might otherwise be called
with addresses from the old image.

        </p><p>In a multithreaded environment <code>function</code> may be called in any
thread. In both single and multithreaded environments <code>function</code>
may be called in any dynamic scope: consequences are unspecified
if <code>function</code> is not fully re-entrant.

        </p><p>Errors from <code>function</code> are handled and cause a <code>warning</code> to be
signalled in whichever thread the <code>function</code> was called in.

        </p><p>Examples:

     </p><pre class="lisp">            ;;; GOOD, assuming RELEASE-HANDLE is re-entrant.
            (let* ((handle (get-handle))
                   (object (make-object handle)))
             (finalize object (lambda () (release-handle handle)))
             object)
          
            ;;; BAD, finalizer refers to object being finalized, causing
            ;;; it to be retained indefinitely!
            (let* ((handle (get-handle))
                   (object (make-object handle)))
              (finalize object
                        (lambda ()
                          (release-handle (object-handle object)))))
          
            ;;; BAD, not re-entrant!
            (defvar *rec* nil)
          
            (defun oops ()
             (when *rec*
               (error "recursive OOPS"))
             (let ((*rec* t))
               (gc))) ; or just cons enough to cause one
          
            (progn
              (finalize "oops" #'oops)
              (oops)) ; GC causes re-entry to #'oops due to the finalizer
                      ; -&gt; ERROR, caught, WARNING signalled
</pre>
        </blockquote></div>

   <p><a name="Function-sb_002dext_003acancel_002dfinalization"></a>

</p><div class="defun">
— Function: <b>cancel-finalization [sb-ext]</b><var> object<a name="index-g_t_0040sbext_007bcancel_002dfinalization_007d-177"></a></var><br>
<blockquote><p>Cancel any finalization for <code>object</code>. 
</p></blockquote></div>

<h4 class="subsection">7.4.2 Weak Pointers</h4>

<p><a name="index-Weak-pointers-178"></a>
Weak pointers allow references to objects to be maintained without
keeping them from being garbage collected: useful for building caches
among other things.

   </p><p>Hash tables can also have weak keys and values: see <a href="#Hash-Table-Extensions">Hash Table Extensions</a>.

   </p><p><a name="Function-sb_002dext_003amake_002dweak_002dpointer"></a>

</p><div class="defun">
— Function: <b>make-weak-pointer [sb-ext]</b><var> object<a name="index-g_t_0040sbext_007bmake_002dweak_002dpointer_007d-179"></a></var><br>
<blockquote><p>Allocate and return a weak pointer which points to <code>object</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aweak_002dpointer_002dvalue"></a>

</p><div class="defun">
— Function: <b>weak-pointer-value [sb-ext]</b><var> weak-pointer<a name="index-g_t_0040sbext_007bweak_002dpointer_002dvalue_007d-180"></a></var><br>
<blockquote><p>If <code>weak-pointer</code> is valid, return the value of <code>weak-pointer</code> and <code>t</code>. 
If the referent of <code>weak-pointer</code> has been garbage collected,
returns the values <code>nil</code> and <code>nil</code>. 
</p></blockquote></div>

<h4 class="subsection">7.4.3 Introspection and Tuning</h4>

<p><a name="Variable-sb_002dext_003a_002agc_002drun_002dtime_002a"></a>

</p><div class="defun">
— Variable: <b>*gc-run-time* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bgc_002drun_002dtime_007d_007d-181"></a></var><br>
<blockquote><p>Total <code>cpu</code> time spent doing garbage collection (as reported by
<code>get-internal-run-time</code>.) Initialized to zero on startup. It is safe to bind
this to zero in order to measure <code>gc</code> time inside a certain section of code, but
doing so may interfere with results reported by eg. <code>time</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003abytes_002dconsed_002dbetween_002dgcs"></a>

</p><div class="defun">
— Function: <b>bytes-consed-between-gcs [sb-ext]</b><var><a name="index-g_t_0040sbext_007bbytes_002dconsed_002dbetween_002dgcs_007d-182"></a></var><br>
<blockquote><p>The amount of memory that will be allocated before the next garbage
collection is initiated. This can be set with <code>setf</code>.

        </p><p>On <code>gencgc</code> platforms this is the nursery size, and defaults to 5% of dynamic
space size.

        </p><p>Note: currently changes to this value are lost when saving core. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003adynamic_002dspace_002dsize"></a>

</p><div class="defun">
— Function: <b>dynamic-space-size [sb-ext]</b><var><a name="index-g_t_0040sbext_007bdynamic_002dspace_002dsize_007d-183"></a></var><br>
<blockquote><p>Size of the dynamic space in bytes. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aget_002dbytes_002dconsed"></a>

</p><div class="defun">
— Function: <b>get-bytes-consed [sb-ext]</b><var><a name="index-g_t_0040sbext_007bget_002dbytes_002dconsed_007d-184"></a></var><br>
<blockquote><p>Return the number of bytes consed since the program began. Typically
this result will be a consed bignum, so if you have an application (e.g. 
profiling) which can't tolerate the overhead of consing bignums, you'll
probably want either to hack in at a lower level (as the code in the
<code>sb-profile</code> package does), or to design a more microefficient interface
and submit it as a patch. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003agc_002dlogfile"></a>

</p><div class="defun">
— Function: <b>gc-logfile [sb-ext]</b><var><a name="index-g_t_0040sbext_007bgc_002dlogfile_007d-185"></a></var><br>
<blockquote><p>Return the pathname used to log garbage collections. Can be <code>setf</code>. 
Default is <code>nil</code>, meaning collections are not logged. If non-null, the
designated file is opened before and after each collection, and generation
statistics are appended to it. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ageneration_002daverage_002dage"></a>

</p><div class="defun">
— Function: <b>generation-average-age [sb-ext]</b><var> generation<a name="index-g_t_0040sbext_007bgeneration_002daverage_002dage_007d-186"></a></var><br>
<blockquote><p>Average age of memory allocated to <code>generation:</code> average number of times
objects allocated to the generation have seen younger objects promoted to it. 
Available on <code>gencgc</code> platforms only.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ageneration_002dbytes_002dallocated"></a>

</p><div class="defun">
— Function: <b>generation-bytes-allocated [sb-ext]</b><var> generation<a name="index-g_t_0040sbext_007bgeneration_002dbytes_002dallocated_007d-187"></a></var><br>
<blockquote><p>Number of bytes allocated to <code>generation</code> currently. Available on <code>gencgc</code>
platforms only.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ageneration_002dbytes_002dconsed_002dbetween_002dgcs"></a>

</p><div class="defun">
— Function: <b>generation-bytes-consed-between-gcs [sb-ext]</b><var> generation<a name="index-g_t_0040sbext_007bgeneration_002dbytes_002dconsed_002dbetween_002dgcs_007d-188"></a></var><br>
<blockquote><p>Number of bytes that can be allocated to <code>generation</code> before that
generation is considered for garbage collection. This value is meaningless for
generation 0 (the nursery): see <code>bytes-consed-between-gcs</code> instead. Default is
5% of the dynamic space size divided by the number of non-nursery generations. 
Can be assigned to using <code>setf</code>. Available on <code>gencgc</code> platforms only.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ageneration_002dminimum_002dage_002dbefore_002dgc"></a>

</p><div class="defun">
— Function: <b>generation-minimum-age-before-gc [sb-ext]</b><var> generation<a name="index-g_t_0040sbext_007bgeneration_002dminimum_002dage_002dbefore_002dgc_007d-189"></a></var><br>
<blockquote><p>Minimum average age of objects allocated to <code>generation</code> before that
generation is may be garbage collected. Default is 0.75. See also
<code>generation-average-age</code>. Can be assigned to using <code>setf</code>. Available on <code>gencgc</code>
platforms only.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ageneration_002dnumber_002dof_002dgcs_002dbefore_002dpromotion"></a>

</p><div class="defun">
— Function: <b>generation-number-of-gcs-before-promotion [sb-ext]</b><var> generation<a name="index-g_t_0040sbext_007bgeneration_002dnumber_002dof_002dgcs_002dbefore_002dpromotion_007d-190"></a></var><br>
<blockquote><p>Number of times garbage collection is done on <code>generation</code> before
automatic promotion to the next generation is triggered. Default is 1. Can be
assigned to using <code>setf</code>. Available on <code>gencgc</code> platforms only.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ageneration_002dnumber_002dof_002dgcs"></a>

</p><div class="defun">
— Function: <b>generation-number-of-gcs [sb-ext]</b><var> generation<a name="index-g_t_0040sbext_007bgeneration_002dnumber_002dof_002dgcs_007d-191"></a></var><br>
<blockquote><p>Number of times garbage collection has been done on <code>generation</code> without
promotion. Available on <code>gencgc</code> platforms only.

        </p><p>Experimental: interface subject to change. 
</p></blockquote></div>

<div class="node">
<a name="Metaobject-Protocol"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Extensible-Sequences">Extensible Sequences</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Garbage-Collection">Garbage Collection</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.5 Metaobject Protocol</h3>

<h4 class="subsection">7.5.1 AMOP Compatibility of Metaobject Protocol</h4>

<p>SBCL supports a metaobject protocol which is intended to be compatible
with AMOP; present exceptions to this (as distinct from current bugs)
are:

     </p><ul>
<li><a name="index-g_t_0040sbmop_007bcompute_002deffective_002dmethod_007d-192"></a><code>compute-effective-method</code> only returns one value, not two.

     <p>There is no record of what the second return value was meant to
indicate, and apparently no clients for it.

     </p></li><li><a name="index-g_t_0040cl_007bgeneric_002dfunction_007d-193"></a><a name="index-g_t_0040cl_007bstandard_002dgeneric_002dfunction_007d-194"></a><a name="index-g_t_0040sbmop_007bfuncallable_002dstandard_002dobject_007d-195"></a><a name="index-g_t_0040cl_007bstandard_002dobject_007d-196"></a><a name="index-g_t_0040cl_007bfunction_007d-197"></a>The direct superclasses of <code>funcallable-standard-object</code> are
<code>(function standard-object)</code>, not <code>(standard-object function)</code>.

     <p>This is to ensure that the <code>standard-object</code> class is the last of
the standardized classes before <code>t</code> appearing in the class
precedence list of <code>generic-function</code> and
<code>standard-generic-function</code>, as required by section 1.4.4.5 of the
ANSI specification.

     </p></li><li><a name="index-g_t_0040cl_007bensure_002dgeneric_002dfunction_007d-198"></a><a name="index-g_t_0040sbmop_007bgeneric_002dfunction_002ddeclarations_007d-199"></a>the arguments <code>:declare</code> and <code>:declarations</code> to
<code>ensure-generic-function</code> are both accepted, with the leftmost
argument defining the declarations to be stored and returned by
<code>generic-function-declarations</code>.

     <p>Where AMOP specifies <code>:declarations</code> as the keyword argument to
<code>ensure-generic-function</code>, the Common Lisp standard specifies
<code>:declare</code>.  Portable code should use <code>:declare</code>.

     </p></li><li><a name="index-g_t_0040sbmop_007bvalidate_002dsuperclass_007d-200"></a><a name="index-g_t_0040sbmop_007bfinalize_002dinheritance_007d-201"></a><a name="index-g_t_0040cl_007bstandard_002dclass_007d-202"></a><a name="index-g_t_0040sbmop_007bfuncallable_002dstandard_002dclass_007d-203"></a><a name="index-g_t_0040cl_007bfunction_007d-204"></a><a name="index-g_t_0040sbmop_007bclass_002dprototype_007d-205"></a>although SBCL obeys the requirement in AMOP that
<code>validate-superclass</code> should treat <code>standard-class</code> and
<code>funcallable-standard-class</code> as compatible metaclasses, we
impose an additional requirement at class finalization time: a class
of metaclass <code>funcallable-standard-class</code> must have
<code>function</code> in its superclasses, and a class of metaclass
<code>standard-class</code> must not.

     <p><a name="index-g_t_0040cl_007btypep_007d-206"></a><a name="index-g_t_0040cl_007bclass_002dof_007d-207"></a><a name="index-g_t_0040cl_007bsubtypep_007d-208"></a>After a class has been finalized, it is associated with a class
prototype which is accessible by a standard mop function
<code>class-prototype</code>.  The user can then ask whether this object is a
<code>function</code> or not in several different ways: whether it is a
function according to <code>typep</code>; whether its <code>class-of</code> is
<code>subtypep</code> <code>function</code>, or whether <code>function</code> appears in
the superclasses of the class.  The additional consistency requirement
comes from the desire to make all of these answers the same.

     </p><p>The following class definitions are bad, and will lead to errors
either immediately or if an instance is created:
     </p><pre class="lisp">          (defclass bad-object (funcallable-standard-object)
            ()
            (:metaclass standard-class))
</pre>
     <pre class="lisp">          (defclass bad-funcallable-object (standard-object)
            ()
            (:metaclass funcallable-standard-class))
</pre>
     <p>The following definition is acceptable:
     </p><pre class="lisp">          (defclass mixin ()
            ((slot :initarg slot)))
          (defclass funcallable-object (funcallable-standard-object mixin)
            ()
            (:metaclass funcallable-standard-class))
</pre>
     <p>and leads to a class whose instances are funcallable and have one slot.

     </p><p><a name="index-g_t_0040sbmop_007bfuncallable_002dstandard_002dobject_007d-209"></a>Note that this requirement also applies to the class
<code>funcallable-standard-object</code>, which has metaclass
<code>funcallable-standard-class</code> rather than
<code>standard-class</code> as AMOP specifies.

     </p></li><li>the requirement that “No portable class C_p may inherit, by
virtue of being a direct or indirect subclass of a specified class, any
slot for which the name is a symbol accessible in the
<code>common-lisp-user</code> package or exported by any package defined in
the ANSI Common Lisp standard.” is interpreted to mean that the
standardized classes themselves should not have slots named by external
symbols of public packages.

     <p>The rationale behind the restriction is likely to be similar to the ANSI
Common Lisp restriction on defining functions, variables and types named
by symbols in the Common Lisp package: preventing two independent pieces
of software from colliding with each other.

     </p></li><li><a name="index-g_t_0040sbmop_007bslot_002dvalue_002dusing_002dclass_007d-210"></a><a name="index-g_t_0040setf_007b_0040sbmop_007bslot_002dvalue_002dusing_002dclass_007d_007d-211"></a><a name="index-g_t_0040sbmop_007bslot_002dboundp_002dusing_002dclass_007d-212"></a>specializations of the <code>new-value</code> argument to <code>(setf
slot-value-using-class)</code> are not allowed: all user-defined methods must
have a specializer of the class <code>t</code>.

     <p>This prohibition is motivated by a separation of layers: the
<code>slot-value-using-class</code> family of functions is intended for use in
implementing different and new slot allocation strategies, rather than
in performing application-level dispatching.  Additionally, with this
requirement, there is a one-to-one mapping between metaclass, class and
slot-definition-class tuples and effective methods of <code>(setf
slot-value-using-class)</code>, which permits optimization of <code>(setf
slot-value-using-class)</code>'s discriminating function in the same manner as
for <code>slot-value-using-class</code> and <code>slot-boundp-using-class</code>.

     </p><p>Note that application code may specialize on the <code>new-value</code>
argument of slot accessors.

     </p></li><li><a name="index-g_t_0040cl_007bdefclass_007d-213"></a><a name="index-g_t_0040sbmop_007bensure_002dclass_007d-214"></a><a name="index-g_t_0040sbmop_007bensure_002dclass_002dusing_002dclass_007d-215"></a><a name="index-g_t_0040cl_007bfind_002dclass_007d-216"></a><a name="index-g_t_0040cl_007bclass_002dname_007d-217"></a>the class named by the <code>name</code> argument to <code>ensure-class</code>, if
any, is only redefined if it is the proper name of that class;
otherwise, a new class is created.

     <p>This is consistent with the description of <code>ensure-class</code> in AMOP
as the functional version of <code>defclass</code>, which has this behaviour;
however, it is not consistent with the weaker requirement in AMOP, which
states that any class found by <code>find-class</code>, no matter what its
<code>class-name</code>, is redefined.

     </p></li><li><a name="index-g_t_0040sbmop_007bslot_002ddefinition_002dname_007d-218"></a><a name="index-g_t_0040cl_007bstructure_002dclass_007d-219"></a><a name="index-g_t_0040cl_007bdefstruct_007d-220"></a>an error is not signaled in the case of the <code>:name</code> initialization
argument for <code>slot-definition</code> objects being a constant, when the
slot definition is of type <code>structure-slot-definition</code> (i.e. it is
associated with a class of type <code>structure-class</code>).

     <p>This allows code which uses constant names for structure slots to
continue working as specified in ANSI, while enforcing the constraint
for all other types of slot.

     </p></li><li><a name="index-g_t_0040cl_007bt_007d-221"></a><a name="index-g_t_0040cl_007bbuilt_002din_002dclass_007d-222"></a><a name="index-g_t_0040sbmop_007bvalidate_002dsuperclass_007d-223"></a><a name="index-g_t_0040cl_007bdefclass_007d-224"></a>the class named <code>t</code> is not an instance of the <code>built-in-class</code>
metaclass.

     <p>AMOP specifies, in the “Inheritance Structure of Metaobject Classes”
section, that the class named <code>t</code> should be an instance of
<code>built-in-class</code>.  However, it also specifies that
<code>validate-superclass</code> should return true (indicating that a direct
superclass relationship is permissible) if the second argument is the
class named <code>t</code>.  Also, ANSI specifies that classes with metaclass
<code>built-in-class</code> may not be subclassed using <code>defclass</code>, and
also that the class named <code>t</code> is the universal superclass,
inconsistent with it being a <code>built-in-class</code>.

   </p></li></ul>

<h4 class="subsection">7.5.2 Metaobject Protocol Extensions</h4>

<p>In addition, SBCL supports extensions to the Metaobject protocol from
AMOP; at present, they are:

     </p><ul>
<li><a name="index-g_t_0040cl_007bdefmethod_007d-225"></a><a name="index-g_t_0040cl_007bfind_002dclass_007d-226"></a><a name="index-g_t_0040sbmop_007bintern_002deql_002dspecializer_007d-227"></a><a name="index-g_t_0040sbpcl_007bmake_002dmethod_002dspecializers_002dform_007d-228"></a><a name="index-g_t_0040sbmop_007bmake_002dmethod_002dlambda_007d-229"></a>compile-time support for generating specializer metaobjects from
specializer names in <code>defmethod</code> forms is provided by the
<code>make-method-specializers-form</code> function, which returns a form
which, when evaluated in the lexical environment of the
<code>defmethod</code>, returns a list of specializer metaobjects.  This
operator suffers from similar restrictions to those affecting
<code>make-method-lambda</code>, namely that the generic function must be
defined when the <code>defmethod</code> form is expanded, so that the
correct method of <code>make-method-specializers-form</code> is invoked. 
The system-provided method on <code>make-method-specializers-form</code>
generates a call to <code>find-class</code> for each symbol specializer
name, and a call to <code>intern-eql-specializer</code> for each <code>(eql
</code><var>x</var><code>)</code> specializer name.

     </li><li><a name="index-g_t_0040cl_007bfind_002dmethod_007d-230"></a><a name="index-g_t_0040sbpcl_007bparse_002dspecializer_002dusing_002dclass_007d-231"></a><a name="index-g_t_0040sbpcl_007bunparse_002dspecializer_002dusing_002dclass_007d-232"></a>run-time support for converting between specializer names and
specializer metaobjects, mostly for the purposes of
<code>find-method</code>, is provided by
<code>parse-specializer-using-class</code> and
<code>unparse-specializer-using-class</code>, which dispatch on their first
argument, the generic function associated with a method with the given
specializer.  The system-provided methods on those methods convert
between classes and proper names and between lists of the form
<code>(eql </code><var>x</var><code>)</code> and interned eql specializer objects.

     </li><li><a name="index-g_t_0040sbpcl_007b_002bslot_002dunbound_002b_007d-233"></a><a name="index-g_t_0040sbmop_007bstandard_002dinstance_002daccess_007d-234"></a><a name="index-g_t_0040sbmop_007bfuncallable_002dstandard_002dinstance_002daccess_007d-235"></a>distinguishing unbound instance allocated slots from bound ones when
using <code>standard-instance-access</code> and
<code>funcallable-standard-instance-access</code> is possible by comparison
to the constant <code>+slot-unbound+</code>.

   </li></ul>

<div class="node">
<a name="Extensible-Sequences"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Support-For-Unix">Support For Unix</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Metaobject-Protocol">Metaobject Protocol</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.6 Extensible Sequences</h3>

<ul class="menu">
<li><a accesskey="1" href="#Iterator-Protocol">Iterator Protocol</a>
</li><li><a accesskey="2" href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a>
</li></ul>

<p>ANSI Common Lisp has a class <code>sequence</code> with subclasses <code>list</code> and
<code>vector</code> on which the “sequence functions” like <code>find</code>,
<code>subseq</code>, etc. operate. As an extension to the ANSI specification,
SBCL allows additional subclasses of <code>sequence</code> to be defined
<a rel="footnote" href="#fn-6" name="fnd-6"><sup>6</sup></a>. 
<a name="index-g_t_0040cl_007bsequence_007d-236"></a><a name="index-g_t_0040cl_007bvector_007d-237"></a><a name="index-g_t_0040cl_007bfind_007d-238"></a><a name="index-g_t_0040cl_007bsubseq_007d-239"></a>
Users of this extension just make instances of <code>sequence</code> subclasses
and transparently operate on them using sequence functions:
</p><pre class="lisp">     (coerce (subseq (make-instance 'my-sequence) 5 10) 'list)
</pre>
   <p>From this perspective, no distinction between builtin and user-defined
<code>sequence</code> subclasses should be necessary. 
<a name="index-g_t_0040cl_007bcoerce_007d-240"></a><a name="index-g_t_0040cl_007bsubseq_007d-241"></a><a name="index-g_t_0040cl_007bmake_002dinstance_007d-242"></a><a name="index-g_t_0040cl_007blist_007d-243"></a>
Providers of the extension, that is of user-defined <code>sequence</code>
subclasses, have to adhere to a “sequence protocol” which consists of
a set of generic functions in the <code>sequence</code> package.

   </p><p>A minimal <code>sequence</code> subclass has to specify <code>standard-object</code> and
<code>sequence</code> as its superclasses and has to be the specializer of the
<code>sequence</code> parameter of methods on at least the following generic
functions:
<a name="index-g_t_0040cl_007bsequence_007d-244"></a><a name="index-g_t_0040cl_007bstandard_002dobject_007d-245"></a>

   </p><p><a name="Generic_002dFunction-sb_002dsequence_003alength"></a>

</p><div class="defun">
— Generic Function: <b>length [sb-sequence]</b><var> sequence<a name="index-g_t_0040sequence_007blength_007d-246"></a></var><br>
<blockquote><p>Returns the length of <code>sequence</code> or signals a <code>protocol-unimplemented</code>
   error if the sequence protocol is not implemented for the class of
   <code>sequence</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aelt"></a>

</p><div class="defun">
— Generic Function: <b>elt [sb-sequence]</b><var> sequence index<a name="index-g_t_0040sequence_007belt_007d-247"></a></var><br>
<blockquote><p>Returns the element at position <code>index</code> of <code>sequence</code> or signals a
   <code>protocol-unimplemented</code> error if the sequence protocol is not
   implemented for the class of <code>sequence</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-_0028setf-sb_002dsequence_003aelt_0029"></a>

</p><div class="defun">
— Generic Function: <b>(setf elt [sb-sequence])</b><var><a name="index-g_t_0040setf_007b_0040sequence_007belt_007d_007d-248"></a></var><br>
<blockquote><p>Replaces the element at position <code>index</code> of <code>sequence</code> with <code>new-value</code>
   and returns <code>new-value</code> or signals a <code>protocol-unimplemented</code> error if
   the sequence protocol is not implemented for the class of
   <code>sequence</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aadjust_002dsequence"></a>

</p><div class="defun">
— Generic Function: <b>adjust-sequence [sb-sequence]</b><var> sequence length &amp;key initial-element initial-contents<a name="index-g_t_0040sequence_007badjust_002dsequence_007d-249"></a></var><br>
<blockquote><p>Return destructively modified <code>sequence</code> or a freshly allocated
   sequence of the same class as <code>sequence</code> of length <code>length</code>. Elements
   of the returned sequence are initialized to <code>initial-element</code>, if
   supplied, initialized to <code>initial-contents</code> if supplied, or identical
   to the elements of <code>sequence</code> if neither is supplied. Signals a
   <code>protocol-unimplemented</code> error if the sequence protocol is not
   implemented for the class of <code>sequence</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003amake_002dsequence_002dlike"></a>

</p><div class="defun">
— Generic Function: <b>make-sequence-like [sb-sequence]</b><var> sequence length &amp;key initial-element initial-contents<a name="index-g_t_0040sequence_007bmake_002dsequence_002dlike_007d-250"></a></var><br>
<blockquote><p>Returns a freshly allocated sequence of length <code>length</code> and of the
   same class as <code>sequence</code>. Elements of the new sequence are
   initialized to <code>initial-element</code>, if supplied, initialized to
   <code>initial-contents</code> if supplied, or identical to the elements of
   <code>sequence</code> if neither is supplied. Signals a <code>protocol-unimplemented</code>
   error if the sequence protocol is not implemented for the class of
   <code>sequence</code>. 
</p></blockquote></div>

   <p><code>make-sequence-like</code> is needed for functions returning
freshly-allocated sequences such as <code>subseq</code> or
<code>copy-seq</code>. <code>adjust-sequence</code> is needed for functions which
destructively modify their arguments such as <code>delete</code>. In fact, all
other sequence functions can be implemented in terms of the above
functions and actually are, if no additional methods are
defined. However, relying on these generic implementations, in
particular not implementing the iterator protocol can incur a high
performance penalty See <a href="#Iterator-Protocol">Iterator Protocol</a>. 
<a name="index-g_t_0040cl_007bsequence_007d-251"></a><a name="index-g_t_0040sequence_007bmake_002dsequence_002dlike_007d-252"></a><a name="index-g_t_0040cl_007bsubseq_007d-253"></a><a name="index-g_t_0040cl_007bcopy_002dseq_007d-254"></a><a name="index-g_t_0040sequence_007badjust_002dsequence_007d-255"></a>
When the sequence protocol is only partially implemented for a given
<code>sequence</code> subclass, an attempt to apply one of the missing
operations to instances of that class signals the following condition:

   </p><p><a name="Condition-sb_002dsequence_003aprotocol_002dunimplemented"></a>

</p><div class="defun">
— Condition: <b>protocol-unimplemented [sb-sequence]</b><var><a name="index-g_t_0040sequence_007bprotocol_002dunimplemented_007d-256"></a></var><br>
<blockquote><p>Class precedence list: <code>protocol-unimplemented, type-error, error, serious-condition, condition, t</code>

        </p><p>This error is signaled if a sequence operation is applied to an
   instance of a sequence class that does not support the
   operation. 
</p></blockquote></div>

   <p>In addition to the mandatory functions above, methods on the sequence
functions listed below can be defined.

   </p><p>There are two noteworthy irregularities:
     </p><ul>
<li>The function <code>sb-sequence:emptyp</code> does not have a counterpart in
the <code>cl</code> package. It is intended to be used instead of
<code>length</code> when working with lazy or infinite sequences.

     </li><li>The functions <code>map</code>, <code>concatenate</code> and <code>merge</code> receive a
type designator specifying the type of the constructed sequence as their
first argument. However, the corresponding generic functions
<code>sb-sequence:map</code>, <code>sb-sequence:concatenate</code> and
<code>sb-sequence:merge</code> receive a prototype instance of the requested
<code>sequence</code> subclass instead. 
</li></ul>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aemptyp"></a>

</p><div class="defun">
— Generic Function: <b>emptyp [sb-sequence]</b><var> sequence<a name="index-g_t_0040sequence_007bemptyp_007d-257"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>sequence</code> is an empty sequence and <code>nil</code>
   otherwise. Signals an error if <code>sequence</code> is not a sequence. 
</p></blockquote></div>

     <ul>
<li><code>sb-sequence:count</code>, <code>sb-sequence:count-if</code>, <code>sb-sequence:count-if-not</code>

     </li><li><code>sb-sequence:find</code>, <code>sb-sequence:find-if</code>, <code>sb-sequence:find-if-not</code>

     </li><li><code>sb-sequence:position</code>, <code>sb-sequence:position-if</code>, <code>sb-sequence:position-if-not</code>

     </li><li><code>sb-sequence:subseq</code>

     </li><li><code>sb-sequence:copy-seq</code>

     </li><li><code>sb-sequence:fill</code>

     </li><li><a name="Generic_002dFunction-sb_002dsequence_003amap"></a>

     <div class="defun">
— Generic Function: <b>map [sb-sequence]</b><var> result-prototype function sequence &amp;rest sequences<a name="index-g_t_0040sequence_007bmap_007d-258"></a></var><br>
<blockquote> <p>Implements <code>cl:map</code> for extended sequences.

             </p><p><code>result-prototype</code> corresponds to the <code>result-type</code> of <code>cl:map</code> but
    receives a prototype instance of an extended sequence class
    instead of a type specifier. By dispatching on <code>result-prototype</code>,
    methods on this generic function specify how extended sequence
    classes act when they are specified as the result type in a <code>cl:map</code>
    call. <code>result-prototype</code> may not be fully initialized and thus
    should only be used for dispatch and to determine its class.

             </p><p>Another difference to <code>cl:map</code> is that <code>function</code> is a function, not a
    function designator. 
</p></blockquote></div>

     </li><li><code>sb-sequence:nsubstitute</code>, <code>sb-sequence:nsubstitute-if</code>,
<code>sb-sequence:nsubstitute-if-not</code>, <code>sb-sequence:substitute</code>,
<code>sb-sequence:substitute-if</code>, <code>sb-sequence:substitute-if-not</code>

     </li><li><code>sb-sequence:replace</code>

     </li><li><code>sb-sequence:nreverse</code>, <code>sb-sequence:reverse</code>

     </li><li><a name="Generic_002dFunction-sb_002dsequence_003aconcatenate"></a>

     <div class="defun">
— Generic Function: <b>concatenate [sb-sequence]</b><var> result-prototype &amp;rest sequences<a name="index-g_t_0040sequence_007bconcatenate_007d-259"></a></var><br>
<blockquote> <p>Implements <code>cl:concatenate</code> for extended sequences.

             </p><p><code>result-prototype</code> corresponds to the <code>result-type</code> of <code>cl:concatenate</code>
    but receives a prototype instance of an extended sequence class
    instead of a type specifier. By dispatching on <code>result-prototype</code>,
    methods on this generic function specify how extended sequence
    classes act when they are specified as the result type in a
    <code>cl:concatenate</code> call. <code>result-prototype</code> may not be fully initialized
    and thus should only be used for dispatch and to determine its
    class. 
</p></blockquote></div>

     </li><li><code>sb-sequence:reduce</code>

     </li><li><code>sb-sequence:mismatch</code>

     </li><li><code>sb-sequence:search</code>

     </li><li><code>sb-sequence:delete</code>, <code>sb-sequence:delete-if</code>, <code>sb-sequence:delete-if-not</code>,
<code>sb-sequence:remove</code>, <code>sb-sequence:remove-if</code>, <code>sb-sequence:remove-if-not</code>,

     </li><li><code>sb-sequence:delete-duplicates</code>, <code>sb-sequence:remove-duplicates</code>

     </li><li><code>sb-sequence:sort</code>, <code>sb-sequence:stable-sort</code>

     </li><li><a name="Generic_002dFunction-sb_002dsequence_003amerge"></a>

     <div class="defun">
— Generic Function: <b>merge [sb-sequence]</b><var> result-prototype sequence1 sequence2 predicate &amp;key key<a name="index-g_t_0040sequence_007bmerge_007d-260"></a></var><br>
<blockquote> <p>Implements <code>cl:merge</code> for extended sequences.

             </p><p><code>result-prototype</code> corresponds to the <code>result-type</code> of <code>cl:merge</code> but
    receives a prototype instance of an extended sequence class
    instead of a type specifier. By dispatching on <code>result-prototype</code>,
    methods on this generic function specify how extended sequence
    classes act when they are specified as the result type in a
    <code>cl:merge</code> call. <code>result-prototype</code> may not be fully initialized and
    thus should only be used for dispatch and to determine its class.

             </p><p>Another difference to <code>cl:merge</code> is that <code>predicate</code> is a function,
    not a function designator. 
</p></blockquote></div>
     </li></ul>

   <p>In the spirit of <code>dolist</code>, generic sequences can be traversed using
the macro
<a name="index-g_t_0040cl_007bdolist_007d-261"></a>

   </p><p><a name="Macro-sb_002dsequence_003adosequence"></a>

</p><div class="defun">
— Macro: <b>dosequence [sb-sequence]</b> (<var>element sequence &amp;optional return</var>)<var> &amp;body body<a name="index-g_t_0040sequence_007bdosequence_007d-262"></a></var><br>
<blockquote><p>Executes <code>body</code> with <code>element</code> subsequently bound to each element of
  <code>sequence</code>, then returns <code>return</code>. 
</p></blockquote></div>

<div class="node">
<a name="Iterator-Protocol"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Extensible-Sequences">Extensible Sequences</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">7.6.1 Iterator Protocol</h4>

<p>The iterator protocol allows subsequently accessing some or all elements
of a sequence in forward or reverse direction. Users first call
<code>make-sequence-iterator</code> to create an iteration state and
receive functions to query and mutate it. These functions allow, among
other things, moving to, retrieving or modifying elements of the
sequence. An iteration state consists of a state object, a limit object,
a from-end indicator and the following six functions to query or mutate
this state:
<a name="index-g_t_0040sequence_007bmake_002dsequence_002diterator_007d-263"></a>

</p><div class="defun">
— Function: <code>step function</code><var> sequence iterator from-end<a name="index-g_t_0040code_007bstep-function_007d-264"></a></var><br>
<blockquote><p>Moves the iterator one position forward or backward in the associated
sequence depending on the iteration direction. 
</p></blockquote></div>

<div class="defun">
— Function: <code>endp function</code><var> sequence iterator limit from-end<a name="index-g_t_0040code_007bendp-function_007d-265"></a></var><br>
<blockquote><p>Returns non-<code>nil</code> when the iterator has reached the end of the
associated sequence with respect to the iteration direction. 
</p></blockquote></div>

<div class="defun">
— Function: <code>element function</code><var> sequence iterator<a name="index-g_t_0040code_007belement-function_007d-266"></a></var><br>
<blockquote><p>Returns the sequence element associated to the current position of the
iteration. 
</p></blockquote></div>

<div class="defun">
— Function: <code>setf element function</code><var> new-value sequence iterator<a name="index-g_t_0040code_007bsetf-element-function_007d-267"></a></var><br>
<blockquote><p>Destructively modifies the associates sequence by replacing the sequence
element associated to the current iteration position with a new value. 
</p></blockquote></div>

<div class="defun">
— Function: <code>index function</code><var> sequence iterator<a name="index-g_t_0040code_007bindex-function_007d-268"></a></var><br>
<blockquote><p>Returns the position of the iteration in the associated sequence. 
</p></blockquote></div>

<div class="defun">
— Function: <code>copy function</code><var> sequence iterator<a name="index-g_t_0040code_007bcopy-function_007d-269"></a></var><br>
<blockquote><p>Returns a copy of the iteration state which can be mutated independently
of the copied iteration state. 
</p></blockquote></div>

   <p>An iterator is created by calling:

   </p><p><a name="Generic_002dFunction-sb_002dsequence_003amake_002dsequence_002diterator"></a>

</p><div class="defun">
— Generic Function: <b>make-sequence-iterator [sb-sequence]</b><var> sequence &amp;key from-end start end<a name="index-g_t_0040sequence_007bmake_002dsequence_002diterator_007d-270"></a></var><br>
<blockquote><p>Returns a sequence iterator for <code>sequence</code> or, if <code>start</code> and/or <code>end</code>
   are supplied, the subsequence bounded by <code>start</code> and <code>end</code> as nine
   values:

        </p><p>1. iterator state
   2. limit
   3. from-end
   4. step function
   5. endp function
   6. element function
   7. setf element function
   8. index function
   9. copy state function

        </p><p>If <code>from-end</code> is <code>nil</code>, the constructed iterator visits the specified
   elements in the order in which they appear in <code>sequence</code>. Otherwise,
   the elements are visited in the opposite order. 
</p></blockquote></div>

   <p>Note that <code>make-sequence-iterator</code> calls
<code>make-simple-sequence-iterator</code> when there is no specialized
method for a particular <code>sequence</code> subclass. See <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a>. 
<a name="index-g_t_0040sequence_007bmake_002dsequence_002diterator_007d-271"></a><a name="index-g_t_0040sequence_007bmake_002dsimple_002dsequence_002diterator_007d-272"></a><a name="index-g_t_0040cl_007bsequence_007d-273"></a>
The following convenience macros simplify traversing sequences using
iterators:

   </p><p><a name="Macro-sb_002dsequence_003awith_002dsequence_002diterator"></a>

</p><div class="defun">
— Macro: <b>with-sequence-iterator [sb-sequence]</b> (<var>&amp;rest vars</var>) (<var>sequence &amp;rest args &amp;key from-end start end</var>)<var> &amp;body body<a name="index-g_t_0040sequence_007bwith_002dsequence_002diterator_007d-274"></a></var><br>
<blockquote><p>Executes <code>body</code> with the elements of <code>vars</code> bound to the iteration
  state returned by <code>make-sequence-iterator</code> for <code>sequence</code> and
  <code>args</code>. Elements of <code>vars</code> may be <code>nil</code> in which case the corresponding
  value returned by <code>make-sequence-iterator</code> is ignored. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dsequence_003awith_002dsequence_002diterator_002dfunctions"></a>

</p><div class="defun">
— Macro: <b>with-sequence-iterator-functions [sb-sequence]</b> (<var>step endp elt setf index copy</var>) (<var>sequence &amp;rest args &amp;key from-end start end</var>)<var> &amp;body body<a name="index-g_t_0040sequence_007bwith_002dsequence_002diterator_002dfunctions_007d-275"></a></var><br>
<blockquote><p>Executes <code>body</code> with the names <code>step</code>, <code>endp</code>, <code>elt</code>, <code>setf</code>, <code>index</code> and <code>copy</code>
  bound to local functions which execute the iteration state query and
  mutation functions returned by <code>make-sequence-iterator</code> for <code>sequence</code>
  and <code>args</code>. <code>step</code>, <code>endp</code>, <code>elt</code>, <code>setf</code>, <code>index</code> and <code>copy</code> have dynamic
  extent. 
</p></blockquote></div>

<div class="node">
<a name="Simple-Iterator-Protocol"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Iterator-Protocol">Iterator Protocol</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Extensible-Sequences">Extensible Sequences</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">7.6.2 Simple Iterator Protocol</h4>

<p>For cases in which the full flexibility and performance of the general
sequence iterator protocol is not required, there is a simplified
sequence iterator protocol consisting of a few generic functions which
can be specialized for iterator classes:

   </p><p><a name="Generic_002dFunction-sb_002dsequence_003aiterator_002dstep"></a>

</p><div class="defun">
— Generic Function: <b>iterator-step [sb-sequence]</b><var> sequence iterator from-end<a name="index-g_t_0040sequence_007biterator_002dstep_007d-276"></a></var><br>
<blockquote><p>Moves <code>iterator</code> one position forward or backward in <code>sequence</code>
   depending on the iteration direction encoded in <code>from-end</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aiterator_002dendp"></a>

</p><div class="defun">
— Generic Function: <b>iterator-endp [sb-sequence]</b><var> sequence iterator limit from-end<a name="index-g_t_0040sequence_007biterator_002dendp_007d-277"></a></var><br>
<blockquote><p>Returns non-NIL when <code>iterator</code> has reached <code>limit</code> (which may
   correspond to the end of SEQUENCE) with respect to the iteration
   direction encoded in <code>from-end</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aiterator_002delement"></a>

</p><div class="defun">
— Generic Function: <b>iterator-element [sb-sequence]</b><var> sequence iterator<a name="index-g_t_0040sequence_007biterator_002delement_007d-278"></a></var><br>
<blockquote><p>Returns the element of <code>sequence</code> associated to the position of
   <code>iterator</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-_0028setf-sb_002dsequence_003aiterator_002delement_0029"></a>

</p><div class="defun">
— Generic Function: <b>(setf iterator-element [sb-sequence])</b><var><a name="index-g_t_0040setf_007b_0040sequence_007biterator_002delement_007d_007d-279"></a></var><br>
<blockquote><p>Destructively modifies <code>sequence</code> by replacing the sequence element
   associated to position of <code>iterator</code> with <code>new-value</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aiterator_002dindex"></a>

</p><div class="defun">
— Generic Function: <b>iterator-index [sb-sequence]</b><var> sequence iterator<a name="index-g_t_0040sequence_007biterator_002dindex_007d-280"></a></var><br>
<blockquote><p>Returns the position of <code>iterator</code> in <code>sequence</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dsequence_003aiterator_002dcopy"></a>

</p><div class="defun">
— Generic Function: <b>iterator-copy [sb-sequence]</b><var> sequence iterator<a name="index-g_t_0040sequence_007biterator_002dcopy_007d-281"></a></var><br>
<blockquote><p>Returns a copy of <code>iterator</code> which also traverses <code>sequence</code> but can
   be mutated independently of <code>iterator</code>. 
</p></blockquote></div>

   <p>Iterator objects implementing the above simple iteration protocol are
created by calling the following generic function:

   </p><p><a name="Generic_002dFunction-sb_002dsequence_003amake_002dsimple_002dsequence_002diterator"></a>

</p><div class="defun">
— Generic Function: <b>make-simple-sequence-iterator [sb-sequence]</b><var> sequence &amp;key from-end start end<a name="index-g_t_0040sequence_007bmake_002dsimple_002dsequence_002diterator_007d-282"></a></var><br>
<blockquote><p>Returns a sequence iterator for <code>sequence</code>, <code>start</code>, <code>end</code> and <code>from-end</code>
   as three values:

        </p><p>1. iterator state
   2. limit
   3. from-end

        </p><p>The returned iterator can be used with the generic iterator
   functions <code>iterator-step</code>, <code>iterator-endp</code>, <code>iterator-element</code>, (SETF
   ITERATOR-ELEMENT), <code>iterator-index</code> and <code>iterator-copy</code>. 
</p></blockquote></div>

<div class="node">
<a name="Support-For-Unix"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Unicode-Support">Unicode Support</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Extensible-Sequences">Extensible Sequences</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.7 Support For Unix</h3>

<ul class="menu">
<li><a accesskey="1" href="#Command_002dline-arguments">Command-line arguments</a>
</li><li><a accesskey="2" href="#Querying-the-process-environment">Querying the process environment</a>
</li><li><a accesskey="3" href="#Running-external-programs">Running external programs</a>
</li></ul>

<div class="node">
<a name="Command-line-arguments"></a>
<a name="Command_002dline-arguments"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Querying-the-process-environment">Querying the process environment</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Support-For-Unix">Support For Unix</a>

</div>

<h4 class="subsection">7.7.1 Command-line arguments</h4>

<p><a name="index-g_t_0040sbext_007b_0040earmuffs_007bposix_002dargv_007d_007d-283"></a>
The UNIX command line can be read from the variable
<code>sb-ext:*posix-argv*</code>.

</p><div class="node">
<a name="Querying-the-process-environment"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Running-external-programs">Running external programs</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Command_002dline-arguments">Command-line arguments</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Support-For-Unix">Support For Unix</a>

</div>

<h4 class="subsection">7.7.2 Querying the process environment</h4>

<p>The UNIX environment can be queried with the
<code>sb-ext:posix-getenv</code> function.

   </p><p><a name="Function-sb_002dext_003aposix_002dgetenv"></a>

</p><div class="defun">
— Function: <b>posix-getenv [sb-ext]</b><var> name<a name="index-g_t_0040sbext_007bposix_002dgetenv_007d-284"></a></var><br>
<blockquote><p>Return the "value" part of the environment string "name=value" which
corresponds to <code>name</code>, or <code>nil</code> if there is none. 
</p></blockquote></div>

<div class="node">
<a name="Running-external-programs"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Querying-the-process-environment">Querying the process environment</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Support-For-Unix">Support For Unix</a>

</div>

<h4 class="subsection">7.7.3 Running external programs</h4>

<p>External programs can be run with <code>sb-ext:run-program</code>. 
<a rel="footnote" href="#fn-7" name="fnd-7"><sup>7</sup></a>

   </p><p><a name="Function-sb_002dext_003arun_002dprogram"></a>

</p><div class="defun">
— Function: <b>run-program [sb-ext]</b><var> program args &amp;key env 
environment wait search pty input if-input-does-not-exist output 
if-output-exists error if-error-exists status-hook external-format 
directory<a name="index-g_t_0040sbext_007brun_002dprogram_007d-285"></a></var><br>
<blockquote><p><code>run-program</code> creates a new process specified by the <code>program</code>
argument. <code>args</code> are the standard arguments that can be passed to a
program. For no arguments, use <code>nil</code> (which means that just the
name of the program is passed as arg 0).

        </p><p>The program arguments and the environment are encoded using the
default external format for streams.

        </p><p><code>run-program</code> will return a <code>process</code> structure. See the <code>cmu</code> Common Lisp
Users Manual for details about the <code>process</code> structure.

        </p><p>Notes about Unix environments (as in the <code>:environment</code> and <code>:env</code> args):

          </p><ul>
<li>The <code>sbcl</code> implementation of <code>run-program</code>, like Perl and many other
     programs, but unlike the original <code>cmu</code> <code>cl</code> implementation, copies
     the Unix environment by default. 
</li><li>Running Unix programs from a setuid process, or in any other
     situation where the Unix environment is under the control of someone
     else, is a mother lode of security problems. If you are contemplating
     doing this, read about it first. (The Perl community has a lot of good
     documentation about this and other security issues in script-like
     programs.)

        </li></ul>

          <dl>
<dt><em>The </em><code>&amp;key</code><em> arguments have the following meanings:</em></dt><dt><code>:environment</code></dt><dd>      a list of STRINGs describing the new Unix environment
      (as in "man environ"). The default is to copy the environment of
      the current process.

          <br></dd><dt><code>:env</code></dt><dd>      an alternative lossy representation of the new Unix environment,
      for compatibility with <code>cmu</code> <code>cl</code>

          <br></dd><dt><code>:search</code></dt><dd>      Look for <code>program</code> in each of the directories in the child's $PATH
      environment variable.  Otherwise an absolute pathname is required.

          <br></dd><dt><code>:wait</code></dt><dd>      If non-NIL (default), wait until the created process finishes.  If
      <code>nil</code>, continue running Lisp until the program finishes.

          <br></dd><dt><code>:pty</code></dt><dd>      Either <code>t</code>, <code>nil</code>, or a stream.  Unless <code>nil</code>, the subprocess is established
      under a <code>pty</code>.  If :pty is a stream, all output to this pty is sent to
      this stream, otherwise the <code>process-pty</code> slot is filled in with a stream
      connected to pty that can read output and write input.

          <br></dd><dt><code>:input</code></dt><dd>      Either <code>t</code>, <code>nil</code>, a pathname, a stream, or <code>:stream</code>.  If <code>t</code>, the standard
      input for the current process is inherited.  If <code>nil</code>, /dev/null
      is used.  If a pathname, the file so specified is used.  If a stream,
      all the input is read from that stream and sent to the subprocess.  If
      <code>:stream</code>, the <code>process-input</code> slot is filled in with a stream that sends
      its output to the process. Defaults to <code>nil</code>.

          <br></dd><dt><code>:if-input-does-not-exist</code><em> (when </em><code>:input</code><em> is the name of a file)</em></dt><dd>      can be one of:
         <code>:error</code> to generate an error
         <code>:create</code> to create an empty file
         <code>nil</code> (the default) to return <code>nil</code> from <code>run-program</code>

          <br></dd><dt><code>:output</code></dt><dd>      Either <code>t</code>, <code>nil</code>, a pathname, a stream, or <code>:stream</code>.  If <code>t</code>, the standard
      output for the current process is inherited.  If <code>nil</code>, /dev/null
      is used.  If a pathname, the file so specified is used.  If a stream,
      all the output from the process is written to this stream. If
      <code>:stream</code>, the <code>process-output</code> slot is filled in with a stream that can
      be read to get the output. Defaults to <code>nil</code>.

          <br></dd><dt><code>:if-output-exists</code><em> (when </em><code>:output</code><em> is the name of a file)</em></dt><dd>      can be one of:
         <code>:error</code> (the default) to generate an error
         <code>:supersede</code> to supersede the file with output from the program
         <code>:append</code> to append output from the program to the file
         <code>nil</code> to return <code>nil</code> from <code>run-program</code>, without doing anything

          <br></dd><dt><code>:error</code><em> and </em><code>:if-error-exists</code></dt><dd>      Same as <code>:output</code> and <code>:if-output-exists</code>, except that <code>:error</code> can also be
      specified as <code>:output</code> in which case all error output is routed to the
      same place as normal output.

          <br></dd><dt><code>:status-hook</code></dt><dd>      This is a function the system calls whenever the status of the
      process changes.  The function takes the process as an argument.

          <br></dd><dt><code>:external-format</code></dt><dd>      The external-format to use for <code>:input</code>, <code>:output</code>, and <code>:error</code> :STREAMs.

          <br></dd><dt><code>:directory</code></dt><dd>      Specifies the directory in which the program should be run. 
      <code>nil</code> (the default) means the directory is unchanged.

          <br></dd><dt><em>Windows specific options:</em></dt><dt><code>:escape-arguments</code><em> (default T)</em></dt><dd>      Controls escaping of the arguments passed to CreateProcess. 
</dd></dl>

        </blockquote></div>

   <p>When <code>sb-ext:run-program</code> is called with <code>wait</code> equal to
NIL, an instance of class <var>sb-ext:process</var> is returned.  The
following functions are available for use with processes:

   </p><p><a name="Function-sb_002dext_003aprocess_002dp"></a>

</p><div class="defun">
— Function: <b>process-p [sb-ext]</b><var> object<a name="index-g_t_0040sbext_007bprocess_002dp_007d-286"></a></var><br>
<blockquote><p><code>t</code> if <code>object</code> is a <code>process</code>, <code>nil</code> otherwise. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dinput"></a>

</p><div class="defun">
— Function: <b>process-input [sb-ext]</b><var> instance<a name="index-g_t_0040sbext_007bprocess_002dinput_007d-287"></a></var><br>
<blockquote><p>The input stream of the process or <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002doutput"></a>

</p><div class="defun">
— Function: <b>process-output [sb-ext]</b><var> instance<a name="index-g_t_0040sbext_007bprocess_002doutput_007d-288"></a></var><br>
<blockquote><p>The output stream of the process or <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002derror"></a>

</p><div class="defun">
— Function: <b>process-error [sb-ext]</b><var> instance<a name="index-g_t_0040sbext_007bprocess_002derror_007d-289"></a></var><br>
<blockquote><p>The error stream of the process or <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dalive_002dp"></a>

</p><div class="defun">
— Function: <b>process-alive-p [sb-ext]</b><var> process<a name="index-g_t_0040sbext_007bprocess_002dalive_002dp_007d-290"></a></var><br>
<blockquote><p>Return <code>t</code> if <code>process</code> is still alive, <code>nil</code> otherwise. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dstatus"></a>

</p><div class="defun">
— Function: <b>process-status [sb-ext]</b><var> process<a name="index-g_t_0040sbext_007bprocess_002dstatus_007d-291"></a></var><br>
<blockquote><p>Return the current status of <code>process</code>.  The result is one of <code>:running</code>,
   <code>:stopped</code>, <code>:exited</code>, or <code>:signaled</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dwait"></a>

</p><div class="defun">
— Function: <b>process-wait [sb-ext]</b><var> process &amp;optional check-for-stopped<a name="index-g_t_0040sbext_007bprocess_002dwait_007d-292"></a></var><br>
<blockquote><p>Wait for <code>process</code> to quit running for some reason. When
<code>check-for-stopped</code> is <code>t</code>, also returns when <code>process</code> is stopped. Returns
<code>process</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dexit_002dcode"></a>

</p><div class="defun">
— Function: <b>process-exit-code [sb-ext]</b><var> process<a name="index-g_t_0040sbext_007bprocess_002dexit_002dcode_007d-293"></a></var><br>
<blockquote><p>The exit code or the signal of a stopped process. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dcore_002ddumped"></a>

</p><div class="defun">
— Function: <b>process-core-dumped [sb-ext]</b><var> instance<a name="index-g_t_0040sbext_007bprocess_002dcore_002ddumped_007d-294"></a></var><br>
<blockquote><p><code>t</code> if a core image was dumped by the process. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dclose"></a>

</p><div class="defun">
— Function: <b>process-close [sb-ext]</b><var> process<a name="index-g_t_0040sbext_007bprocess_002dclose_007d-295"></a></var><br>
<blockquote><p>Close all streams connected to <code>process</code> and stop maintaining the
status slot. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aprocess_002dkill"></a>

</p><div class="defun">
— Function: <b>process-kill [sb-ext]</b><var> process signal &amp;optional whom<a name="index-g_t_0040sbext_007bprocess_002dkill_007d-296"></a></var><br>
<blockquote><p>Hand <code>signal</code> to <code>process</code>. If <code>whom</code> is <code>:pid</code>, use the kill Unix system call. If
   <code>whom</code> is <code>:process-group</code>, use the killpg Unix system call. If <code>whom</code> is
   <code>:pty-process-group</code> deliver the signal to whichever process group is
   currently in the foreground. 
</p></blockquote></div>

<div class="node">
<a name="Unicode-Support"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Customization-Hooks-for-Users">Customization Hooks for Users</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Support-For-Unix">Support For Unix</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.8 Unicode Support</h3>

<p>SBCL provides support for working with Unicode text and querying the
standard Unicode database for information about individual codepoints. 
Unicode-related functions are located in the <code>sb-unicode</code> package.

   </p><p>SBCL also extends ANSI character literal syntax to support Unicode
codepoints. You can either specify a character by its Unicode name, with
spaces replaced by underscores, if a unique name exists <a rel="footnote" href="#fn-8" name="fnd-8"><sup>8</sup></a> or
by giving its hexadecimal codepoint preceded by a “U”, an optional
“+”, and an arbitrary number of leading zeros. You may also input the
character directly into your source code if it can be encoded in your
file. If a character had an assigned name in Unicode 1.0 that was
distinct from its current name, you may also use that name (with spaces
replaced by underscores) to specify the character, unless the name is
already associated with a codepoint in the latest Unicode standard (such
as “BELL”).

   </p><p>For example, you can specify the codepoint U+00E1 (“Latin
Small Letter A With Acute”) as
     </p><ul>
<li><code>#\LATIN_SMALL_LETTER_A_WITH_ACUTE</code>
</li><li><code>#\LATIN_SMALL_LETTER_A_ACUTE</code>
</li><li><code>#\á</code> assuming a Unicode source file
</li><li><code>#\U00E1</code>
</li><li><code>#\UE1</code>
</li><li><code>#\U+00E1</code>
</li></ul>

<h4 class="subsection">7.8.1 Unicode property access</h4>

<p>The following functions can be used to find information about a Unicode
codepoint.

   </p><p><a name="Function-sb_002dunicode_003ageneral_002dcategory"></a>

</p><div class="defun">
— Function: <b>general-category [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bgeneral_002dcategory_007d-297"></a></var><br>
<blockquote><p>Returns the general category of <code>character</code> as it appears in UnicodeData.txt
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003abidi_002dclass"></a>

</p><div class="defun">
— Function: <b>bidi-class [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bbidi_002dclass_007d-298"></a></var><br>
<blockquote><p>Returns the bidirectional class of <code>character</code>
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003acombining_002dclass"></a>

</p><div class="defun">
— Function: <b>combining-class [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bcombining_002dclass_007d-299"></a></var><br>
<blockquote><p>Returns the canonical combining class (CCC) of <code>character</code>
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003adecimal_002dvalue"></a>

</p><div class="defun">
— Function: <b>decimal-value [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bdecimal_002dvalue_007d-300"></a></var><br>
<blockquote><p>Returns the decimal digit value associated with <code>character</code> or <code>nil</code> if
there is no such value.

        </p><p>The only characters in Unicode with a decimal digit value are those
that are part of a range of characters that encode the digits 0-9. 
Because of this, `(decimal-digit c) &lt;=&gt; (digit-char-p c 10)` in
#+sb-unicode builds
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003adigit_002dvalue"></a>

</p><div class="defun">
— Function: <b>digit-value [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bdigit_002dvalue_007d-301"></a></var><br>
<blockquote><p>Returns the Unicode digit value of <code>character</code> or <code>nil</code> if it doesn't exist.

        </p><p>Digit values are guaranteed to be integers between 0 and 9 inclusive. 
All characters with decimal digit values have the same digit value,
but there are characters (such as digits of number systems without a 0 value)
that have a digit value but no decimal digit value
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003anumeric_002dvalue"></a>

</p><div class="defun">
— Function: <b>numeric-value [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bnumeric_002dvalue_007d-302"></a></var><br>
<blockquote><p>Returns the numeric value of <code>character</code> or <code>nil</code> if there is no such value. 
Numeric value is the most general of the Unicode numeric properties. 
The only constraint on the numeric value is that it be a rational number. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003amirrored_002dp"></a>

</p><div class="defun">
— Function: <b>mirrored-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bmirrored_002dp_007d-303"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> needs to be mirrored in bidirectional text. 
Otherwise, returns <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003abidi_002dmirroring_002dglyph"></a>

</p><div class="defun">
— Function: <b>bidi-mirroring-glyph [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bbidi_002dmirroring_002dglyph_007d-304"></a></var><br>
<blockquote><p>Returns the mirror image of <code>character</code> if it exists. 
Otherwise, returns <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aage"></a>

</p><div class="defun">
— Function: <b>age [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bage_007d-305"></a></var><br>
<blockquote><p>Returns the version of Unicode in which <code>character</code> was assigned as a pair
of values, both integers, representing the major and minor version respectively. 
If <code>character</code> is not assigned in Unicode, returns <code>nil</code> for both values. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003ahangul_002dsyllable_002dtype"></a>

</p><div class="defun">
— Function: <b>hangul-syllable-type [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bhangul_002dsyllable_002dtype_007d-306"></a></var><br>
<blockquote><p>Returns the Hangul syllable type of <code>character</code>. 
The syllable type can be one of <code>:l</code>, <code>:v</code>, <code>:t</code>, <code>:lv</code>, or <code>:lvt</code>. 
If the character is not a Hangul syllable or Jamo, returns <code>nil</code>
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aeast_002dasian_002dwidth"></a>

</p><div class="defun">
— Function: <b>east-asian-width [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007beast_002dasian_002dwidth_007d-307"></a></var><br>
<blockquote><p>Returns the East Asian Width property of <code>character</code> as
one of the keywords <code>:n</code> (Narrow), <code>:a</code> (Ambiguous), <code>:h</code> (Halfwidth),
<code>:w</code> (Wide), <code>:f</code> (Fullwidth), or <code>:na</code> (Not applicable)
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003ascript"></a>

</p><div class="defun">
— Function: <b>script [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bscript_007d-308"></a></var><br>
<blockquote><p>Returns the Script property of <code>character</code> as a keyword. 
If <code>character</code> does not have a known script, returns <code>:unknown</code>
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003achar_002dblock"></a>

</p><div class="defun">
— Function: <b>char-block [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bchar_002dblock_007d-309"></a></var><br>
<blockquote><p>Returns the Unicode block in which <code>character</code> resides as a keyword. 
If <code>character</code> does not have a known block, returns <code>:no-block</code>
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aunicode_002d1_002dname"></a>

</p><div class="defun">
— Function: <b>unicode-1-name [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bunicode_002d1_002dname_007d-310"></a></var><br>
<blockquote><p>Returns the name assigned to <code>character</code> in Unicode 1.0 if it is distinct
from the name currently assigned to <code>character</code>. Otherwise, returns <code>nil</code>. 
This property has been officially obsoleted by the Unicode standard, and
is only included for backwards compatibility. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aproplist_002dp"></a>

</p><div class="defun">
— Function: <b>proplist-p [sb-unicode]</b><var> character property<a name="index-g_t_0040sbunicode_007bproplist_002dp_007d-311"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> has the specified <code>property</code>. 
<code>property</code> is a keyword representing one of the properties from PropList.txt,
with underscores replaced by dashes. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003auppercase_002dp"></a>

</p><div class="defun">
— Function: <b>uppercase-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007buppercase_002dp_007d-312"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> has the Unicode property Uppercase and <code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003alowercase_002dp"></a>

</p><div class="defun">
— Function: <b>lowercase-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007blowercase_002dp_007d-313"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> has the Unicode property Lowercase and <code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003acased_002dp"></a>

</p><div class="defun">
— Function: <b>cased-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bcased_002dp_007d-314"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> has a (Unicode) case, and <code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003acase_002dignorable_002dp"></a>

</p><div class="defun">
— Function: <b>case-ignorable-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bcase_002dignorable_002dp_007d-315"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> is Case Ignorable as defined in Unicode 6.3, Chapter
3
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aalphabetic_002dp"></a>

</p><div class="defun">
— Function: <b>alphabetic-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007balphabetic_002dp_007d-316"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> is Alphabetic according to the Unicode standard
and <code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aideographic_002dp"></a>

</p><div class="defun">
— Function: <b>ideographic-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bideographic_002dp_007d-317"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> has the Unicode property Ideographic,
which loosely corresponds to the set of "Chinese characters"
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003amath_002dp"></a>

</p><div class="defun">
— Function: <b>math-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bmath_002dp_007d-318"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> is a mathematical symbol according to Unicode and
<code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003awhitespace_002dp"></a>

</p><div class="defun">
— Function: <b>whitespace-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bwhitespace_002dp_007d-319"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> is whitespace according to Unicode
and <code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003asoft_002ddotted_002dp"></a>

</p><div class="defun">
— Function: <b>soft-dotted-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bsoft_002ddotted_002dp_007d-320"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> has a soft dot (such as the dots on i and j) which
disappears when accents are placed on top of it. and <code>nil</code> otherwise
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003ahex_002ddigit_002dp"></a>

</p><div class="defun">
— Function: <b>hex-digit-p [sb-unicode]</b><var> character &amp;key ascii<a name="index-g_t_0040sbunicode_007bhex_002ddigit_002dp_007d-321"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> is a hexadecimal digit and <code>nil</code> otherwise. 
If <code>:ascii</code> is non-NIL, fullwidth equivalents of the Latin letters A through <code>f</code>
are excluded. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003adefault_002dignorable_002dp"></a>

</p><div class="defun">
— Function: <b>default-ignorable-p [sb-unicode]</b><var> character<a name="index-g_t_0040sbunicode_007bdefault_002dignorable_002dp_007d-322"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>character</code> is a Default_Ignorable_Code_Point
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003agrapheme_002dbreak_002dclass"></a>

</p><div class="defun">
— Function: <b>grapheme-break-class [sb-unicode]</b><var> char<a name="index-g_t_0040sbunicode_007bgrapheme_002dbreak_002dclass_007d-323"></a></var><br>
<blockquote><p>Returns the grapheme breaking class of <code>character</code>, as specified in <code>uax</code> #29. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aword_002dbreak_002dclass"></a>

</p><div class="defun">
— Function: <b>word-break-class [sb-unicode]</b><var> char<a name="index-g_t_0040sbunicode_007bword_002dbreak_002dclass_007d-324"></a></var><br>
<blockquote><p>Returns the word breaking class of <code>character</code>, as specified in <code>uax</code> #29. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003asentence_002dbreak_002dclass"></a>

</p><div class="defun">
— Function: <b>sentence-break-class [sb-unicode]</b><var> char<a name="index-g_t_0040sbunicode_007bsentence_002dbreak_002dclass_007d-325"></a></var><br>
<blockquote><p>Returns the sentence breaking class of <code>character</code>, as specified in <code>uax</code> #29. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aline_002dbreak_002dclass"></a>

</p><div class="defun">
— Function: <b>line-break-class [sb-unicode]</b><var> character &amp;key resolve<a name="index-g_t_0040sbunicode_007bline_002dbreak_002dclass_007d-326"></a></var><br>
<blockquote><p>Returns the line breaking class of <code>character</code>, as specified in <code>uax</code> #14. 
If <code>:resolve</code> is <code>nil</code>, returns the character class found in the property file. 
If <code>:resolve</code> is non-NIL, centain line-breaking classes will be mapped to othec
classes as specified in the applicable standards. Addinionally, if <code>:resolve</code>
is <code>:east-asian</code>, Ambigious (class :AI) characters will be mapped to the
Ideographic (:ID) class instead of Alphabetic (:AL). 
</p></blockquote></div>

<h4 class="subsection">7.8.2 String operations</h4>

<p>SBCL can normalize strings using:

   </p><p><a name="Function-sb_002dunicode_003anormalize_002dstring"></a>

</p><div class="defun">
— Function: <b>normalize-string [sb-unicode]</b><var> string &amp;optional form filter<a name="index-g_t_0040sbunicode_007bnormalize_002dstring_007d-327"></a></var><br>
<blockquote><p>Normalize <code>string</code> to the Unicode normalization form form. 
Acceptable values for form are <code>:nfd</code>, <code>:nfc</code>, <code>:nfkd</code>, and <code>:nfkc</code>. 
If <code>filter</code> is a function it is called on each decomposed character and
only characters for which it returns <code>t</code> are collected. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003anormalized_002dp"></a>

</p><div class="defun">
— Function: <b>normalized-p [sb-unicode]</b><var> string &amp;optional form<a name="index-g_t_0040sbunicode_007bnormalized_002dp_007d-328"></a></var><br>
<blockquote><p>Tests if <code>string</code> is normalized to <code>form</code>
</p></blockquote></div>

   <p>SBCL implements the full range of Unicode case operations with the
functions

   </p><p><a name="Function-sb_002dunicode_003auppercase"></a>

</p><div class="defun">
— Function: <b>uppercase [sb-unicode]</b><var> string &amp;key locale<a name="index-g_t_0040sbunicode_007buppercase_007d-329"></a></var><br>
<blockquote><p>Returns the full uppercase of <code>string</code> according to the Unicode standard. 
The result is not guaranteed to have the same length as the input. If <code>:locale</code>
is <code>nil</code>, no language-specific case transformations are applied. If <code>:locale</code> is a
keyword representing a two-letter <code>iso</code> country code, the case transforms of that
locale are used. If <code>:locale</code> is <code>t</code>, the user's current locale is used (Unix and
Win32 only). 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003alowercase"></a>

</p><div class="defun">
— Function: <b>lowercase [sb-unicode]</b><var> string &amp;key locale<a name="index-g_t_0040sbunicode_007blowercase_007d-330"></a></var><br>
<blockquote><p>Returns the full lowercase of <code>string</code> according to the Unicode standard. 
The result is not guaranteed to have the same length as the input. 
<code>:locale</code> has the same semantics as the <code>:locale</code> argument to <code>uppercase</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003atitlecase"></a>

</p><div class="defun">
— Function: <b>titlecase [sb-unicode]</b><var> string &amp;key locale<a name="index-g_t_0040sbunicode_007btitlecase_007d-331"></a></var><br>
<blockquote><p>Returns the titlecase of <code>string</code>. The resulting string can
be longer than the input. 
<code>:locale</code> has the same semantics as the <code>:locale</code> argument to <code>uppercase</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003acasefold"></a>

</p><div class="defun">
— Function: <b>casefold [sb-unicode]</b><var> string<a name="index-g_t_0040sbunicode_007bcasefold_007d-332"></a></var><br>
<blockquote><p>Returns the full casefolding of <code>string</code> according to the Unicode standard. 
Casefolding removes case information in a way that allows the results to be used
for case-insensitive comparisons. 
The result is not guaranteed to have the same length as the input. 
</p></blockquote></div>

   <p>It also extends standard Common Lisp case functions such as
<a name="index-g_t_0040cl_007bstring_002dupcase_007d-333"></a><code>string-upcase</code> and
<a name="index-g_t_0040cl_007bchar_002ddowncase_007d-334"></a><code>string-downcase</code> to support a subset of Unicode's casing behavior. 
Specifically, a character is
<a name="index-g_t_0040cl_007bboth_002dcase_002dp_007d-335"></a><code>both-case-p</code> if its case mapping in Unicode is one-to-one and
invertable.

   </p><p>The <code>sb-unicode</code> package also provides functions for
collating/sorting strings according to the Unicode Collation Algorithm.

   </p><p><a name="Function-sb_002dunicode_003aunicode_003c"></a>

</p><div class="defun">
— Function: <b>unicode&lt; [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2<a name="index-g_t_0040sbunicode_007bunicode_003c_007d-336"></a></var><br>
<blockquote><p>Determines whether STRING1 sorts before STRING2 using the Unicode Collation
Algorithm, The function uses an untailored Default Unicode Collation Element Table
to produce the sort keys. The function uses the Shifted method for dealing
with variable-weight characters, as described in <code>uts</code> #10
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aunicode_003d"></a>

</p><div class="defun">
— Function: <b>unicode= [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2 strict<a name="index-g_t_0040sbunicode_007bunicode_003d_007d-337"></a></var><br>
<blockquote><p>Determines whether STRING1 and STRING2 are canonically equivalent according
to Unicode. The <code>start</code> and <code>end</code> arguments behave like the arguments to STRING=. 
If <code>:strict</code> is <code>nil</code>, UNICODE= tests compatibility equavalence instead. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aunicode_002dequal"></a>

</p><div class="defun">
— Function: <b>unicode-equal [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2 strict<a name="index-g_t_0040sbunicode_007bunicode_002dequal_007d-338"></a></var><br>
<blockquote><p>Determines whether STRING1 and STRING2 are canonically equivalent after
casefoldin8 (that is, ignoring case differences) according to Unicode. The
<code>start</code> and <code>end</code> arguments behave like the arguments to STRING=. If <code>:strict</code> is
<code>nil</code>, UNICODE= tests compatibility equavalence instead. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aunicode_003c_003d"></a>

</p><div class="defun">
— Function: <b>unicode&lt;= [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2<a name="index-g_t_0040sbunicode_007bunicode_003c_003d_007d-339"></a></var><br>
<blockquote><p>Tests if STRING1 and STRING2 are either UNICODE&lt; or UNICODE=
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aunicode_003e"></a>

</p><div class="defun">
— Function: <b>unicode&gt; [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2<a name="index-g_t_0040sbunicode_007bunicode_003e_007d-340"></a></var><br>
<blockquote><p>Tests if STRING2 is UNICODE&lt; STRING1. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003aunicode_003e_003d"></a>

</p><div class="defun">
— Function: <b>unicode&gt;= [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2<a name="index-g_t_0040sbunicode_007bunicode_003e_003d_007d-341"></a></var><br>
<blockquote><p>Tests if STRING1 and STRING2 are either UNICODE= or UNICODE&gt;
</p></blockquote></div>

   <p>The following functions are provided for detecting visually confusable strings:

   </p><p><a name="Function-sb_002dunicode_003aconfusable_002dp"></a>

</p><div class="defun">
— Function: <b>confusable-p [sb-unicode]</b><var> string1 string2 &amp;key start1 end1 start2 end2<a name="index-g_t_0040sbunicode_007bconfusable_002dp_007d-342"></a></var><br>
<blockquote><p>Determines whether STRING1 and STRING2 could be visually confusable
according to the <code>idna</code> confusableSummary.txt table
</p></blockquote></div>

<h4 class="subsection">7.8.3 Breaking strings</h4>

<p>The <code>sb-unicode</code> package includes several functions for breaking a
Unicode string into useful parts.

   </p><p><a name="Function-sb_002dunicode_003agraphemes"></a>

</p><div class="defun">
— Function: <b>graphemes [sb-unicode]</b><var> string<a name="index-g_t_0040sbunicode_007bgraphemes_007d-343"></a></var><br>
<blockquote><p>Breaks <code>string</code> into graphemes acording to the default
grapheme breaking rules specified in <code>uax</code> #29, returning a list of strings. 
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003awords"></a>

</p><div class="defun">
— Function: <b>words [sb-unicode]</b><var> string<a name="index-g_t_0040sbunicode_007bwords_007d-344"></a></var><br>
<blockquote><p>Breaks <code>string</code> into words acording to the default
word breaking rules specified in <code>uax</code> #29. Returns a list of strings
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003asentences"></a>

</p><div class="defun">
— Function: <b>sentences [sb-unicode]</b><var> string<a name="index-g_t_0040sbunicode_007bsentences_007d-345"></a></var><br>
<blockquote><p>Breaks <code>string</code> into sentences acording to the default
sentence breaking rules specified in <code>uax</code> #29
</p></blockquote></div>

   <p><a name="Function-sb_002dunicode_003alines"></a>

</p><div class="defun">
— Function: <b>lines [sb-unicode]</b><var> string &amp;key margin<a name="index-g_t_0040sbunicode_007blines_007d-346"></a></var><br>
<blockquote><p>Breaks <code>string</code> into lines that are no wider than <code>:margin</code> according to the
line breaking rules outlined in <code>uax</code> #14. Combining marks will always be kept
together with their base characters, and spaces (but not other types of
whitespace) will be removed from the end of lines. If <code>:margin</code> is unspecified,
it defaults to 80 characters
</p></blockquote></div>

<div class="node">
<a name="Customization-Hooks-for-Users"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Tools-To-Help-Developers">Tools To Help Developers</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Unicode-Support">Unicode Support</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.9 Customization Hooks for Users</h3>

<p>The toplevel repl prompt may be customized, and the function
that reads user input may be replaced completely. 
<!-- <!- FIXME but I don't currently remember how -> -->

   </p><p>The behaviour of <code>require</code> when called with only one argument is
implementation-defined.  In SBCL, <code>require</code> behaves in the
following way:

   </p><p><a name="Function-common_002dlisp_003arequire"></a>

</p><div class="defun">
— Function: <b>require [cl]</b><var> module-name &amp;optional pathnames<a name="index-g_t_0040cl_007brequire_007d-347"></a></var><br>
<blockquote><p>Loads a module, unless it already has been loaded. <code>pathnames</code>, if supplied,
   is a designator for a list of pathnames to be loaded if the module
   needs to be. If <code>pathnames</code> is not supplied, functions from the list
   <code>*module-provider-functions*</code> are called in order with <code>module-name</code>
   as an argument, until one of them returns non-NIL.  User code is
   responsible for calling <code>provide</code> to indicate a successful load of the
   module. 
</p></blockquote></div>

   <p><a name="Variable-sb_002dext_003a_002amodule_002dprovider_002dfunctions_002a"></a>

</p><div class="defun">
— Variable: <b>*module-provider-functions* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bmodule_002dprovider_002dfunctions_007d_007d-348"></a></var><br>
<blockquote><p>See function documentation for <code>require</code>. 
</p></blockquote></div>

   <p>Although SBCL does not provide a resident editor, the <code>ed</code>
function can be customized to hook into user-provided editing
mechanisms as follows:

   </p><p><a name="Function-common_002dlisp_003aed"></a>

</p><div class="defun">
— Function: <b>ed [cl]</b><var> &amp;optional x<a name="index-g_t_0040cl_007bed_007d-349"></a></var><br>
<blockquote><p>Starts the editor (on a file or a function if named).  Functions
from the list <code>*ed-functions*</code> are called in order with <code>x</code> as an argument
until one of them returns non-NIL; these functions are responsible for
signalling a <code>file-error</code> to indicate failure to perform an operation on
the file system. 
</p></blockquote></div>

   <p><a name="Variable-sb_002dext_003a_002aed_002dfunctions_002a"></a>

</p><div class="defun">
— Variable: <b>*ed-functions* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bed_002dfunctions_007d_007d-350"></a></var><br>
<blockquote><p>See function documentation for <code>ed</code>. 
</p></blockquote></div>

   <p>Conditions of type <code>warning</code> and <code>style-warning</code> are
sometimes signaled at runtime, especially during execution of Common
Lisp defining forms such as <code>defun</code>, <code>defmethod</code>, etc.  To
muffle these warnings at runtime, SBCL provides a variable
<code>sb-ext:*muffled-warnings*</code>:

   </p><p><a name="Variable-sb_002dext_003a_002amuffled_002dwarnings_002a"></a>

</p><div class="defun">
— Variable: <b>*muffled-warnings* [sb-ext]</b><var><a name="index-g_t_0040sbext_007b_0040earmuffs_007bmuffled_002dwarnings_007d_007d-351"></a></var><br>
<blockquote><p>A type that ought to specify a subtype of <code>warning</code>.  Whenever a
warning is signaled, if the warning is of this type and is not
handled by any other handler, it will be muffled. 
</p></blockquote></div>

<div class="node">
<a name="Tools-To-Help-Developers"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Resolution-of-Name-Conflicts">Resolution of Name Conflicts</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Customization-Hooks-for-Users">Customization Hooks for Users</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.10 Tools To Help Developers</h3>

<p><a name="index-g_t_0040cl_007btrace_007d-352"></a><a name="index-g_t_0040cl_007binspect_007d-353"></a>
SBCL provides a profiler and other extensions to the ANSI <code>trace</code>
facility.  For more information, see <a href="#Macro-common_002dlisp_003atrace">Macro common-lisp:trace</a>.

   </p><p>The debugger supports a number of options. Its documentation is
accessed by typing <kbd>help</kbd> at the debugger prompt. See <a href="#Debugger">Debugger</a>.

   </p><p>Documentation for <code>inspect</code> is accessed by typing <kbd>help</kbd> at
the <code>inspect</code> prompt.

</p><div class="node">
<a name="Resolution-of-Name-Conflicts"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Hash-Table-Extensions">Hash Table Extensions</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Tools-To-Help-Developers">Tools To Help Developers</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<h3 class="section">7.11 Resolution of Name Conflicts</h3>

<p><a name="index-g_t_0040sbext_007bname_002dconflict_007d-354"></a><a name="index-g_t_0040sbext_007bname_002dconflict_002dsymbols_007d-355"></a>
The ANSI standard (section 11.1.1.2.5) requires that name conflicts in
packages be resolvable in favour of any of the conflicting symbols.  In
the interactive debugger, this is achieved by prompting for the symbol
in whose favour the conflict should be resolved; for programmatic use,
the <code>sb-ext:resolve-conflict</code> restart should be invoked with one
argument, which should be a member of the list returned by the condition
accessor <code>sb-ext:name-conflict-symbols</code>.

</p><div class="node">
<a name="Hash-Table-Extensions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Random-Number-Generation">Random Number Generation</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Resolution-of-Name-Conflicts">Resolution of Name Conflicts</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.12 Hash Table Extensions</h3>

<p><a name="index-Hash-tables-356"></a>
Hash table extensions supported by SBCL are all controlled by keyword
arguments to <code>make-hash-table</code>.

   </p><p><a name="Function-common_002dlisp_003amake_002dhash_002dtable"></a>

</p><div class="defun">
— Function: <b>make-hash-table [cl]</b><var> &amp;key test size rehash-size rehash-threshold hash-function weakness synchronized<a name="index-g_t_0040cl_007bmake_002dhash_002dtable_007d-357"></a></var><br>
<blockquote><p>Create and return a new hash table. The keywords are as follows:

          </p><dl>
<dt><code>:test</code></dt><dd>    Determines how keys are compared. Must a designator for one of the
    standard hash table tests, or a hash table test defined using
    <code>sb-ext:define-hash-table-test</code>. Additionally, when an explicit
    <code>hash-function</code> is provided (see below), any two argument equivalence
    predicate can be used as the <code>test</code>.

          <br></dd><dt><code>:size</code></dt><dd>    A hint as to how many elements will be put in this hash table.

          <br></dd><dt><code>:rehash-size</code></dt><dd>    Indicates how to expand the table when it fills up. If an integer, add
    space for that many elements. If a floating point number (which must be
    greater than 1.0), multiply the size by that amount.

          <br></dd><dt><code>:rehash-threshold</code></dt><dd>    Indicates how dense the table can become before forcing a rehash. Can be
    any positive number &lt;=1, with density approaching zero as the threshold
    approaches 0. Density 1 means an average of one entry per bucket.

          <br></dd><dt><code>:hash-function</code></dt><dd>    If <code>nil</code> (the default), a hash function based on the <code>test</code> argument is used,
    which then must be one of the standardized hash table test functions, or
    one for which a default hash function has been defined using
    <code>sb-ext:define-hash-table-test</code>. If <code>hash-function</code> is specified, the <code>test</code>
    argument can be any two argument predicate consistent with it. The
    <code>hash-function</code> is expected to return a non-negative fixnum hash code.

          <br></dd><dt><code>:weakness</code></dt><dd>    When <code>:weakness</code> is not <code>nil</code>, garbage collection may remove entries from the
    hash table. The value of <code>:weakness</code> specifies how the presence of a key or
    value in the hash table preserves their entries from garbage collection.

          <p>Valid values are:

          </p><p><code>:key</code> means that the key of an entry must be live to guarantee that the
        entry is preserved.

          </p><p><code>:value</code> means that the value of an entry must be live to guarantee that
        the entry is preserved.

          </p><p><code>:key-and-value</code> means that both the key and the value must be live to
        guarantee that the entry is preserved.

          </p><p><code>:key-or-value</code> means that either the key or the value must be live to
        guarantee that the entry is preserved.

          </p><p><code>nil</code> (the default) means that entries are always preserved.

          <br></p></dd><dt><code>:synchronized</code></dt><dd>    If <code>nil</code> (the default), the hash-table may have multiple concurrent readers,
    but results are undefined if a thread writes to the hash-table
    concurrently with another reader or writer. If <code>t</code>, all concurrent accesses
    are safe, but note that <code>clhs</code> 3.6 (Traversal Rules and Side Effects)
    remains in force. See also: <code>sb-ext:with-locked-hash-table</code>. This keyword
    argument is experimental, and may change incompatibly or be removed in the
    future. 
</dd></dl>

        </blockquote></div>

   <p><a name="Macro-sb_002dext_003adefine_002dhash_002dtable_002dtest"></a>

</p><div class="defun">
— Macro: <b>define-hash-table-test [sb-ext]</b><var> name hash-function<a name="index-g_t_0040sbext_007bdefine_002dhash_002dtable_002dtest_007d-358"></a></var><br>
<blockquote><p>Defines <code>name</code> as a new kind of hash table test for use with the <code>:test</code>
argument to <code>make-hash-table</code>, and associates a default <code>hash-function</code> with it.

        </p><p><code>name</code> must be a symbol naming a global two argument equivalence predicate. 
Afterwards both <code>'name</code> and <code>#'name</code> can be used with <code>:test</code> argument. In both
cases <code>hash-table-test</code> will return the symbol <code>name</code>.

        </p><p><code>hash-function</code> must be a symbol naming a global hash function consistent with
the predicate, or be a <code>lambda</code> form implementing one in the current lexical
environment. The hash function must compute the same hash code for any two
objects for which <code>name</code> returns true, and subsequent calls with already hashed
objects must always return the same hash code.

        </p><p>Note: The <code>:hash-function</code> keyword argument to <code>make-hash-table</code> can be used to
override the specified default hash-function.

        </p><p>Attempting to define <code>name</code> in a locked package as hash-table test causes a
package lock violation.

        </p><p>Examples:

     </p><pre class="lisp">            ;;; 1.
          
            ;; We want to use objects of type FOO as keys (by their
            ;; names.) EQUALP would work, but would make the names
            ;; case-insensitive -- which we don't want.
            (defstruct foo (name nil :type (or null string)))
          
            ;; Define an equivalence test function and a hash function.
            (defun foo-name= (f1 f2) (equal (foo-name f1) (foo-name f2)))
            (defun sxhash-foo-name (f) (sxhash (foo-name f)))
          
            (define-hash-table-test foo-name= sxhash-foo-name)
          
            ;; #'foo-name would work too.
            (defun make-foo-table () (make-hash-table :test 'foo-name=))
          
            ;;; 2.
          
            (defun == (x y) (= x y))
          
            (define-hash-table-test ==
              (lambda (x)
                ;; Hash codes must be consistent with test, so
                ;; not (SXHASH X), since
                ;;   (= 1 1.0)                   =&gt; T
                ;;   (= (SXHASH 1) (SXHASH 1.0)) =&gt; NIL
                ;; Note: this doesn't deal with complex numbers or
                ;; bignums too large to represent as double floats.
                (sxhash (coerce x 'double-float))))
          
            ;; #'== would work too
            (defun make-number-table () (make-hash-table :test '==))
</pre>
        </blockquote></div>

   <p><a name="Macro-sb_002dext_003awith_002dlocked_002dhash_002dtable"></a>

</p><div class="defun">
— Macro: <b>with-locked-hash-table [sb-ext]</b> (<var>hash-table</var>)<var> &amp;body body<a name="index-g_t_0040sbext_007bwith_002dlocked_002dhash_002dtable_007d-359"></a></var><br>
<blockquote><p>Limits concurrent accesses to <code>hash-table</code> for the duration of <code>body</code>. 
If <code>hash-table</code> is synchronized, <code>body</code> will execute with exclusive
ownership of the table. If <code>hash-table</code> is not synchronized, <code>body</code> will
execute with other <code>with-locked-hash-table</code> bodies excluded <code>--</code> exclusion
of hash-table accesses not surrounded by <code>with-locked-hash-table</code> is
unspecified. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ahash_002dtable_002dsynchronized_002dp"></a>

</p><div class="defun">
— Function: <b>hash-table-synchronized-p [sb-ext]</b><var> instance<a name="index-g_t_0040sbext_007bhash_002dtable_002dsynchronized_002dp_007d-360"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>hash-table</code> is synchronized. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003ahash_002dtable_002dweakness"></a>

</p><div class="defun">
— Function: <b>hash-table-weakness [sb-ext]</b><var> instance<a name="index-g_t_0040sbext_007bhash_002dtable_002dweakness_007d-361"></a></var><br>
<blockquote><p>Return the <code>weakness</code> of <code>hash-table</code> which is one of <code>nil</code>, <code>:key</code>,
<code>:value</code>, <code>:key-and-value</code>, <code>:key-or-value</code>. 
</p></blockquote></div>

<div class="node">
<a name="Random-Number-Generation"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Miscellaneous-Extensions">Miscellaneous Extensions</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Hash-Table-Extensions">Hash Table Extensions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.13 Random Number Generation</h3>

<p><a name="index-Random-Number-Generation-362"></a>
The initial value of <code>*random-state*</code> is the same each time SBCL
is started. This makes it possible for user code to obtain repeatable
pseudo random numbers using only standard-provided functionality. See
<code>seed-random-state</code> below for an SBCL extension that allows to
seed the random number generator from given data for an additional
possibility to achieve this. Non-repeatable random numbers can always
be obtained using <code>(make-random-state t)</code>.

   </p><p>The sequence of numbers produced by repeated calls to <code>random</code>
starting with the same random state and using the same sequence of
<code>limit</code> arguments is guaranteed to be reproducible only in the
same version of SBCL on the same platform, using the same code under
the same evaluator mode and compiler optimization qualities. Just two
examples of differences that may occur otherwise: calls to
<code>random</code> can be compiled differently depending on how much is
known about the <code>limit</code> argument at compile time, yielding
different results even if called with the same argument at run time,
and the results can differ depending on the machine's word size, for
example for limits that are fixnums under 64-bit word size but bignums
under 32-bit word size.

   </p><p><a name="Function-sb_002dext_003aseed_002drandom_002dstate"></a>

</p><div class="defun">
— Function: <b>seed-random-state [sb-ext]</b><var> &amp;optional state<a name="index-g_t_0040sbext_007bseed_002drandom_002dstate_007d-363"></a></var><br>
<blockquote><p>Make a random state object. The optional <code>state</code> argument specifies a seed
for deterministic pseudo-random number generation.

        </p><p>As per the Common Lisp standard for <code>make-random-state</code>,
          </p><ul>
<li>If <code>state</code> is <code>nil</code> or not supplied, return a copy of the default
  <code>*random-state*</code>. 
</li><li>If <code>state</code> is a random state, return a copy of it. 
</li><li>If <code>state</code> is <code>t</code>, return a randomly initialized state (using operating-system
  provided randomness where available, otherwise a poor substitute based on
  internal time and pid).

        </li></ul>
        As a supported <code>sbcl</code> extension, we also support receiving as a seed an object
of the following types:
          <ul>
<li><code>(simple-array (unsigned-byte 8) (*))</code>
</li><li><code>unsigned-byte</code>
</li></ul>
        While we support arguments of any size and will mix the provided bits into
the random state, it is probably overkill to provide more than 256 bits worth
of actual information.

        <p>This particular <code>sbcl</code> version also accepts an argument of the following type:
<code>(simple-array (unsigned-byte 32) (*))</code>

        </p><p>This particular <code>sbcl</code> version uses the popular MT19937 <code>prng</code> algorithm, and its
internal state only effectively contains about 19937 bits of information. 
http://www.math.sci.hiroshima-u.ac.jp/~m-mat/MT/emt.html
</p></blockquote></div>

   <p>Some notes on random floats: The standard doesn't prescribe a specific
method of generating random floats. The following paragraph describes
SBCL's current implementation and should be taken purely informational,
that is, user code should not depend on any of its specific properties. 
The method used has been chosen because it is common, conceptually
simple and fast.

   </p><p>To generate random floats, SBCL evaluates code that has an equivalent
effect as
</p><pre class="lisp">     (* limit
        (float (/ (random (expt 2 23)) (expt 2 23)) 1.0f0))
</pre>
   <p>(for single-floats) and correspondingly (with <code>52</code> and
<code>1.0d0</code> instead of <code>23</code> and <code>1.0f0</code>) for double-floats. 
Note especially that this means that zero is a possible return value
occurring with probability <code>(expt 2 -23)</code> respectively
<code>(expt 2 -52)</code>. Also note that there exist twice as many
equidistant floats between 0 and 1 as are generated. For example, the
largest number that <code>(random 1.0f0)</code> ever returns is
<code>(float (/ (1- (expt 2 23)) (expt 2 23)) 1.0f0)</code> while
<code>(float (/ (1- (expt 2 24)) (expt 2 24)) 1.0f0)</code> is the
largest single-float less than 1. This is a side effect of the fact
that the implementation uses the fastest possible conversion from bits
to floats.

   </p><p>SBCL currently uses the Mersenne Twister as its random number
generator, specifically the 32-bit version under both 32- and 64-bit
word size. The seeding algorithm has been improved several times by
the authors of the Mersenne Twister; SBCL uses the third version
(from 2002) which is still the most recent as of June 2012. The
implementation has been tested to provide output identical to the
recommended C implementation.

   </p><p>While the Mersenne Twister generates random numbers of much better
statistical quality than other widely used generators, it uses only
linear operations modulo 2 and thus fails some statistical
tests<a rel="footnote" href="#fn-9" name="fnd-9"><sup>9</sup></a>. 
For example, the distribution of ranks of (sufficiently large) random
binary matrices is much distorted compared to the theoretically
expected one when the matrices are generated by the Mersenne Twister. 
Thus, applications that are sensitive to this aspect should use a
different type of generator.

</p><div class="node">
<a name="Miscellaneous-Extensions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Stale-Extensions">Stale Extensions</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Random-Number-Generation">Random Number Generation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.14 Miscellaneous Extensions</h3>

<p><a name="Function-sb_002dext_003aarray_002dstorage_002dvector"></a>

</p><div class="defun">
— Function: <b>array-storage-vector [sb-ext]</b><var> array<a name="index-g_t_0040sbext_007barray_002dstorage_002dvector_007d-364"></a></var><br>
<blockquote><p>Returns the underlying storage vector of <code>array</code>, which must be a non-displaced array.

        </p><p>In <code>sbcl</code>, if <code>array</code> is a of type <code>(simple-array * (*))</code>, it is its own storage
vector. Multidimensional arrays, arrays with fill pointers, and adjustable
arrays have an underlying storage vector with the same <code>array-element-type</code> as
<code>array</code>, which this function returns.

        </p><p>Important note: the underlying vector is an implementation detail. Even though
this function exposes it, changes in the implementation may cause this
function to be removed without further warning. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003adelete_002ddirectory"></a>

</p><div class="defun">
— Function: <b>delete-directory [sb-ext]</b><var> pathspec &amp;key recursive<a name="index-g_t_0040sbext_007bdelete_002ddirectory_007d-365"></a></var><br>
<blockquote><p>Deletes the directory designated by <code>pathspec</code> (a pathname designator). 
Returns the truename of the directory deleted.

        </p><p>If <code>recursive</code> is false (the default), signals an error unless the directory is
empty. If <code>recursive</code> is true, first deletes all files and subdirectories. If
<code>recursive</code> is true and the directory contains symbolic links, the links are
deleted, not the files and directories they point to.

        </p><p>Signals an error if <code>pathspec</code> designates a file or a symbolic link instead of a
directory, or if the directory could not be deleted for any reason.

        </p><p>Both

     </p><pre class="lisp">             (DELETE-DIRECTORY "/tmp/foo")
             (DELETE-DIRECTORY "/tmp/foo/")
</pre>
        <p>delete the "foo" subdirectory of "/tmp", or signal an error if it does not
exist or if is a file or a symbolic link. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aget_002dtime_002dof_002dday"></a>

</p><div class="defun">
— Function: <b>get-time-of-day [sb-ext]</b><var><a name="index-g_t_0040sbext_007bget_002dtime_002dof_002dday_007d-366"></a></var><br>
<blockquote><p>Return the number of seconds and microseconds since the beginning of
the <code>unix</code> epoch (January 1st 1970.) 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003await_002dfor"></a>

</p><div class="defun">
— Macro: <b>wait-for [sb-ext]</b><var> test-form &amp;key timeout<a name="index-g_t_0040sbext_007bwait_002dfor_007d-367"></a></var><br>
<blockquote><p>Wait until <code>test-form</code> evaluates to true, then return its primary value. 
If <code>timeout</code> is provided, waits at most approximately <code>timeout</code> seconds before
returning <code>nil</code>.

        </p><p>If <code>with-deadline</code> has been used to provide a global deadline, signals a
<code>deadline-timeout</code> if <code>test-form</code> doesn't evaluate to true before the
deadline.

        </p><p>Experimental: subject to change without prior notice. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aassert_002dversion_002d_003e_003d"></a>

</p><div class="defun">
— Function: <b>assert-version-&gt;= [sb-ext]</b><var> &amp;rest subversions<a name="index-g_t_0040sbext_007bassert_002dversion_002d_003e_003d_007d-368"></a></var><br>
<blockquote><p>Asserts that the current <code>sbcl</code> is of version equal to or greater than
the version specified in the arguments.  A continuable error is signaled
otherwise.

        </p><p>The arguments specify a sequence of subversion numbers in big endian order. 
They are compared lexicographically with the runtime version, and versions
are treated as though trailed by an unbounded number of 0s.

        </p><p>For example, (assert-version-&gt;= 1 1 4) asserts that the current <code>sbcl</code> is
version 1.1.4[.0.0...] or greater, and (assert-version-&gt;= 1) that it is
version 1[.0.0...] or greater. 
</p></blockquote></div>

<div class="node">
<a name="Stale-Extensions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Efficiency-Hacks">Efficiency Hacks</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Miscellaneous-Extensions">Miscellaneous Extensions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.15 Stale Extensions</h3>

<p>SBCL has inherited from CMUCL various hooks to allow the user to
tweak and monitor the garbage collection process. These are somewhat
stale code, and their interface might need to be cleaned up. If you
have urgent need of them, look at the code in <samp><span class="file">src/code/gc.lisp</span></samp>
and bring it up on the developers' mailing list.

   </p><p>SBCL has various hooks inherited from CMUCL, like
<code>sb-ext:float-denormalized-p</code>, to allow a program to take
advantage of IEEE floating point arithmetic properties which aren't
conveniently or efficiently expressible using the ANSI standard. These
look good, and their interface looks good, but IEEE support is
slightly broken due to a stupid decision to remove some support for
infinities (because it wasn't in the ANSI spec and it didn't occur to
me that it was in the IEEE spec). If you need this stuff, take a look
at the code and bring it up on the developers' mailing
list.

</p><div class="node">
<a name="Efficiency-Hacks"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Stale-Extensions">Stale Extensions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">7.16 Efficiency Hacks</h3>

<p>The <code>sb-ext:purify</code> function causes SBCL first to collect all
garbage, then to mark all uncollected objects as permanent, never again
attempting to collect them as garbage. This can cause a large increase
in efficiency when using a primitive garbage collector, or a more
moderate increase in efficiency when using a more sophisticated garbage
collector which is well suited to the program's memory usage pattern. It
also allows permanent code to be frozen at fixed addresses, a
precondition for using copy-on-write to share code between multiple Lisp
processes.  This is less important with modern generational garbage
collectors, but not all SBCL platforms use such a garbage collector.

   </p><p><a name="Function-sb_002dext_003apurify"></a>

</p><div class="defun">
— Function: <b>purify [sb-ext]</b><var> &amp;key root-structures environment-name<a name="index-g_t_0040sbext_007bpurify_007d-369"></a></var><br>
<blockquote><p>This function optimizes garbage collection by moving all currently live
   objects into non-collected storage. <code>root-structures</code> is an optional list of
   objects which should be copied first to maximize locality.

        </p><p><code>defstruct</code> structures defined with the <code>(:pure t) </code>option are moved into
   read-only storage, further reducing <code>gc</code> cost. List and vector slots of pure
   structures are also moved into read-only storage.

        </p><p><code>environment-name</code> is unused.

        </p><p>This function is a no-op on platforms using the generational garbage
   collector (x86, x86-64, ppc, arm, arm64). 
</p></blockquote></div>

   <p>The <code>sb-ext:truly-the</code> special form declares the type of the
result of the operations, producing its argument; the declaration is
not checked. In short: don't use it.

   </p><p><a name="Special_002dOperator-sb_002dext_003atruly_002dthe"></a>

</p><div class="defun">
— Special Operator: <b>truly-the [sb-ext]</b><var> value-type form<a name="index-g_t_0040sbext_007btruly_002dthe_007d-370"></a></var><br>
<blockquote><p>Specifies that the values returned by <code>form</code> conform to the
<code>value-type</code>, and causes the compiler to trust this information
unconditionally.

        </p><p>Consequences are undefined if any result is not of the declared type
<code>--</code> typical symptoms including memory corruptions. Use with great
care. 
</p></blockquote></div>

   <p>The <code>sb-ext:freeze-type</code> declaration declares that a
type will never change, which can make type testing
(<code>typep</code>, etc.) more efficient for structure types.

</p><div class="node">
<a name="Foreign-Function-Interface"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Pathnames">Pathnames</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Beyond-the-ANSI-Standard">Beyond the ANSI Standard</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">8 Foreign Function Interface</h2>

<p>This chapter describes SBCL's interface to C programs and
libraries (and, since C interfaces are a sort of <em>lingua
franca</em> of the Unix world, to other programs and libraries in
general.)

   </p><blockquote>
Note: In the modern Lisp world, the usual term for this functionality
is Foreign Function Interface, or <acronym>FFI</acronym>, where despite the
mention of “function” in this term, <acronym>FFI</acronym> also
refers to direct manipulation of C data structures as well as
functions. The traditional CMUCL terminology is Alien Interface, and
while that older terminology is no longer used much in the system
documentation, it still reflected in names in the implementation,
notably in the name of the <code>SB-ALIEN</code> package. 
</blockquote>

<ul class="menu">
<li><a accesskey="1" href="#Introduction-to-the-Foreign-Function-Interface">Introduction to the Foreign Function Interface</a>
</li><li><a accesskey="2" href="#Foreign-Types">Foreign Types</a>
</li><li><a accesskey="3" href="#Operations-On-Foreign-Values">Operations On Foreign Values</a>
</li><li><a accesskey="4" href="#Foreign-Variables">Foreign Variables</a>
</li><li><a accesskey="5" href="#Foreign-Data-Structure-Examples">Foreign Data Structure Examples</a>
</li><li><a accesskey="6" href="#Loading-Shared-Object-Files">Loading Shared Object Files</a>
</li><li><a accesskey="7" href="#Foreign-Function-Calls">Foreign Function Calls</a>
</li><li><a accesskey="8" href="#Step_002dBy_002dStep-Example-of-the-Foreign-Function-Interface">Step-By-Step Example of the Foreign Function Interface</a>
</li></ul>

<div class="node">
<a name="Introduction-to-the-Foreign-Function-Interface"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Types">Foreign Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.1 Introduction to the Foreign Function Interface</h3>

<!-- AKA "Introduction to Aliens" in the CMU CL manual -->
<p>Because of Lisp's emphasis on dynamic memory allocation and garbage
collection, Lisp implementations use non-C-like memory representations
for objects.  This representation mismatch creates friction when a Lisp
program must share objects with programs which expect C data.  There
are three common approaches to establishing communication:

     </p><ul>
<li>The burden can be placed on the foreign program (and programmer) by
requiring the knowledge and use of the representations used internally
by the Lisp implementation.  This can require a considerable amount of
“glue” code on the C side, and that code tends to be sensitively
dependent on the internal implementation details of the Lisp system.

     </li><li>The Lisp system can automatically convert objects back and forth between
the Lisp and foreign representations.  This is convenient, but
translation becomes prohibitively slow when large or complex data
structures must be shared. This approach is supported by the SBCL
<acronym>FFI</acronym>, and used automatically when passing integers and strings.

     </li><li>The Lisp program can directly manipulate foreign objects through the
use of extensions to the Lisp language.

   </li></ul>

   <p>SBCL, like CMUCL before it, relies primarily on the automatic
conversion and direct manipulation approaches. The <code>SB-ALIEN</code>
package provides a facility wherein foreign values of simple scalar
types are automatically converted and complex types are directly
manipulated in their foreign representation.  Additionally the
lower-level System Area Pointers (or <acronym>SAP</acronym>s) can be used where
necessary to provide untyped access to foreign memory.

   </p><p>Any foreign objects that can't automatically be converted into Lisp
values are represented by objects of type <code>alien-value</code>.  Since
Lisp is a dynamically typed language, even foreign objects must have a
run-time type; this type information is provided by encapsulating the
raw pointer to the foreign data within an <code>alien-value</code> object.

   </p><p>The type language and operations on foreign types are
intentionally similar to those of the C language.

</p><div class="node">
<a name="Foreign-Types"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Operations-On-Foreign-Values">Operations On Foreign Values</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Introduction-to-the-Foreign-Function-Interface">Introduction to the Foreign Function Interface</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.2 Foreign Types</h3>

<!-- AKA "Alien Types" in the CMU CL manual -->
<p>Alien types have a description language based on nested list
structure. For example the C type

</p><pre class="example">     struct foo {
         int a;
         struct foo *b[100];
     };
</pre>
   <p>has the corresponding SBCL <acronym>FFI</acronym> type

</p><pre class="lisp">     (struct foo
       (a int)
       (b (array (* (struct foo)) 100)))
</pre>
   <ul class="menu">
<li><a accesskey="1" href="#Defining-Foreign-Types">Defining Foreign Types</a>
</li><li><a accesskey="2" href="#Foreign-Types-and-Lisp-Types">Foreign Types and Lisp Types</a>
</li><li><a accesskey="3" href="#Foreign-Type-Specifiers">Foreign Type Specifiers</a>
</li></ul>

<div class="node">
<a name="Defining-Foreign-Types"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Types-and-Lisp-Types">Foreign Types and Lisp Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Types">Foreign Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.2.1 Defining Foreign Types</h4>

<p>Types may be either named or anonymous.  With structure and union
types, the name is part of the type specifier, allowing recursively
defined types such as:

</p><pre class="lisp">     (struct foo (a (* (struct foo))))
</pre>
   <p>An anonymous structure or union type is specified by using the name
<code>nil</code>.  The <code>with-alien</code> macro defines a local scope which
“captures” any named type definitions.  Other types are not
inherently named, but can be given named abbreviations using the
<code>define-alien-type</code> macro.

</p><div class="node">
<a name="Foreign-Types-and-Lisp-Types"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Type-Specifiers">Foreign Type Specifiers</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Defining-Foreign-Types">Defining Foreign Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Types">Foreign Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.2.2 Foreign Types and Lisp Types</h4>

<p>The foreign types form a subsystem of the SBCL type system.  An
<code>alien</code> type specifier provides a way to use any foreign type as a
Lisp type specifier.  For example,

</p><pre class="lisp">     (typep <var>foo</var> '(alien (* int)))
</pre>
   <p>can be used to determine whether <var>foo</var> is a pointer to a foreign
<code>int</code>. <code>alien</code> type specifiers can be used in the same ways
as ordinary Lisp type specifiers (like <code>string</code>.) Alien type
declarations are subject to the same precise type checking as any
other declaration.  See <a href="#Precise-Type-Checking">Precise Type Checking</a>.

   </p><p>Note that the type identifiers used in the foreign type system overlap
with native Lisp type specifiers in some cases.  For example, the type
specifier <code>(alien single-float)</code> is identical to
<code>single-float</code>, since foreign floats are automatically converted
to Lisp floats.  When <code>type-of</code> is called on an alien value that
is not automatically converted to a Lisp value, then it will return an
<code>alien</code> type specifier.

</p><div class="node">
<a name="Foreign-Type-Specifiers"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-Types-and-Lisp-Types">Foreign Types and Lisp Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Types">Foreign Types</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.2.3 Foreign Type Specifiers</h4>

<p>Note: All foreign type names are exported from the <code>sb-alien</code>
package. Some foreign type names are also symbols in
the <code>common-lisp</code> package, in which case they are
reexported from the <code>sb-alien</code> package, so that
e.g. it is legal to refer to <code>sb-alien:single-float</code>.

   </p><p>These are the basic foreign type specifiers:

     </p><ul>
<li>The foreign type specifier <code>(* </code><var>foo</var><code>)</code> describes a pointer to
an object of type <var>foo</var>.  A pointed-to type <var>foo</var> of <code>t</code>
indicates a pointer to anything, similar to <code>void *</code> in
ANSI C. A null alien pointer can be detected with the
<code>sb-alien:null-alien</code> function.

     </li><li>The foreign type specifier <code>(array </code><var>foo</var><code> &amp;rest
dimensions)</code> describes array of the specified <code>dimensions</code>,
holding elements of type <var>foo</var>. Note that (unlike in C) <code>(*
</code><var>foo</var><code>)</code> and <code>(array </code><var>foo</var><code>)</code> are considered to be
different types when type checking is done. If equivalence of pointer
and array types is desired, it may be explicitly coerced using
<code>sb-alien:cast</code>.

     <p>Arrays are accessed using <code>sb-alien:deref</code>, passing the indices
as additional arguments.  Elements are stored in column-major order
(as in C), so the first dimension determines only the size of the
memory block, and not the layout of the higher dimensions.  An array
whose first dimension is variable may be specified by using <code>nil</code>
as the first dimension.  Fixed-size arrays can be allocated as array
elements, structure slots or <code>sb-alien:with-alien</code>
variables. Dynamic arrays can only be allocated using
<code>sb-alien:make-alien</code>.

     </p></li><li>The foreign type specifier <code>(sb-alien:struct </code><var>name</var><code> &amp;rest
</code><var>fields</var><code>)</code> describes a structure type with the specified
<var>name</var> and <var>fields</var>. Fields are allocated at the same offsets
used by the implementation's C compiler, as guessed by the SBCL
internals. An optional <code>:alignment</code> keyword argument can be
specified for each field to explicitly control the alignment of a
field. If <var>name</var> is <code>nil</code> then the structure is anonymous.

     <p>If a named foreign <code>struct</code> specifier is passed to
<code>define-alien-type</code> or <code>with-alien</code>, then this defines,
respectively, a new global or local foreign structure type.  If no
<var>fields</var> are specified, then the fields are taken
from the current (local or global) alien structure type definition of
<var>name</var>.

     </p></li><li>The foreign type specifier <code>(sb-alien:union </code><var>name</var><code> &amp;rest
</code><var>fields</var><code>)</code> is similar to <code>sb-alien:struct</code>, but describes a
union type.  All fields are allocated at the same offset, and the size
of the union is the size of the largest field.  The programmer must
determine which field is active from context.

     </li><li>The foreign type specifier <code>(sb-alien:enum </code><var>name</var><code> &amp;rest
</code><var>specs</var><code>)</code> describes an enumeration type that maps between integer
values and symbols. If <var>name</var> is <code>nil</code>, then the type is
anonymous.  Each element of the <var>specs</var> list is either a Lisp
symbol, or a list <code>(</code><var>symbol</var> <var>value</var><code>)</code>.  <var>value</var> is
an integer. If <var>value</var> is not supplied, then it defaults to one
greater than the value for the preceding spec (or to zero if it is the
first spec).

     </li><li>The foreign type specifier <code>(sb-alien:signed &amp;optional
</code><var>bits</var><code>)</code> specifies a signed integer with the specified number of
<var>bits</var> precision. The upper limit on integer
precision is determined by the machine's word size. If
<var>bits</var> is not specified, the maximum size will be
used.

     </li><li>The foreign type specifier <code>(integer &amp;optional </code><var>bits</var><code>)</code>
is equivalent to the corresponding type specifier using
<code>sb-alien:signed</code> instead of <code>integer</code>.

     </li><li>The foreign type specifier <code>(sb-alien:unsigned &amp;optional
</code><var>bits</var><code>)</code> is like corresponding type specifier using
<code>sb-alien:signed</code> except that the variable is treated as an
unsigned integer.

     </li><li>The foreign type specifier <code>(boolean &amp;optional </code><var>bits</var><code>)</code> is
similar to an enumeration type, but maps from Lisp <code>nil</code> and
<code>t</code> to C <code>0</code> and <code>1</code> respectively. <var>bits</var>
determines the amount of storage allocated to hold the truth value.

     </li><li>The foreign type specifier <code>single-float</code> describes a
floating-point number in IEEE single-precision format.

     </li><li>The foreign type specifier <code>double-float</code> describes a
floating-point number in IEEE double-precision format.

     </li><li>The foreign type specifier <code>(function </code><var>result-type</var><code> &amp;rest
</code><var>arg-types</var><code>)</code> describes a foreign function that takes arguments of
the specified <var>arg-types</var> and returns a result of type
<var>result-type</var>.  Note that the only context where a foreign
<code>function</code> type is directly specified is in the argument to
<code>sb-alien:alien-funcall</code>.  In all other contexts, foreign
functions are represented by foreign function pointer types: <code>(*
(function ...))</code>.

     </li><li>The foreign type specifier <code>sb-alien:system-area-pointer</code>
describes a pointer which is represented in Lisp as a
<code>system-area-pointer</code> object.  SBCL exports this type from
<code>sb-alien</code> because CMUCL did, but tentatively (as of the first
draft of this section of the manual, SBCL 0.7.6) it is deprecated,
since it doesn't seem to be required by user code.

     </li><li>The foreign type specifier <code>sb-alien:void</code> is used in function
types to declare that no useful value is returned.  Using
<code>alien-funcall</code> to call a <code>void</code> foreign function will
return zero values.

     </li><li><a name="index-External-formats-371"></a>The foreign type specifier <code>(sb-alien:c-string &amp;key
external-format element-type not-null)</code> is similar to
<code>(* char)</code>, but is interpreted as a null-terminated string, and
is automatically converted into a Lisp string when accessed; or if the
pointer is C <code>NULL</code> or <code>0</code>, then accessing it gives Lisp
<code>nil</code> unless <code>not-null</code> is true, in which case a type-error
is signalled.

     <p>External format conversion is automatically done when Lisp strings are
passed to foreign code, or when foreign strings are passed to Lisp code. 
If the type specifier has an explicit <code>external-format</code>, that
external format will be used. Otherwise a default external format that
has been determined at SBCL startup time based on the current locale
settings will be used. For example, when the following alien routine is
called, the Lisp string given as argument is converted to an
<code>ebcdic</code> octet representation.

     </p><pre class="lisp">          (define-alien-routine test int (str (c-string :external-format :ebcdic-us)))
</pre>
     <p>Lisp strings of type <code>base-string</code> are stored with a trailing NUL
termination, so no copying (either by the user or the implementation) is
necessary when passing them to foreign code, assuming that the
<code>external-format</code> and <code>element-type</code> of the <code>c-string</code>
type are compatible with the internal representation of the string. For
an SBCL built with Unicode support that means an <code>external-format</code>
of <code>:ascii</code> and an <code>element-type</code> of <code>base-char</code>. Without
Unicode support the <code>external-format</code> can also be
<code>:iso-8859-1</code>, and the <code>element-type</code> can also be
<code>character</code>. If the <code>external-format</code> or <code>element-type</code>
is not compatible, or the string is a <code>(simple-array character
(*))</code>, this data is copied by the implementation as required.

     </p><p>Assigning a Lisp string to a <code>c-string</code> structure field or
variable stores the contents of the string to the memory already
pointed to by that variable.  When a foreign object of type <code>(*
char)</code> is assigned to a <code>c-string</code>, then the
<code>c-string</code> pointer is assigned to.  This allows
<code>c-string</code> pointers to be initialized.  For example:

     </p><pre class="lisp">          (cl:in-package "CL-USER") ; which USEs package "SB-ALIEN"
          
          (define-alien-type nil (struct foo (str c-string)))
          
          (defun make-foo (str)
            (let ((my-foo (make-alien (struct foo))))
              (setf (slot my-foo 'str) (make-alien char (length str))
                    (slot my-foo 'str) str)
              my-foo))
</pre>
     <p>Storing Lisp <code>NIL</code> in a <code>c-string</code> writes C <code>NULL</code> to
the variable.

     </p></li><li><code>sb-alien</code> also exports translations of these C type
specifiers as foreign type specifiers:
<code>char</code>,
<code>short</code>,
<code>int</code>,
<code>long</code>,
<code>unsigned-char</code>,
<code>unsigned-short</code>,
<code>unsigned-int</code>,
<code>unsigned-long</code>,
<code>float</code>, <code>double</code>,
<code>size-t</code>, and <code>off-t</code>.

   </li></ul>

<div class="node">
<a name="Operations-On-Foreign-Values"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Variables">Foreign Variables</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-Types">Foreign Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.3 Operations On Foreign Values</h3>

<!-- AKA "Alien Operations" in the CMU CL manual -->
<p>This section describes how to read foreign values as Lisp values, how
to coerce foreign values to different kinds of foreign values, and how
to dynamically allocate and free foreign variables.

</p><ul class="menu">
<li><a accesskey="1" href="#Accessing-Foreign-Values">Accessing Foreign Values</a>
</li><li><a accesskey="2" href="#Coercing-Foreign-Values">Coercing Foreign Values</a>
</li><li><a accesskey="3" href="#Foreign-Dynamic-Allocation">Foreign Dynamic Allocation</a>
</li></ul>

<div class="node">
<a name="Accessing-Foreign-Values"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Coercing-Foreign-Values">Coercing Foreign Values</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Operations-On-Foreign-Values">Operations On Foreign Values</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.3.1 Accessing Foreign Values</h4>

<div class="defun">
— Function: <b>deref [sb-alien]</b><var> pointer-or-array &amp;rest indices<a name="index-g_t_0040sbalien_007bderef_007d-372"></a></var><br>
<blockquote>
        <p>The <code>sb-alien:deref</code> function returns the value pointed to by a
foreign pointer, or the value of a foreign array element. When
dereferencing a pointer, an optional single index can be specified to
give the equivalent of C pointer arithmetic; this index is scaled by
the size of the type pointed to. When dereferencing an array, the
number of indices must be the same as the number of dimensions in the
array type. <code>deref</code> can be set with <code>setf</code> to assign a new
value. 
</p></blockquote></div>

<div class="defun">
— Function: <b>slot [sb-alien]</b><var> struct-or-union slot-name<a name="index-g_t_0040sbalien_007bslot_007d-373"></a></var><br>
<blockquote>
        <p>The <code>sb-alien:slot</code> function extracts the value of the slot named
<var>slot-name</var> from a foreign <code>struct</code> or <code>union</code>. If
<var>struct-or-union</var> is a pointer to a structure or union, then it is
automatically dereferenced.  <code>sb-alien:slot</code> can be set with
<code>setf</code> to assign a new value. Note that <var>slot-name</var> is
evaluated, and need not be a compile-time constant (but only constant
slot accesses are efficiently compiled). 
</p></blockquote></div>

<h5 class="subsubsection">8.3.1.1 Untyped memory</h5>

<p>As noted at the beginning of the chapter, the System Area Pointer
facilities allow untyped access to foreign memory.  <acronym>SAP</acronym>s can
be converted to and from the usual typed foreign values using
<code>sap-alien</code> and <code>alien-sap</code> (described elsewhere), and also
to and from integers - raw machine addresses.  They should thus be
used with caution; corrupting the Lisp heap or other memory with
<acronym>SAP</acronym>s is trivial.

</p><div class="defun">
— Function: <b>int-sap [sb-sys]</b><var> machine-address<a name="index-g_t_0040sbsys_007bint_002dsap_007d-374"></a></var><br>
<blockquote>
        <p>Creates a <acronym>SAP</acronym> pointing at the virtual address
<var>machine-address</var>. 
</p></blockquote></div>

<div class="defun">
— Function: <b>sap-ref-32 [sb-sys]</b><var> sap offset<a name="index-g_t_0040sbsys_007bsap_002dref_002d32_007d-375"></a></var><br>
<blockquote>
        <p>Access the value of the memory location at <var>offset</var> bytes from
<var>sap</var>.  This form may also be used with <code>setf</code> to alter the
memory at that location. 
</p></blockquote></div>

<div class="defun">
— Function: <b>sap= [sb-sys]</b><var> sap1 sap2<a name="index-g_t_0040sbsys_007bsap_003d_007d-376"></a></var><br>
<blockquote>
        <p>Compare <var>sap1</var> and <var>sap2</var> for equality. 
</p></blockquote></div>

   <p>Similarly named functions exist for accessing other sizes of word,
other comparisons, and other conversions.  The reader is invited to
use <code>apropos</code> and <code>describe</code> for more details

</p><pre class="lisp">     (apropos "sap" :sb-sys)
</pre>
   <div class="node">
<a name="Coercing-Foreign-Values"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Dynamic-Allocation">Foreign Dynamic Allocation</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Accessing-Foreign-Values">Accessing Foreign Values</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Operations-On-Foreign-Values">Operations On Foreign Values</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.3.2 Coercing Foreign Values</h4>

<div class="defun">
— Macro: <b>addr [sb-alien]</b><var> alien-expr<a name="index-g_t_0040sbalien_007baddr_007d-377"></a></var><br>
<blockquote>
        <p>The <code>sb-alien:addr</code> macro returns a pointer to the location
specified by <var>alien-expr</var>, which must be either a foreign
variable, a use of <code>sb-alien:deref</code>, a use of
<code>sb-alien:slot</code>, or a use of <code>sb-alien:extern-alien</code>. 
</p></blockquote></div>

<div class="defun">
— Macro: <b>cast [sb-alien]</b><var> foreign-value new-type<a name="index-g_t_0040sbalien_007bcast_007d-378"></a></var><br>
<blockquote>
        <p>The <code>sb-alien:cast</code> macro converts <var>foreign-value</var> to a new
foreign value with the specified <var>new-type</var>. Both types, old and
new, must be foreign pointer, array or function types.  Note that the
resulting Lisp foreign variable object is not <code>eq</code> to the
argument, but it does refer to the same foreign data bits. 
</p></blockquote></div>

<div class="defun">
— Macro: <b>sap-alien [sb-alien]</b><var> sap type<a name="index-g_t_0040sbalien_007bsap_002dalien_007d-379"></a></var><br>
<blockquote>
        <p>The <code>sb-alien:sap-alien</code> macro converts <var>sap</var> (a system
area pointer) to a foreign value with the specified
<var>type</var>. <var>type</var> is not evaluated.

        </p><p>The <var>type</var> must be some foreign pointer, array, or record type. 
</p></blockquote></div>

<div class="defun">
— Function: <b>alien-sap [sb-alien]</b><var> foreign-value<a name="index-g_t_0040sbalien_007balien_002dsap_007d-380"></a></var><br>
<blockquote>
        <p>The <code>sb-alien:alien-sap</code> function returns the <acronym>SAP</acronym> which
points to <var>alien-value</var>'s data.

        </p><p>The <var>foreign-value</var> must be of some foreign pointer, array, or
record type. 
</p></blockquote></div>

<div class="node">
<a name="Foreign-Dynamic-Allocation"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Coercing-Foreign-Values">Coercing Foreign Values</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Operations-On-Foreign-Values">Operations On Foreign Values</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.3.3 Foreign Dynamic Allocation</h4>

<p>Lisp code can call the C standard library functions <code>malloc</code> and
<code>free</code> to dynamically allocate and deallocate foreign variables. 
The Lisp code shares the same allocator with foreign C code, so it's
OK for foreign code to call <code>free</code> on the result of Lisp
<code>sb-alien:make-alien</code>, or for Lisp code to call
<code>sb-alien:free-alien</code> on foreign objects allocated by C code.

   </p><p><a name="Macro-sb_002dalien_003amake_002dalien"></a>

</p><div class="defun">
— Macro: <b>make-alien [sb-alien]</b><var> type &amp;optional size<a name="index-g_t_0040sbalien_007bmake_002dalien_007d-381"></a></var><br>
<blockquote><p>Allocate an alien of type <code>type</code> in foreign heap, and return an alien
pointer to it. The allocated memory is not initialized, and may
contain garbage. The memory is allocated using malloc(3), so it can be
passed to foreign functions which use free(3), or released using
<code>free-alien</code>.

        </p><p>For alien stack allocation, see macro <code>with-alien</code>.

        </p><p>The <code>type</code> argument is not evaluated. If <code>size</code> is supplied, how it is
interpreted depends on <code>type:</code>

          </p><ul>
<li>When <code>type</code> is a foreign array type, an array of that type is
    allocated, and a pointer to it is returned. Note that you
    must use <code>deref</code> to first access the array through the pointer.

          <p>If supplied, <code>size</code> is used as the first dimension for the array.

          </p></li><li>When <code>type</code> is any other foreign type, then an object for that
    type is allocated, and a pointer to it is returned. So
    (make-alien int) returns a <code>(* int)</code>.

          <p>If <code>size</code> is specified, then a block of that many objects is
    allocated, with the result pointing to the first one.

        </p></li></ul>
        Examples:

     <pre class="lisp">            (defvar *foo* (make-alien (array char 10)))
            (type-of *foo*)                 ; =&gt; (alien (* (array (signed 8) 10)))
            (setf (deref (deref foo) 0) 10) ; =&gt; 10
          
            (make-alien char 12)            ; =&gt; (alien (* (signed 8)))
</pre>
        </blockquote></div>

   <p><a name="Function-sb_002dalien_003amake_002dalien_002dstring"></a>

</p><div class="defun">
— Function: <b>make-alien-string [sb-alien]</b><var> string &amp;rest rest &amp;key start end external-format null-terminate<a name="index-g_t_0040sbalien_007bmake_002dalien_002dstring_007d-382"></a></var><br>
<blockquote><p>Copy part of <code>string</code> delimited by <code>start</code> and <code>end</code> into freshly
allocated foreign memory, freeable using free(3) or <code>free-alien</code>. 
Returns the allocated string as a <code>(* char) </code>alien, and the number of
bytes allocated as secondary value.

        </p><p>The string is encoded using <code>external-format</code>. If <code>null-terminate</code> is
true (the default), the alien string is terminated by an additional
null byte. 
</p></blockquote></div>

   <p><a name="Function-sb_002dalien_003afree_002dalien"></a>

</p><div class="defun">
— Function: <b>free-alien [sb-alien]</b><var> alien<a name="index-g_t_0040sbalien_007bfree_002dalien_007d-383"></a></var><br>
<blockquote><p>Dispose of the storage pointed to by <code>alien</code>. The <code>alien</code> must have been
allocated by <code>make-alien</code>, <code>make-alien-string</code> or malloc(3). 
</p></blockquote></div>

<div class="node">
<a name="Foreign-Variables"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Data-Structure-Examples">Foreign Data Structure Examples</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Operations-On-Foreign-Values">Operations On Foreign Values</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.4 Foreign Variables</h3>

<!-- AKA "Alien Variables" in the CMU CL manual -->
<p>Both local (stack allocated) and external (C global) foreign variables
are supported.

</p><ul class="menu">
<li><a accesskey="1" href="#Local-Foreign-Variables">Local Foreign Variables</a>
</li><li><a accesskey="2" href="#External-Foreign-Variables">External Foreign Variables</a>
</li></ul>

<div class="node">
<a name="Local-Foreign-Variables"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#External-Foreign-Variables">External Foreign Variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Variables">Foreign Variables</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.4.1 Local Foreign Variables</h4>

<div class="defun">
— Macro: <b>with-alien [sb-alien]</b><var> var-definitions &amp;body body<a name="index-g_t_0040sbalien_007bwith_002dalien_007d-384"></a></var><br>
<blockquote>
        <p>The <code>with-alien</code> macro establishes local foreign variables with
the specified alien types and names.  This form is analogous to
defining a local variable in C: additional storage is allocated, and
the initial value is copied.  This form is less analogous to
<code>LET</code>-allocated Lisp variables, since the variables can't be
captured in closures: they live only for the dynamic extent of the
body, and referring to them outside is a gruesome error.

        </p><p>The <var>var-definitions</var> argument is a list of
variable definitions, each of the form
     </p><pre class="lisp">          (<var>name</var> <var>type</var> &amp;optional <var>initial-value</var>)
</pre>
        <p>The names of the variables are established as symbol-macros; the
bindings have lexical scope, and may be assigned with <code>setq</code> or
<code>setf</code>.

        </p><p>The <code>with-alien</code> macro also establishes a new scope for named
structures and unions.  Any <var>type</var> specified for a variable may
contain named structure or union types with the slots specified. 
Within the lexical scope of the binding specifiers and body, a locally
defined foreign structure type <var>foo</var> can be referenced by its name
using <code>(struct </code><var>foo</var><code>)</code>. 
</p></blockquote></div>

<div class="node">
<a name="External-Foreign-Variables"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Local-Foreign-Variables">Local Foreign Variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Variables">Foreign Variables</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.4.2 External Foreign Variables</h4>

<p>External foreign names are strings, and Lisp names are symbols. When
an external foreign value is represented using a Lisp variable, there
must be a way to convert from one name syntax into the other. The
macros <code>extern-alien</code>, <code>define-alien-variable</code> and
<code>define-alien-routine</code> use this conversion heuristic:

     </p><ul>
<li>Alien names are converted to Lisp names by uppercasing and replacing
underscores with hyphens.

     </li><li>Conversely, Lisp names are converted to alien names by lowercasing and
replacing hyphens with underscores.

     </li><li>Both the Lisp symbol and alien string names may be separately
specified by using a list of the form

     <pre class="lisp">          (alien-string lisp-symbol)
</pre>
     </li></ul>

<div class="defun">
— Macro: <b>define-alien-variable [sb-alien]</b><var> name type<a name="index-g_t_0040sbalien_007bdefine_002dalien_002dvariable_007d-385"></a></var><br>
<blockquote>
        <p>The <code>define-alien-variable</code> macro defines <var>name</var> as an
external foreign variable of the specified foreign <code>type</code>. 
<var>name</var> and <code>type</code> are not evaluated.  The Lisp name of the
variable (see above) becomes a global alien variable.  Global alien
variables are effectively “global symbol macros”; a reference to the
variable fetches the contents of the external variable.  Similarly,
setting the variable stores new contents – the new contents must be
of the declared <code>type</code>. Someday, they may well be implemented
using the <acronym>ANSI</acronym> <code>define-symbol-macro</code> mechanism, but as
of SBCL 0.7.5, they are still implemented using an older more-or-less
parallel mechanism inherited from CMUCL.

        </p><p>For example, to access a C-level counter <var>foo</var>, one could write

     </p><pre class="lisp">          (define-alien-variable "foo" int)
          ;; Now it is possible to get the value of the C variable foo simply by
          ;; referencing that Lisp variable:
          (print foo)
          (setf foo 14)
          (incf foo)
</pre>
        </blockquote></div>

<div class="defun">
— Function: <b>get-errno [sb-alien]</b><var><a name="index-g_t_0040sbalien_007bget_002derrno_007d-386"></a></var><br>
<blockquote>
        <p>Since in modern C libraries, the <code>errno</code> “variable” is typically
no longer a variable, but some bizarre artificial construct
which behaves superficially like a variable within a given thread,
it can no longer reliably be accessed through the ordinary
<code>define-alien-variable</code> mechanism. Instead, SBCL provides
the operator <code>sb-alien:get-errno</code> to allow Lisp code to read it. 
</p></blockquote></div>

<div class="defun">
— Macro: <b>extern-alien [sb-alien]</b><var> name type<a name="index-g_t_0040sbalien_007bextern_002dalien_007d-387"></a></var><br>
<blockquote>
        <p>The <code>extern-alien</code> macro returns an alien with the specified
<var>type</var> which points to an externally defined value.  <var>name</var> is
not evaluated, and may be either a string or a symbol.  <var>type</var> is
an unevaluated alien type specifier. 
</p></blockquote></div>

<div class="node">
<a name="Foreign-Data-Structure-Examples"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Loading-Shared-Object-Files">Loading Shared Object Files</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-Variables">Foreign Variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.5 Foreign Data Structure Examples</h3>

<!-- AKA "Alien Data Structure Example" in the CMU CL manual -->
<p>Now that we have alien types, operations and variables, we can
manipulate foreign data structures.  This C declaration

</p><pre class="example">     struct foo {
         int a;
         struct foo *b[100];
     };
</pre>
   <p>can be translated into the following alien type:

</p><pre class="lisp">     (define-alien-type nil
       (struct foo
         (a int)
         (b (array (* (struct foo)) 100))))
</pre>
   <p>Once the <code>foo</code> alien type has been defined as above, the C
expression

</p><pre class="example">     struct foo f;
     f.b[7].a;
</pre>
   <p>can be translated in this way:

</p><pre class="lisp">     (with-alien ((f (struct foo)))
       (slot (deref (slot f 'b) 7) 'a)
       ;;
       ;; Do something with f...
       )
</pre>
   <p>Or consider this example of an external C variable and some accesses:

</p><pre class="example">     struct c_struct {
             short x, y;
             char a, b;
             int z;
             c_struct *n;
     };
     extern struct c_struct *my_struct;
     my_struct-&gt;x++;
     my_struct-&gt;a = 5;
     my_struct = my_struct-&gt;n;
</pre>
   <p>which can be manipulated in Lisp like this:

</p><pre class="lisp">     (define-alien-type nil
       (struct c-struct
               (x short)
               (y short)
               (a char)
               (b char)
               (z int)
               (n (* c-struct))))
     (define-alien-variable "my_struct" (* c-struct))
     (incf (slot my-struct 'x))
     (setf (slot my-struct 'a) 5)
     (setq my-struct (slot my-struct 'n))
</pre>
   <div class="node">
<a name="Loading-Shared-Object-Files"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-Function-Calls">Foreign Function Calls</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-Data-Structure-Examples">Foreign Data Structure Examples</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.6 Loading Shared Object Files</h3>

<p>Foreign object files can be loaded into the running Lisp process by
calling <code>load-shared-object</code>.

   </p><p><a name="Function-sb_002dalien_003aload_002dshared_002dobject"></a>

</p><div class="defun">
— Function: <b>load-shared-object [sb-alien]</b><var> pathname &amp;key dont-save<a name="index-g_t_0040sbalien_007bload_002dshared_002dobject_007d-388"></a></var><br>
<blockquote><p>Load a shared library / dynamic shared object file / similar foreign
container specified by designated <code>pathname</code>, such as a .so on an <code>elf</code> platform.

        </p><p>Locating the shared object follows standard rules of the platform, consult the
manual page for dlopen(3) for details. Typically paths specified by
environment variables such as LD_LIBRARY_PATH are searched if the <code>pathname</code> has
no directory, but on some systems (eg. Mac <code>os</code> X) search may happen even if
<code>pathname</code> is absolute. (On Windows LoadLibrary is used instead of dlopen(3).)

        </p><p>On non-Windows platforms calling <code>load-shared-object</code> again with a <code>pathname</code>
<code>equal</code> to the designated pathname of a previous call will replace the old
definitions; if a symbol was previously referenced through the object and
is not present in the reloaded version an error will be signalled. Reloading
may not work as expected if user or library-code has called dlopen(3) on the
same shared object.

        </p><p><code>load-shared-object</code> interacts with <code>sb-ext:save-lisp-and-die:</code>

        </p><p>1. If <code>dont-save</code> is true (default is NIL), the shared object will be dropped
when <code>save-lisp-and-die</code> is called <code>--</code> otherwise shared objects are reloaded
automatically when a saved core starts up. Specifying <code>dont-save</code> can be useful
when the location of the shared object on startup is uncertain.

        </p><p>2. On most platforms references in compiled code to foreign symbols in shared
objects (such as those generated by DEFINE-ALIEN-ROUTINE) remain valid across
<code>save-lisp-and-die</code>. On those platforms where this is not supported, a <code>warning</code>
will be signalled when the core is saved <code>--</code> this is orthogonal from <code>dont-save</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dalien_003aunload_002dshared_002dobject"></a>

</p><div class="defun">
— Function: <b>unload-shared-object [sb-alien]</b><var> pathname<a name="index-g_t_0040sbalien_007bunload_002dshared_002dobject_007d-389"></a></var><br>
<blockquote><p>Unloads the shared object loaded earlier using the designated <code>pathname</code> with
<code>load-shared-object</code>, to the degree supported on the platform.

        </p><p>Experimental. 
</p></blockquote></div>

<div class="node">
<a name="Foreign-Function-Calls"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Step_002dBy_002dStep-Example-of-the-Foreign-Function-Interface">Step-By-Step Example of the Foreign Function Interface</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Loading-Shared-Object-Files">Loading Shared Object Files</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.7 Foreign Function Calls</h3>

<p>The foreign function call interface allows a Lisp program to call
many functions written in languages that use the C calling convention.

   </p><p>Lisp sets up various signal handling routines and other environment
information when it first starts up, and expects these to be in place
at all times. The C functions called by Lisp should not change the
environment, especially the signal handlers: the signal handlers
installed by Lisp typically have interesting flags set (e.g to request
machine context information, or for signal delivery on an alternate
stack) which the Lisp runtime relies on for correct operation. 
Precise details of how this works may change without notice between
versions; the source, or the brain of a friendly SBCL developer, is
the only documentation.  Users of a Lisp built with the
<code>:sb-thread</code> feature should also read the section about threads,
<a href="#Threading">Threading</a>.

</p><ul class="menu">
<li><a accesskey="1" href="#The-alien_002dfuncall-Primitive">The alien-funcall Primitive</a>
</li><li><a accesskey="2" href="#The-define_002dalien_002droutine-Macro">The define-alien-routine Macro</a>
</li><li><a accesskey="3" href="#define_002dalien_002droutine-Example">define-alien-routine Example</a>
</li><li><a accesskey="4" href="#Calling-Lisp-From-C">Calling Lisp From C</a>
</li></ul>

<div class="node">
<a name="The-alien-funcall-Primitive"></a>
<a name="The-alien_002dfuncall-Primitive"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#The-define_002dalien_002droutine-Macro">The define-alien-routine Macro</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Calls">Foreign Function Calls</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.7.1 The <code>alien-funcall</code> Primitive</h4>

<div class="defun">
— Function: <b>alien-funcall [sb-alien]</b><var> alien-function &amp;rest arguments<a name="index-g_t_0040sbalien_007balien_002dfuncall_007d-390"></a></var><br>
<blockquote>
        <p>The <code>alien-funcall</code> function is the foreign function call
primitive: <var>alien-function</var> is called with the supplied
<var>arguments</var> and its C return value is returned as a Lisp value. 
The <var>alien-function</var> is an arbitrary run-time expression; to refer
to a constant function, use <code>extern-alien</code> or a value defined by
<code>define-alien-routine</code>.

        </p><p>The type of <code>alien-function</code> must be <code>(alien (function
...))</code>  or <code>(alien (* (function ...)))</code>.  The function type is
used to determine how to call the function (as though it was declared
with a prototype.)  The type need not be known at compile time, but
only known-type calls are efficiently compiled.  Limitations:

          </p><ul>
<li>Structure type return values are not implemented.

          </li><li>Passing of structures by value is not implemented.

        </li></ul>

     </blockquote></div>

   <p>Here is an example which allocates a <code>(struct foo)</code>, calls a
foreign function to initialize it, then returns a Lisp vector of all
the <code>(* (struct foo))</code> objects filled in by the foreign call:

</p><pre class="lisp">     ;; Allocate a foo on the stack.
     (with-alien ((f (struct foo)))
       ;; Call some C function to fill in foo fields.
       (alien-funcall (extern-alien "mangle_foo" (function void (* foo)))
                      (addr f))
       ;; Find how many foos to use by getting the A field.
       (let* ((num (slot f 'a))
              (result (make-array num)))
         ;; Get a pointer to the array so that we don't have to keep extracting it:
         (with-alien ((a (* (array (* (struct foo)) 100)) (addr (slot f 'b))))
           ;; Loop over the first N elements and stash them in the result vector.
           (dotimes (i num)
             (setf (svref result i) (deref (deref a) i)))
           ;; Voila.
           result)))
</pre>
   <div class="node">
<a name="The-define-alien-routine-Macro"></a>
<a name="The-define_002dalien_002droutine-Macro"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#define_002dalien_002droutine-Example">define-alien-routine Example</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#The-alien_002dfuncall-Primitive">The alien-funcall Primitive</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Calls">Foreign Function Calls</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.7.2 The <code>define-alien-routine</code> Macro</h4>

<div class="defun">
— Macro: <b>define-alien-routine [sb-alien]</b><var> name result-type &amp;rest arg-specifiers<a name="index-g_t_0040sbalien_007bdefine_002dalien_002droutine_007d-391"></a></var><br>
<blockquote>
        <p>The <code>define-alien-routine</code> macro is a convenience for
automatically generating Lisp interfaces to simple foreign functions. 
The primary feature is the parameter style specification, which
translates the C pass-by-reference idiom into additional return
values.

        </p><p><var>name</var> is usually a string external symbol, but may also be a
symbol Lisp name or a list of the foreign name and the Lisp name.  If
only one name is specified, the other is automatically derived as for
<code>extern-alien</code>.  <var>result-type</var> is the alien type of the
return value.

        </p><p>Each element of the <var>arg-specifiers</var> list
specifies an argument to the foreign function, and is
of the form
     </p><pre class="lisp">          (aname atype &amp;amp;optional style)
</pre>
        <p><var>aname</var> is the symbol name of the argument to the constructed
function (for documentation). <var>atype</var> is the alien type of
corresponding foreign argument.  The semantics of the actual call are
the same as for <code>alien-funcall</code>. <var>style</var> specifies how this
argument should be handled at call and return time, and should be one
of the following:

          </p><ul>
<li><code>:in</code> specifies that the argument is passed by value. This is the
default. <code>:in</code> arguments have no corresponding return value from
the Lisp function.

          </li><li><code>:copy</code> is similar to <code>:in</code>, but the argument is copied to a
pre-allocated object and a pointer to this object is passed to the
foreign routine.

          </li><li><code>:out</code> specifies a pass-by-reference output value.  The type of
the argument must be a pointer to a fixed-sized object (such as an
integer or pointer).  <code>:out</code> and <code>:in-out</code> style cannot be
used with pointers to arrays, records or functions.  An object of the
correct size is allocated on the stack, and its address is passed to
the foreign function.  When the function returns, the contents of this
location are returned as one of the values of the Lisp function (and
the location is automatically deallocated).

          </li><li><code>:in-out</code> is a combination of <code>:copy</code> and <code>:out</code>.  The
argument is copied to a pre-allocated object and a pointer to this
object is passed to the foreign routine.  On return, the contents of
this location is returned as an additional value.

        </li></ul>

        <blockquote>
Note: Any efficiency-critical foreign interface function should be inline
expanded, which can be done by preceding the
<code>define-alien-routine</code> call with:

     <pre class="lisp">          (declaim (inline lisp-name))
</pre>
        <p>In addition to avoiding the Lisp call overhead, this allows
pointers, word-integers and floats to be passed using non-descriptor
representations, avoiding consing.) 
</p></blockquote>

     </blockquote></div>

<div class="node">
<a name="define-alien-routine-Example"></a>
<a name="define_002dalien_002droutine-Example"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Calling-Lisp-From-C">Calling Lisp From C</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#The-define_002dalien_002droutine-Macro">The define-alien-routine Macro</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Calls">Foreign Function Calls</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.7.3 <code>define-alien-routine</code> Example</h4>

<p>Consider the C function <code>cfoo</code> with the following calling
convention:

</p><pre class="example">     void
     cfoo (str, a, i)
         char *str;
         char *a; /* update */
         int *i; /* out */
     {
       /* body of cfoo(...) */
     }
</pre>
   <p>This can be described by the following call to
<code>define-alien-routine</code>:

</p><pre class="lisp">     (define-alien-routine "cfoo" void
       (str c-string)
       (a char :in-out)
       (i int :out))
</pre>
   <p>The Lisp function <code>cfoo</code> will have two arguments (<var>str</var> and
<var>a</var>) and two return values (<var>a</var> and <var>i</var>).

</p><div class="node">
<a name="Calling-Lisp-From-C"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#define_002dalien_002droutine-Example">define-alien-routine Example</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Calls">Foreign Function Calls</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">8.7.4 Calling Lisp From C</h4>

<p>Calling Lisp functions from C is sometimes possible, but is extremely
hackish and poorly supported as of SBCL 0.7.5.  See <code>funcall0</code>
<small class="dots">...</small> <code>funcall3</code> in the runtime system. The arguments must be
valid SBCL object descriptors (so that e.g. fixnums must be
left-shifted by 2.) As of SBCL 0.7.5, the format of object descriptors
is documented only by the source code and, in parts, by the old CMUCL
<samp><span class="file">INTERNALS</span></samp> documentation.

   </p><p>Note that the garbage collector moves objects, and won't be
able to fix up any references in C variables.  There are three
mechanisms for coping with this:

     </p><ol start="1" type="1">
<li>The <code>sb-ext:purify</code> moves all live Lisp
data into static or read-only areas such that it will never be moved
(or freed) again in the life of the Lisp session

     </li><li><code>sb-sys:with-pinned-objects</code> is a macro which arranges for some
set of objects to be pinned in memory for the dynamic extent of its
body forms.  On ports which use the generational garbage collector (as
of SBCL 0.8.3, only the x86) this has a page granularity - i.e. the
entire 4k page or pages containing the objects will be locked down. On
other ports it is implemented by turning off GC for the duration (so
could be said to have a whole-world granularity).

     </li><li>Disable GC, using the <code>without-gcing</code> macro.
        </li></ol>

<!-- <!- FIXME: This is a "changebar" section from the CMU CL manual. -->
<!-- I (WHN 2002-07-14) am not very familiar with this content, so -->
<!-- I'm not immediately prepared to try to update it for SBCL, and -->
<!-- I'm not feeling masochistic enough to work to encourage this -->
<!-- kind of low-level hack anyway. However, I acknowledge that callbacks -->
<!-- are sometimes really really necessary, so I include the original -->
<!-- text in case someone is hard-core enough to benefit from it. If -->
<!-- anyone brings the information up to date for SBCL, it belong -->
<!-- either in the main manual or on a CLiki SBCL Internals page. -->
<!-- LaTeX \subsection{Accessing Lisp Arrays} -->
<!-- LaTeX -->
<!-- LaTeX Due to the way \cmucl{} manages memory, the amount of memory that can -->
<!-- LaTeX be dynamically allocated by \code{malloc} or \funref{make-alien} is -->
<!-- LaTeX limited\footnote{\cmucl{} mmaps a large piece of memory for it's own -->
<!-- LaTeX   use and this memory is typically about 8 MB above the start of the C -->
<!-- LaTeX   heap.  Thus, only about 8 MB of memory can be dynamically -->
<!-- LaTeX   allocated.}. -->
<!-- Empirically determined to be considerably >8Mb on this x86 linux -->
<!-- machine, but I don't know what the actual values are - dan 2003.09.01 -->
<!-- Note that this technique is used in SB-GROVEL in the SBCL contrib -->
<!-- LaTeX -->
<!-- LaTeX To overcome this limitation, it is possible to access the content of -->
<!-- LaTeX Lisp arrays which are limited only by the amount of physical memory -->
<!-- LaTeX and swap space available.  However, this technique is only useful if -->
<!-- LaTeX the foreign function takes pointers to memory instead of allocating -->
<!-- LaTeX memory for itself.  In latter case, you will have to modify the -->
<!-- LaTeX foreign functions. -->
<!-- LaTeX -->
<!-- LaTeX This technique takes advantage of the fact that \cmucl{} has -->
<!-- LaTeX specialized array types (\pxlref{specialized-array-types}) that match -->
<!-- LaTeX a typical C array.  For example, a \code{(simple-array double-float -->
<!-- LaTeX   (100))} is stored in memory in essentially the same way as the C -->
<!-- LaTeX array \code{double x[100]} would be.  The following function allows us -->
<!-- LaTeX to get the physical address of such a Lisp array: -->
<!-- LaTeX \begin{example} -->
<!-- LaTeX (defun array-data-address (array) -->
<!-- LaTeX   "Return the physical address of where the actual data of an array is -->
<!-- LaTeX stored. -->
<!-- LaTeX -->
<!-- LaTeX ARRAY must be a specialized array type in CMU Lisp.  This means ARRAY -->
<!-- LaTeX must be an array of one of the following types: -->
<!-- LaTeX -->
<!-- LaTeX                   double-float -->
<!-- LaTeX                   single-float -->
<!-- LaTeX                   (unsigned-byte 32) -->
<!-- LaTeX                   (unsigned-byte 16) -->
<!-- LaTeX                   (unsigned-byte  8) -->
<!-- LaTeX                   (signed-byte 32) -->
<!-- LaTeX                   (signed-byte 16) -->
<!-- LaTeX                   (signed-byte  8) -->
<!-- LaTeX " -->
<!-- LaTeX   (declare (type (or #+signed-array (array (signed-byte 8)) -->
<!-- LaTeX                      #+signed-array (array (signed-byte 16)) -->
<!-- LaTeX                      #+signed-array (array (signed-byte 32)) -->
<!-- LaTeX                      (array (unsigned-byte 8)) -->
<!-- LaTeX                      (array (unsigned-byte 16)) -->
<!-- LaTeX                      (array (unsigned-byte 32)) -->
<!-- LaTeX                      (array single-float) -->
<!-- LaTeX                      (array double-float)) -->
<!-- LaTeX                  array) -->
<!-- LaTeX            (optimize (speed 3) (safety 0)) -->
<!-- LaTeX            (ext:optimize-interface (safety 3))) -->
<!-- LaTeX   ;; with-array-data will get us to the actual data.  However, because -->
<!-- LaTeX   ;; the array could have been displaced, we need to know where the -->
<!-- LaTeX   ;; data starts. -->
<!-- LaTeX   (lisp::with-array-data ((data array) -->
<!-- LaTeX                           (start) -->
<!-- LaTeX                           (end)) -->
<!-- LaTeX     (declare (ignore end)) -->
<!-- LaTeX     ;; DATA is a specialized simple-array.  Memory is laid out like this: -->
<!-- LaTeX     ;; -->
<!-- LaTeX     ;;   byte offset    Value -->
<!-- LaTeX     ;;        0         type code (should be 70 for double-float vector) -->
<!-- LaTeX     ;;        4         4 * number of elements in vector -->
<!-- LaTeX     ;;        8         1st element of vector -->
<!-- LaTeX     ;;      ...         ... -->
<!-- LaTeX     ;; -->
<!-- LaTeX     (let ((addr (+ 8 (logandc1 7 (kernel:get-lisp-obj-address data)))) -->
<!-- LaTeX           (type-size (let ((type (array-element-type data))) -->
<!-- LaTeX                        (cond ((or (equal type '(signed-byte 8)) -->
<!-- LaTeX                                   (equal type '(unsigned-byte 8))) -->
<!-- LaTeX                               1) -->
<!-- LaTeX                              ((or (equal type '(signed-byte 16)) -->
<!-- LaTeX                                   (equal type '(unsigned-byte 16))) -->
<!-- LaTeX                               2) -->
<!-- LaTeX                              ((or (equal type '(signed-byte 32)) -->
<!-- LaTeX                                   (equal type '(unsigned-byte 32))) -->
<!-- LaTeX                               4) -->
<!-- LaTeX                              ((equal type 'single-float) -->
<!-- LaTeX                               4) -->
<!-- LaTeX                              ((equal type 'double-float) -->
<!-- LaTeX                               8) -->
<!-- LaTeX                              (t -->
<!-- LaTeX                               (error "Unknown specialized array element type")))))) -->
<!-- LaTeX       (declare (type (unsigned-byte 32) addr) -->
<!-- LaTeX                (optimize (speed 3) (safety 0) (ext:inhibit-warnings 3))) -->
<!-- LaTeX       (system:int-sap (the (unsigned-byte 32) -->
<!-- LaTeX                         (+ addr (* type-size start))))))) -->
<!-- LaTeX \end{example} -->
<!-- LaTeX -->
<!-- LaTeX Assume we have the C function below that we wish to use: -->
<!-- LaTeX \begin{example} -->
<!-- LaTeX   double dotprod(double* x, double* y, int n) -->
<!-- LaTeX   \{ -->
<!-- LaTeX     int k; -->
<!-- LaTeX     double sum = 0; -->
<!-- LaTeX -->
<!-- LaTeX     for (k = 0; k < n; ++k) \{ -->
<!-- LaTeX       sum += x[k] * y[k]; -->
<!-- LaTeX     \} -->
<!-- LaTeX   \} -->
<!-- LaTeX \end{example} -->
<!-- LaTeX The following example generates two large arrays in Lisp, and calls the C -->
<!-- LaTeX function to do the desired computation.  This would not have been -->
<!-- LaTeX possible using \code{malloc} or \code{make-alien} since we need about -->
<!-- LaTeX 16 MB of memory to hold the two arrays. -->
<!-- LaTeX \begin{example} -->
<!-- LaTeX   (define-alien-routine "dotprod" double -->
<!-- LaTeX     (x (* double-float) :in) -->
<!-- LaTeX     (y (* double-float) :in) -->
<!-- LaTeX     (n int :in)) -->
<!-- LaTeX -->
<!-- LaTeX   (let ((x (make-array 1000000 :element-type 'double-float)) -->
<!-- LaTeX         (y (make-array 1000000 :element-type 'double-float))) -->
<!-- LaTeX     ;; Initialize X and Y somehow -->
<!-- LaTeX     (let ((x-addr (system:int-sap (array-data-address x))) -->
<!-- LaTeX           (y-addr (system:int-sap (array-data-address y)))) -->
<!-- LaTeX       (dotprod x-addr y-addr 1000000))) -->
<!-- LaTeX \end{example} -->
<!-- LaTeX In this example, it may be useful to wrap the inner \code{let} -->
<!-- LaTeX expression in an \code{unwind-protect} that first turns off garbage -->
<!-- LaTeX collection and then turns garbage collection on afterwards.  This will -->
<!-- LaTeX prevent garbage collection from moving \code{x} and \code{y} after we -->
<!-- LaTeX have obtained the (now erroneous) addresses but before the call to -->
<!-- LaTeX \code{dotprod} is made. -->
<!-- LaTeX -->
<!-- > -->
<div class="node">
<a name="Step-By-Step-Example-of-the-Foreign-Function-Interface"></a>
<a name="Step_002dBy_002dStep-Example-of-the-Foreign-Function-Interface"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-Function-Calls">Foreign Function Calls</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Foreign-Function-Interface">Foreign Function Interface</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">8.8 Step-By-Step Example of the Foreign Function Interface</h3>

<p>This section presents a complete example of an interface to a somewhat
complicated C function.

   </p><p>Suppose you have the following C function which you want to be able to
call from Lisp in the file <samp><span class="file">test.c</span></samp>

</p><pre class="example">     struct c_struct
     {
       int x;
       char *s;
     };
     
     struct c_struct *c_function (i, s, r, a)
         int i;
         char *s;
         struct c_struct *r;
         int a[10];
     {
       int j;
       struct c_struct *r2;
     
       printf("i = %d\n", i);
       printf("s = %s\n", s);
       printf("r-&gt;x = %d\n", r-&gt;x);
       printf("r-&gt;s = %s\n", r-&gt;s);
       for (j = 0; j &lt; 10; j++) printf("a[%d] = %d.\n", j, a[j]);
       r2 = (struct c_struct *) malloc (sizeof(struct c_struct));
       r2-&gt;x = i + 5;
       r2-&gt;s = "a C string";
       return(r2);
     };
</pre>
   <p>It is possible to call this C function from Lisp using the file
<samp><span class="file">test.lisp</span></samp> containing

</p><pre class="lisp">     (cl:defpackage "TEST-C-CALL" (:use "CL" "SB-ALIEN" "SB-C-CALL"))
     (cl:in-package "TEST-C-CALL")
     
     ;;; Define the record C-STRUCT in Lisp.
     (define-alien-type nil
         (struct c-struct
                 (x int)
                 (s c-string)))
     
     ;;; Define the Lisp function interface to the C routine.  It returns a
     ;;; pointer to a record of type C-STRUCT.  It accepts four parameters:
     ;;; I, an int; S, a pointer to a string; R, a pointer to a C-STRUCT
     ;;; record; and A, a pointer to the array of 10 ints.
     ;;;
     ;;; The INLINE declaration eliminates some efficiency notes about heap
     ;;; allocation of alien values.
     (declaim (inline c-function))
     (define-alien-routine c-function
         (* (struct c-struct))
       (i int)
       (s c-string)
       (r (* (struct c-struct)))
       (a (array int 10)))
     
     ;;; a function which sets up the parameters to the C function and
     ;;; actually calls it
     (defun call-cfun ()
       (with-alien ((ar (array int 10))
                    (c-struct (struct c-struct)))
         (dotimes (i 10)                     ; Fill array.
           (setf (deref ar i) i))
         (setf (slot c-struct 'x) 20)
         (setf (slot c-struct 's) "a Lisp string")
     
         (with-alien ((res (* (struct c-struct))
                           (c-function 5 "another Lisp string" (addr c-struct) ar)))
           (format t "~&amp;amp;back from C function~%")
           (multiple-value-prog1
               (values (slot res 'x)
                       (slot res 's))
     
             ;; Deallocate result. (after we are done referring to it:
             ;; "Pillage, *then* burn.")
             (free-alien res)))))
</pre>
   <p>To execute the above example, it is necessary to compile the C
routine, e.g.: ‘<samp><span class="samp">cc -c test.c &amp;&amp; ld -shared -o test.so test.o</span></samp>’ (In
order to enable incremental loading with some linkers, you may need to
say ‘<samp><span class="samp">cc -G 0 -c test.c</span></samp>’)

   </p><p>Once the C code has been compiled, you can start up Lisp and load it in:
‘<samp><span class="samp">sbcl</span></samp>’.  Lisp should start up with its normal prompt.

   </p><p>Within Lisp, compile the Lisp file. (This step can be done
separately. You don't have to recompile every time.) 
‘<samp><span class="samp">(compile-file "test.lisp")</span></samp>’

   </p><p>Within Lisp, load the foreign object file to define the necessary
symbols: ‘<samp><span class="samp">(load-shared-object "test.so")</span></samp>’.

   </p><p>Now you can load the compiled Lisp (“fasl”) file into Lisp:
‘<samp><span class="samp">(load "test.fasl")</span></samp>’
And once the Lisp file is loaded, you can call the
Lisp routine that sets up the parameters and calls the C
function:
‘<samp><span class="samp">(test-c-call::call-cfun)</span></samp>’

   </p><p>The C routine should print the following information to standard output:

</p><pre class="example">     i = 5
     s = another Lisp string
     r-&gt;x = 20
     r-&gt;s = a Lisp string
     a[0] = 0.
     a[1] = 1.
     a[2] = 2.
     a[3] = 3.
     a[4] = 4.
     a[5] = 5.
     a[6] = 6.
     a[7] = 7.
     a[8] = 8.
     a[9] = 9.
</pre>
   <p>After return from the C function,
the Lisp wrapper function should print the following output:

</p><pre class="example">     back from C function
</pre>
   <p>And upon return from the Lisp wrapper function,
before the next prompt is printed, the
Lisp read-eval-print loop should print the following return values:

</p><pre class="example">     10
     "a C string"
</pre>
   <div class="node">
<a name="Pathnames"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Streams">Streams</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-Function-Interface">Foreign Function Interface</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">9 Pathnames</h2>

<p><a name="index-Pathnames-392"></a>

</p><ul class="menu">
<li><a accesskey="1" href="#Lisp-Pathnames">Lisp Pathnames</a>
</li><li><a accesskey="2" href="#Native-Filenames">Native Filenames</a>
</li></ul>

<div class="node">
<a name="Lisp-Pathnames"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Native-Filenames">Native Filenames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Pathnames">Pathnames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">9.1 Lisp Pathnames</h3>

<p>There are many aspects of ANSI Common Lisp's pathname support which are
implementation-defined and so need documentation.

<!-- FIXME: as a matter of ANSI conformance, we are required to document -->
<!-- implementation-defined stuff, which for pathnames (chapter 19 of CLtS) -->
<!-- includes: -->
<!-- * Otherwise, the parsing of thing is implementation-defined. -->
<!-- (PARSE-NAMESTRING) -->
<!-- * If thing contains an explicit host name and no explicit device name, -->
<!-- then it is implementation-defined whether parse-namestring will supply -->
<!-- the standard default device for that host as the device component of -->
<!-- the resulting pathname.  (PARSE-NAMESTRING) -->
<!-- * The specific nature of the search is implementation-defined. -->
<!-- (LOAD-LOGICAL-PATHNAME-TRANSLATIONS) -->
<!-- * Any additional elements are implementation-defined. -->
<!-- (LOGICAL-PATHNAME-TRANSLATIONS) -->
<!-- * The matching rules are implementation-defined but should be consistent -->
<!-- with directory.  (PATHNAME-MATCH-P) -->
<!-- * Any such additional translations are implementation-defined. -->
<!-- (TRANSLATE-LOGICAL-PATHNAMES) -->
<!-- * ...or an implementation-defined portion of a component... -->
<!-- (TRANSLATE-PATHNAME) -->
<!-- * The portion of source that is copied into the resulting pathname is -->
<!-- implementation-defined.  (TRANSLATE-PATHNAME) -->
<!-- * During the copying of a portion of source into the resulting -->
<!-- pathname, additional implementation-defined translations of case or -->
<!-- file naming conventions might occur.  (TRANSLATE-PATHNAME) -->
<!-- * In general, the syntax of namestrings involves the use of -->
<!-- implementation-defined conventions.  (19.1.1) -->
<!-- * The nature of the mapping between structure imposed by pathnames and -->
<!-- the structure, if any, that is used by the underlying file system is -->
<!-- implementation-defined.  (19.1.2) -->
<!-- * The mapping of the pathname components into the concepts peculiar to -->
<!-- each file system is implementation-defined.  (19.1.2) -->
<!-- * Whether separator characters are permitted as part of a string in a -->
<!-- pathname component is implementation-defined;  (19.2.2.1.1) -->
<!-- * Whether a value of :unspecific is permitted for any component on any -->
<!-- given file system accessible to the implementation is -->
<!-- implementation-defined.  (19.2.2.2.3) -->
<!-- * Other symbols and integers have implementation-defined meaning. -->
<!-- (19.2.2.4.6) -->
</p><h4 class="subsection">9.1.1 Home Directory Specifiers</h4>

<p>SBCL accepts the keyword <code>:home</code> and a list of the form
<code>(:home "username")</code> as a directory component immediately
following <code>:absolute</code>.

   </p><p><code>:home</code> is represented in namestrings by <code>~/</code> and
<code>(:home "username"</code> by <code>~username/</code> at the start of the
namestring. Tilde-characters elsewhere in namestrings represent
themselves.

   </p><p>Home directory specifiers are resolved to home directory of the
current or specified user by <code>native-namestring</code>, which is used
by the implementation to translate pathnames before passing them on to
operating system specific routines.

   </p><p>Using <code>(:home "user")</code> form on Windows signals an error.

</p><h4 class="subsection">9.1.2 The SYS Logical Pathname Host</h4>

<p><a name="index-Logical-pathnames-393"></a><a name="index-Pathnames_002c-logical-394"></a><a name="index-g_t_0040cl_007blogical_002dpathname_002dtranslations_007d-395"></a><a name="index-g_t_0040setf_007b_0040cl_007blogical_002dpathname_002dtranslations_007d_007d-396"></a>
<!-- * The existence and meaning of SYS: logical pathnames is -->
<!-- implementation-defined.  (19.3.1.1.1) -->

   </p><p>The logical pathname host named by <code>"SYS"</code> exists in SBCL.  Its
<code>logical-pathname-translations</code> may be set by the site or the user
applicable to point to the locations of the system's sources; in
particular, the core system's source files match the logical pathname
<code>"SYS:SRC;**;*.*.*"</code>, and the contributed modules' source files
match <code>"SYS:CONTRIB;**;*.*.*"</code>.

   </p><p><a name="Function-sb_002dext_003aset_002dsbcl_002dsource_002dlocation"></a>

</p><div class="defun">
— Function: <b>set-sbcl-source-location [sb-ext]</b><var> pathname<a name="index-g_t_0040sbext_007bset_002dsbcl_002dsource_002dlocation_007d-397"></a></var><br>
<blockquote><p>Initialize the <code>sys</code> logical host based on <code>pathname</code>, which should be
the top-level directory of the <code>sbcl</code> sources. This will replace any
existing translations for "SYS:SRC;", "SYS:CONTRIB;", and
"SYS:OUTPUT;". Other "SYS:" translations are preserved. 
</p></blockquote></div>

<div class="node">
<a name="Native-Filenames"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Lisp-Pathnames">Lisp Pathnames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Pathnames">Pathnames</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">9.2 Native Filenames</h3>

<p>In some circumstances, what is wanted is a Lisp pathname object which
corresponds to a string produced by the Operating System.  In this case,
some of the default parsing rules are inappropriate: most filesystems do
not have a native understanding of wild pathnames; such functionality is
often provided by shells above the OS, often in mutually-incompatible
ways.

   </p><p>To allow the user to deal with this, the following functions are
provided: <code>parse-native-namestring</code> and <code>native-pathname</code>
return the closest equivalent Lisp pathname to a given string
(appropriate for the Operating System), while <code>native-namestring</code>
converts a non-wild pathname designator to the equivalent native
namestring, if possible.  Some Lisp pathname concepts (such as the
<code>:back</code> directory component) have no direct equivalents in most
Operating Systems; the behaviour of <code>native-namestring</code> is
unspecified if an inappropriate pathname designator is passed to it. 
Additionally, note that conversion from pathname to native filename
and back to pathname should not be expected to preserve equivalence
under <code>equal</code>.

   </p><p><a name="Function-sb_002dext_003aparse_002dnative_002dnamestring"></a>

</p><div class="defun">
— Function: <b>parse-native-namestring [sb-ext]</b><var> thing &amp;optional host defaults &amp;key start end junk-allowed as-directory<a name="index-g_t_0040sbext_007bparse_002dnative_002dnamestring_007d-398"></a></var><br>
<blockquote><p>Convert <code>thing</code> into a pathname, using the native conventions
appropriate for the pathname host <code>host</code>, or if not specified the
host of <code>defaults</code>.  If <code>thing</code> is a string, the parse is bounded by
<code>start</code> and <code>end</code>, and error behaviour is controlled by <code>junk-allowed</code>,
as with <code>parse-namestring</code>.  For file systems whose native
conventions allow directories to be indicated as files, if
<code>as-directory</code> is true, return a pathname denoting <code>thing</code> as a
directory. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003anative_002dpathname"></a>

</p><div class="defun">
— Function: <b>native-pathname [sb-ext]</b><var> pathspec<a name="index-g_t_0040sbext_007bnative_002dpathname_007d-399"></a></var><br>
<blockquote><p>Convert <code>pathspec</code> (a pathname designator) into a pathname, assuming
the operating system native pathname conventions. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003anative_002dnamestring"></a>

</p><div class="defun">
— Function: <b>native-namestring [sb-ext]</b><var> pathname &amp;key as-file<a name="index-g_t_0040sbext_007bnative_002dnamestring_007d-400"></a></var><br>
<blockquote><p>Construct the full native (name)string form of <code>pathname</code>.  For
file systems whose native conventions allow directories to be
indicated as files, if <code>as-file</code> is true and the name, type, and
version components of <code>pathname</code> are all <code>nil</code> or <code>:unspecific</code>,
construct a string that names the directory according to the file
system's syntax for files. 
</p></blockquote></div>

   <p>Because some file systems permit the names of directories to be
expressed in multiple ways, it is occasionally necessary to parse a
native file name “as a directory name” or to produce a native file
name that names a directory “as a file”.  For these cases,
<code>parse-native-namestring</code> accepts the keyword argument
<code>as-directory</code> to force a filename to parse as a directory, and
<code>native-namestring</code> accepts the keyword argument <code>as-file</code>
to force a pathname to unparse as a file.  For example,

</p><pre class="lisp">     ; On Unix, the directory "/tmp/" can be denoted by "/tmp/" or "/tmp".
     ; Under the default rules for native filenames, these parse and
     ; unparse differently.
     (defvar *p*)
     (setf *p* (parse-native-namestring "/tmp/")) ⇒ #P"/tmp/"
     (pathname-name *p*) ⇒ NIL
     (pathname-directory *p*) ⇒ (:ABSOLUTE "tmp")
     (native-namestring *p*) ⇒ "/tmp/"
     
     (setf *p* (parse-native-namestring "/tmp")) ⇒ #P"/tmp"
     (pathname-name *p*) ⇒ "tmp"
     (pathname-directory *p*) ⇒ (:ABSOLUTE)
     (native-namestring *p*) ⇒ "/tmp"
     
     ; A non-NIL AS-DIRECTORY argument to PARSE-NATIVE-NAMESTRING forces
     ; both the second string to parse the way the first does.
     (setf *p* (parse-native-namestring "/tmp"
                                        nil *default-pathname-defaults*
                                        :as-directory t)) ⇒ #P"/tmp/"
     (pathname-name *p*) ⇒ NIL
     (pathname-directory *p*) ⇒ (:ABSOLUTE "tmp")
     
     ; A non-NIL AS-FILE argument to NATIVE-NAMESTRING forces the pathname
     ; parsed from the first string to unparse as the second string.
     (setf *p* (parse-native-namestring "/tmp/")) ⇒ #P"/tmp/"
     (native-namestring *p* :as-file t) ⇒ "/tmp"
</pre>
   <div class="node">
<a name="Streams"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Package-Locks">Package Locks</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Pathnames">Pathnames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">10 Streams</h2>

<p>Streams which read or write Lisp character data from or to the outside
world – files, sockets or other external entities – require the
specification of a conversion between the external, binary data and the
Lisp characters.  In ANSI Common Lisp, this is done by specifying the
<code>:external-format</code> argument when the stream is created.  The major
information required is an <em>encoding</em>, specified by a keyword
naming that encoding; however, it is also possible to specify
refinements to that encoding as additional options to the external
format designator.

   </p><p>In addition, SBCL supports various extensions of ANSI Common Lisp
streams:

     </p><dl>
<dt><strong>Bivalent Streams</strong></dt><dd>A type of stream that can read and write both <code>character</code> and
<code>(unsigned-byte 8)</code> values.

     <br></dd><dt><strong>Gray Streams</strong></dt><dd>User-overloadable CLOS classes whose instances can be used as Lisp
streams (e.g. passed as the first argument to <code>format</code>).

     <br></dd><dt><strong>Simple Streams</strong></dt><dd>The bundled contrib module <dfn>sb-simple-streams</dfn> implements a subset
of the Franz Allegro simple-streams proposal.

   </dd></dl>

<ul class="menu">
<li><a accesskey="1" href="#External-Formats">External Formats</a>
</li><li><a accesskey="2" href="#Bivalent-Streams">Bivalent Streams</a>
</li><li><a accesskey="3" href="#Gray-Streams">Gray Streams</a>
</li><li><a accesskey="4" href="#Simple-Streams">Simple Streams</a>
</li></ul>

<div class="node">
<a name="External-Formats"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Bivalent-Streams">Bivalent Streams</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Streams">Streams</a>

</div>

<h3 class="section">10.1 External Formats</h3>

<p><a name="index-External-formats-401"></a>
<a name="index-g_t_0040cl_007bstream_002dexternal_002dformat_007d-402"></a>The encodings supported by SBCL as external formats are named by
keyword.  Each encoding has a canonical name, which will be encoding
returned by <code>stream-external-format</code>, and a number of aliases for
convenience, as shown in the table below:

     </p><dl>
<dt><code>:ASCII</code></dt><dd><code>:US-ASCII</code>, <code>:ANSI_X3.4-1968</code>, <code>:ISO-646</code>, <code>:ISO-646-US</code>, <code>:|646|</code>

     <br></dd><dt><code>:CP1250</code></dt><dd><code>:|cp1250|</code>, <code>:WINDOWS-1250</code>, <code>:|windows-1250|</code>

     <br></dd><dt><code>:CP1251</code></dt><dd><code>:|cp1251|</code>, <code>:WINDOWS-1251</code>, <code>:|windows-1251|</code>

     <br></dd><dt><code>:CP1252</code></dt><dd><code>:|cp1252|</code>, <code>:WINDOWS-1252</code>, <code>:|windows-1252|</code>

     <br></dd><dt><code>:CP1253</code></dt><dd><code>:|cp1253|</code>, <code>:WINDOWS-1253</code>, <code>:|windows-1253|</code>

     <br></dd><dt><code>:CP1254</code></dt><dd><code>:|cp1254|</code>

     <br></dd><dt><code>:CP1255</code></dt><dd><code>:|cp1255|</code>, <code>:WINDOWS-1255</code>, <code>:|windows-1255|</code>

     <br></dd><dt><code>:CP1256</code></dt><dd><code>:|cp1256|</code>, <code>:WINDOWS-1256</code>, <code>:|windows-1256|</code>

     <br></dd><dt><code>:CP1257</code></dt><dd><code>:|cp1257|</code>, <code>:WINDOWS-1257</code>, <code>:|windows-1257|</code>

     <br></dd><dt><code>:CP1258</code></dt><dd><code>:|cp1258|</code>, <code>:WINDOWS-1258</code>, <code>:|windows-1258|</code>

     <br></dd><dt><code>:CP437</code></dt><dd><code>:|cp437|</code>

     <br></dd><dt><code>:CP850</code></dt><dd><code>:|cp850|</code>

     <br></dd><dt><code>:CP852</code></dt><dd><code>:|cp852|</code>

     <br></dd><dt><code>:CP855</code></dt><dd><code>:|cp855|</code>

     <br></dd><dt><code>:CP857</code></dt><dd><code>:|cp857|</code>

     <br></dd><dt><code>:CP860</code></dt><dd><code>:|cp860|</code>

     <br></dd><dt><code>:CP861</code></dt><dd><code>:|cp861|</code>

     <br></dd><dt><code>:CP862</code></dt><dd><code>:|cp862|</code>

     <br></dd><dt><code>:CP863</code></dt><dd><code>:|cp863|</code>

     <br></dd><dt><code>:CP864</code></dt><dd><code>:|cp864|</code>

     <br></dd><dt><code>:CP865</code></dt><dd><code>:|cp865|</code>

     <br></dd><dt><code>:CP866</code></dt><dd><code>:|cp866|</code>

     <br></dd><dt><code>:CP869</code></dt><dd><code>:|cp869|</code>

     <br></dd><dt><code>:CP874</code></dt><dd><code>:|cp874|</code>

     <br></dd><dt><code>:EBCDIC-US</code></dt><dd><code>:CP037</code>, <code>:|cp037|</code>, <code>:IBM-037</code>, <code>:IBM037</code>

     <br></dd><dt><code>:EUC-JP</code></dt><dd><code>:EUCJP</code>, <code>:|eucJP|</code>

     <br></dd><dt><code>:GBK</code></dt><dd><code>:CP936</code>

     <br></dd><dt><code>:ISO-8859-10</code></dt><dd><code>:|iso-8859-10|</code>, <code>:LATIN-6</code>, <code>:|latin-6|</code>

     <br></dd><dt><code>:ISO-8859-11</code></dt><dd><code>:|iso-8859-11|</code>

     <br></dd><dt><code>:ISO-8859-13</code></dt><dd><code>:|iso-8859-13|</code>, <code>:LATIN-7</code>, <code>:|latin-7|</code>

     <br></dd><dt><code>:ISO-8859-14</code></dt><dd><code>:|iso-8859-14|</code>, <code>:LATIN-8</code>, <code>:|latin-8|</code>

     <br></dd><dt><code>:ISO-8859-2</code></dt><dd><code>:|iso-8859-2|</code>, <code>:LATIN-2</code>, <code>:|latin-2|</code>

     <br></dd><dt><code>:ISO-8859-3</code></dt><dd><code>:|iso-8859-3|</code>, <code>:LATIN-3</code>, <code>:|latin-3|</code>

     <br></dd><dt><code>:ISO-8859-4</code></dt><dd><code>:|iso-8859-4|</code>, <code>:LATIN-4</code>, <code>:|latin-4|</code>

     <br></dd><dt><code>:ISO-8859-5</code></dt><dd><code>:|iso-8859-5|</code>

     <br></dd><dt><code>:ISO-8859-6</code></dt><dd><code>:|iso-8859-6|</code>

     <br></dd><dt><code>:ISO-8859-7</code></dt><dd><code>:|iso-8859-7|</code>

     <br></dd><dt><code>:ISO-8859-8</code></dt><dd><code>:|iso-8859-8|</code>

     <br></dd><dt><code>:ISO-8859-9</code></dt><dd><code>:|iso-8859-9|</code>, <code>:LATIN-5</code>, <code>:|latin-5|</code>

     <br></dd><dt><code>:KOI8-R</code></dt><dd><code>:|koi8-r|</code>

     <br></dd><dt><code>:KOI8-U</code></dt><dd><code>:|koi8-u|</code>

     <br></dd><dt><code>:LATIN-1</code></dt><dd><code>:LATIN1</code>, <code>:ISO-8859-1</code>, <code>:ISO8859-1</code>

     <br></dd><dt><code>:LATIN-9</code></dt><dd><code>:LATIN9</code>, <code>:ISO-8859-15</code>, <code>:ISO8859-15</code>

     <br></dd><dt><code>:MAC-ROMAN</code></dt><dd><code>:|mac-roman|</code>, <code>:|MacRoman|</code>, <code>:MAC</code>, <code>:|mac|</code>, <code>:MACINTOSH</code>, <code>:|macintosh|</code>

     <br></dd><dt><code>:SHIFT_JIS</code></dt><dd><code>:SJIS</code>, <code>:|Shift_JIS|</code>, <code>:CP932</code>

     <br></dd><dt><code>:UCS-2BE</code></dt><dd><code>:UCS2BE</code>

     <br></dd><dt><code>:UCS-2LE</code></dt><dd><code>:UCS2LE</code>

     <br></dd><dt><code>:UCS-4BE</code></dt><dd><code>:UCS4BE</code>

     <br></dd><dt><code>:UCS-4LE</code></dt><dd><code>:UCS4LE</code>

     <br></dd><dt><code>:UTF-16BE</code></dt><dd><code>:UTF16BE</code>

     <br></dd><dt><code>:UTF-16LE</code></dt><dd><code>:UTF16LE</code>

     <br></dd><dt><code>:UTF-32BE</code></dt><dd><code>:UTF32BE</code>

     <br></dd><dt><code>:UTF-32LE</code></dt><dd><code>:UTF32LE</code>

     <br></dd><dt><code>:UTF-8</code></dt><dd><code>:UTF8</code>

     <br></dd><dt><code>:X-MAC-CYRILLIC</code></dt><dd><code>:|x-mac-cyrillic|</code>

   </dd></dl>

   <p><a name="index-g_t_0040cl_007bopen_007d-403"></a><a name="index-g_t_0040cl_007bwith_002dopen_002dfile_007d-404"></a>In situations where an external file format designator is required, such
as the <code>:external-format</code> argument in calls to <code>open</code> or
<code>with-open-file</code>, users may supply the name of an encoding to
denote the external format which is applying that encoding to Lisp
characters.

   </p><p>In addition to the basic encoding for an external format, options
controlling various special cases may be passed, by using a list (whose
first element must be an encoding name and whose rest is a plist) as an
external file format designator.  At present, the only supported key in
the plist is <code>:replacement</code>, where the corresponding value is a
string designator which is used as a replacement when an encoding or
decoding error happens, handling those errors without user intervention;
for example:
</p><pre class="lisp">     (with-open-file (i pathname :external-format '(:utf-8 :replacement #\?))
       (read-line i))
</pre>
   <p>will read the first line of <var>pathname</var>, replacing any invalid utf-8
sequences with question marks.

</p><div class="node">
<a name="Bivalent-Streams"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Gray-Streams">Gray Streams</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#External-Formats">External Formats</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Streams">Streams</a>

</div>

<h3 class="section">10.2 Bivalent Streams</h3>

<p>A <dfn>bivalent stream</dfn> can be used to read and write both
<code>character</code> and <code>(unsigned-byte 8)</code> values.  A bivalent
stream is created by calling <code>open</code> with the argument <code>:element-type
:default</code>.  On such a stream, both binary and character data can be
read and written with the usual input and output functions.

<!-- Horrible visual markup -->
   </p><blockquote>
Streams are <em>not</em> created bivalent by default for performance
reasons.  Bivalent streams are incompatible with
<code>fast-read-char</code>, an internal optimization in SBCL's stream
machinery that bulk-converts octets to characters and implements a
fast path through <code>read-char</code>. 
</blockquote>

<div class="node">
<a name="Gray-Streams"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Simple-Streams">Simple Streams</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Bivalent-Streams">Bivalent Streams</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Streams">Streams</a>

</div>

<h3 class="section">10.3 Gray Streams</h3>

<p>The Gray Streams interface is a widely supported extension that
provides for definition of CLOS-extensible stream classes.  Gray
stream classes are implemented by adding methods to generic functions
analogous to Common Lisp's standard I/O functions.  Instances of Gray
stream classes may be used with any I/O operation where a non-Gray
stream can, provided that all required methods have been implemented
suitably.

</p><ul class="menu">
<li><a accesskey="1" href="#Gray-Streams-classes">Gray Streams classes</a>
</li><li><a accesskey="2" href="#Methods-common-to-all-streams">Methods common to all streams</a>
</li><li><a accesskey="3" href="#Input-stream-methods">Input stream methods</a>
</li><li><a accesskey="4" href="#Character-input-stream-methods">Character input stream methods</a>
</li><li><a accesskey="5" href="#Output-stream-methods">Output stream methods</a>
</li><li><a accesskey="6" href="#Character-output-stream-methods">Character output stream methods</a>
</li><li><a accesskey="7" href="#Binary-stream-methods">Binary stream methods</a>
</li><li><a accesskey="8" href="#Gray-Streams-examples">Gray Streams examples</a>
</li></ul>

<div class="node">
<a name="Gray-Streams-classes"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Methods-common-to-all-streams">Methods common to all streams</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.1 Gray Streams classes</h4>

<p>The defined Gray Stream classes are these:

   </p><p><a name="Class-sb_002dgray_003afundamental_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dstream_007d-405"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-stream, standard-object, stream, t</code>

        </p><p>Base class for all Gray streams. 
</p></blockquote></div>

   <p><a name="Class-sb_002dgray_003afundamental_002dinput_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-input-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dinput_002dstream_007d-406"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-input-stream, fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray input streams. 
</p></blockquote></div>

<p class="noindent">The function input-stream-p will return true of any generalized
instance of fundamental-input-stream.

   </p><p><a name="Class-sb_002dgray_003afundamental_002doutput_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-output-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002doutput_002dstream_007d-407"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-output-stream, fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray output streams. 
</p></blockquote></div>

<p class="noindent">The function output-stream-p will return true of any generalized
instance of fundamental-output-stream.

   </p><p><a name="Class-sb_002dgray_003afundamental_002dbinary_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-binary-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dbinary_002dstream_007d-408"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-binary-stream, fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray streams whose element-type
is a subtype of unsigned-byte or signed-byte. 
</p></blockquote></div>

<p class="noindent">Note that instantiable subclasses of fundamental-binary-stream should
provide (or inherit) an applicable method for the generic function
stream-element-type.

   </p><p><a name="Class-sb_002dgray_003afundamental_002dcharacter_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-character-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dcharacter_002dstream_007d-409"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-character-stream, fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray streams whose element-type is a subtype of character. 
</p></blockquote></div>

   <p><a name="Class-sb_002dgray_003afundamental_002dbinary_002dinput_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-binary-input-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dbinary_002dinput_002dstream_007d-410"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-binary-input-stream,
 fundamental-input-stream, fundamental-binary-stream, 
fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray input streams whose element-type
is a subtype of unsigned-byte or signed-byte. 
</p></blockquote></div>

   <p><a name="Class-sb_002dgray_003afundamental_002dbinary_002doutput_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-binary-output-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dbinary_002doutput_002dstream_007d-411"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-binary-output-stream,
 fundamental-output-stream, fundamental-binary-stream, 
fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray output streams whose element-type
is a subtype of unsigned-byte or signed-byte. 
</p></blockquote></div>

   <p><a name="Class-sb_002dgray_003afundamental_002dcharacter_002dinput_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-character-input-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dcharacter_002dinput_002dstream_007d-412"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-character-input-stream,
 fundamental-input-stream, fundamental-character-stream, 
fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray input streams whose element-type
is a subtype of character. 
</p></blockquote></div>

   <p><a name="Class-sb_002dgray_003afundamental_002dcharacter_002doutput_002dstream"></a>

</p><div class="defun">
— Class: <b>fundamental-character-output-stream [sb-gray]</b><var><a name="index-g_t_0040sbgray_007bfundamental_002dcharacter_002doutput_002dstream_007d-413"></a></var><br>
<blockquote><p>Class precedence list: <code>fundamental-character-output-stream,
 fundamental-output-stream, fundamental-character-stream, 
fundamental-stream, standard-object, stream, t</code>

        </p><p>Superclass of all Gray output streams whose element-type
is a subtype of character. 
</p></blockquote></div>

<div class="node">
<a name="Methods-common-to-all-streams"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Input-stream-methods">Input stream methods</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Gray-Streams-classes">Gray Streams classes</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.2 Methods common to all streams</h4>

<p>These generic functions can be specialized on any generalized instance
of fundamental-stream.

   </p><p><a name="Generic_002dFunction-common_002dlisp_003astream_002delement_002dtype"></a>

</p><div class="defun">
— Generic Function: <b>stream-element-type [cl]</b><var> stream<a name="index-g_t_0040cl_007bstream_002delement_002dtype_007d-414"></a></var><br>
<blockquote><p>Return a type specifier for the kind of object returned by the
  <code>stream</code>. The class <code>fundamental-character-stream</code> provides a default method
  which returns <code>character</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-common_002dlisp_003aclose"></a>

</p><div class="defun">
— Generic Function: <b>close [cl]</b><var> stream &amp;key abort<a name="index-g_t_0040cl_007bclose_007d-415"></a></var><br>
<blockquote><p>Close the given <code>stream</code>. No more I/O may be performed, but
  inquiries may still be made. If <code>:abort</code> is true, an attempt is made
  to clean up the side effects of having created the stream. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dfile_002dposition"></a>

</p><div class="defun">
— Generic Function: <b>stream-file-position [sb-gray]</b><var> stream &amp;optional position-spec<a name="index-g_t_0040sbgray_007bstream_002dfile_002dposition_007d-416"></a></var><br>
<blockquote><p>Used by <code>file-position</code>. Returns or changes the current position within <code>stream</code>. 
</p></blockquote></div>

<div class="node">
<a name="Input-stream-methods"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Character-input-stream-methods">Character input stream methods</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Methods-common-to-all-streams">Methods common to all streams</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.3 Input stream methods</h4>

<p>These generic functions may be specialized on any generalized instance
of fundamental-input-stream.

   </p><p><a name="Generic_002dFunction-sb_002dgray_003astream_002dclear_002dinput"></a>

</p><div class="defun">
— Generic Function: <b>stream-clear-input [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dclear_002dinput_007d-417"></a></var><br>
<blockquote><p>This is like <code>cl:clear-input</code>, but for Gray streams, returning <code>nil</code>. 
  The default method does nothing. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dread_002dsequence"></a>

</p><div class="defun">
— Generic Function: <b>stream-read-sequence [sb-gray]</b><var> stream seq &amp;optional start end<a name="index-g_t_0040sbgray_007bstream_002dread_002dsequence_007d-418"></a></var><br>
<blockquote><p>This is like <code>cl:read-sequence</code>, but for Gray streams. 
</p></blockquote></div>

<div class="node">
<a name="Character-input-stream-methods"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Output-stream-methods">Output stream methods</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Input-stream-methods">Input stream methods</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.4 Character input stream methods</h4>

<p>These generic functions are used to implement subclasses of
fundamental-input-stream:

   </p><p><a name="Generic_002dFunction-sb_002dgray_003astream_002dpeek_002dchar"></a>

</p><div class="defun">
— Generic Function: <b>stream-peek-char [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dpeek_002dchar_007d-419"></a></var><br>
<blockquote><p>This is used to implement <code>peek-char</code>; this corresponds to <code>peek-type</code> of <code>nil</code>. 
  It returns either a character or <code>:eof</code>. The default method calls
  <code>stream-read-char</code> and <code>stream-unread-char</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dread_002dchar_002dno_002dhang"></a>

</p><div class="defun">
— Generic Function: <b>stream-read-char-no-hang [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dread_002dchar_002dno_002dhang_007d-420"></a></var><br>
<blockquote><p>This is used to implement <code>read-char-no-hang</code>. It returns either a
  character, or <code>nil</code> if no input is currently available, or <code>:eof</code> if
  end-of-file is reached. The default method provided by
  <code>fundamental-character-input-stream</code> simply calls <code>stream-read-char</code>; this
  is sufficient for file streams, but interactive streams should define
  their own method. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dread_002dchar"></a>

</p><div class="defun">
— Generic Function: <b>stream-read-char [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dread_002dchar_007d-421"></a></var><br>
<blockquote><p>Read one character from the stream. Return either a
  character object, or the symbol <code>:eof</code> if the stream is at end-of-file. 
  Every subclass of <code>fundamental-character-input-stream</code> must define a
  method for this function. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dread_002dline"></a>

</p><div class="defun">
— Generic Function: <b>stream-read-line [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dread_002dline_007d-422"></a></var><br>
<blockquote><p>This is used by <code>read-line</code>. A string is returned as the first value. The
  second value is true if the string was terminated by end-of-file
  instead of the end of a line. The default method uses repeated
  calls to <code>stream-read-char</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dlisten"></a>

</p><div class="defun">
— Generic Function: <b>stream-listen [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dlisten_007d-423"></a></var><br>
<blockquote><p>This is used by <code>listen</code>. It returns true or false. The default method uses
  <code>stream-read-char-no-hang</code> and <code>stream-unread-char</code>. Most streams should
  define their own method since it will usually be trivial and will
  always be more efficient than the default method. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dunread_002dchar"></a>

</p><div class="defun">
— Generic Function: <b>stream-unread-char [sb-gray]</b><var> stream character<a name="index-g_t_0040sbgray_007bstream_002dunread_002dchar_007d-424"></a></var><br>
<blockquote><p>Undo the last call to <code>stream-read-char</code>, as in <code>unread-char</code>. 
  Return <code>nil</code>. Every subclass of <code>fundamental-character-input-stream</code>
  must define a method for this function. 
</p></blockquote></div>

<div class="node">
<a name="Output-stream-methods"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Character-output-stream-methods">Character output stream methods</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Character-input-stream-methods">Character input stream methods</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.5 Output stream methods</h4>

<p>These generic functions are used to implement subclasses of
fundamental-output-stream:

   </p><p><a name="Generic_002dFunction-sb_002dgray_003astream_002dclear_002doutput"></a>

</p><div class="defun">
— Generic Function: <b>stream-clear-output [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dclear_002doutput_007d-425"></a></var><br>
<blockquote><p>This is like <code>cl:clear-output</code>, but for Gray streams: clear the given
  output <code>stream</code>. The default method does nothing. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dfinish_002doutput"></a>

</p><div class="defun">
— Generic Function: <b>stream-finish-output [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dfinish_002doutput_007d-426"></a></var><br>
<blockquote><p>Attempts to ensure that all output sent to the Stream has reached
  its destination, and only then returns false. Implements
  <code>finish-output</code>. The default method does nothing. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dforce_002doutput"></a>

</p><div class="defun">
— Generic Function: <b>stream-force-output [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dforce_002doutput_007d-427"></a></var><br>
<blockquote><p>Attempts to force any buffered output to be sent. Implements
  <code>force-output</code>. The default method does nothing. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dwrite_002dsequence"></a>

</p><div class="defun">
— Generic Function: <b>stream-write-sequence [sb-gray]</b><var> stream seq &amp;optional start end<a name="index-g_t_0040sbgray_007bstream_002dwrite_002dsequence_007d-428"></a></var><br>
<blockquote><p>This is like <code>cl:write-sequence</code>, but for Gray streams. 
</p></blockquote></div>

<div class="node">
<a name="Character-output-stream-methods"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Binary-stream-methods">Binary stream methods</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Output-stream-methods">Output stream methods</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.6 Character output stream methods</h4>

<p>These generic functions are used to implement subclasses of
fundamental-character-output-stream:

   </p><p><a name="Generic_002dFunction-sb_002dgray_003astream_002dadvance_002dto_002dcolumn"></a>

</p><div class="defun">
— Generic Function: <b>stream-advance-to-column [sb-gray]</b><var> stream column<a name="index-g_t_0040sbgray_007bstream_002dadvance_002dto_002dcolumn_007d-429"></a></var><br>
<blockquote><p>Write enough blank space so that the next character will be
  written at the specified column. Returns true if the operation is
  successful, or <code>nil</code> if it is not supported for this stream. This is
  intended for use by by <code>pprint</code> and <code>format</code> ~T. The default method uses
  <code>stream-line-column</code> and repeated calls to <code>stream-write-char</code> with a
  <code>#space</code> character; it returns <code>nil</code> if <code>stream-line-column</code> returns <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dfresh_002dline"></a>

</p><div class="defun">
— Generic Function: <b>stream-fresh-line [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dfresh_002dline_007d-430"></a></var><br>
<blockquote><p>Outputs a new line to the Stream if it is not positioned at the
  beginning of a line. Returns <code>t</code> if it output a new line, nil
  otherwise. Used by <code>fresh-line</code>. The default method uses
  <code>stream-start-line-p</code> and <code>stream-terpri</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dline_002dcolumn"></a>

</p><div class="defun">
— Generic Function: <b>stream-line-column [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dline_002dcolumn_007d-431"></a></var><br>
<blockquote><p>Return the column number where the next character
  will be written, or <code>nil</code> if that is not meaningful for this stream. 
  The first column on a line is numbered 0. This function is used in
  the implementation of <code>pprint</code> and the <code>format</code> ~T directive. For every
  character output stream class that is defined, a method must be
  defined for this function, although it is permissible for it to
  always return <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dline_002dlength"></a>

</p><div class="defun">
— Generic Function: <b>stream-line-length [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dline_002dlength_007d-432"></a></var><br>
<blockquote><p>Return the stream line length or <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dstart_002dline_002dp"></a>

</p><div class="defun">
— Generic Function: <b>stream-start-line-p [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dstart_002dline_002dp_007d-433"></a></var><br>
<blockquote><p>Is <code>stream</code> known to be positioned at the beginning of a line? 
  It is permissible for an implementation to always return
  <code>nil</code>. This is used in the implementation of <code>fresh-line</code>. Note that
  while a value of 0 from <code>stream-line-column</code> also indicates the
  beginning of a line, there are cases where <code>stream-start-line-p</code> can be
  meaningfully implemented although <code>stream-line-column</code> can't be. For
  example, for a window using variable-width characters, the column
  number isn't very meaningful, but the beginning of the line does have
  a clear meaning. The default method for <code>stream-start-line-p</code> on class
  <code>fundamental-character-output-stream</code> uses <code>stream-line-column</code>, so if
  that is defined to return <code>nil</code>, then a method should be provided for
  either <code>stream-start-line-p</code> or <code>stream-fresh-line</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dterpri"></a>

</p><div class="defun">
— Generic Function: <b>stream-terpri [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dterpri_007d-434"></a></var><br>
<blockquote><p>Writes an end of line, as for <code>terpri</code>. Returns <code>nil</code>. The default
  method does (<code>stream-write-char</code> stream #NEWLINE). 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dwrite_002dchar"></a>

</p><div class="defun">
— Generic Function: <b>stream-write-char [sb-gray]</b><var> stream character<a name="index-g_t_0040sbgray_007bstream_002dwrite_002dchar_007d-435"></a></var><br>
<blockquote><p>Write <code>character</code> to <code>stream</code> and return <code>character</code>. Every
  subclass of <code>fundamental-character-output-stream</code> must have a method
  defined for this function. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dwrite_002dstring"></a>

</p><div class="defun">
— Generic Function: <b>stream-write-string [sb-gray]</b><var> stream string &amp;optional start end<a name="index-g_t_0040sbgray_007bstream_002dwrite_002dstring_007d-436"></a></var><br>
<blockquote><p>This is used by <code>write-string</code>. It writes the string to the stream,
  optionally delimited by start and end, which default to 0 and <code>nil</code>. 
  The string argument is returned. The default method provided by
  <code>fundamental-character-output-stream</code> uses repeated calls to
  <code>stream-write-char</code>. 
</p></blockquote></div>

<div class="node">
<a name="Binary-stream-methods"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Gray-Streams-examples">Gray Streams examples</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Character-output-stream-methods">Character output stream methods</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.7 Binary stream methods</h4>

<p>The following generic functions are available for subclasses of
fundamental-binary-stream:

   </p><p><a name="Generic_002dFunction-sb_002dgray_003astream_002dread_002dbyte"></a>

</p><div class="defun">
— Generic Function: <b>stream-read-byte [sb-gray]</b><var> stream<a name="index-g_t_0040sbgray_007bstream_002dread_002dbyte_007d-437"></a></var><br>
<blockquote><p>Used by <code>read-byte</code>; returns either an integer, or the symbol <code>:eof</code>
  if the stream is at end-of-file. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dgray_003astream_002dwrite_002dbyte"></a>

</p><div class="defun">
— Generic Function: <b>stream-write-byte [sb-gray]</b><var> stream integer<a name="index-g_t_0040sbgray_007bstream_002dwrite_002dbyte_007d-438"></a></var><br>
<blockquote><p>Implements <code>write-byte</code>; writes the integer to the stream and
  returns the integer as the result. 
</p></blockquote></div>

<div class="node">
<a name="Gray-Streams-examples"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Binary-stream-methods">Binary stream methods</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams">Gray Streams</a>

</div>

<h4 class="subsection">10.3.8 Gray Streams examples</h4>

<p>Below are two classes of stream that can be conveniently defined as
wrappers for Common Lisp streams.  These are meant to serve as
examples of minimal implementations of the protocols that must be
followed when defining Gray streams.  Realistic uses of the Gray
Streams API would implement the various methods that can do I/O in
batches, such as <code>stream-read-line<!-- /@w --></code>, <code>stream-write-string<!-- /@w --></code>,
<code>stream-read-sequence<!-- /@w --></code>, and <code>stream-write-sequence<!-- /@w --></code>.

</p><ul class="menu">
<li><a accesskey="1" href="#Character-counting-input-stream">Character counting input stream</a>
</li><li><a accesskey="2" href="#Output-prefixing-character-stream">Output prefixing character stream</a>
</li></ul>

<div class="node">
<a name="Character-counting-input-stream"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Output-prefixing-character-stream">Output prefixing character stream</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams-examples">Gray Streams examples</a>

</div>

<h5 class="subsubsection">10.3.8.1 Character counting input stream</h5>

<p>It is occasionally handy for programs that process input files to
count the number of characters and lines seen so far, and the number
of characters seen on the current line, so that useful messages may be
reported in case of parsing errors, etc.  Here is a character input
stream class that keeps track of these counts.  Note that all
character input streams must implement <code>stream-read-char<!-- /@w --></code> and
<code>stream-unread-char<!-- /@w --></code>.

</p><pre class="lisp">     (defclass wrapped-stream (fundamental-stream)
       ((stream :initarg :stream :reader stream-of)))
     
     (defmethod stream-element-type ((stream wrapped-stream))
       (stream-element-type (stream-of stream)))
     
     (defmethod close ((stream wrapped-stream) &amp;key abort)
       (close (stream-of stream) :abort abort))
     
     (defclass wrapped-character-input-stream
         (wrapped-stream fundamental-character-input-stream)
       ())
     
     (defmethod stream-read-char ((stream wrapped-character-input-stream))
       (read-char (stream-of stream) nil :eof))
     
     (defmethod stream-unread-char ((stream wrapped-character-input-stream)
                                    char)
       (unread-char char (stream-of stream)))
     
     (defclass counting-character-input-stream
         (wrapped-character-input-stream)
       ((char-count :initform 1 :accessor char-count-of)
        (line-count :initform 1 :accessor line-count-of)
        (col-count :initform 1 :accessor col-count-of)
        (prev-col-count :initform 1 :accessor prev-col-count-of)))
     
     (defmethod stream-read-char ((stream counting-character-input-stream))
       (with-accessors ((inner-stream stream-of) (chars char-count-of)
                        (lines line-count-of) (cols col-count-of)
                        (prev prev-col-count-of)) stream
           (let ((char (call-next-method)))
             (cond ((eql char :eof)
                    :eof)
                   ((char= char #\Newline)
                    (incf lines)
                    (incf chars)
                    (setf prev cols)
                    (setf cols 1)
                    char)
                   (t
                    (incf chars)
                    (incf cols)
                    char)))))
     
     (defmethod stream-unread-char ((stream counting-character-input-stream)
                                    char)
       (with-accessors ((inner-stream stream-of) (chars char-count-of)
                        (lines line-count-of) (cols col-count-of)
                        (prev prev-col-count-of)) stream
           (cond ((char= char #\Newline)
                  (decf lines)
                  (decf chars)
                  (setf cols prev))
                 (t
                  (decf chars)
                  (decf cols)
                  char))
           (call-next-method)))
</pre>
   <p>The default methods for <code>stream-read-char-no-hang<!-- /@w --></code>,
<code>stream-peek-char<!-- /@w --></code>, <code>stream-listen<!-- /@w --></code>,
<code>stream-clear-input<!-- /@w --></code>, <code>stream-read-line<!-- /@w --></code>, and
<code>stream-read-sequence<!-- /@w --></code> should be sufficient (though the last two
will probably be slower than methods that forwarded directly).

   </p><p>Here's a sample use of this class:

</p><pre class="lisp">     (with-input-from-string (input "1 2
      3 :foo  ")
       (let ((counted-stream (make-instance 'counting-character-input-stream
                              :stream input)))
         (loop for thing = (read counted-stream) while thing
            unless (numberp thing) do
              (error "Non-number ~S (line ~D, column ~D)" thing
                     (line-count-of counted-stream)
                     (- (col-count-of counted-stream)
                        (length (format nil "~S" thing))))
            end
            do (print thing))))
<pre class="verbatim">     1
     2
     3
     Non-number :FOO (line 2, column 5)
       [Condition of type SIMPLE-ERROR]
</pre>
</pre>
   <div class="node">
<a name="Output-prefixing-character-stream"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Character-counting-input-stream">Character counting input stream</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Gray-Streams-examples">Gray Streams examples</a>

</div>

<h5 class="subsubsection">10.3.8.2 Output prefixing character stream</h5>

<p>One use for a wrapped output stream might be to prefix each line of
text with a timestamp, e.g., for a logging stream.  Here's a simple
stream that does this, though without any fancy line-wrapping.  Note
that all character output stream classes must implement
<code>stream-write-char<!-- /@w --></code> and <code>stream-line-column<!-- /@w --></code>.

</p><pre class="lisp">     (defclass wrapped-stream (fundamental-stream)
       ((stream :initarg :stream :reader stream-of)))
     
     (defmethod stream-element-type ((stream wrapped-stream))
       (stream-element-type (stream-of stream)))
     
     (defmethod close ((stream wrapped-stream) &amp;key abort)
       (close (stream-of stream) :abort abort))
     
     (defclass wrapped-character-output-stream
         (wrapped-stream fundamental-character-output-stream)
       ((col-index :initform 0 :accessor col-index-of)))
     
     (defmethod stream-line-column ((stream wrapped-character-output-stream))
       (col-index-of stream))
     
     (defmethod stream-write-char ((stream wrapped-character-output-stream)
                                   char)
       (with-accessors ((inner-stream stream-of) (cols col-index-of)) stream
         (write-char char inner-stream)
         (if (char= char #\Newline)
             (setf cols 0)
             (incf cols))))
     
     (defclass prefixed-character-output-stream
         (wrapped-character-output-stream)
       ((prefix :initarg :prefix :reader prefix-of)))
     
     (defgeneric write-prefix (prefix stream)
       (:method ((prefix string) stream) (write-string prefix stream))
       (:method ((prefix function) stream) (funcall prefix stream)))
     
     (defmethod stream-write-char ((stream prefixed-character-output-stream)
                                   char)
       (with-accessors ((inner-stream stream-of) (cols col-index-of)
                        (prefix prefix-of)) stream
         (when (zerop cols)
           (write-prefix prefix inner-stream))
         (call-next-method)))
</pre>
   <p>As with the example input stream, this implements only the minimal
protocol.  A production implementation should also provide methods for
at least <code>stream-write-line<!-- /@w --></code>, <code>stream-write-sequence<!-- /@w --></code>.

   </p><p>And here's a sample use of this class:

</p><pre class="lisp">     (flet ((format-timestamp (stream)
              (apply #'format stream "[~2@*~2,' D:~1@*~2,'0D:~0@*~2,'0D] "
                     (multiple-value-list (get-decoded-time)))))
       (let ((output (make-instance 'prefixed-character-output-stream
                                    :stream *standard-output*
                                    :prefix #'format-timestamp)))
         (loop for string in '("abc" "def" "ghi") do
              (write-line string output)
              (sleep 1))))
<pre class="verbatim">     [ 0:30:05] abc
     [ 0:30:06] def
     [ 0:30:07] ghi
     NIL
</pre>
</pre>
   <div class="node">
<a name="Simple-Streams"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Gray-Streams">Gray Streams</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Streams">Streams</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">10.4 Simple Streams</h3>

<p>Simple streams are an extensible streams protocol that avoids some
problems with Gray streams.

   </p><p>Documentation about simple streams is available at:

   </p><p><a href="http://www.franz.com/support/documentation/6.2/doc/streams.htm">http://www.franz.com/support/documentation/6.2/doc/streams.htm</a>

   </p><p>The implementation should be considered Alpha-quality; the basic
framework is there, but many classes are just stubs at the moment.

   </p><p>See <samp><span class="file">SYS:CONTRIB;SB-SIMPLE-STREAMS;SIMPLE-STREAM-TEST.LISP</span></samp> for
things that should work.

   </p><p>Known differences to the ACL behaviour:

     </p><ul>
<li><code>open</code> not return a simple-stream by default. This can be
adjusted; see default-open-class in the file cl.lisp

     </li><li><code>write-vector</code> is unimplemented.

   </li></ul>

<div class="node">
<a name="Package-Locks"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Threading">Threading</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Streams">Streams</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">11 Package Locks</h2>

<p><a name="index-Packages_002c-locked-439"></a>
None of the following sections apply to SBCL built without package
locking support.

   </p><blockquote>
<b>warning:</b> The interface described here is experimental: incompatible changes in
future SBCL releases are possible, even expected: the concept of
“implementation packages” and the associated operators may be renamed;
more operations (such as naming restarts or catch tags) may be added to
the list of operations violating package locks. 
</blockquote>

<ul class="menu">
<li><a accesskey="1" href="#Package-Lock-Concepts">Package Lock Concepts</a>
</li><li><a accesskey="2" href="#Package-Lock-Dictionary">Package Lock Dictionary</a>
</li></ul>

<div class="node">
<a name="Package-Lock-Concepts"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Package-Lock-Dictionary">Package Lock Dictionary</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Locks">Package Locks</a>

</div>

<h3 class="section">11.1 Package Lock Concepts</h3>

<ul class="menu">
<li><a accesskey="1" href="#Package-Lock-Overview">Package Lock Overview</a>
</li><li><a accesskey="2" href="#Implementation-Packages">Implementation Packages</a>
</li><li><a accesskey="3" href="#Package-Lock-Violations">Package Lock Violations</a>
</li><li><a accesskey="4" href="#Package-Locks-in-Compiled-Code">Package Locks in Compiled Code</a>
</li><li><a accesskey="5" href="#Operations-Violating-Package-Locks">Operations Violating Package Locks</a>
</li></ul>

<div class="node">
<a name="Package-Lock-Overview"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Implementation-Packages">Implementation Packages</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Lock-Concepts">Package Lock Concepts</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h4 class="subsection">11.1.1 Package Locking Overview</h4>

<p>Package locks protect against unintentional modifications of a package:
they provide similar protection to user packages as is mandated to
<code>common-lisp</code> package by the ANSI specification. They are not, and
should not be used as, a security measure.

   </p><p>Newly created packages are by default unlocked (see the <code>:lock</code>
option to <code>defpackage</code>).

   </p><p>The package <code>common-lisp</code> and SBCL internal implementation
packages are locked by default, including <code>sb-ext</code>.

   </p><p>It may be beneficial to lock <code>common-lisp-user</code> as well, to
ensure that various libraries don't pollute it without asking,
but this is not currently done by default.

</p><div class="node">
<a name="Implementation-Packages"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Package-Lock-Violations">Package Lock Violations</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package-Lock-Overview">Package Lock Overview</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Lock-Concepts">Package Lock Concepts</a>

</div>

<h4 class="subsection">11.1.2 Implementation Packages</h4>

<p><a name="index-g_t_0040cl_007b_0040earmuffs_007bpackage_007d_007d-440"></a><a name="index-g_t_0040cl_007bdefpackage_007d-441"></a>
Each package has a list of associated implementation packages. A
locked package, and the symbols whose home package it is, can be
modified without violating package locks only when <code>*package*</code> is
bound to one of the implementation packages of the locked package.

   </p><p>Unless explicitly altered by <code>defpackage</code>,
<code>sb-ext:add-implementation-package</code>, or
<code>sb-ext:remove-implementation-package</code> each package is its own
(only) implementation package.

</p><div class="node">
<a name="Package-Lock-Violations"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Package-Locks-in-Compiled-Code">Package Locks in Compiled Code</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Implementation-Packages">Implementation Packages</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Lock-Concepts">Package Lock Concepts</a>

</div>

<h4 class="subsection">11.1.3 Package Lock Violations</h4>

<p><a name="index-g_t_0040sbext_007bpackage_002dlock_002dviolation_007d-442"></a><a name="index-g_t_0040sbext_007bpackage_002dlocked_002derror_007d-443"></a><a name="index-g_t_0040sbext_007bsymbol_002dpackage_002dlocked_002derror_007d-444"></a><a name="index-g_t_0040cl_007bpackage_002derror_007d-445"></a>

</p><h5 class="subsubsection">11.1.3.1 Lexical Bindings and Declarations</h5>

<p><a name="index-g_t_0040cl_007blet_007d-446"></a><a name="index-g_t_0040cl_007blet_002a_007d-447"></a><a name="index-g_t_0040cl_007bflet_007d-448"></a><a name="index-g_t_0040cl_007blabels_007d-449"></a><a name="index-g_t_0040cl_007bmacrolet_007d-450"></a><a name="index-g_t_0040cl_007bsymbol_002dmacrolet_007d-451"></a><a name="index-g_t_0040cl_007bdeclare_007d-452"></a><a name="index-Declarations-453"></a><a name="index-g_t_0040sbext_007bdisable_002dpackage_002dlocks_007d-454"></a><a name="index-g_t_0040sbext_007benable_002dpackage_002dlocks_007d-455"></a>
Lexical bindings or declarations that violate package locks cause a
compile-time warning, and a runtime <code>program-error</code> when the form
that violates package locks would be executed.

   </p><p>A complete listing of operators affect by this is: <code>let</code>,
<code>let*</code>, <code>flet</code>, <code>labels</code>, <code>macrolet</code>, and
<code>symbol-macrolet</code>, <code>declare</code>.

   </p><p>Package locks affecting both lexical bindings and declarations can be
disabled locally with <code>sb-ext:disable-package-locks</code> declaration,
and re-enabled with <code>sb-ext:enable-package-locks</code> declaration.

   </p><p>Example:

</p><pre class="lisp">     (in-package :locked)
     
     (defun foo () ...)
     
     (defmacro with-foo (&amp;body body)
       `(locally (declare (disable-package-locks locked:foo))
          (flet ((foo () ...))
            (declare (enable-package-locks locked:foo)) ; re-enable for body
            ,@body)))
</pre>
   <h5 class="subsubsection">11.1.3.2 Other Operations</h5>

<p>If an non-lexical operation violates a package lock, a continuable
error that is of a subtype of <code>sb-ext:package-lock-violation</code>
(subtype of <code>package-error</code>) is signalled when the operation is
attempted.

   </p><p>Additional restarts may be established for continuable package lock
violations for interactive use.

   </p><p>The actual type of the error depends on circumstances that caused the
violation: operations on packages signal errors of type
<code>sb-ext:package-locked-error</code>, and operations on symbols signal
errors of type <code>sb-ext:symbol-package-locked-error</code>.

</p><div class="node">
<a name="Package-Locks-in-Compiled-Code"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Operations-Violating-Package-Locks">Operations Violating Package Locks</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package-Lock-Violations">Package Lock Violations</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Lock-Concepts">Package Lock Concepts</a>

</div>

<h4 class="subsection">11.1.4 Package Locks in Compiled Code</h4>

<h5 class="subsubsection">11.1.4.1 Interned Symbols</h5>

<p>If file-compiled code contains interned symbols, then loading that code
into an image without the said symbols will not cause a package lock
violation, even if the packages in question are locked.

</p><h5 class="subsubsection">11.1.4.2 Other Limitations on Compiled Code</h5>

<p>With the exception of interned symbols, behaviour is unspecified if
package locks affecting compiled code are not the same during loading
of the code or execution.

   </p><p>Specifically, code compiled with packages unlocked may or may not fail
to signal package-lock-violations even if the packages are locked at
runtime, and code compiled with packages locked may or may not signal
spurious package-lock-violations at runtime even if the packages are
unlocked.

   </p><p>In practice all this means that package-locks have a negligible
performance penalty in compiled code as long as they are not violated.

</p><div class="node">
<a name="Operations-Violating-Package-Locks"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package-Locks-in-Compiled-Code">Package Locks in Compiled Code</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Lock-Concepts">Package Lock Concepts</a>

</div>

<h4 class="subsection">11.1.5 Operations Violating Package Locks</h4>

<h5 class="subsubsection">11.1.5.1 Operations on Packages</h5>

<p>The following actions cause a package lock violation if the package
operated on is locked, and <code>*package*</code> is not an implementation
package of that package, and the action would cause a change in the
state of the package (so e.g. exporting already external symbols is
never a violation). Package lock violations caused by these operations
signal errors of type <code>sb-ext:package-locked-error</code>.

     </p><ol start="1" type="1">
<li>Shadowing a symbol in a package.

     </li><li>Importing a symbol to a package.

     </li><li>Uninterning a symbol from a package.

     </li><li>Exporting a symbol from a package.

     </li><li>Unexporting a symbol from a package.

     </li><li>Changing the packages used by a package.

     </li><li>Renaming a package.

     </li><li>Deleting a package.

     </li><li>Adding a new package local nickname to a package.

     </li><li>Removing an existing package local nickname to a package.

        </li></ol>

<h5 class="subsubsection">11.1.5.2 Operations on Symbols</h5>

<p>Following actions cause a package lock violation if the home package
of the symbol operated on is locked, and <code>*package*</code> is not an
implementation package of that package. Package lock violations caused
by these action signal errors of type
<code>sb-ext:symbol-package-locked-error</code>.

   </p><p>These actions cause only one package lock violation per lexically
apparent violated package.

   </p><p>Example:

</p><pre class="lisp">     ;;; Packages FOO and BAR are locked.
     ;;;
     ;;; Two lexically apparent violated packages: exactly two
     ;;; package-locked-errors will be signalled.
     
     (defclass foo:point ()
       ((x :accessor bar:x)
        (y :accessor bar:y)))
</pre>
     <ol start="1" type="1">
<li>Binding or altering its value lexically or dynamically, or
establishing it as a symbol-macro.

     <p>Exceptions:

          </p><ul>
<li>If the symbol is not defined as a constant, global symbol-macro or a
global dynamic variable, it may be lexically bound or established as a
local symbol macro.

          </li><li>If the symbol is defined as a global dynamic variable, it may be
assigned or bound.

     </li></ul>

     </li><li>Defining, undefining, or binding it, or its setf name as a function.

     <p>Exceptions:

          </p><ul>
<li>If the symbol is not defined as a function, macro, or special operator
it and its setf name may be lexically bound as a function.

     </li></ul>

     </li><li>Defining, undefining, or binding it as a macro or compiler macro.

     <p>Exceptions:

          </p><ul>
<li>If the symbol is not defined as a function, macro, or special operator
it may be lexically bound as a macro.

     </li></ul>

     </li><li>Defining it as a type specifier or structure.

     </li><li>Defining it as a declaration with a declaration proclamation.

     </li><li>Declaring or proclaiming it special.

     </li><li>Declaring or proclaiming its type or ftype.

     <p>Exceptions:

          </p><ul>
<li>If the symbol may be lexically bound, the type of that binding may be
declared.

          </li><li>If the symbol may be lexically bound as a function, the ftype of that
binding may be declared.

     </li></ul>

     </li><li>Defining a setf expander for it.

     </li><li>Defining it as a method combination type.

     </li><li>Using it as the class-name argument to setf of find-class.

     </li><li>Defining it as a hash table test using <code>sb-ext:define-hash-table-test</code>.

        </li></ol>

<div class="node">
<a name="Package-Lock-Dictionary"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package-Lock-Concepts">Package Lock Concepts</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Package-Locks">Package Locks</a>

</div>

<h3 class="section">11.2 Package Lock Dictionary</h3>

<div class="defun">
— Declaration: <b>disable-package-locks [sb-ext]</b><var><a name="index-g_t_0040sbext_007bdisable_002dpackage_002dlocks_007d-456"></a></var><br>
<blockquote>
        <p>Syntax: <code>(sb-ext:disable-package-locks symbol*)</code>

        </p><p>Disables package locks affecting the named symbols during compilation
in the lexical scope of the declaration. Disabling locks on symbols
whose home package is unlocked, or disabling an already disabled lock,
has no effect. 
</p></blockquote></div>

<div class="defun">
— Declaration: <b>enable-package-locks [sb-ext]</b><var><a name="index-g_t_0040sbext_007benable_002dpackage_002dlocks_007d-457"></a></var><br>
<blockquote>
        <p>Syntax: <code>(sb-ext:enable-package-locks symbol*)</code>

        </p><p>Re-enables package locks affecting the named symbols during compilation
in the lexical scope of the declaration. Enabling locks that were not
first disabled with <code>sb-ext:disable-package-locks</code> declaration, or
enabling locks that are already enabled has no effect. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003apackage_002dlock_002dviolation"></a>

</p><div class="defun">
— Condition: <b>package-lock-violation [sb-ext]</b><var><a name="index-g_t_0040sbext_007bpackage_002dlock_002dviolation_007d-458"></a></var><br>
<blockquote><p>Class precedence list: <code>package-lock-violation, package-error, error, serious-condition, condition, t</code>

        </p><p>Subtype of <code>cl:package-error</code>. A subtype of this error is signalled
when a package-lock is violated. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003apackage_002dlocked_002derror"></a>

</p><div class="defun">
— Condition: <b>package-locked-error [sb-ext]</b><var><a name="index-g_t_0040sbext_007bpackage_002dlocked_002derror_007d-459"></a></var><br>
<blockquote><p>Class precedence list: <code>package-locked-error, package-lock-violation, package-error, error, serious-condition, condition, t</code>

        </p><p>Subtype of <code>sb-ext:package-lock-violation</code>. An error of this type is
signalled when an operation on a package violates a package lock. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003asymbol_002dpackage_002dlocked_002derror"></a>

</p><div class="defun">
— Condition: <b>symbol-package-locked-error [sb-ext]</b><var><a name="index-g_t_0040sbext_007bsymbol_002dpackage_002dlocked_002derror_007d-460"></a></var><br>
<blockquote><p>Class precedence list: <code>symbol-package-locked-error, package-lock-violation, package-error, error, serious-condition, condition, t</code>

        </p><p>Subtype of <code>sb-ext:package-lock-violation</code>. An error of this type is
signalled when an operation on a symbol violates a package lock. The
symbol that caused the violation is accessed by the function
<code>sb-ext:package-locked-error-symbol</code>. 
</p></blockquote></div>

<div class="defun">
— Function: <b>package-locked-error-symbol [sb-ext]</b><var> symbol-package-locked-error<a name="index-g_t_0040sbext_007bpackage_002dlocked_002derror_002dsymbol_007d-461"></a></var><br>
<blockquote>
        <p>Returns the symbol that caused the <code>symbol-package-locked-error</code>
condition. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003apackage_002dlocked_002dp"></a>

</p><div class="defun">
— Function: <b>package-locked-p [sb-ext]</b><var> package<a name="index-g_t_0040sbext_007bpackage_002dlocked_002dp_007d-462"></a></var><br>
<blockquote><p>Returns <code>t</code> when <code>package</code> is locked, <code>nil</code> otherwise. Signals an error
if <code>package</code> doesn't designate a valid package. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003alock_002dpackage"></a>

</p><div class="defun">
— Function: <b>lock-package [sb-ext]</b><var> package<a name="index-g_t_0040sbext_007block_002dpackage_007d-463"></a></var><br>
<blockquote><p>Locks <code>package</code> and returns <code>t</code>. Has no effect if <code>package</code> was already
locked. Signals an error if <code>package</code> is not a valid package designator
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aunlock_002dpackage"></a>

</p><div class="defun">
— Function: <b>unlock-package [sb-ext]</b><var> package<a name="index-g_t_0040sbext_007bunlock_002dpackage_007d-464"></a></var><br>
<blockquote><p>Unlocks <code>package</code> and returns <code>t</code>. Has no effect if <code>package</code> was already
unlocked. Signals an error if <code>package</code> is not a valid package designator. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003apackage_002dimplemented_002dby_002dlist"></a>

</p><div class="defun">
— Function: <b>package-implemented-by-list [sb-ext]</b><var> package<a name="index-g_t_0040sbext_007bpackage_002dimplemented_002dby_002dlist_007d-465"></a></var><br>
<blockquote><p>Returns a list containing the implementation packages of
<code>package</code>. Signals an error if <code>package</code> is not a valid package designator. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003apackage_002dimplements_002dlist"></a>

</p><div class="defun">
— Function: <b>package-implements-list [sb-ext]</b><var> package<a name="index-g_t_0040sbext_007bpackage_002dimplements_002dlist_007d-466"></a></var><br>
<blockquote><p>Returns the packages that <code>package</code> is an implementation package
of. Signals an error if <code>package</code> is not a valid package designator. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aadd_002dimplementation_002dpackage"></a>

</p><div class="defun">
— Function: <b>add-implementation-package [sb-ext]</b><var> packages-to-add &amp;optional package<a name="index-g_t_0040sbext_007badd_002dimplementation_002dpackage_007d-467"></a></var><br>
<blockquote><p>Adds <code>packages-to-add</code> as implementation packages of <code>package</code>. Signals
an error if <code>package</code> or any of the <code>packages-to-add</code> is not a valid
package designator. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aremove_002dimplementation_002dpackage"></a>

</p><div class="defun">
— Function: <b>remove-implementation-package [sb-ext]</b><var> packages-to-remove &amp;optional package<a name="index-g_t_0040sbext_007bremove_002dimplementation_002dpackage_007d-468"></a></var><br>
<blockquote><p>Removes <code>packages-to-remove</code> from the implementation packages of
<code>package</code>. Signals an error if <code>package</code> or any of the <code>packages-to-remove</code>
is not a valid package designator. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003awithout_002dpackage_002dlocks"></a>

</p><div class="defun">
— Macro: <b>without-package-locks [sb-ext]</b><var> &amp;body body<a name="index-g_t_0040sbext_007bwithout_002dpackage_002dlocks_007d-469"></a></var><br>
<blockquote><p>Ignores all runtime package lock violations during the execution of
body. Body can begin with declarations. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003awith_002dunlocked_002dpackages"></a>

</p><div class="defun">
— Macro: <b>with-unlocked-packages [sb-ext]</b> (<var>&amp;rest packages</var>)<var> &amp;body forms<a name="index-g_t_0040sbext_007bwith_002dunlocked_002dpackages_007d-470"></a></var><br>
<blockquote><p>Unlocks <code>packages</code> for the dynamic scope of the body. Signals an
error if any of <code>packages</code> is not a valid package designator. 
</p></blockquote></div>

<div class="defun">
— Macro: <b>defpackage [cl]</b><var> name </var>[[<var>option</var>]]<var>* ⇒ package<a name="index-g_t_0040cl_007bdefpackage_007d-471"></a></var><br>
<blockquote>
        <p>Options are extended to include the following:

          </p><ul>
<li><code>:lock</code> <var>boolean</var>

          <p>If the argument to <code>:lock</code> is <code>t</code>, the package is initially
locked.  If <code>:lock</code> is not provided it defaults to <code>nil</code>.

          </p></li><li><code>:implement</code> <var>package-designator</var>*

          <p>The package is added as an implementation package to the packages
named. If <code>:implement</code> is not provided, it defaults to the
package itself. 
</p></li></ul>

        <p>Example:

     </p><pre class="lisp">          (defpackage "FOO" (:export "BAR") (:lock t) (:implement))
          (defpackage "FOO-INT" (:use "FOO") (:implement "FOO" "FOO-INT"))
          
          ;;; is equivalent to
          
          (defpackage "FOO") (:export "BAR"))
          (lock-package "FOO")
          (remove-implementation-package "FOO" "FOO")
          (defpackage "FOO-INT" (:use "BAR"))
          (add-implementation-package "FOO-INT" "FOO")
</pre>
        </blockquote></div>

<div class="node">
<a name="Threading"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Timers">Timers</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Package-Locks">Package Locks</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">12 Threading</h2>

<p>SBCL supports a fairly low-level threading interface that maps onto
the host operating system's concept of threads or lightweight
processes.  This means that threads may take advantage of hardware
multiprocessing on machines that have more than one CPU, but it does
not allow Lisp control of the scheduler.  This is found in the
SB-THREAD package.

   </p><p>Threads are part of the default build on x86[-64]/ARM64 Linux and Windows.

   </p><p>They are also supported on: x86[-64] Darwin (Mac OS X), x86[-64]
FreeBSD, x86 SunOS (Solaris), PPC Linux, ARM64 Linux. On these
platforms threads must be explicitly enabled at build-time, see
<samp><span class="file">INSTALL</span></samp> for directions.

</p><ul class="menu">
<li><a accesskey="1" href="#Threading-basics">Threading basics</a>
</li><li><a accesskey="2" href="#Special-Variables">Special Variables</a>
</li><li><a accesskey="3" href="#Atomic-Operations">Atomic Operations</a>
</li><li><a accesskey="4" href="#Mutex-Support">Mutex Support</a>
</li><li><a accesskey="5" href="#Semaphores">Semaphores</a>
</li><li><a accesskey="6" href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a>
</li><li><a accesskey="7" href="#Barriers">Barriers</a>
</li><li><a accesskey="8" href="#Sessions_002fDebugging">Sessions/Debugging</a>
</li><li><a accesskey="9" href="#Foreign-threads">Foreign threads</a>
</li><li><a href="#Implementation-_0028Linux-x86_002fx86_002d64_0029">Implementation (Linux x86/x86-64)</a>
</li></ul>

<div class="node">
<a name="Threading-basics"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Special-Variables">Special Variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.1 Threading basics</h3>

<pre class="lisp">     (make-thread (lambda () (write-line "Hello, world")))
</pre>
<h4 class="subsection">12.1.1 Thread Objects</h4>

<p><a name="Structure-sb_002dthread_003athread"></a>

</p><div class="defun">
— Structure: <b>thread [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bthread_007d-472"></a></var><br>
<blockquote><p>Class precedence list: <code>thread, structure-object, t</code>

        </p><p>Thread type. Do not rely on threads being structs as it may change
in future versions. 
</p></blockquote></div>

   <p><a name="Variable-sb_002dthread_003a_002acurrent_002dthread_002a"></a>

</p><div class="defun">
— Variable: <b>*current-thread* [sb-thread]</b><var><a name="index-g_t_0040sbthread_007b_0040earmuffs_007bcurrent_002dthread_007d_007d-473"></a></var><br>
<blockquote><p>Bound in each thread to the thread itself. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003alist_002dall_002dthreads"></a>

</p><div class="defun">
— Function: <b>list-all-threads [sb-thread]</b><var><a name="index-g_t_0040sbthread_007blist_002dall_002dthreads_007d-474"></a></var><br>
<blockquote><p>Return a list of the live threads. Note that the return value is
potentially stale even before the function returns, as new threads may be
created and old ones may exit at any time. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003athread_002dalive_002dp"></a>

</p><div class="defun">
— Function: <b>thread-alive-p [sb-thread]</b><var> thread<a name="index-g_t_0040sbthread_007bthread_002dalive_002dp_007d-475"></a></var><br>
<blockquote><p>Return <code>t</code> if <code>thread</code> is still alive. Note that the return value is
potentially stale even before the function returns, as the thread may exit at
any time. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003athread_002dname"></a>

</p><div class="defun">
— Function: <b>thread-name [sb-thread]</b><var> instance<a name="index-g_t_0040sbthread_007bthread_002dname_007d-476"></a></var><br>
<blockquote><p>Name of the thread. Can be assigned to using <code>setf</code>. Thread names can be
arbitrary printable objects, and need not be unique. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amain_002dthread_002dp"></a>

</p><div class="defun">
— Function: <b>main-thread-p [sb-thread]</b><var> &amp;optional thread<a name="index-g_t_0040sbthread_007bmain_002dthread_002dp_007d-477"></a></var><br>
<blockquote><p>True if <code>thread</code>, defaulting to current thread, is the main thread of the process. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amain_002dthread"></a>

</p><div class="defun">
— Function: <b>main-thread [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bmain_002dthread_007d-478"></a></var><br>
<blockquote><p>Returns the main thread of the process. 
</p></blockquote></div>

<h4 class="subsection">12.1.2 Making, Returning From, Joining, and Yielding Threads</h4>

<p><a name="Function-sb_002dthread_003amake_002dthread"></a>

</p><div class="defun">
— Function: <b>make-thread [sb-thread]</b><var> function &amp;key name arguments ephemeral<a name="index-g_t_0040sbthread_007bmake_002dthread_007d-479"></a></var><br>
<blockquote><p>Create a new thread of <code>name</code> that runs <code>function</code> with the argument
list designator provided (defaults to no argument). Thread exits when
the function returns. The return values of <code>function</code> are kept around
and can be retrieved by <code>join-thread</code>.

        </p><p>Invoking the initial <code>abort</code> restart established by <code>make-thread</code>
terminates the thread.

        </p><p>See also: <code>return-from-thread</code>, <code>abort-thread</code>. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dthread_003areturn_002dfrom_002dthread"></a>

</p><div class="defun">
— Macro: <b>return-from-thread [sb-thread]</b><var> values-form &amp;key allow-exit<a name="index-g_t_0040sbthread_007breturn_002dfrom_002dthread_007d-480"></a></var><br>
<blockquote><p>Unwinds from and terminates the current thread, with values from
<code>values-form</code> as the results visible to <code>join-thread</code>.

        </p><p>If current thread is the main thread of the process (see
MAIN-THREAD-P), signals an error unless <code>allow-exit</code> is true, as
terminating the main thread would terminate the entire process. If
<code>allow-exit</code> is true, returning from the main thread is equivalent to
calling <code>sb-ext:exit</code> with <code>:code</code> 0 and <code>:abort</code> <code>nil</code>.

        </p><p>See also: <code>abort-thread</code> and <code>sb-ext:exit</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003aabort_002dthread"></a>

</p><div class="defun">
— Function: <b>abort-thread [sb-thread]</b><var> &amp;key allow-exit<a name="index-g_t_0040sbthread_007babort_002dthread_007d-481"></a></var><br>
<blockquote><p>Unwinds from and terminates the current thread abnormally, causing
<code>join-thread</code> on current thread to signal an error unless a
default-value is provided.

        </p><p>If current thread is the main thread of the process (see
MAIN-THREAD-P), signals an error unless <code>allow-exit</code> is true, as
terminating the main thread would terminate the entire process. If
<code>allow-exit</code> is true, aborting the main thread is equivalent to calling
<code>sb-ext:exit</code> code 1 and <code>:abort</code> <code>nil</code>.

        </p><p>Invoking the initial <code>abort</code> restart established by <code>make-thread</code> is
equivalent to calling <code>abort-thread</code> in other than main threads. 
However, whereas <code>abort</code> restart may be rebound, <code>abort-thread</code> always
unwinds the entire thread. (Behaviour of the initial <code>abort</code> restart for
main thread depends on the <code>:toplevel</code> argument to
<code>sb-ext:save-lisp-and-die</code>.)

        </p><p>See also: <code>return-from-thread</code> and <code>sb-ext:exit</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003ajoin_002dthread"></a>

</p><div class="defun">
— Function: <b>join-thread [sb-thread]</b><var> thread &amp;key default timeout<a name="index-g_t_0040sbthread_007bjoin_002dthread_007d-482"></a></var><br>
<blockquote><p>Suspend current thread until <code>thread</code> exits. Return the result values
of the thread function.

        </p><p>If <code>thread</code> does not exit within <code>timeout</code> seconds and <code>default</code> is
supplied, return two values: 1) <code>default</code> 2) <code>:timeout</code>. If <code>default</code> is not
supplied, signal a <code>join-thread-error</code> with <code>join-thread-problem</code> equal
to <code>:timeout</code>.

        </p><p>If <code>thread</code> does not exit normally (i.e. aborted) and <code>default</code> is
supplied, return two values: 1) <code>default</code> 2) <code>:abort</code>. If <code>default</code> is not
supplied, signal a <code>join-thread-error</code> with <code>join-thread-problem</code> equal
to <code>:abort</code>.

        </p><p>If <code>thread</code> is the current thread, signal a <code>join-thread-error</code> with
<code>join-thread-problem</code> equal to <code>:self-join</code>.

        </p><p>Trying to join the main thread causes <code>join-thread</code> to block until
<code>timeout</code> occurs or the process exits: when the main thread exits, the
entire process exits.

        </p><p><code>note:</code> Return convention in case of a timeout is experimental and
subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003athread_002dyield"></a>

</p><div class="defun">
— Function: <b>thread-yield [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bthread_002dyield_007d-483"></a></var><br>
<blockquote><p>Yield the processor to other threads. 
</p></blockquote></div>

<h4 class="subsection">12.1.3 Asynchronous Operations</h4>

<p><a name="Function-sb_002dthread_003ainterrupt_002dthread"></a>

</p><div class="defun">
— Function: <b>interrupt-thread [sb-thread]</b><var> thread function<a name="index-g_t_0040sbthread_007binterrupt_002dthread_007d-484"></a></var><br>
<blockquote><p>Interrupt <code>thread</code> and make it run <code>function</code>.

        </p><p>The interrupt is asynchronous, and can occur anywhere with the exception of
sections protected using <code>sb-sys:without-interrupts</code>.

        </p><p><code>function</code> is called with interrupts disabled, under
<code>sb-sys:allow-with-interrupts</code>. Since functions such as <code>grab-mutex</code> may try to
enable interrupts internally, in most cases <code>function</code> should either enter
<code>sb-sys:with-interrupts</code> to allow nested interrupts, or
<code>sb-sys:without-interrupts</code> to prevent them completely.

        </p><p>When a thread receives multiple interrupts, they are executed in the order
they were sent <code>--</code> first in, first out.

        </p><p>This means that a great degree of care is required to use <code>interrupt-thread</code>
safely and sanely in a production environment. The general recommendation is
to limit uses of <code>interrupt-thread</code> for interactive debugging, banning it
entirely from production environments <code>--</code> it is simply exceedingly hard to use
correctly.

        </p><p>With those caveats in mind, what you need to know when using it:

          </p><ul>
<li>If calling <code>function</code> causes a non-local transfer of control (ie. an
   unwind), all normal cleanup forms will be executed.

          <p>However, if the interrupt occurs during cleanup forms of an <code>unwind-protect</code>,
   it is just as if that had happened due to a regular <code>go</code>, <code>throw</code>, or
   <code>return-from:</code> the interrupted cleanup form and those following it in the
   same <code>unwind-protect</code> do not get executed.

          </p><p><code>sbcl</code> tries to keep its own internals asynch-unwind-safe, but this is
   frankly an unreasonable expectation for third party libraries, especially
   given that asynch-unwind-safety does not compose: a function calling
   only asynch-unwind-safe function isn't automatically asynch-unwind-safe.

          </p><p>This means that in order for an asynch unwind to be safe, the entire
   callstack at the point of interruption needs to be asynch-unwind-safe.

          </p></li><li>In addition to asynch-unwind-safety you must consider the issue of
   reentrancy. <code>interrupt-thread</code> can cause function that are never normally
   called recursively to be re-entered during their dynamic contour,
   which may cause them to misbehave. (Consider binding of special variables,
   values of global variables, etc.)

        </li></ul>
        Taken together, these two restrict the "safe" things to do using
<code>interrupt-thread</code> to a fairly minimal set. One useful one <code>--</code> exclusively for
interactive development use is using it to force entry to debugger to inspect
the state of a thread:

     <pre class="lisp">            (interrupt-thread thread #'break)
</pre>
        <p>Short version: be careful out there. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003aterminate_002dthread"></a>

</p><div class="defun">
— Function: <b>terminate-thread [sb-thread]</b><var> thread<a name="index-g_t_0040sbthread_007bterminate_002dthread_007d-485"></a></var><br>
<blockquote><p>Terminate the thread identified by <code>thread</code>, by interrupting it and
causing it to call <code>sb-ext:abort-thread</code> with <code>:allow-exit</code> <code>t</code>.

        </p><p>The unwind caused by <code>terminate-thread</code> is asynchronous, meaning that
eg. thread executing

     </p><pre class="lisp">            (let (foo)
               (unwind-protect
                   (progn
                      (setf foo (get-foo))
                      (work-on-foo foo))
                 (when foo
                   ;; An interrupt occurring inside the cleanup clause
                   ;; will cause cleanups from the current UNWIND-PROTECT
                   ;; to be dropped.
                   (release-foo foo))))
</pre>
        <p>might miss calling <code>release-foo</code> despite <code>get-foo</code> having returned true if
the interrupt occurs inside the cleanup clause, eg. during execution
of <code>release-foo</code>.

        </p><p>Thus, in order to write an asynch unwind safe <code>unwind-protect</code> you need
to use <code>without-interrupts:</code>

     </p><pre class="lisp">            (let (foo)
              (sb-sys:without-interrupts
                (unwind-protect
                    (progn
                      (setf foo (sb-sys:allow-with-interrupts
                                  (get-foo)))
                      (sb-sys:with-local-interrupts
                        (work-on-foo foo)))
                 (when foo
                   (release-foo foo)))))
</pre>
        <p>Since most libraries using <code>unwind-protect</code> do not do this, you should never
assume that unknown code can safely be terminated using <code>terminate-thread</code>. 
</p></blockquote></div>

<h4 class="subsection">12.1.4 Miscellaneous Operations</h4>

<p><a name="Function-sb_002dthread_003asymbol_002dvalue_002din_002dthread"></a>

</p><div class="defun">
— Function: <b>symbol-value-in-thread [sb-thread]</b><var> symbol thread &amp;optional errorp<a name="index-g_t_0040sbthread_007bsymbol_002dvalue_002din_002dthread_007d-486"></a></var><br>
<blockquote><p>Return the local value of <code>symbol</code> in <code>thread</code>, and a secondary value of <code>t</code>
on success.

        </p><p>If the value cannot be retrieved (because the thread has exited or because it
has no local binding for NAME) and <code>errorp</code> is true signals an error of type
<code>symbol-value-in-thread-error</code>; if <code>errorp</code> is false returns a primary value of
<code>nil</code>, and a secondary value of <code>nil</code>.

        </p><p>Can also be used with <code>setf</code> to change the thread-local value of <code>symbol</code>.

        </p><p><code>symbol-value-in-thread</code> is primarily intended as a debugging tool, and not as a
mechanism for inter-thread communication. 
</p></blockquote></div>

<h4 class="subsection">12.1.5 Error Conditions</h4>

<p><a name="Condition-sb_002dthread_003athread_002derror"></a>

</p><div class="defun">
— Condition: <b>thread-error [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bthread_002derror_007d-487"></a></var><br>
<blockquote><p>Class precedence list: <code>thread-error, error, serious-condition, condition, t</code>

        </p><p>Conditions of type <code>thread-error</code> are signalled when thread operations fail. 
The offending thread is initialized by the <code>:thread</code> initialization argument and
read by the function <code>thread-error-thread</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003athread_002derror_002dthread"></a>

</p><div class="defun">
— Function: <b>thread-error-thread [sb-thread]</b><var> condition<a name="index-g_t_0040sbthread_007bthread_002derror_002dthread_007d-488"></a></var><br>
<blockquote><p>Return the offending thread that the <code>thread-error</code> pertains to. 
</p></blockquote></div>

<!-- @include condition-sb-thread-symbol-value-in-thread-error.texinfo -->
   <p><a name="Condition-sb_002dthread_003ainterrupt_002dthread_002derror"></a>

</p><div class="defun">
— Condition: <b>interrupt-thread-error [sb-thread]</b><var><a name="index-g_t_0040sbthread_007binterrupt_002dthread_002derror_007d-489"></a></var><br>
<blockquote><p>Class precedence list: <code>interrupt-thread-error, thread-error, error, serious-condition, condition, t</code>

        </p><p>Signalled when interrupting a thread fails because the thread has already
exited. The offending thread can be accessed using <code>thread-error-thread</code>. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dthread_003ajoin_002dthread_002derror"></a>

</p><div class="defun">
— Condition: <b>join-thread-error [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bjoin_002dthread_002derror_007d-490"></a></var><br>
<blockquote><p>Class precedence list: <code>join-thread-error, thread-error, error, serious-condition, condition, t</code>

        </p><p>Signalled when joining a thread fails due to abnormal exit of the thread
to be joined. The offending thread can be accessed using
<code>thread-error-thread</code>. 
</p></blockquote></div>

<div class="node">
<a name="Special-Variables"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Atomic-Operations">Atomic Operations</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Threading-basics">Threading basics</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.2 Special Variables</h3>

<p>The interaction of special variables with multiple threads is mostly
as one would expect, with behaviour very similar to other
implementations.

     </p><ul>
<li>global special values are visible across all threads;
</li><li>bindings (e.g. using LET) are local to the thread;
</li><li>threads do not inherit dynamic bindings from the parent thread
</li></ul>

   <p>The last point means that

</p><pre class="lisp">     (defparameter *x* 0)
     (let ((*x* 1))
       (sb-thread:make-thread (lambda () (print *x*))))
</pre>
   <p>prints <code>0</code> and not <code>1</code> as of 0.9.6.

</p><div class="node">
<a name="Atomic-Operations"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Mutex-Support">Mutex Support</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Special-Variables">Special Variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.3 Atomic Operations</h3>

<p>Following atomic operations are particularly useful for implementing
lockless algorithms.

   </p><p><a name="Macro-sb_002dext_003aatomic_002ddecf"></a>

</p><div class="defun">
— Macro: <b>atomic-decf [sb-ext]</b><var> place &amp;optional diff<a name="index-g_t_0040sbext_007batomic_002ddecf_007d-491"></a></var><br>
<blockquote><p>Atomically decrements <code>place</code> by <code>diff</code>, and returns the value of <code>place</code> before
the decrement.

        </p><p><code>place</code> must access one of the following:
          </p><ul>
<li>a <code>defstruct</code> slot with declared type <code>(unsigned-byte 64)</code>
   or <code>aref</code> of a <code>(simple-array (unsigned-byte 64) (*))</code>
   The type <code>sb-ext:word</code> can be used for these purposes. 
</li><li><code>car</code> or <code>cdr</code> (respectively <code>first</code> or REST) of a <code>cons</code>. 
</li><li>a variable defined using <code>defglobal</code> with a proclaimed type of <code>fixnum</code>. 
</li></ul>
        Macroexpansion is performed on <code>place</code> before expanding <code>atomic-decf</code>.

        <p>Decrementing is done using modular arithmetic,
which is well-defined over two different domains:
          </p><ul>
<li>For structures and arrays, the operation accepts and produces
   an <code>(unsigned-byte 64)</code>, and <code>diff</code> must be of type <code>(signed-byte 64)</code>. 
   <code>atomic-decf</code> of #x0 by one results in #xFFFFFFFFFFFFFFFF being stored in <code>place</code>. 
</li><li>For other places, the domain is <code>fixnum</code>, and <code>diff</code> must be a <code>fixnum</code>. 
   <code>atomic-decf</code> of #x-4000000000000000 by one results in #x3FFFFFFFFFFFFFFF
   being stored in <code>place</code>.

        </li></ul>
        <code>diff</code> defaults to 1.

        <p><code>experimental:</code> Interface subject to change. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003aatomic_002dincf"></a>

</p><div class="defun">
— Macro: <b>atomic-incf [sb-ext]</b><var> place &amp;optional diff<a name="index-g_t_0040sbext_007batomic_002dincf_007d-492"></a></var><br>
<blockquote><p>Atomically increments <code>place</code> by <code>diff</code>, and returns the value of <code>place</code> before
the increment.

        </p><p><code>place</code> must access one of the following:
          </p><ul>
<li>a <code>defstruct</code> slot with declared type <code>(unsigned-byte 64)</code>
   or <code>aref</code> of a <code>(simple-array (unsigned-byte 64) (*))</code>
   The type <code>sb-ext:word</code> can be used for these purposes. 
</li><li><code>car</code> or <code>cdr</code> (respectively <code>first</code> or REST) of a <code>cons</code>. 
</li><li>a variable defined using <code>defglobal</code> with a proclaimed type of <code>fixnum</code>. 
</li></ul>
        Macroexpansion is performed on <code>place</code> before expanding <code>atomic-incf</code>.

        <p>Incrementing is done using modular arithmetic,
which is well-defined over two different domains:
          </p><ul>
<li>For structures and arrays, the operation accepts and produces
   an <code>(unsigned-byte 64)</code>, and <code>diff</code> must be of type <code>(signed-byte 64)</code>. 
   <code>atomic-incf</code> of #xFFFFFFFFFFFFFFFF by one results in #x0 being stored in <code>place</code>. 
</li><li>For other places, the domain is <code>fixnum</code>, and <code>diff</code> must be a <code>fixnum</code>. 
   <code>atomic-incf</code> of #x3FFFFFFFFFFFFFFF by one results in #x-4000000000000000
   being stored in <code>place</code>.

        </li></ul>
        <code>diff</code> defaults to 1.

        <p><code>experimental:</code> Interface subject to change. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003aatomic_002dpop"></a>

</p><div class="defun">
— Macro: <b>atomic-pop [sb-ext]</b><var> place<a name="index-g_t_0040sbext_007batomic_002dpop_007d-493"></a></var><br>
<blockquote><p>Like <code>pop</code>, but atomic. <code>place</code> may be read multiple times before
the operation completes <code>--</code> the write does not occur until such time
that no other thread modified <code>place</code> between the read and the write.

        </p><p>Works on all CASable places. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003aatomic_002dpush"></a>

</p><div class="defun">
— Macro: <b>atomic-push [sb-ext]</b><var> obj place<a name="index-g_t_0040sbext_007batomic_002dpush_007d-494"></a></var><br>
<blockquote><p>Like <code>push</code>, but atomic. <code>place</code> may be read multiple times before
the operation completes <code>--</code> the write does not occur until such time
that no other thread modified <code>place</code> between the read and the write.

        </p><p>Works on all CASable places. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003aatomic_002dupdate"></a>

</p><div class="defun">
— Macro: <b>atomic-update [sb-ext]</b><var> place update-fn &amp;rest arguments<a name="index-g_t_0040sbext_007batomic_002dupdate_007d-495"></a></var><br>
<blockquote><p>Updates <code>place</code> atomically to the value returned by calling function
designated by <code>update-fn</code> with <code>arguments</code> and the previous value of <code>place</code>.

        </p><p><code>place</code> may be read and <code>update-fn</code> evaluated and called multiple times before the
update succeeds: atomicity in this context means that the value of <code>place</code> did
not change between the time it was read, and the time it was replaced with the
computed value.

        </p><p><code>place</code> can be any place supported by <code>sb-ext:compare-and-swap</code>.

        </p><p>Examples:

     </p><pre class="lisp">            ;;; Conses T to the head of FOO-LIST.
            (defstruct foo list)
            (defvar *foo* (make-foo))
            (atomic-update (foo-list *foo*) #'cons t)
          
            (let ((x (cons :count 0)))
               (mapc #'sb-thread:join-thread
                     (loop repeat 1000
                           collect (sb-thread:make-thread
                                    (lambda ()
                                      (loop repeat 1000
                                            do (atomic-update (cdr x) #'1+)
                                               (sleep 0.00001))))))
               ;; Guaranteed to be (:COUNT . 1000000) -- if you replace
               ;; atomic update with (INCF (CDR X)) above, the result becomes
               ;; unpredictable.
               x)
</pre>
        </blockquote></div>

   <p><a name="Macro-sb_002dext_003acompare_002dand_002dswap"></a>

</p><div class="defun">
— Macro: <b>compare-and-swap [sb-ext]</b><var> place old new<a name="index-g_t_0040sbext_007bcompare_002dand_002dswap_007d-496"></a></var><br>
<blockquote><p>Atomically stores <code>new</code> in <code>place</code> if <code>old</code> matches the current value of <code>place</code>. 
Two values are considered to match if they are <code>eq</code>. Returns the previous value
of <code>place:</code> if the returned value is <code>eq</code> to <code>old</code>, the swap was carried out.

        </p><p><code>place</code> must be an CAS-able place. Built-in CAS-able places are accessor forms
whose <code>car</code> is one of the following:

        </p><p><code>car</code>, <code>cdr</code>, <code>first</code>, <code>rest</code>, <code>svref</code>, <code>symbol-plist</code>, <code>symbol-value</code>, <code>svref</code>, <code>slot-value</code>
 <code>sb-mop:standard-instance-access</code>, <code>sb-mop:funcallable-standard-instance-access</code>,

        </p><p>or the name of a <code>defstruct</code> created accessor for a slot whose declared type is
either <code>fixnum</code> or <code>t</code>. Results are unspecified if the slot has a declared type
other than <code>fixnum</code> or <code>t</code>.

        </p><p>In case of <code>slot-value</code>, if the slot is unbound, <code>slot-unbound</code> is called unless
<code>old</code> is <code>eq</code> to <code>sb-pcl:+slot-unbound+</code> in which case <code>sb-pcl:+slot-unbound+</code> is
returned and <code>new</code> is assigned to the slot. Additionally, the results are
unspecified if there is an applicable method on either
<code>sb-mop:slot-value-using-class</code>, <code>(setf sb-mop:slot-value-using-class)</code>, or
<code>sb-mop:slot-boundp-using-class</code>.

        </p><p>Additionally, the <code>place</code> can be a anything for which a CAS-expansion has been
specified using <code>defcas</code>, <code>define-cas-expander</code>, or for which a CAS-function has
been defined. (See <code>sb-ext:cas</code> for more information.) 
</p></blockquote></div>

<h4 class="unnumberedsubsec">CAS Protocol</h4>

<p>Our <code>compare-and-swap</code> is user-extensible using a protocol
similar to <code>setf</code>, allowing users to add CAS support to new
places via e.g. <code>defcas</code>.

   </p><p>At the same time, new atomic operations can be built on top of CAS
using <code>get-cas-expansion</code>. See <code>atomic-update</code>,
<code>atomic-push</code>, and <code>atomic-pop</code> for examples of how to do
this.

   </p><p><a name="Macro-sb_002dext_003acas"></a>

</p><div class="defun">
— Macro: <b>cas [sb-ext]</b><var> place old new<a name="index-g_t_0040sbext_007bcas_007d-497"></a></var><br>
<blockquote><p>Synonym for <code>compare-and-swap</code>.

        </p><p>Additionally <code>defun</code>, <code>defgeneric</code>, <code>defmethod</code>, <code>flet</code>, and <code>labels</code> can be also used to
define CAS-functions analogously to SETF-functions:

     </p><pre class="lisp">            (defvar *foo* nil)
          
            (defun (cas foo) (old new)
              (cas (symbol-value '*foo*) old new))
</pre>
        <p>First argument of a <code>cas</code> function is the expected old value, and the second
argument of is the new value. Note that the system provides no automatic
atomicity for <code>cas</code> functions, nor can it verify that they are atomic: it is up
to the implementor of a <code>cas</code> function to ensure its atomicity.

        </p><p><code>experimental:</code> Interface subject to change. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003adefine_002dcas_002dexpander"></a>

</p><div class="defun">
— Macro: <b>define-cas-expander [sb-ext]</b><var> accessor lambda-list &amp;body body<a name="index-g_t_0040sbext_007bdefine_002dcas_002dexpander_007d-498"></a></var><br>
<blockquote><p>Analogous to <code>define-setf-expander</code>. Defines a CAS-expansion for <code>accessor</code>. 
<code>body</code> must return six values as specified in <code>get-cas-expansion</code>.

        </p><p>Note that the system provides no automatic atomicity for <code>cas</code> expansion, nor
can it verify that they are atomic: it is up to the implementor of a <code>cas</code>
expansion to ensure its atomicity.

        </p><p><code>experimental:</code> Interface subject to change. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dext_003adefcas"></a>

</p><div class="defun">
— Macro: <b>defcas [sb-ext]</b><var> accessor lambda-list function &amp;optional docstring<a name="index-g_t_0040sbext_007bdefcas_007d-499"></a></var><br>
<blockquote><p>Analogous to short-form <code>defsetf</code>. Defines <code>function</code> as responsible
for compare-and-swap on places accessed using <code>accessor</code>. <code>lambda-list</code>
must correspond to the lambda-list of the accessor.

        </p><p>Note that the system provides no automatic atomicity for <code>cas</code> expansions
resulting from <code>defcas</code>, nor can it verify that they are atomic: it is up to the
user of <code>defcas</code> to ensure that the function specified is atomic.

        </p><p><code>experimental:</code> Interface subject to change. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aget_002dcas_002dexpansion"></a>

</p><div class="defun">
— Function: <b>get-cas-expansion [sb-ext]</b><var> place &amp;optional environment<a name="index-g_t_0040sbext_007bget_002dcas_002dexpansion_007d-500"></a></var><br>
<blockquote><p>Analogous to <code>get-setf-expansion</code>. Returns the following six values:

          </p><ul>
<li>list of temporary variables

          </li><li>list of value-forms whose results those variable must be bound

          </li><li>temporary variable for the old value of <code>place</code>

          </li><li>temporary variable for the new value of <code>place</code>

          </li><li>form using the aforementioned temporaries which performs the
   compare-and-swap operation on <code>place</code>

          </li><li>form using the aforementioned temporaries with which to perform a volatile
   read of <code>place</code>

        </li></ul>
        Example:

     <pre class="lisp">            (get-cas-expansion '(car x))
            ; =&gt; (#:CONS871), (X), #:OLD872, #:NEW873,
            ;    (SB-KERNEL:%COMPARE-AND-SWAP-CAR #:CONS871 #:OLD872 :NEW873).
            ;    (CAR #:CONS871)
          
            (defmacro my-atomic-incf (place &amp;optional (delta 1) &amp;environment env)
              (multiple-value-bind (vars vals old new cas-form read-form)
                  (get-cas-expansion place env)
               (let ((delta-value (gensym "DELTA")))
                 `(let* (,@(mapcar 'list vars vals)
                         (,old ,read-form)
                         (,delta-value ,delta)
                         (,new (+ ,old ,delta-value)))
                    (loop until (eq ,old (setf ,old ,cas-form))
                          do (setf ,new (+ ,old ,delta-value)))
                    ,new))))
</pre>
        <p><code>experimental:</code> Interface subject to change. 
</p></blockquote></div>

<div class="node">
<a name="Mutex-Support"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Semaphores">Semaphores</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Atomic-Operations">Atomic Operations</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.4 Mutex Support</h3>

<p>Mutexes are used for controlling access to a shared resource. One
thread is allowed to hold the mutex, others which attempt to take it
will be made to wait until it's free. Threads are woken in the order
that they go to sleep.

</p><pre class="lisp">     (defpackage :demo (:use "CL" "SB-THREAD" "SB-EXT"))
     
     (in-package :demo)
     
     (defvar *a-mutex* (make-mutex :name "my lock"))
     
     (defun thread-fn ()
       (format t "Thread ~A running ~%" *current-thread*)
       (with-mutex (*a-mutex*)
         (format t "Thread ~A got the lock~%" *current-thread*)
         (sleep (random 5)))
       (format t "Thread ~A dropped lock, dying now~%" *current-thread*))
     
     (make-thread #'thread-fn)
     (make-thread #'thread-fn)
</pre>
   <p><a name="Structure-sb_002dthread_003amutex"></a>

</p><div class="defun">
— Structure: <b>mutex [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bmutex_007d-501"></a></var><br>
<blockquote><p>Class precedence list: <code>mutex, structure-object, t</code>

        </p><p>Mutex type. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dthread_003awith_002dmutex"></a>

</p><div class="defun">
— Macro: <b>with-mutex [sb-thread]</b> (<var>mutex &amp;key wait-p timeout value</var>)<var> &amp;body body<a name="index-g_t_0040sbthread_007bwith_002dmutex_007d-502"></a></var><br>
<blockquote><p>Acquire <code>mutex</code> for the dynamic scope of <code>body</code>. If <code>wait-p</code> is true (the default),
and the <code>mutex</code> is not immediately available, sleep until it is available.

        </p><p>If <code>timeout</code> is given, it specifies a relative timeout, in seconds, on how long
the system should try to acquire the lock in the contested case.

        </p><p>If the mutex isn't acquired successfully due to either <code>wait-p</code> or <code>timeout</code>, the
body is not executed, and <code>with-mutex</code> returns <code>nil</code>.

        </p><p>Otherwise body is executed with the mutex held by current thread, and
<code>with-mutex</code> returns the values of <code>body</code>.

        </p><p>Historically <code>with-mutex</code> also accepted a <code>value</code> argument, which when provided
was used as the new owner of the mutex instead of the current thread. This is
no longer supported: if <code>value</code> is provided, it must be either <code>nil</code> or the
current thread. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dthread_003awith_002drecursive_002dlock"></a>

</p><div class="defun">
— Macro: <b>with-recursive-lock [sb-thread]</b> (<var>mutex &amp;key wait-p timeout</var>)<var> &amp;body body<a name="index-g_t_0040sbthread_007bwith_002drecursive_002dlock_007d-503"></a></var><br>
<blockquote><p>Acquire <code>mutex</code> for the dynamic scope of <code>body</code>.

        </p><p>If <code>wait-p</code> is true (the default), and the <code>mutex</code> is not immediately available or
held by the current thread, sleep until it is available.

        </p><p>If <code>timeout</code> is given, it specifies a relative timeout, in seconds, on how long
the system should try to acquire the lock in the contested case.

        </p><p>If the mutex isn't acquired successfully due to either <code>wait-p</code> or <code>timeout</code>, the
body is not executed, and <code>with-recursive-lock</code> returns <code>nil</code>.

        </p><p>Otherwise body is executed with the mutex held by current thread, and
<code>with-recursive-lock</code> returns the values of <code>body</code>.

        </p><p>Unlike <code>with-mutex</code>, which signals an error on attempt to re-acquire an already
held mutex, <code>with-recursive-lock</code> allows recursive lock attempts to succeed. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amake_002dmutex"></a>

</p><div class="defun">
— Function: <b>make-mutex [sb-thread]</b><var> &amp;key name<a name="index-g_t_0040sbthread_007bmake_002dmutex_007d-504"></a></var><br>
<blockquote><p>Create a mutex. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amutex_002dname"></a>

</p><div class="defun">
— Function: <b>mutex-name [sb-thread]</b><var> instance<a name="index-g_t_0040sbthread_007bmutex_002dname_007d-505"></a></var><br>
<blockquote><p>The name of the mutex. Setfable. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amutex_002downer"></a>

</p><div class="defun">
— Function: <b>mutex-owner [sb-thread]</b><var> mutex<a name="index-g_t_0040sbthread_007bmutex_002downer_007d-506"></a></var><br>
<blockquote><p>Current owner of the mutex, <code>nil</code> if the mutex is free. Naturally,
this is racy by design (another thread may acquire the mutex after
this function returns), it is intended for informative purposes. For
testing whether the current thread is holding a mutex see
<code>holding-mutex-p</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amutex_002dvalue"></a>

</p><div class="defun">
— Function: <b>mutex-value [sb-thread]</b><var> mutex<a name="index-g_t_0040sbthread_007bmutex_002dvalue_007d-507"></a></var><br>
<blockquote><p>Current owner of the mutex, <code>nil</code> if the mutex is free. May return a
stale value, use <code>mutex-owner</code> instead. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003agrab_002dmutex"></a>

</p><div class="defun">
— Function: <b>grab-mutex [sb-thread]</b><var> mutex &amp;key waitp timeout<a name="index-g_t_0040sbthread_007bgrab_002dmutex_007d-508"></a></var><br>
<blockquote><p>Acquire <code>mutex</code> for the current thread. If <code>waitp</code> is true (the default) and
the mutex is not immediately available, sleep until it is available.

        </p><p>If <code>timeout</code> is given, it specifies a relative timeout, in seconds, on how long
<code>grab-mutex</code> should try to acquire the lock in the contested case.

        </p><p>If <code>grab-mutex</code> returns <code>t</code>, the lock acquisition was successful. In case of <code>waitp</code>
being <code>nil</code>, or an expired <code>timeout</code>, <code>grab-mutex</code> may also return <code>nil</code> which denotes
that <code>grab-mutex</code> did -not- acquire the lock.

        </p><p>Notes:

          </p><ul>
<li><code>grab-mutex</code> is not interrupt safe. The correct way to call it is:

          <p>(WITHOUT-INTERRUPTS
        ... 
        (<code>allow-with-interrupts</code> (<code>grab-mutex</code> ...)) 
        ...)

          </p><p><code>without-interrupts</code> is necessary to avoid an interrupt unwinding the call
    while the mutex is in an inconsistent state while <code>allow-with-interrupts</code>
    allows the call to be interrupted from sleep.

          </p></li><li><code>(grab-mutex &lt;mutex&gt; :timeout 0.0) </code>differs from
    <code>(grab-mutex &lt;mutex&gt; :waitp nil) </code>in that the former may signal a
    <code>deadline-timeout</code> if the global deadline was due already on entering
    <code>grab-mutex</code>.

          <p>The exact interplay of <code>grab-mutex</code> and deadlines are reserved to change in
    future versions.

          </p></li><li>It is recommended that you use <code>with-mutex</code> instead of calling <code>grab-mutex</code>
    directly. 
</li></ul>
        <p></p></blockquote></div>

   <p><a name="Function-sb_002dthread_003arelease_002dmutex"></a>

</p><div class="defun">
— Function: <b>release-mutex [sb-thread]</b><var> mutex &amp;key if-not-owner<a name="index-g_t_0040sbthread_007brelease_002dmutex_007d-509"></a></var><br>
<blockquote><p>Release <code>mutex</code> by setting it to <code>nil</code>. Wake up threads waiting for
this mutex.

        </p><p><code>release-mutex</code> is not interrupt safe: interrupts should be disabled
around calls to it.

        </p><p>If the current thread is not the owner of the mutex then it silently
returns without doing anything (if <code>if-not-owner</code> is :PUNT), signals a
<code>warning</code> (if <code>if-not-owner</code> is :WARN), or releases the mutex anyway (if
<code>if-not-owner</code> is :FORCE). 
</p></blockquote></div>

<div class="node">
<a name="Semaphores"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Mutex-Support">Mutex Support</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.5 Semaphores</h3>

<p>Semaphores are among other things useful for keeping track of a
countable resource, e.g. messages in a queue, and sleep when the
resource is exhausted.

   </p><p><a name="Structure-sb_002dthread_003asemaphore"></a>

</p><div class="defun">
— Structure: <b>semaphore [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bsemaphore_007d-510"></a></var><br>
<blockquote><p>Class precedence list: <code>semaphore, structure-object, t</code>

        </p><p>Semaphore type. The fact that a <code>semaphore</code> is a <code>structure-object</code>
should be considered an implementation detail, and may change in the
future. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amake_002dsemaphore"></a>

</p><div class="defun">
— Function: <b>make-semaphore [sb-thread]</b><var> &amp;key name count<a name="index-g_t_0040sbthread_007bmake_002dsemaphore_007d-511"></a></var><br>
<blockquote><p>Create a semaphore with the supplied <code>count</code> and <code>name</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003asignal_002dsemaphore"></a>

</p><div class="defun">
— Function: <b>signal-semaphore [sb-thread]</b><var> semaphore &amp;optional n<a name="index-g_t_0040sbthread_007bsignal_002dsemaphore_007d-512"></a></var><br>
<blockquote><p>Increment the count of <code>semaphore</code> by <code>n</code>. If there are threads waiting
on this semaphore, then <code>n</code> of them is woken up. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003await_002don_002dsemaphore"></a>

</p><div class="defun">
— Function: <b>wait-on-semaphore [sb-thread]</b><var> semaphore &amp;key n timeout notification<a name="index-g_t_0040sbthread_007bwait_002don_002dsemaphore_007d-513"></a></var><br>
<blockquote><p>Decrement the count of <code>semaphore</code> by <code>n</code> if the count would not be negative.

        </p><p>Else blocks until the semaphore can be decremented. Returns the new count of
<code>semaphore</code> on success.

        </p><p>If <code>timeout</code> is given, it is the maximum number of seconds to wait. If the count
cannot be decremented in that time, returns <code>nil</code> without decrementing the
count.

        </p><p>If <code>notification</code> is given, it must be a <code>semaphore-notification</code> object whose
<code>semaphore-notification-status</code> is <code>nil</code>. If <code>wait-on-semaphore</code> succeeds and
decrements the count, the status is set to <code>t</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003atry_002dsemaphore"></a>

</p><div class="defun">
— Function: <b>try-semaphore [sb-thread]</b><var> semaphore &amp;optional n notification<a name="index-g_t_0040sbthread_007btry_002dsemaphore_007d-514"></a></var><br>
<blockquote><p>Try to decrement the count of <code>semaphore</code> by <code>n</code>. If the count were to
become negative, punt and return <code>nil</code>, otherwise return the new count of
<code>semaphore</code>.

        </p><p>If <code>notification</code> is given it must be a semaphore notification object
with <code>semaphore-notification-status</code> of <code>nil</code>. If the count is decremented,
the status is set to <code>t</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003asemaphore_002dcount"></a>

</p><div class="defun">
— Function: <b>semaphore-count [sb-thread]</b><var> instance<a name="index-g_t_0040sbthread_007bsemaphore_002dcount_007d-515"></a></var><br>
<blockquote><p>Returns the current count of the semaphore <code>instance</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003asemaphore_002dname"></a>

</p><div class="defun">
— Function: <b>semaphore-name [sb-thread]</b><var> instance<a name="index-g_t_0040sbthread_007bsemaphore_002dname_007d-516"></a></var><br>
<blockquote><p>The name of the semaphore <code>instance</code>. Setfable. 
</p></blockquote></div>

   <p><a name="Structure-sb_002dthread_003asemaphore_002dnotification"></a>

</p><div class="defun">
— Structure: <b>semaphore-notification [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bsemaphore_002dnotification_007d-517"></a></var><br>
<blockquote><p>Class precedence list: <code>semaphore-notification, structure-object, t</code>

        </p><p>Semaphore notification object. Can be passed to <code>wait-on-semaphore</code> and
<code>try-semaphore</code> as the <code>:notification</code> argument. Consequences are undefined if
multiple threads are using the same notification object in parallel. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amake_002dsemaphore_002dnotification"></a>

</p><div class="defun">
— Function: <b>make-semaphore-notification [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bmake_002dsemaphore_002dnotification_007d-518"></a></var><br>
<blockquote><p>Constructor for <code>semaphore-notification</code> objects. <code>semaphore-notification-status</code>
is initially <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003asemaphore_002dnotification_002dstatus"></a>

</p><div class="defun">
— Function: <b>semaphore-notification-status [sb-thread]</b><var> semaphore-notification<a name="index-g_t_0040sbthread_007bsemaphore_002dnotification_002dstatus_007d-519"></a></var><br>
<blockquote><p>Returns <code>t</code> if a <code>wait-on-semaphore</code> or <code>try-semaphore</code> using
<code>semaphore-notification</code> has succeeded since the notification object was created
or cleared. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003aclear_002dsemaphore_002dnotification"></a>

</p><div class="defun">
— Function: <b>clear-semaphore-notification [sb-thread]</b><var> semaphore-notification<a name="index-g_t_0040sbthread_007bclear_002dsemaphore_002dnotification_007d-520"></a></var><br>
<blockquote><p>Resets the <code>semaphore-notification</code> object for use with another call to
<code>wait-on-semaphore</code> or <code>try-semaphore</code>. 
</p></blockquote></div>

<div class="node">
<a name="Waitqueue/condition-variables"></a>
<a name="Waitqueue_002fcondition-variables"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Barriers">Barriers</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Semaphores">Semaphores</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.6 Waitqueue/condition variables</h3>

<p>These are based on the POSIX condition variable design, hence the
annoyingly CL-conflicting name. For use when you want to check a
condition and sleep until it's true. For example: you have a shared
queue, a writer process checking “queue is empty” and one or more
readers that need to know when “queue is not empty”. It sounds
simple, but is astonishingly easy to deadlock if another process runs
when you weren't expecting it to.

   </p><p>There are three components:

     </p><ul>
<li>the condition itself (not represented in code)

     </li><li>the condition variable (a.k.a. waitqueue) which proxies for it

     </li><li>a lock to hold while testing the condition
</li></ul>

   <p>Important stuff to be aware of:

     </p><ul>
<li>when calling condition-wait, you must hold the mutex. condition-wait
will drop the mutex while it waits, and obtain it again before
returning for whatever reason;

     </li><li>likewise, you must be holding the mutex around calls to
condition-notify;

     </li><li>a process may return from condition-wait in several circumstances: it
is not guaranteed that the underlying condition has become true. You
must check that the resource is ready for whatever you want to do to
it.

   </li></ul>

<pre class="lisp">     (defvar *buffer-queue* (make-waitqueue))
     (defvar *buffer-lock* (make-mutex :name "buffer lock"))
     
     (defvar *buffer* (list nil))
     
     (defun reader ()
       (with-mutex (*buffer-lock*)
         (loop
          (condition-wait *buffer-queue* *buffer-lock*)
          (loop
           (unless *buffer* (return))
           (let ((head (car *buffer*)))
             (setf *buffer* (cdr *buffer*))
             (format t "reader ~A woke, read ~A~%"
                     *current-thread* head))))))
     
     (defun writer ()
       (loop
        (sleep (random 5))
        (with-mutex (*buffer-lock*)
          (let ((el (intern
                     (string (code-char
                              (+ (char-code #\A) (random 26)))))))
            (setf *buffer* (cons el *buffer*)))
          (condition-notify *buffer-queue*))))
     
     (make-thread #'writer)
     (make-thread #'reader)
     (make-thread #'reader)
</pre>
   <p><a name="Structure-sb_002dthread_003awaitqueue"></a>

</p><div class="defun">
— Structure: <b>waitqueue [sb-thread]</b><var><a name="index-g_t_0040sbthread_007bwaitqueue_007d-521"></a></var><br>
<blockquote><p>Class precedence list: <code>waitqueue, structure-object, t</code>

        </p><p>Waitqueue type. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003amake_002dwaitqueue"></a>

</p><div class="defun">
— Function: <b>make-waitqueue [sb-thread]</b><var> &amp;key name<a name="index-g_t_0040sbthread_007bmake_002dwaitqueue_007d-522"></a></var><br>
<blockquote><p>Create a waitqueue. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003awaitqueue_002dname"></a>

</p><div class="defun">
— Function: <b>waitqueue-name [sb-thread]</b><var> instance<a name="index-g_t_0040sbthread_007bwaitqueue_002dname_007d-523"></a></var><br>
<blockquote><p>The name of the waitqueue. Setfable. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003acondition_002dwait"></a>

</p><div class="defun">
— Function: <b>condition-wait [sb-thread]</b><var> queue mutex &amp;key timeout<a name="index-g_t_0040sbthread_007bcondition_002dwait_007d-524"></a></var><br>
<blockquote><p>Atomically release <code>mutex</code> and start waiting on <code>queue</code> until another thread
wakes us up using either <code>condition-notify</code> or <code>condition-broadcast</code> on
<code>queue</code>, at which point we re-acquire <code>mutex</code> and return <code>t</code>.

        </p><p>Spurious wakeups are possible.

        </p><p>If <code>timeout</code> is given, it is the maximum number of seconds to wait,
including both waiting for the wakeup and the time to re-acquire
<code>mutex</code>. When neither a wakeup nor a re-acquisition occurs within the
given time, returns <code>nil</code> without re-acquiring <code>mutex</code>.

        </p><p>If <code>condition-wait</code> unwinds, it may do so with or without <code>mutex</code> being
held.

        </p><p>Important: Since <code>condition-wait</code> may return without <code>condition-notify</code> or
<code>condition-broadcast</code> having occurred, the correct way to write code
that uses <code>condition-wait</code> is to loop around the call, checking the
associated data:

     </p><pre class="lisp">            (defvar *data* nil)
            (defvar *queue* (make-waitqueue))
            (defvar *lock* (make-mutex))
          
            ;; Consumer
            (defun pop-data (&amp;optional timeout)
              (with-mutex (*lock*)
                (loop until *data*
                      do (or (condition-wait *queue* *lock* :timeout timeout)
                             ;; Lock not held, must unwind without touching *data*.
                             (return-from pop-data nil)))
                (pop *data*)))
          
            ;; Producer
            (defun push-data (data)
              (with-mutex (*lock*)
                (push data *data*)
                (condition-notify *queue*)))
</pre>
        </blockquote></div>

   <p><a name="Function-sb_002dthread_003acondition_002dnotify"></a>

</p><div class="defun">
— Function: <b>condition-notify [sb-thread]</b><var> queue &amp;optional n<a name="index-g_t_0040sbthread_007bcondition_002dnotify_007d-525"></a></var><br>
<blockquote><p>Notify <code>n</code> threads waiting on <code>queue</code>.

        </p><p><code>important:</code> The same mutex that is used in the corresponding <code>condition-wait</code>
must be held by this thread during this call. 
</p></blockquote></div>

   <p><a name="Function-sb_002dthread_003acondition_002dbroadcast"></a>

</p><div class="defun">
— Function: <b>condition-broadcast [sb-thread]</b><var> queue<a name="index-g_t_0040sbthread_007bcondition_002dbroadcast_007d-526"></a></var><br>
<blockquote><p>Notify all threads waiting on <code>queue</code>.

        </p><p><code>important:</code> The same mutex that is used in the corresponding <code>condition-wait</code>
must be held by this thread during this call. 
</p></blockquote></div>

<div class="node">
<a name="Barriers"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Sessions_002fDebugging">Sessions/Debugging</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.7 Barriers</h3>

<p>These are based on the Linux kernel barrier design, which is in turn
based on the Alpha CPU memory model. They are presently implemented
for x86, x86-64, PPC, and ARM64 systems, and behave as compiler
barriers on all other CPUs.

   </p><p>In addition to explicit use of the <code>sb-thread:barrier</code> macro, the
following functions and macros also serve as <code>:memory</code> barriers:

     </p><ul>
<li><code>sb-ext:atomic-decf</code>, <code>sb-ext:atomic-incf</code>, <code>sb-ext:atomic-push</code>,
and <code>sb-ext:atomic-pop</code>. 
</li><li><code>sb-ext:compare-and-swap</code>. 
</li><li><code>sb-thread:grab-mutex</code>, <code>sb-thread:release-mutex</code>,
<code>sb-thread:with-mutex</code> and <code>sb-thread:with-recursive-lock</code>. 
</li><li><code>sb-thread:signal-semaphore</code>, <code>sb-thread:try-semaphore</code> and
<code>sb-thread:wait-on-semaphore</code>. 
</li><li><code>sb-thread:condition-wait</code>, <code>sb-thread:condition-notify</code> and
<code>sb-thread:condition-broadcast</code>. 
</li></ul>

   <p><a name="Macro-sb_002dthread_003abarrier"></a>

</p><div class="defun">
— Macro: <b>barrier [sb-thread]</b> (<var>kind</var>)<var> &amp;body forms<a name="index-g_t_0040sbthread_007bbarrier_007d-527"></a></var><br>
<blockquote><p>Insert a barrier in the code stream, preventing some sort of
reordering.

        </p><p><code>kind</code> should be one of:

          </p><dl>
<dt><code>:compiler</code></dt><dd>    Prevent the compiler from reordering memory access across the
    barrier.

          <br></dd><dt><code>:memory</code></dt><dd>    Prevent the cpu from reordering any memory access across the
    barrier.

          <br></dd><dt><code>:read</code></dt><dd>    Prevent the cpu from reordering any read access across the
    barrier.

          <br></dd><dt><code>:write</code></dt><dd>    Prevent the cpu from reordering any write access across the
    barrier.

          <br></dd><dt><code>:data-dependency</code></dt><dd>    Prevent the cpu from reordering dependent memory reads across the
    barrier (requiring reads before the barrier to complete before any
    reads after the barrier that depend on them).  This is a weaker
    form of the <code>:read</code> barrier.

        </dd></dl>

        <p><code>forms</code> is an implicit <code>progn</code>, evaluated before the barrier.  <code>barrier</code>
returns the values of the last form in <code>forms</code>.

        </p><p>The file "memory-barriers.txt" in the Linux kernel documentation is
highly recommended reading for anyone programming at this level. 
</p></blockquote></div>

<div class="node">
<a name="Sessions/Debugging"></a>
<a name="Sessions_002fDebugging"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Foreign-threads">Foreign threads</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Barriers">Barriers</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.8 Sessions/Debugging</h3>

<p>If the user has multiple views onto the same Lisp image (for example,
using multiple terminals, or a windowing system, or network access)
they are typically set up as multiple <dfn>sessions</dfn> such that each
view has its own collection of foreground/background/stopped threads. 
A thread which wishes to create a new session can use
<code>sb-thread:with-new-session</code> to remove itself from the current
session (which it shares with its parent and siblings) and create a
fresh one. 
# See also <code>sb-thread:make-listener-thread</code>.

   </p><p>Within a single session, threads arbitrate between themselves for the
user's attention.  A thread may be in one of three notional states:
foreground, background, or stopped.  When a background process
attempts to print a repl prompt or to enter the debugger, it will stop
and print a message saying that it has stopped.  The user at his
leisure may switch to that thread to find out what it needs.  If a
background thread enters the debugger, selecting any restart will put
it back into the background before it resumes.  Arbitration for the
input stream is managed by calls to <code>sb-thread:get-foreground</code>
(which may block) and <code>sb-thread:release-foreground</code>.

</p><div class="node">
<a name="Foreign-threads"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Implementation-_0028Linux-x86_002fx86_002d64_0029">Implementation (Linux x86/x86-64)</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Sessions_002fDebugging">Sessions/Debugging</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.9 Foreign threads</h3>

<p>Direct calls to <code>pthread_create</code> (instead of <code>MAKE-THREAD</code>)
create threads that SBCL is not aware of, these are called foreign
threads. Currently, it is not possible to run Lisp code in such
threads. This means that the Lisp side signal handlers cannot work. 
The best solution is to start foreign threads with signals blocked,
but since third party libraries may create threads, it is not always
feasible to do so. As a workaround, upon receiving a signal in a
foreign thread, SBCL changes the thread's sigmask to block all signals
that it wants to handle and resends the signal to the current process
which should land in a thread that does not block it, that is, a Lisp
thread.

   </p><p>The resignalling trick cannot work for synchronously triggered signals
(SIGSEGV and co), take care not to trigger any. Resignalling for
synchronously triggered signals in foreign threads is subject to
<code>--lose-on-corruption</code>, see <a href="#Runtime-Options">Runtime Options</a>.

</p><div class="node">
<a name="Implementation-(Linux-x86/x86-64)"></a>
<a name="Implementation-_0028Linux-x86_002fx86_002d64_0029"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Foreign-threads">Foreign threads</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Threading">Threading</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">12.10 Implementation (Linux x86/x86-64)</h3>

<p>Threading is implemented using pthreads and some Linux specific bits
like futexes.

   </p><p>On x86 the per-thread local bindings for special variables is achieved
using the %fs segment register to point to a per-thread storage area. 
This may cause interesting results if you link to foreign code that
expects threading or creates new threads, and the thread library in
question uses %fs in an incompatible way. On x86-64 the r12 register
has a similar role.

   </p><p>Queues require the <code>sys_futex()</code> system call to be available:
this is the reason for the NPTL requirement.  We test at runtime that
this system call exists.

   </p><p>Garbage collection is done with the existing Conservative Generational
GC.  Allocation is done in small (typically 8k) regions: each thread
has its own region so this involves no stopping. However, when a
region fills, a lock must be obtained while another is allocated, and
when a collection is required, all processes are stopped.  This is
achieved by sending them signals, which may make for interesting
behaviour if they are interrupted in system calls.  The streams
interface is believed to handle the required system call restarting
correctly, but this may be a consideration when making other blocking
calls e.g. from foreign library code.

   </p><p>Large amounts of the SBCL library have not been inspected for
thread-safety.  Some of the obviously unsafe areas have large locks
around them, so compilation and fasl loading, for example, cannot be
parallelized.  Work is ongoing in this area.

   </p><p>A new thread by default is created in the same POSIX process group and
session as the thread it was created by.  This has an impact on
keyboard interrupt handling: pressing your terminal's intr key
(typically <kbd>Control-C</kbd>) will interrupt all processes in the
foreground process group, including Lisp threads that SBCL considers
to be notionally `background'.  This is undesirable, so background
threads are set to ignore the SIGINT signal.

   </p><p><code>sb-thread:make-listener-thread</code> in addition to creating a new
Lisp session makes a new POSIX session, so that pressing
<kbd>Control-C</kbd> in one window will not interrupt another listener -
this has been found to be embarrassing.

</p><div class="node">
<a name="Timers"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Networking">Networking</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Threading">Threading</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">13 Timers</h2>

<p>SBCL supports a system-wide event scheduler implemented on top of
<code>setitimer</code> that also works with threads but does not require a
separate scheduler thread.

   </p><p>The following example schedules a timer that writes “Hello, word” after
two seconds.

</p><pre class="lisp">     (schedule-timer (make-timer (lambda ()
                                   (write-line "Hello, world")
                                   (force-output)))
                     2)
</pre>
   <p>It should be noted that writing timer functions requires special care,
as the dynamic environment in which they run is unpredictable: dynamic
variable bindings, locks held, etc, all depend on whatever code was
running when the timer fired. The following example should serve as
a cautionary tale:

</p><pre class="lisp">     (defvar *foo* nil)
     
     (defun show-foo ()
       (format t "~&amp;foo=~S~%" *foo*)
       (force-output t))
     
     (defun demo ()
       (schedule-timer (make-timer #'show-foo) 0.5)
       (schedule-timer (make-timer #'show-foo) 1.5)
       (let ((*foo* t))
         (sleep 1.0))
       (let ((*foo* :surprise!))
         (sleep 2.0)))
</pre>
   <h3 class="section">13.1 Timer Dictionary</h3>

<p><a name="Structure-sb_002dext_003atimer"></a>

</p><div class="defun">
— Structure: <b>timer [sb-ext]</b><var><a name="index-g_t_0040sbext_007btimer_007d-528"></a></var><br>
<blockquote><p>Class precedence list: <code>timer, structure-object, t</code>

        </p><p>Timer type. Do not rely on timers being structs as it may change in
future versions. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003amake_002dtimer"></a>

</p><div class="defun">
— Function: <b>make-timer [sb-ext]</b><var> function &amp;key name thread<a name="index-g_t_0040sbext_007bmake_002dtimer_007d-529"></a></var><br>
<blockquote><p>Create a timer that runs <code>function</code> when triggered.

        </p><p>If a <code>thread</code> is supplied, <code>function</code> is run in that thread. If <code>thread</code> is
<code>t</code>, a new thread is created for <code>function</code> each time the timer is
triggered. If <code>thread</code> is <code>nil</code>, <code>function</code> is run in an unspecified thread.

        </p><p>When <code>thread</code> is not <code>t</code>, <code>interrupt-thread</code> is used to run <code>function</code> and the
ordering guarantees of <code>interrupt-thread</code> apply. In that case, <code>function</code>
runs with interrupts disabled but <code>with-interrupts</code> is allowed. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003atimer_002dname"></a>

</p><div class="defun">
— Function: <b>timer-name [sb-ext]</b><var> timer<a name="index-g_t_0040sbext_007btimer_002dname_007d-530"></a></var><br>
<blockquote><p>Return the name of <code>timer</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003atimer_002dscheduled_002dp"></a>

</p><div class="defun">
— Function: <b>timer-scheduled-p [sb-ext]</b><var> timer &amp;key delta<a name="index-g_t_0040sbext_007btimer_002dscheduled_002dp_007d-531"></a></var><br>
<blockquote><p>See if <code>timer</code> will still need to be triggered after <code>delta</code> seconds
from now. For timers with a repeat interval it returns true. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aschedule_002dtimer"></a>

</p><div class="defun">
— Function: <b>schedule-timer [sb-ext]</b><var> timer time &amp;key repeat-interval absolute-p catch-up<a name="index-g_t_0040sbext_007bschedule_002dtimer_007d-532"></a></var><br>
<blockquote><p>Schedule <code>timer</code> to be triggered at <code>time</code>. If <code>absolute-p</code> then <code>time</code> is
universal time, but non-integral values are also allowed, else <code>time</code> is
measured as the number of seconds from the current time.

        </p><p>If <code>repeat-interval</code> is given, <code>timer</code> is automatically rescheduled upon
expiry.

        </p><p>If <code>repeat-interval</code> is non-NIL, the Boolean <code>catch-up</code> controls whether
<code>timer</code> will "catch up" by repeatedly calling its function without
delay in case calls are missed because of a clock discontinuity such
as a suspend and resume cycle of the computer. The default is <code>nil</code>,
i.e. do not catch up. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003aunschedule_002dtimer"></a>

</p><div class="defun">
— Function: <b>unschedule-timer [sb-ext]</b><var> timer<a name="index-g_t_0040sbext_007bunschedule_002dtimer_007d-533"></a></var><br>
<blockquote><p>Cancel <code>timer</code>. Once this function returns it is guaranteed that
<code>timer</code> shall not be triggered again and there are no unfinished
triggers. 
</p></blockquote></div>

   <p><a name="Function-sb_002dext_003alist_002dall_002dtimers"></a>

</p><div class="defun">
— Function: <b>list-all-timers [sb-ext]</b><var><a name="index-g_t_0040sbext_007blist_002dall_002dtimers_007d-534"></a></var><br>
<blockquote><p>Return a list of all timers in the system. 
</p></blockquote></div>

<div class="node">
<a name="Networking"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Profiling">Profiling</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Timers">Timers</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">14 Networking</h2>

<p><a name="index-Sockets_002c-Networking-535"></a>
The <code>sb-bsd-sockets</code> module provides a thinly disguised BSD
socket API for SBCL. Ideas have been stolen from the BSD socket API
for C and Graham Barr's IO::Socket classes for Perl.

   </p><p>Sockets are represented as CLOS objects, and the API naming
conventions attempt to balance between the BSD names and good lisp style.

</p><ul class="menu">
<li><a accesskey="1" href="#Sockets-Overview">Sockets Overview</a>
</li><li><a accesskey="2" href="#General-Sockets">General Sockets</a>:       Methods applicable to all sockets
</li><li><a accesskey="3" href="#Socket-Options">Socket Options</a>
</li><li><a accesskey="4" href="#INET-Domain-Sockets">INET Domain Sockets</a>
</li><li><a accesskey="5" href="#Local-_0028Unix_0029-Domain-Sockets">Local (Unix) Domain Sockets</a>
</li><li><a accesskey="6" href="#Name-Service">Name Service</a>
</li></ul>

<div class="node">
<a name="Sockets-Overview"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#General-Sockets">General Sockets</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Networking">Networking</a>

</div>

<h3 class="section">14.1 Sockets Overview</h3>

<p>Most of the functions are modelled on the BSD socket API.  BSD sockets
are widely supported, portably <em>(“portable” by Unix standards, at least)</em>
available on a variety of systems, and documented.  There are some
differences in approach where we have taken advantage of some of the
more useful features of Common Lisp - briefly:

     </p><ul>
<li>Where the C API would typically return -1 and set <code>errno</code>,
<code>sb-bsd-sockets</code> signals an error. All the errors are subclasses
of <code>sb-bsd-sockets:socket-condition</code> and generally correspond one
for one with possible <code>errno</code> values.

     </li><li>We use multiple return values in many places where the C API would use
pass-by-reference values.

     </li><li>We can often avoid supplying an explicit <em>length</em> argument to
functions because we already know how long the argument is.

     </li><li>IP addresses and ports are represented in slightly friendlier fashion
than "network-endian integers".

   </li></ul>

<div class="node">
<a name="General-Sockets"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Socket-Options">Socket Options</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Sockets-Overview">Sockets Overview</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Networking">Networking</a>

</div>

<h3 class="section">14.2 General Sockets</h3>

<p><a name="Class-sb_002dbsd_002dsockets_003asocket"></a>

</p><div class="defun">
— Class: <b>socket [sb-bsd-sockets]</b><var><a name="index-g_t_0040sbbsdsockets_007bsocket_007d-536"></a></var><br>
<blockquote><p>Class precedence list: <code>socket, standard-object, t</code>

        </p><p>Slots:
          </p><ul>
<li><code>protocol</code> — initarg: <code>:protocol<!-- /@w --></code>; reader: <code>sb-bsd-sockets:socket-protocol<!-- /@w --></code>

          <p>Protocol used by the socket. If a
keyword, the symbol-name of the keyword will be passed to
<code>get-protocol-by-name</code> downcased, and the returned value used as
protocol. Other values are used as-is. 
</p></li><li><code>type</code> — initarg: <code>:type<!-- /@w --></code>; reader: <code>sb-bsd-sockets:socket-type<!-- /@w --></code>

          <p>Type of the socket: <code>:stream</code> or <code>:datagram</code>. 
</p></li></ul>

        <p>Common superclass of all sockets, not meant to be
directly instantiated. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dbind"></a>

</p><div class="defun">
— Generic Function: <b>socket-bind [sb-bsd-sockets]</b><var> socket &amp;rest address<a name="index-g_t_0040sbbsdsockets_007bsocket_002dbind_007d-537"></a></var><br>
<blockquote><p>Bind <code>socket</code> to <code>address</code>, which may vary according to socket family. 
For the <code>inet</code> family, pass <code>address</code> and <code>port</code> as two arguments; for <code>file</code>
address family sockets, pass the filename string.  See also bind(2)
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002daccept"></a>

</p><div class="defun">
— Generic Function: <b>socket-accept [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsocket_002daccept_007d-538"></a></var><br>
<blockquote><p>Perform the accept(2) call, returning a newly-created connected
socket and the peer address as multiple values
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dconnect"></a>

</p><div class="defun">
— Generic Function: <b>socket-connect [sb-bsd-sockets]</b><var> socket &amp;rest address<a name="index-g_t_0040sbbsdsockets_007bsocket_002dconnect_007d-539"></a></var><br>
<blockquote><p>Perform the connect(2) call to connect <code>socket</code> to a remote <code>peer</code>. 
No useful return value. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dpeername"></a>

</p><div class="defun">
— Generic Function: <b>socket-peername [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsocket_002dpeername_007d-540"></a></var><br>
<blockquote><p>Return SOCKET's peer; depending on the address family this may
return multiple values
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dname"></a>

</p><div class="defun">
— Generic Function: <b>socket-name [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsocket_002dname_007d-541"></a></var><br>
<blockquote><p>Return the address (as vector of bytes) and port that <code>socket</code> is
bound to, as multiple values. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dreceive"></a>

</p><div class="defun">
— Generic Function: <b>socket-receive [sb-bsd-sockets]</b><var> socket buffer length &amp;key oob peek waitall dontwait element-type<a name="index-g_t_0040sbbsdsockets_007bsocket_002dreceive_007d-542"></a></var><br>
<blockquote><p>Read <code>length</code> octets from <code>socket</code> into <code>buffer</code> (or a freshly-consed
buffer if NIL), using recvfrom(2). If <code>length</code> is <code>nil</code>, the length of
<code>buffer</code> is used, so at least one of these two arguments must be
non-NIL. If <code>buffer</code> is supplied, it had better be of an element type
one octet wide. Returns the buffer, its length, and the address of the
peer that sent it, as multiple values. On datagram sockets, sets
MSG_TRUNC so that the actual packet length is returned even if the
buffer was too small. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dsend"></a>

</p><div class="defun">
— Generic Function: <b>socket-send [sb-bsd-sockets]</b><var> socket buffer length &amp;key address external-format oob eor dontroute dontwait nosignal confirm more<a name="index-g_t_0040sbbsdsockets_007bsocket_002dsend_007d-543"></a></var><br>
<blockquote><p>Send <code>length</code> octets from <code>buffer</code> into <code>socket</code>, using sendto(2). If
<code>buffer</code> is a string, it will converted to octets according to
<code>external-format</code>. If <code>length</code> is <code>nil</code>, the length of the octet buffer is
used. The format of <code>address</code> depends on the socket type (for example
for <code>inet</code> domain sockets it would be a list of an <code>ip</code> address and a
port). If no socket address is provided, send(2) will be called
instead. Returns the number of octets written. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dlisten"></a>

</p><div class="defun">
— Generic Function: <b>socket-listen [sb-bsd-sockets]</b><var> socket backlog<a name="index-g_t_0040sbbsdsockets_007bsocket_002dlisten_007d-544"></a></var><br>
<blockquote><p>Mark <code>socket</code> as willing to accept incoming connections.  The
integer <code>backlog</code> defines the maximum length that the queue of pending
connections may grow to before new connection attempts are refused. 
See also listen(2)
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dopen_002dp"></a>

</p><div class="defun">
— Generic Function: <b>socket-open-p [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsocket_002dopen_002dp_007d-545"></a></var><br>
<blockquote><p>Return true if <code>socket</code> is open; otherwise, return false. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dclose"></a>

</p><div class="defun">
— Generic Function: <b>socket-close [sb-bsd-sockets]</b><var> socket &amp;key abort<a name="index-g_t_0040sbbsdsockets_007bsocket_002dclose_007d-546"></a></var><br>
<blockquote><p>Close <code>socket</code>, unless it was already closed.

        </p><p>If <code>socket-make-stream</code> has been called, calls <code>close</code> using <code>abort</code> on that
stream.  Otherwise closes the socket file descriptor using
close(2). 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dshutdown"></a>

</p><div class="defun">
— Generic Function: <b>socket-shutdown [sb-bsd-sockets]</b><var> socket &amp;key direction<a name="index-g_t_0040sbbsdsockets_007bsocket_002dshutdown_007d-547"></a></var><br>
<blockquote><p>Indicate that no communication in <code>direction</code> will be performed on
<code>socket</code>.

        </p><p><code>direction</code> has to be one of <code>:input</code>, <code>:output</code> or <code>:io</code>.

        </p><p>After a shutdown, no input and/or output of the indicated <code>direction</code>
can be performed on <code>socket</code>. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003asocket_002dmake_002dstream"></a>

</p><div class="defun">
— Generic Function: <b>socket-make-stream [sb-bsd-sockets]</b><var> socket &amp;key input output element-type external-format buffering timeout auto-close serve-events<a name="index-g_t_0040sbbsdsockets_007bsocket_002dmake_002dstream_007d-548"></a></var><br>
<blockquote><p>Find or create a <code>stream</code> that can be used for <code>io</code> on <code>socket</code> (which
must be connected).  Specify whether the stream is for <code>input</code>, <code>output</code>,
or both (it is an error to specify neither).

        </p><p><code>element-type</code> and <code>external-format</code> are as per <code>open</code>.

        </p><p><code>timeout</code> specifies a read timeout for the stream. 
</p></blockquote></div>
   <a name="Method-sb_002dbsd_002dsockets_003asocket_002dmake_002dstream-_0028_0028socket-socket_0029-_0026key-input-output-_0028element_002dtype-_0027character_0029-_0028buffering-full_0029-_0028external_002dformat-default_0029-timeout-auto_002dclose-serve_002devents_0029"></a>

<div class="defun">
— Method: <b>socket-make-stream [sb-bsd-sockets]</b> (<var>socket socket</var>)<var> &amp;key input output </var>(<var>element-type </var>(<var>quote character</var>)) (<var>buffering full</var>) (<var>external-format default</var>)<var> timeout auto-close serve-events<a name="index-g_t_0040sbbsdsockets_007bsocket_002dmake_002dstream_007d-549"></a></var><br>
<blockquote><p>Default method for <code>socket</code> objects.

        </p><p><code>element-type</code> defaults to <code>character</code>, to construct a bivalent stream,
capable of both binary and character <code>io</code> use <code>:default</code>.

        </p><p>Acceptable values for <code>buffering</code> are <code>:full</code>, <code>:line</code> and <code>:none</code>, default
is <code>:full</code>, ie. output is buffered till it is explicitly flushed using
<code>close</code> or <code>finish-output</code>. (<code>force-output</code> forces some output to be
flushed: to ensure all buffered output is flused use <code>finish-output</code>.)

        </p><p>Streams have no <code>timeout</code> by default. If one is provided, it is the
number of seconds the system will at most wait for input to appear on
the socket stream when trying to read from it.

        </p><p>If <code>auto-close</code> is true, the underlying <code>os</code> socket is automatically
closed after the stream and the socket have been garbage collected. 
Default is false.

        </p><p>If <code>serve-events</code> is true, blocking <code>io</code> on the socket will dispatch to
the recursive event loop. Default is false.

        </p><p>The stream for <code>socket</code> will be cached, and a second invocation of this
method will return the same stream. This may lead to oddities if this
function is invoked with inconsistent arguments (e.g., one might
request an input stream and get an output stream in response). 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asocket_002derror"></a>

</p><div class="defun">
— Function: <b>socket-error [sb-bsd-sockets]</b><var> where &amp;optional errno<a name="index-g_t_0040sbbsdsockets_007bsocket_002derror_007d-550"></a></var><br>
        </div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003anon_002dblocking_002dmode"></a>

</p><div class="defun">
— Generic Function: <b>non-blocking-mode [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bnon_002dblocking_002dmode_007d-551"></a></var><br>
<blockquote><p>Is <code>socket</code> in non-blocking mode? 
</p></blockquote></div>

<div class="node">
<a name="Socket-Options"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#INET-Domain-Sockets">INET Domain Sockets</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#General-Sockets">General Sockets</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Networking">Networking</a>

</div>

<h3 class="section">14.3 Socket Options</h3>

<p>A subset of socket options are supported, using a fairly general
framework which should make it simple to add more as required - see
<samp><span class="file">SYS:CONTRIB;SB-BSD-SOCKETS:SOCKOPT.LISP</span></samp> for details. The name
mapping from C is fairly straightforward: <code>SO_RCVLOWAT</code> becomes
<code>sockopt-receive-low-water</code> and <code>(setf
sockopt-receive-low-water)</code>.

   </p><p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002dreuse_002daddress"></a>

</p><div class="defun">
— Function: <b>sockopt-reuse-address [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002dreuse_002daddress_007d-552"></a></var><br>
<blockquote><p>Return the value of the <code>so-reuseaddr</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002dkeep_002dalive"></a>

</p><div class="defun">
— Function: <b>sockopt-keep-alive [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002dkeep_002dalive_007d-553"></a></var><br>
<blockquote><p>Return the value of the <code>so-keepalive</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002doob_002dinline"></a>

</p><div class="defun">
— Function: <b>sockopt-oob-inline [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002doob_002dinline_007d-554"></a></var><br>
<blockquote><p>Return the value of the <code>so-oobinline</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002dbsd_002dcompatible"></a>

</p><div class="defun">
— Function: <b>sockopt-bsd-compatible [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002dbsd_002dcompatible_007d-555"></a></var><br>
<blockquote><p>Return the value of the <code>so-bsdcompat</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. Available only on Linux. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002dpass_002dcredentials"></a>

</p><div class="defun">
— Function: <b>sockopt-pass-credentials [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002dpass_002dcredentials_007d-556"></a></var><br>
<blockquote><p>Return the value of the <code>so-passcred</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. Available only on Linux. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002ddebug"></a>

</p><div class="defun">
— Function: <b>sockopt-debug [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002ddebug_007d-557"></a></var><br>
<blockquote><p>Return the value of the <code>so-debug</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002ddont_002droute"></a>

</p><div class="defun">
— Function: <b>sockopt-dont-route [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002ddont_002droute_007d-558"></a></var><br>
<blockquote><p>Return the value of the <code>so-dontroute</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002dbroadcast"></a>

</p><div class="defun">
— Function: <b>sockopt-broadcast [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002dbroadcast_007d-559"></a></var><br>
<blockquote><p>Return the value of the <code>so-broadcast</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003asockopt_002dtcp_002dnodelay"></a>

</p><div class="defun">
— Function: <b>sockopt-tcp-nodelay [sb-bsd-sockets]</b><var> socket<a name="index-g_t_0040sbbsdsockets_007bsockopt_002dtcp_002dnodelay_007d-560"></a></var><br>
<blockquote><p>Return the value of the <code>tcp-nodelay</code> socket option for <code>socket</code>. This can also be
updated with <code>setf</code>. 
</p></blockquote></div>

<div class="node">
<a name="INET-Domain-Sockets"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Local-_0028Unix_0029-Domain-Sockets">Local (Unix) Domain Sockets</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Socket-Options">Socket Options</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Networking">Networking</a>

</div>

<h3 class="section">14.4 INET Domain Sockets</h3>

<p>The TCP and UDP sockets that you know and love. Some representation
issues:

     </p><ul>
<li>IPv4 Internet addresses are represented by vectors of
<code>(unsigned-byte 8)</code> - viz. <code>#(127 0 0 1)</code>. Ports are just
integers: 6010. No conversion between network- and host-order data is
needed from the user of this package.

     </li><li>IPv6 Internet addresses are represented by vectors of 16
<code>(unsigned-byte 8)</code> - viz. <code>#(0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
1)</code>. Ports are just integers. As for IPv4 addresses, no conversion
between network- and host-order data is needed from the user of this
package.

     </li><li>Socket addresses are represented by the two values for address and port,
so for example, <code>(socket-connect socket #(192 168 1 1) 80)</code> for
IPv4 and <code>(socket-connect socket #(0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1)
80)</code> for IPv6.

   </li></ul>

   <p><a name="Class-sb_002dbsd_002dsockets_003ainet_002dsocket"></a>

</p><div class="defun">
— Class: <b>inet-socket [sb-bsd-sockets]</b><var><a name="index-g_t_0040sbbsdsockets_007binet_002dsocket_007d-561"></a></var><br>
<blockquote><p>Class precedence list: <code>inet-socket, socket, standard-object, t</code>

        </p><p>Class representing <code>tcp</code> and <code>udp</code> over IPv4 sockets.

        </p><p>Examples:

     </p><pre class="lisp">           (make-instance 'sb-bsd-sockets:inet-socket :type :stream :protocol :tcp)
          
           (make-instance 'sb-bsd-sockets:inet-socket :type :datagram :protocol :udp)
</pre>
        </blockquote></div>

   <p><a name="Class-sb_002dbsd_002dsockets_003ainet6_002dsocket"></a>

</p><div class="defun">
— Class: <b>inet6-socket [sb-bsd-sockets]</b><var><a name="index-g_t_0040sbbsdsockets_007binet6_002dsocket_007d-562"></a></var><br>
<blockquote><p>Class precedence list: <code>inet6-socket, socket, standard-object, t</code>

        </p><p>Class representing <code>tcp</code> and <code>udp</code> over IPv6 sockets.

        </p><p>Examples:

     </p><pre class="lisp">           (make-instance 'sb-bsd-sockets:inet6-socket :type :stream :protocol :tcp)
          
           (make-instance 'sb-bsd-sockets:inet6-socket :type :datagram :protocol :udp)
</pre>
        </blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003amake_002dinet_002daddress"></a>

</p><div class="defun">
— Function: <b>make-inet-address [sb-bsd-sockets]</b><var> dotted-quads<a name="index-g_t_0040sbbsdsockets_007bmake_002dinet_002daddress_007d-563"></a></var><br>
<blockquote><p>Return a vector of octets given a string <code>dotted-quads</code> in the format
"127.0.0.1". Signals an error if the string is malformed. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003amake_002dinet6_002daddress"></a>

</p><div class="defun">
— Function: <b>make-inet6-address [sb-bsd-sockets]</b><var> colon-separated-integers<a name="index-g_t_0040sbbsdsockets_007bmake_002dinet6_002daddress_007d-564"></a></var><br>
<blockquote><p>Return a vector of octets given a string representation of an IPv6
address <code>colon-separated-integers</code>. Signal an error if the string is
malformed. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003aget_002dprotocol_002dby_002dname"></a>

</p><div class="defun">
— Function: <b>get-protocol-by-name [sb-bsd-sockets]</b><var> name<a name="index-g_t_0040sbbsdsockets_007bget_002dprotocol_002dby_002dname_007d-565"></a></var><br>
<blockquote><p>Given a protocol name, return the protocol number, the protocol name, and
a list of protocol aliases
</p></blockquote></div>

<div class="node">
<a name="Local-(Unix)-Domain-Sockets"></a>
<a name="Local-_0028Unix_0029-Domain-Sockets"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Name-Service">Name Service</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#INET-Domain-Sockets">INET Domain Sockets</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Networking">Networking</a>

</div>

<h3 class="section">14.5 Local (Unix) Domain Sockets</h3>

<p>Local domain (<code>AF_LOCAL</code>) sockets are also known as Unix-domain
sockets, but were renamed by POSIX presumably on the basis that they
may be available on other systems too.

   </p><p>A local socket address is a string, which is used to create a node in
the local filesystem. This means of course that they cannot be used
across a network.

   </p><p><a name="Class-sb_002dbsd_002dsockets_003alocal_002dsocket"></a>

</p><div class="defun">
— Class: <b>local-socket [sb-bsd-sockets]</b><var><a name="index-g_t_0040sbbsdsockets_007blocal_002dsocket_007d-566"></a></var><br>
<blockquote><p>Class precedence list: <code>local-socket, socket, standard-object, t</code>

        </p><p>Class representing local domain (AF_LOCAL) sockets,
also known as unix-domain sockets. 
</p></blockquote></div>

<div class="node">
<a name="Name-Service"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Local-_0028Unix_0029-Domain-Sockets">Local (Unix) Domain Sockets</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Networking">Networking</a>

</div>

<h3 class="section">14.6 Name Service</h3>

<p>Presently name service is implemented by calling out to the
<code>getaddrinfo(3)</code> and <code>gethostinfo(3)</code>, or to
<code>gethostbyname(3)</code> <code>gethostbyaddr(3)</code> on platforms where
the preferred functions are not available. The exact details of
the name resolving process (for example the choice of whether
DNS or a hosts file is used for lookup) are platform dependent.

<!-- Direct links to the asynchronous @code{resolver(3)} routines would be -->
<!-- nice to have eventually, so that we can do DNS lookups in parallel -->
<!-- with other things. -->
   </p><p><a name="Class-sb_002dbsd_002dsockets_003ahost_002dent"></a>

</p><div class="defun">
— Class: <b>host-ent [sb-bsd-sockets]</b><var><a name="index-g_t_0040sbbsdsockets_007bhost_002dent_007d-567"></a></var><br>
<blockquote><p>Class precedence list: <code>host-ent, standard-object, t</code>

        </p><p>Slots:
          </p><ul>
<li><code>name</code> — initarg: <code>:name<!-- /@w --></code>; reader: <code>sb-bsd-sockets:host-ent-name<!-- /@w --></code>

          <p>The name of the host
</p></li><li><code>addresses</code> — initarg: <code>:addresses<!-- /@w --></code>; reader: <code>sb-bsd-sockets:host-ent-addresses<!-- /@w --></code>

          <p>A list of addresses for this host. 
</p></li></ul>

        <p>This class represents the results of an address lookup. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003aget_002dhost_002dby_002dname"></a>

</p><div class="defun">
— Function: <b>get-host-by-name [sb-bsd-sockets]</b><var> node<a name="index-g_t_0040sbbsdsockets_007bget_002dhost_002dby_002dname_007d-568"></a></var><br>
<blockquote><p>Returns a <code>host-ent</code> instance for <code>node</code> or signals a <code>name-service-error</code>.

        </p><p>Another <code>host-ent</code> instance containing zero, one or more IPv6 addresses
may be returned as a second return value.

        </p><p><code>node</code> may also be an <code>ip</code> address in dotted quad notation or some other
weird stuff <code>-</code> see getaddrinfo(3) for the details. 
</p></blockquote></div>

   <p><a name="Function-sb_002dbsd_002dsockets_003aget_002dhost_002dby_002daddress"></a>

</p><div class="defun">
— Function: <b>get-host-by-address [sb-bsd-sockets]</b><var> address<a name="index-g_t_0040sbbsdsockets_007bget_002dhost_002dby_002daddress_007d-569"></a></var><br>
<blockquote><p>Returns a <code>host-ent</code> instance for <code>address</code>, which should be a vector of
(integer 0 255) with 4 elements in case of an IPv4 address and 16
elements in case of an IPv6 address, or signals a <code>name-service-error</code>. 
See gethostbyaddr(3) for details. 
</p></blockquote></div>

   <p><a name="Generic_002dFunction-sb_002dbsd_002dsockets_003ahost_002dent_002daddress"></a>

</p><div class="defun">
— Generic Function: <b>host-ent-address [sb-bsd-sockets]</b><var> host-ent<a name="index-g_t_0040sbbsdsockets_007bhost_002dent_002daddress_007d-570"></a></var><br>
<blockquote><p>Return some valid address for <code>host-ent</code>. 
</p></blockquote></div>

<div class="node">
<a name="Profiling"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Contributed-Modules">Contributed Modules</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Networking">Networking</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">15 Profiling</h2>

<p><a name="index-Profiling-571"></a>
SBCL includes both a deterministic profiler, that can collect statistics
on individual functions, and a more “modern” statistical profiler.

   </p><p>Inlined functions do not appear in the results reported by either.

</p><ul class="menu">
<li><a accesskey="1" href="#Deterministic-Profiler">Deterministic Profiler</a>
</li><li><a accesskey="2" href="#Statistical-Profiler">Statistical Profiler</a>
</li></ul>

<div class="node">
<a name="Deterministic-Profiler"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Statistical-Profiler">Statistical Profiler</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Profiling">Profiling</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">15.1 Deterministic Profiler</h3>

<p><a name="index-Profiling_002c-deterministic-572"></a>
The package <code>sb-profile</code> provides a classic, per-function-call
profiler.

   </p><blockquote>
<b>note:</b> When profiling code executed by multiple threads in parallel, the
consing attributed to each function is inaccurate. 
</blockquote>

   <p><a name="Macro-sb_002dprofile_003aprofile"></a>

</p><div class="defun">
— Macro: <b>profile [sb-profile]</b><var> &amp;rest names<a name="index-g_t_0040sbprofile_007bprofile_007d-573"></a></var><br>
<blockquote><p><code>profile</code> Name*

        </p><p>If no names are supplied, return the list of profiled functions.

        </p><p>If names are supplied, wrap profiling code around the named functions. 
   As in <code>trace</code>, the names are not evaluated. A symbol names a function. 
   A string names all the functions named by symbols in the named
   package. If a function is already profiled, then unprofile and
   reprofile (useful to notice function redefinition.)  If a name is
   undefined, then we give a warning and ignore it. See also
   <code>unprofile</code>, <code>report</code> and <code>reset</code>. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dprofile_003aunprofile"></a>

</p><div class="defun">
— Macro: <b>unprofile [sb-profile]</b><var> &amp;rest names<a name="index-g_t_0040sbprofile_007bunprofile_007d-574"></a></var><br>
<blockquote><p>Unwrap any profiling code around the named functions, or if no names
  are given, unprofile all profiled functions. A symbol names
  a function. A string names all the functions named by symbols in the
  named package. <code>names</code> defaults to the list of names of all currently
  profiled functions. 
</p></blockquote></div>

   <p><a name="Function-sb_002dprofile_003areport"></a>

</p><div class="defun">
— Function: <b>report [sb-profile]</b><var> &amp;key limit print-no-call-list<a name="index-g_t_0040sbprofile_007breport_007d-575"></a></var><br>
<blockquote><p>Report results from profiling. The results are approximately
adjusted for profiling overhead. The compensation may be rather
inaccurate when bignums are involved in runtime calculation, as in a
very-long-running Lisp process.

        </p><p>If <code>limit</code> is set to an integer, only the top <code>limit</code> results are
reported. If <code>print-no-call-list</code> is <code>t</code> (the default) then a list of
uncalled profiled functions are listed. 
</p></blockquote></div>

   <p><a name="Function-sb_002dprofile_003areset"></a>

</p><div class="defun">
— Function: <b>reset [sb-profile]</b><var><a name="index-g_t_0040sbprofile_007breset_007d-576"></a></var><br>
<blockquote><p>Reset the counters for all profiled functions. 
</p></blockquote></div>

<div class="node">
<a name="Statistical-Profiler"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Deterministic-Profiler">Deterministic Profiler</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Profiling">Profiling</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">15.2 Statistical Profiler</h3>

<p><a name="index-Profiling_002c-statistical-577"></a>
The <code>sb-sprof</code> module, loadable by
</p><pre class="lisp">     (require :sb-sprof)
</pre>
   <p>provides an alternate profiler which works by taking samples of the
program execution at regular intervals, instead of instrumenting
functions like <code>sb-profile:profile</code> does. You might find
<code>sb-sprof</code> more useful than the deterministic profiler when profiling
functions in the <code>common-lisp</code>-package, SBCL internals, or code
where the instrumenting overhead is excessive.

   </p><p>Additionally <code>sb-sprof</code> includes a limited deterministic profiler
which can be used for reporting the amounts of calls to some functions
during

</p><h4 class="subsection">15.2.1 Example Usage</h4>

<pre class="lisp">     (in-package :cl-user)
     
     (require :sb-sprof)
     
     (declaim (optimize speed))
     
     (defun cpu-test-inner (a i)
       (logxor a
               (* i 5)
               (+ a i)))
     
     (defun cpu-test (n)
       (let ((a 0))
         (dotimes (i (expt 2 n) a)
           (setf a (cpu-test-inner a i)))))
     
     ;;;; CPU profiling
     
     ;;; Take up to 1000 samples of running (CPU-TEST 26), and give a flat
     ;;; table report at the end. Profiling will end one the body has been
     ;;; evaluated once, whether or not 1000 samples have been taken.
     (sb-sprof:with-profiling (:max-samples 1000
                               :report :flat
                               :loop nil)
       (cpu-test 26))
     
     ;;; Record call counts for functions defined on symbols in the CL-USER
     ;;; package.
     (sb-sprof:profile-call-counts "CL-USER")
     
     ;;; Take 1000 samples of running (CPU-TEST 24), and give a flat
     ;;; table report at the end. The body will be re-evaluated in a loop
     ;;; until 1000 samples have been taken. A sample count will be printed
     ;;; after each iteration.
     (sb-sprof:with-profiling (:max-samples 1000
                               :report :flat
                               :loop t
                               :show-progress t)
       (cpu-test 24))
     
     ;;;; Allocation profiling
     
     (defun foo (&amp;rest args)
       (mapcar (lambda (x) (float x 1d0)) args))
     
     (defun bar (n)
       (declare (fixnum n))
       (apply #'foo (loop repeat n collect n)))
     
     (sb-sprof:with-profiling (:max-samples 10000
                               :mode :alloc
                               :report :flat)
       (bar 1000))
</pre>
<h4 class="subsection">15.2.2 Output</h4>

<p>The flat report format will show a table of all functions that the
profiler encountered on the call stack during sampling, ordered by the
number of samples taken while executing that function.

</p><pre class="lisp">                Self        Total        Cumul
       Nr  Count     %  Count     %  Count     %    Calls  Function
     ------------------------------------------------------------------------
        1     69  24.4     97  34.3     69  24.4 67108864  CPU-TEST-INNER
        2     64  22.6     64  22.6    133  47.0        -  SB-VM::GENERIC-+
        3     39  13.8    256  90.5    172  60.8        1  CPU-TEST
        4     31  11.0     31  11.0    203  71.7        -  SB-KERNEL:TWO-ARG-XOR
</pre>
   <p>For each function, the table will show three absolute and relative
sample counts. The Self column shows samples taken while directly
executing that function. The Total column shows samples taken while
executing that function or functions called from it (sampled to a
platform-specific depth). The Cumul column shows the sum of all
Self columns up to and including that line in the table.

   </p><p>Additionally the Calls column will record the amount of calls that were
made to the function during the profiling run. This value will only
be reported for functions that have been explicitly marked for call counting
with <code>profile-call-counts</code>.

   </p><p>The profiler also hooks into the disassembler such that instructions which
have been sampled are annotated with their relative frequency of
sampling.  This information is not stored across different sampling
runs.

</p><pre class="lisp">     ;      6CF:       702E             JO L4              ; 6/242 samples
     ;      6D1:       D1E3             SHL EBX, 1
     ;      6D3:       702A             JO L4
     ;      6D5: L2:   F6C303           TEST BL, 3         ; 2/242 samples
     ;      6D8:       756D             JNE L8
     ;      6DA:       8BC3             MOV EAX, EBX       ; 5/242 samples
     ;      6DC: L3:   83F900           CMP ECX, 0         ; 4/242 samples
</pre>
   <h4 class="subsection">15.2.3 Platform support</h4>

<p>This module is known not to work consistently on the Alpha platform,
for technical reasons related to the implementation of a machine
language idiom for marking sections of code to be treated as atomic by
the garbage collector;  However, it should work on other platforms,
and the deficiency on the Alpha will eventually be rectified.

   </p><p>Allocation profiling is only supported on SBCL builds that use
the generational garbage collector. Tracking of call stacks at a
depth of more than two levels is only supported on x86 and x86-64.

</p><h4 class="subsection">15.2.4 Macros</h4>

<p><a name="Macro-sb_002dsprof_003awith_002dprofiling"></a>

</p><div class="defun">
— Macro: <b>with-profiling [sb-sprof]</b> (<var>&amp;key sample-interval alloc-interval max-samples reset mode loop max-depth show-progress threads report</var>)<var> &amp;body body<a name="index-g_t_0040sbsprof_007bwith_002dprofiling_007d-578"></a></var><br>
<blockquote><p>Evaluate <code>body</code> with statistical profiling turned on. If <code>loop</code> is true,
loop around the <code>body</code> until a sufficient number of samples has been collected. 
Returns the values from the last evaluation of <code>body</code>.

        </p><p>In multithreaded operation, only the thread in which <code>with-profiling</code> was
evaluated will be profiled by default. If you want to profile multiple
threads, invoke the profiler with <code>start-profiling</code>.

        </p><p>The following keyword args are recognized:

          </p><dl>
<dt><code>:sample-interval</code><em> &lt;n&gt;</em></dt><dd>   Take a sample every &lt;n&gt; seconds. Default is <code>*sample-interval*</code>.

          <br></dd><dt><code>:alloc-interval</code><em> &lt;n&gt;</em></dt><dd>   Take a sample every time &lt;n&gt; allocation regions (approximately
   8kB) have been allocated since the last sample. Default is
   <code>*alloc-interval*</code>.

          <br></dd><dt><code>:mode</code><em> &lt;mode&gt;</em></dt><dd>   If <code>:cpu</code>, run the profiler in <code>cpu</code> profiling mode. If <code>:alloc</code>, run the
   profiler in allocation profiling mode. If <code>:time</code>, run the profiler
   in wallclock profiling mode.

          <br></dd><dt><code>:max-samples</code><em> &lt;max&gt;</em></dt><dd>   Repeat evaluating body until &lt;max&gt; samples are taken. 
   Default is <code>*max-samples*</code>.

          <br></dd><dt><code>:max-depth</code><em> &lt;max&gt;</em></dt><dd>   Maximum call stack depth that the profiler should consider. Only
   has an effect on x86 and x86-64.

          <br></dd><dt><code>:report</code><em> &lt;type&gt;</em></dt><dd>   If specified, call <code>report</code> with <code>:type</code> &lt;type&gt; at the end.

          <br></dd><dt><code>:reset</code><em> &lt;bool&gt;</em></dt><dd>   It true, call <code>reset</code> at the beginning.

          <br></dd><dt><code>:threads</code><em> &lt;list-form&gt;</em></dt><dd>   Form that evaluates to the list threads to profile, or <code>:all</code> to indicate
   that all threads should be profiled. Defaults to the current
   thread. (Note: <code>start-profiling</code> defaults to all threads.)

          <p><code>:threads</code> has no effect on call-counting at the moment.

          </p><p>On some platforms (eg. Darwin) the signals used by the profiler are
   not properly delivered to threads in proportion to their <code>cpu</code> usage
   when doing <code>:cpu</code> profiling. If you see empty call graphs, or are obviously
   missing several samples from certain threads, you may be falling afoul
   of this. In this case using <code>:mode</code> <code>:time</code> is likely to work better.

          <br></p></dd><dt><code>:loop</code><em> &lt;bool&gt;</em></dt><dd>   If false (the default), evaluate <code>body</code> only once. If true repeatedly
   evaluate <code>body</code>. 
</dd></dl>

        </blockquote></div>

   <p><a name="Macro-sb_002dsprof_003awith_002dsampling"></a>

</p><div class="defun">
— Macro: <b>with-sampling [sb-sprof]</b> (<var>&amp;optional on</var>)<var> &amp;body body<a name="index-g_t_0040sbsprof_007bwith_002dsampling_007d-579"></a></var><br>
<blockquote><p>Evaluate body with statistical sampling turned on or off. 
</p></blockquote></div>

<h4 class="subsection">15.2.5 Functions</h4>

<p><a name="Function-sb_002dsprof_003areport"></a>

</p><div class="defun">
— Function: <b>report [sb-sprof]</b><var> &amp;key type max min-percent call-graph sort-by sort-order stream show-progress<a name="index-g_t_0040sbsprof_007breport_007d-580"></a></var><br>
<blockquote><p>Report statistical profiling results.  The following keyword
   args are recognized:

          </p><dl>
<dt><code>:type</code><em> &lt;type&gt;</em></dt><dd>      Specifies the type of report to generate.  If <code>:flat</code>, show
      flat report, if <code>:graph</code> show a call graph and a flat report. 
      If nil, don't print out a report.

          <br></dd><dt><code>:stream</code><em> &lt;stream&gt;</em></dt><dd>      Specify a stream to print the report on.  Default is
      <code>*standard-output*</code>.

          <br></dd><dt><code>:max</code><em> &lt;max&gt;</em></dt><dd>      Don't show more than &lt;max&gt; entries in the flat report.

          <br></dd><dt><code>:min-percent</code><em> &lt;min-percent&gt;</em></dt><dd>      Don't show functions taking less than &lt;min-percent&gt; of the
      total time in the flat report.

          <br></dd><dt><code>:sort-by</code><em> &lt;column&gt;</em></dt><dd>      If <code>:samples</code>, sort flat report by number of samples taken. 
      If <code>:cumulative-samples</code>, sort flat report by cumulative number of samples
      taken (shows how much time each function spent on stack.) Default
      is <code>*report-sort-by*</code>.

          <br></dd><dt><code>:sort-order</code><em> &lt;order&gt;</em></dt><dd>      If <code>:descending</code>, sort flat report in descending order. If <code>:ascending</code>,
      sort flat report in ascending order. Default is <code>*report-sort-order*</code>.

          <br></dd><dt><code>:show-progress</code><em> &lt;bool&gt;</em></dt><dd>     If true, print progress messages while generating the call graph.

          <br></dd><dt><code>:call-graph</code><em> &lt;graph&gt;</em></dt><dd>     Print a report from &lt;graph&gt; instead of the latest profiling
     results.

        </dd></dl>

        <p>Value of this function is a <code>call-graph</code> object representing the
resulting call-graph, or <code>nil</code> if there are no samples (eg. right after
calling <code>reset</code>.)

        </p><p>Profiling is stopped before the call graph is generated. 
</p></blockquote></div>

   <p><a name="Function-sb_002dsprof_003areset"></a>

</p><div class="defun">
— Function: <b>reset [sb-sprof]</b><var><a name="index-g_t_0040sbsprof_007breset_007d-581"></a></var><br>
<blockquote><p>Reset the profiler. 
</p></blockquote></div>

   <p><a name="Function-sb_002dsprof_003astart_002dprofiling"></a>

</p><div class="defun">
— Function: <b>start-profiling [sb-sprof]</b><var> &amp;key max-samples mode sample-interval alloc-interval max-depth threads sampling<a name="index-g_t_0040sbsprof_007bstart_002dprofiling_007d-582"></a></var><br>
<blockquote><p>Start profiling statistically in the current thread if not already profiling. 
The following keyword args are recognized:

          </p><dl>
<dt><code>:sample-interval</code><em> &lt;n&gt;</em></dt><dd>     Take a sample every &lt;n&gt; seconds.  Default is <code>*sample-interval*</code>.

          <br></dd><dt><code>:alloc-interval</code><em> &lt;n&gt;</em></dt><dd>     Take a sample every time &lt;n&gt; allocation regions (approximately
     8kB) have been allocated since the last sample. Default is
     <code>*alloc-interval*</code>.

          <br></dd><dt><code>:mode</code><em> &lt;mode&gt;</em></dt><dd>     If <code>:cpu</code>, run the profiler in <code>cpu</code> profiling mode. If <code>:alloc</code>, run
     the profiler in allocation profiling mode. If <code>:time</code>, run the profiler
     in wallclock profiling mode.

          <br></dd><dt><code>:max-samples</code><em> &lt;max&gt;</em></dt><dd>     Maximum number of samples.  Default is <code>*max-samples*</code>.

          <br></dd><dt><code>:max-depth</code><em> &lt;max&gt;</em></dt><dd>     Maximum call stack depth that the profiler should consider. Only
     has an effect on x86 and x86-64.

          <br></dd><dt><code>:threads</code><em> &lt;list&gt;</em></dt><dd>     List threads to profile, or <code>:all</code> to indicate that all threads should be
     profiled. Defaults to <code>:all</code>. (Note: <code>with-profiling</code> defaults to the current
     thread.)

          <p><code>:threads</code> has no effect on call-counting at the moment.

          </p><p>On some platforms (eg. Darwin) the signals used by the profiler are
     not properly delivered to threads in proportion to their <code>cpu</code> usage
     when doing <code>:cpu</code> profiling. If you see empty call graphs, or are obviously
     missing several samples from certain threads, you may be falling afoul
     of this.

          <br></p></dd><dt><code>:sampling</code><em> &lt;bool&gt;</em></dt><dd>     If true, the default, start sampling right away. 
     If false, <code>start-sampling</code> can be used to turn sampling on. 
</dd></dl>

        </blockquote></div>

   <p><a name="Function-sb_002dsprof_003astop_002dprofiling"></a>

</p><div class="defun">
— Function: <b>stop-profiling [sb-sprof]</b><var><a name="index-g_t_0040sbsprof_007bstop_002dprofiling_007d-583"></a></var><br>
<blockquote><p>Stop profiling if profiling. 
</p></blockquote></div>

   <p><a name="Function-sb_002dsprof_003aprofile_002dcall_002dcounts"></a>

</p><div class="defun">
— Function: <b>profile-call-counts [sb-sprof]</b><var> &amp;rest names<a name="index-g_t_0040sbsprof_007bprofile_002dcall_002dcounts_007d-584"></a></var><br>
<blockquote><p>Mark the functions named by <code>names</code> as being subject to call counting
during statistical profiling. If a string is used as a name, it will
be interpreted as a package name. In this case call counting will be
done for all functions with names like <code>x</code> or <code>(setf x)</code>, where <code>x</code> is a symbol
with the package as its home package. 
</p></blockquote></div>

   <p><a name="Function-sb_002dsprof_003aunprofile_002dcall_002dcounts"></a>

</p><div class="defun">
— Function: <b>unprofile-call-counts [sb-sprof]</b><var><a name="index-g_t_0040sbsprof_007bunprofile_002dcall_002dcounts_007d-585"></a></var><br>
<blockquote><p>Clear all call counting information. Call counting will be done for no
functions during statistical profiling. 
</p></blockquote></div>

<h4 class="subsection">15.2.6 Variables</h4>

<p><a name="Variable-sb_002dsprof_003a_002amax_002dsamples_002a"></a>

</p><div class="defun">
— Variable: <b>*max-samples* [sb-sprof]</b><var><a name="index-g_t_0040sbsprof_007b_0040earmuffs_007bmax_002dsamples_007d_007d-586"></a></var><br>
<blockquote><p>Default number of traces taken. This variable is somewhat misnamed:
each trace may actually consist of an arbitrary number of samples, depending
on the depth of the call stack. 
</p></blockquote></div>

   <p><a name="Variable-sb_002dsprof_003a_002asample_002dinterval_002a"></a>

</p><div class="defun">
— Variable: <b>*sample-interval* [sb-sprof]</b><var><a name="index-g_t_0040sbsprof_007b_0040earmuffs_007bsample_002dinterval_007d_007d-587"></a></var><br>
<blockquote><p>Default number of seconds between samples. 
</p></blockquote></div>

<h4 class="subsection">15.2.7 Credits</h4>

<p><code>sb-sprof</code> is an SBCL port, with enhancements, of Gerd
Moellmann's statistical profiler for CMUCL.

</p><div class="node">
<a name="Contributed-Modules"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Deprecation">Deprecation</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Profiling">Profiling</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">16 Contributed Modules</h2>

<p>SBCL comes with a number of modules that are not part of the core
system.  These are loaded via <code>(require :</code><var>modulename</var><code>)</code>
(see <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a>).  This section contains
documentation (or pointers to documentation) for some of the
contributed modules.

</p><ul class="menu">
<li><a accesskey="1" href="#sb_002daclrepl">sb-aclrepl</a>
</li><li><a accesskey="2" href="#sb_002dconcurrency">sb-concurrency</a>
</li><li><a accesskey="3" href="#sb_002dcover">sb-cover</a>
</li><li><a accesskey="4" href="#sb_002dgrovel">sb-grovel</a>
</li><li><a accesskey="5" href="#sb_002dmd5">sb-md5</a>
</li><li><a accesskey="6" href="#sb_002dposix">sb-posix</a>
</li><li><a accesskey="7" href="#sb_002dqueue">sb-queue</a>
</li><li><a accesskey="8" href="#sb_002drotate_002dbyte">sb-rotate-byte</a>
</li></ul>

<div class="node">
<a name="sb-aclrepl"></a>
<a name="sb_002daclrepl"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002dconcurrency">sb-concurrency</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.1 sb-aclrepl</h3>

<p><a name="index-Read_002dEval_002dPrint-Loop-588"></a><a name="index-REPL-589"></a>
<!-- FIXME: I wanted to use @registeredsymbol{}, but that's -->
<!-- only available in Texinfo 4.7.  sigh. -->
The <code>sb-aclrepl</code> module offers an Allegro CL-style
Read-Eval-Print Loop for SBCL, with integrated inspector.  Adding a
debugger interface is planned.

</p><h4 class="subsection">16.1.1 Usage</h4>

<p>To start <code>sb-aclrepl</code> as your read-eval-print loop, put the form
</p><pre class="lisp">     (require 'sb-aclrepl)
</pre>
   <p>in your <samp><span class="file">~/.sbclrc</span></samp> initialization file.

</p><h4 class="subsection">16.1.2 Example Initialization</h4>

<p>Here's a longer example of a <samp><span class="file">~/.sbclrc</span></samp> file that shows off
some of the features of <code>sb-aclrepl</code>:

</p><pre class="lisp">     (ignore-errors (require 'sb-aclrepl))
     
     (when (find-package 'sb-aclrepl)
       (push :aclrepl cl:*features*))
     #+aclrepl
     (progn
       (setq sb-aclrepl:*max-history* 100)
       (setf (sb-aclrepl:alias "asdc")
            #'(lambda (sys) (asdf:operate 'asdf:compile-op sys)))
       (sb-aclrepl:alias "l" (sys) (asdf:operate 'asdf:load-op sys))
       (sb-aclrepl:alias "t" (sys) (asdf:operate 'asdf:test-op sys))
       ;; The 1 below means that two characaters ("up") are required
       (sb-aclrepl:alias ("up" 1 "Use package") (package) (use-package package))
       ;; The 0 below means only the first letter ("r") is required,
       ;; such as ":r base64"
       (sb-aclrepl:alias ("require" 0 "Require module") (sys) (require sys))
       (setq cl:*features* (delete :aclrepl cl:*features*)))
</pre>
   <p>Questions, comments, or bug reports should be sent to Kevin Rosenberg
(<a href="mailto:kevin@rosenberg.net">kevin@rosenberg.net</a>).

</p><h4 class="subsection">16.1.3 Credits</h4>

<p>Allegro CL is a registered trademark of Franz Inc.

</p><div class="node">
<a name="sb-concurrency"></a>
<a name="sb_002dconcurrency"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002dcover">sb-cover</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002daclrepl">sb-aclrepl</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.2 sb-concurrency</h3>

<p><a name="index-Concurrency-590"></a><a name="index-Sb_002dconcurrency-591"></a>
Additional data structures, synchronization primitives and tools for
concurrent programming. Similiar to Java's <code>java.util.concurrent</code>
package.

   </p><p><a name="Section-sb_002dconcurrency_003aqueue"></a>

</p><h4 class="subsection">16.2.1 Queue</h4>

<p><a name="index-Queue_002c-lock_002dfree-592"></a>
<code>sb-concurrency:queue</code> is a lock-free, thread-safe FIFO queue
datatype. 
<br><br>
The implementation is based on <cite>An Optimistic Approach to
Lock-Free FIFO Queues</cite> by Edya Ladan-Mozes and Nir Shavit. 
<br><br>
Before SBCL 1.0.38, this implementation resided in its own contrib
(see <a href="#sb_002dqueue">sb-queue</a>) which is still provided for backwards-compatibility
but which has since been deprecated.

   </p><p><a name="Structure-sb_002dconcurrency_003aqueue"></a>

</p><div class="defun">
— Structure: <b>queue [sb-concurrency]</b><var><a name="index-g_t_0040sbconcurrency_007bqueue_007d-593"></a></var><br>
<blockquote><p>Class precedence list: <code>queue, structure-object, t</code>

        </p><p>Lock-free thread safe <code>fifo</code> queue.

        </p><p>Use <code>enqueue</code> to add objects to the queue, and <code>dequeue</code> to remove them. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003adequeue"></a>

</p><div class="defun">
— Function: <b>dequeue [sb-concurrency]</b><var> queue<a name="index-g_t_0040sbconcurrency_007bdequeue_007d-594"></a></var><br>
<blockquote><p>Retrieves the oldest value in <code>queue</code> and returns it as the primary value,
and <code>t</code> as secondary value. If the queue is empty, returns <code>nil</code> as both primary
and secondary value. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aenqueue"></a>

</p><div class="defun">
— Function: <b>enqueue [sb-concurrency]</b><var> value queue<a name="index-g_t_0040sbconcurrency_007benqueue_007d-595"></a></var><br>
<blockquote><p>Adds <code>value</code> to the end of <code>queue</code>. Returns <code>value</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003alist_002dqueue_002dcontents"></a>

</p><div class="defun">
— Function: <b>list-queue-contents [sb-concurrency]</b><var> queue<a name="index-g_t_0040sbconcurrency_007blist_002dqueue_002dcontents_007d-596"></a></var><br>
<blockquote><p>Returns the contents of <code>queue</code> as a list without removing them from the
<code>queue</code>. Mainly useful for manual examination of queue state, as the list may be
out of date by the time it is returned, and concurrent dequeue operations may
in the worse case force the queue-traversal to be restarted several times. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amake_002dqueue"></a>

</p><div class="defun">
— Function: <b>make-queue [sb-concurrency]</b><var> &amp;key name initial-contents<a name="index-g_t_0040sbconcurrency_007bmake_002dqueue_007d-597"></a></var><br>
<blockquote><p>Returns a new <code>queue</code> with <code>name</code> and contents of the <code>initial-contents</code>
sequence enqueued. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aqueue_002dcount"></a>

</p><div class="defun">
— Function: <b>queue-count [sb-concurrency]</b><var> queue<a name="index-g_t_0040sbconcurrency_007bqueue_002dcount_007d-598"></a></var><br>
<blockquote><p>Returns the number of objects in <code>queue</code>. Mainly useful for manual
examination of queue state, and in <code>print-object</code> methods: inefficient as it
must walk the entire queue. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aqueue_002dempty_002dp"></a>

</p><div class="defun">
— Function: <b>queue-empty-p [sb-concurrency]</b><var> queue<a name="index-g_t_0040sbconcurrency_007bqueue_002dempty_002dp_007d-599"></a></var><br>
<blockquote><p>Returns <code>t</code> if <code>queue</code> is empty, <code>nil</code> otherwise. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aqueue_002dname"></a>

</p><div class="defun">
— Function: <b>queue-name [sb-concurrency]</b><var> instance<a name="index-g_t_0040sbconcurrency_007bqueue_002dname_007d-600"></a></var><br>
<blockquote><p>Name of a <code>queue</code>. Can be assigned to using <code>setf</code>. Queue names
can be arbitrary printable objects, and need not be unique. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aqueuep"></a>

</p><div class="defun">
— Function: <b>queuep [sb-concurrency]</b><var> object<a name="index-g_t_0040sbconcurrency_007bqueuep_007d-601"></a></var><br>
<blockquote><p>Returns true if argument is a <code>queue</code>, <code>nil</code> otherwise. 
</p></blockquote></div>

<h4 class="subsection">16.2.2 Mailbox (lock-free)</h4>

<p><a name="index-Mailbox_002c-lock_002dfree-602"></a>
<code>sb-concurrency:mailbox</code> is a lock-free message queue where one
or multiple ends can send messages to one or multiple receivers. The
difference to <a href="#Section-sb_002dconcurrency_003aqueue">queues</a> is that the receiving
end may block until a message arrives. 
<br><br>
Built on top of the <a href="#Structure-sb_002dconcurrency_003aqueue">queue</a> implementation.

   </p><p><a name="Structure-sb_002dconcurrency_003amailbox"></a>

</p><div class="defun">
— Structure: <b>mailbox [sb-concurrency]</b><var><a name="index-g_t_0040sbconcurrency_007bmailbox_007d-603"></a></var><br>
<blockquote><p>Class precedence list: <code>mailbox, structure-object, t</code>

        </p><p>Mailbox aka message queue.

        </p><p><code>send-message</code> adds a message to the mailbox, <code>receive-message</code> waits till
a message becomes available, whereas <code>receive-message-no-hang</code> is a non-blocking
variant, and <code>receive-pending-messages</code> empties the entire mailbox in one go.

        </p><p>Messages can be arbitrary objects
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003alist_002dmailbox_002dmessages"></a>

</p><div class="defun">
— Function: <b>list-mailbox-messages [sb-concurrency]</b><var> mailbox<a name="index-g_t_0040sbconcurrency_007blist_002dmailbox_002dmessages_007d-604"></a></var><br>
<blockquote><p>Returns a fresh list containing all the messages in the
mailbox. Does not remove messages from the mailbox. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amailbox_002dcount"></a>

</p><div class="defun">
— Function: <b>mailbox-count [sb-concurrency]</b><var> mailbox<a name="index-g_t_0040sbconcurrency_007bmailbox_002dcount_007d-605"></a></var><br>
<blockquote><p>Returns the number of messages currently in the mailbox. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amailbox_002dempty_002dp"></a>

</p><div class="defun">
— Function: <b>mailbox-empty-p [sb-concurrency]</b><var> mailbox<a name="index-g_t_0040sbconcurrency_007bmailbox_002dempty_002dp_007d-606"></a></var><br>
<blockquote><p>Returns true if <code>mailbox</code> is currently empty, <code>nil</code> otherwise. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amailbox_002dname"></a>

</p><div class="defun">
— Function: <b>mailbox-name [sb-concurrency]</b><var> instance<a name="index-g_t_0040sbconcurrency_007bmailbox_002dname_007d-607"></a></var><br>
<blockquote><p>Name of a <code>mailbox</code>. SETFable. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amailboxp"></a>

</p><div class="defun">
— Function: <b>mailboxp [sb-concurrency]</b><var> object<a name="index-g_t_0040sbconcurrency_007bmailboxp_007d-608"></a></var><br>
<blockquote><p>Returns true if argument is a <code>mailbox</code>, <code>nil</code> otherwise. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amake_002dmailbox"></a>

</p><div class="defun">
— Function: <b>make-mailbox [sb-concurrency]</b><var> &amp;key name initial-contents<a name="index-g_t_0040sbconcurrency_007bmake_002dmailbox_007d-609"></a></var><br>
<blockquote><p>Returns a new <code>mailbox</code> with messages in <code>initial-contents</code> enqueued. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003areceive_002dmessage"></a>

</p><div class="defun">
— Function: <b>receive-message [sb-concurrency]</b><var> mailbox &amp;key timeout<a name="index-g_t_0040sbconcurrency_007breceive_002dmessage_007d-610"></a></var><br>
<blockquote><p>Removes the oldest message from <code>mailbox</code> and returns it as the primary
value, and a secondary value of <code>t</code>. If <code>mailbox</code> is empty waits until a message
arrives.

        </p><p>If <code>timeout</code> is provided, and no message arrives within the specified interval,
returns primary and secondary value of <code>nil</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003areceive_002dmessage_002dno_002dhang"></a>

</p><div class="defun">
— Function: <b>receive-message-no-hang [sb-concurrency]</b><var> mailbox<a name="index-g_t_0040sbconcurrency_007breceive_002dmessage_002dno_002dhang_007d-611"></a></var><br>
<blockquote><p>The non-blocking variant of <code>receive-message</code>. Returns two values,
the message removed from <code>mailbox</code>, and a flag specifying whether a
message could be received. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003areceive_002dpending_002dmessages"></a>

</p><div class="defun">
— Function: <b>receive-pending-messages [sb-concurrency]</b><var> mailbox &amp;optional n<a name="index-g_t_0040sbconcurrency_007breceive_002dpending_002dmessages_007d-612"></a></var><br>
<blockquote><p>Removes and returns all (or at most N) currently pending messages
from <code>mailbox</code>, or returns <code>nil</code> if no messages are pending.

        </p><p>Note: Concurrent threads may be snarfing messages during the run of
this function, so even though <code>x</code>,<code>y</code> appear right next to each other in
the result, does not necessarily mean that <code>y</code> was the message sent
right after <code>x</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003asend_002dmessage"></a>

</p><div class="defun">
— Function: <b>send-message [sb-concurrency]</b><var> mailbox message<a name="index-g_t_0040sbconcurrency_007bsend_002dmessage_007d-613"></a></var><br>
<blockquote><p>Adds a <code>message</code> to <code>mailbox</code>. Message can be any object. 
</p></blockquote></div>

   <p><a name="Section-sb_002dconcurrency_003agate"></a>

</p><h4 class="subsection">16.2.3 Gates</h4>

<p><a name="index-Gate-614"></a>
<code>sb-concurrency:gate</code> is a synchronization object suitable for when
multiple threads must wait for a single event before proceeding.

   </p><p><a name="Structure-sb_002dconcurrency_003agate"></a>

</p><div class="defun">
— Structure: <b>gate [sb-concurrency]</b><var><a name="index-g_t_0040sbconcurrency_007bgate_007d-615"></a></var><br>
<blockquote><p>Class precedence list: <code>gate, structure-object, t</code>

        </p><p><code>gate</code> type. Gates are synchronization constructs suitable for making
multiple threads wait for single event before proceeding.

        </p><p>Use <code>wait-on-gate</code> to wait for a gate to open, <code>open-gate</code> to open one,
and <code>close-gate</code> to close an open gate. <code>gate-open-p</code> can be used to test
the state of a gate without blocking. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aclose_002dgate"></a>

</p><div class="defun">
— Function: <b>close-gate [sb-concurrency]</b><var> gate<a name="index-g_t_0040sbconcurrency_007bclose_002dgate_007d-616"></a></var><br>
<blockquote><p>Closes <code>gate</code>. Returns <code>t</code> if the gate was previously open, and <code>nil</code>
if the gate was already closed. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003agate_002dname"></a>

</p><div class="defun">
— Function: <b>gate-name [sb-concurrency]</b><var> instance<a name="index-g_t_0040sbconcurrency_007bgate_002dname_007d-617"></a></var><br>
<blockquote><p>Name of a <code>gate</code>. SETFable. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003agate_002dopen_002dp"></a>

</p><div class="defun">
— Function: <b>gate-open-p [sb-concurrency]</b><var> gate<a name="index-g_t_0040sbconcurrency_007bgate_002dopen_002dp_007d-618"></a></var><br>
<blockquote><p>Returns true if <code>gate</code> is open. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003agatep"></a>

</p><div class="defun">
— Function: <b>gatep [sb-concurrency]</b><var> object<a name="index-g_t_0040sbconcurrency_007bgatep_007d-619"></a></var><br>
<blockquote><p>Returns true if the argument is a <code>gate</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amake_002dgate"></a>

</p><div class="defun">
— Function: <b>make-gate [sb-concurrency]</b><var> &amp;key name open<a name="index-g_t_0040sbconcurrency_007bmake_002dgate_007d-620"></a></var><br>
<blockquote><p>Makes a new gate. Gate will be initially open if <code>open</code> is true, and closed if <code>open</code>
is <code>nil</code> (the default.) <code>name</code>, if provided, is the name of the gate, used when printing
the gate. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003aopen_002dgate"></a>

</p><div class="defun">
— Function: <b>open-gate [sb-concurrency]</b><var> gate<a name="index-g_t_0040sbconcurrency_007bopen_002dgate_007d-621"></a></var><br>
<blockquote><p>Opens <code>gate</code>. Returns <code>t</code> if the gate was previously closed, and <code>nil</code>
if the gate was already open. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003await_002don_002dgate"></a>

</p><div class="defun">
— Function: <b>wait-on-gate [sb-concurrency]</b><var> gate &amp;key timeout<a name="index-g_t_0040sbconcurrency_007bwait_002don_002dgate_007d-622"></a></var><br>
<blockquote><p>Waits for <code>gate</code> to open, or <code>timeout</code> seconds to pass. Returns <code>t</code>
if the gate was opened in time, and <code>nil</code> otherwise. 
</p></blockquote></div>

   <p><a name="Section-sb_002dconcurrency_003afrlock"></a>

</p><h4 class="subsection">16.2.4 Frlocks, aka Fast Read Locks</h4>

<p><a name="index-Frlock-623"></a><a name="index-Fast-Read-Lock-624"></a>

   </p><p><a name="Structure-sb_002dconcurrency_003afrlock"></a>

</p><div class="defun">
— Structure: <b>frlock [sb-concurrency]</b><var><a name="index-g_t_0040sbconcurrency_007bfrlock_007d-625"></a></var><br>
<blockquote><p>Class precedence list: <code>frlock, structure-object, t</code>

        </p><p>FRlock, aka Fast Read Lock.

        </p><p>Fast Read Locks allow multiple readers and one potential writer to operate in
parallel while providing for consistency for readers and mutual exclusion for
writers.

        </p><p>Readers gain entry to protected regions without waiting, but need to retry if
a writer operated inside the region while they were reading. This makes frlocks
very efficient when readers are much more common than writers.

        </p><p>FRlocks are <code>not</code> suitable when it is not safe at all for readers and writers to
operate on the same data in parallel: they provide consistency, not exclusion
between readers and writers. Hence using an frlock to eg. protect an <code>sbcl</code>
hash-table is unsafe. If multiple readers operating in parallel with a writer
would be safe but inconsistent without a lock, frlocks are suitable.

        </p><p>The recommended interface to use is <code>frlock-read</code> and <code>frlock-write</code>, but those
needing it can also use a lower-level interface.

        </p><p>Example:

     </p><pre class="lisp">            ;; Values returned by FOO are always consistent so that
            ;; the third value is the sum of the two first ones.
            (let ((a 0)
                  (b 0)
                  (c 0)
                  (lk (make-frlock)))
              (defun foo ()
                 (frlock-read (lk) a b c))
              (defun bar (x y)
                 (frlock-write (lk)
                   (setf a x
                         b y
                         c (+ x y)))))
</pre>
        </blockquote></div>

   <p><a name="Macro-sb_002dconcurrency_003afrlock_002dread"></a>

</p><div class="defun">
— Macro: <b>frlock-read [sb-concurrency]</b> (<var>frlock</var>)<var> &amp;body value-forms<a name="index-g_t_0040sbconcurrency_007bfrlock_002dread_007d-626"></a></var><br>
<blockquote><p>Evaluates <code>value-forms</code> under <code>frlock</code> till it obtains a consistent
set, and returns that as multiple values. 
</p></blockquote></div>

   <p><a name="Macro-sb_002dconcurrency_003afrlock_002dwrite"></a>

</p><div class="defun">
— Macro: <b>frlock-write [sb-concurrency]</b> (<var>frlock &amp;key wait-p timeout</var>)<var> &amp;body body<a name="index-g_t_0040sbconcurrency_007bfrlock_002dwrite_007d-627"></a></var><br>
<blockquote><p>Executes <code>body</code> while holding <code>frlock</code> for writing. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003amake_002dfrlock"></a>

</p><div class="defun">
— Function: <b>make-frlock [sb-concurrency]</b><var> &amp;key name<a name="index-g_t_0040sbconcurrency_007bmake_002dfrlock_007d-628"></a></var><br>
<blockquote><p>Returns a new <code>frlock</code> with <code>name</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003afrlock_002dname"></a>

</p><div class="defun">
— Function: <b>frlock-name [sb-concurrency]</b><var> instance<a name="index-g_t_0040sbconcurrency_007bfrlock_002dname_007d-629"></a></var><br>
<blockquote><p>Name of an <code>frlock</code>. SETFable. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003afrlock_002dread_002dbegin"></a>

</p><div class="defun">
— Function: <b>frlock-read-begin [sb-concurrency]</b><var> frlock<a name="index-g_t_0040sbconcurrency_007bfrlock_002dread_002dbegin_007d-630"></a></var><br>
<blockquote><p>Start a read sequence on <code>frlock</code>. Returns a read-token and an epoch to be
validated later.

        </p><p>Using <code>frlock-read</code> instead is recommended. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003afrlock_002dread_002dend"></a>

</p><div class="defun">
— Function: <b>frlock-read-end [sb-concurrency]</b><var> frlock<a name="index-g_t_0040sbconcurrency_007bfrlock_002dread_002dend_007d-631"></a></var><br>
<blockquote><p>Ends a read sequence on <code>frlock</code>. Returns a token and an epoch. If the token
and epoch are <code>eql</code> to the read-token and epoch returned by <code>frlock-read-begin</code>,
the values read under the <code>frlock</code> are consistent and can be used: if the values
differ, the values are inconsistent and the read must be restated.

        </p><p>Using <code>frlock-read</code> instead is recommended.

        </p><p>Example:

     </p><pre class="lisp">            (multiple-value-bind (t0 e0) (frlock-read-begin *fr*)
              (let ((a (get-a))
                    (b (get-b)))
                (multiple-value-bind (t1 e1) (frlock-read-end *fr*)
                  (if (and (eql t0 t1) (eql e0 e1))
                      (list :a a :b b)
                      :aborted))))
</pre>
        </blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003agrab_002dfrlock_002dwrite_002dlock"></a>

</p><div class="defun">
— Function: <b>grab-frlock-write-lock [sb-concurrency]</b><var> frlock &amp;key wait-p timeout<a name="index-g_t_0040sbconcurrency_007bgrab_002dfrlock_002dwrite_002dlock_007d-632"></a></var><br>
<blockquote><p>Acquires <code>frlock</code> for writing, invalidating existing and future read-tokens
for the duration. Returns <code>t</code> on success, and <code>nil</code> if the lock wasn't acquired
due to eg. a timeout. Using <code>frlock-write</code> instead is recommended. 
</p></blockquote></div>

   <p><a name="Function-sb_002dconcurrency_003arelease_002dfrlock_002dwrite_002dlock"></a>

</p><div class="defun">
— Function: <b>release-frlock-write-lock [sb-concurrency]</b><var> frlock<a name="index-g_t_0040sbconcurrency_007brelease_002dfrlock_002dwrite_002dlock_007d-633"></a></var><br>
<blockquote><p>Releases <code>frlock</code> after writing, allowing valid read-tokens to be acquired again. 
Signals an error if the current thread doesn't hold <code>frlock</code> for writing. Using <code>frlock-write</code>
instead is recommended. 
</p></blockquote></div>

<div class="node">
<a name="sb-cover"></a>
<a name="sb_002dcover"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002dgrovel">sb-grovel</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002dconcurrency">sb-concurrency</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.3 sb-cover</h3>

<p><a name="index-Code-Coverage-634"></a>
The <code>sb-cover</code> module provides a code coverage tool for SBCL. The
tool has support for expression coverage, and for some branch coverage. 
Coverage reports are only generated for code compiled using
<code>compile-file</code> with the value of the
<code>sb-cover:store-coverage-data</code> optimization quality set to 3.

   </p><p>As of SBCL 1.0.6 <code>sb-cover</code> is still experimental, and the
interfaces documented here might change in later versions.

</p><h4 class="subsection">16.3.1 Example Usage</h4>

<pre class="lisp">     ;;; Load SB-COVER
     (require :sb-cover)
     
     ;;; Turn on generation of code coverage instrumentation in the compiler
     (declaim (optimize sb-cover:store-coverage-data))
     
     ;;; Load some code, ensuring that it's recompiled with the new optimization
     ;;; policy.
     (asdf:oos 'asdf:load-op :cl-ppcre-test :force t)
     
     ;;; Run the test suite.
     (cl-ppcre-test:test)
     
     ;;; Produce a coverage report
     (sb-cover:report "/tmp/report/")
     
     ;;; Turn off instrumentation
     (declaim (optimize (sb-cover:store-coverage-data 0)))
</pre>
<!-- @subsection Output -->
<!-- Write some documentation about how to interpret the results -->
<h4 class="subsection">16.3.2 Functions</h4>

<p><a name="Function-sb_002dcover_003areport"></a>

</p><div class="defun">
— Function: <b>report [sb-cover]</b><var> directory &amp;key form-mode external-format<a name="index-g_t_0040sbcover_007breport_007d-635"></a></var><br>
<blockquote><p>Print a code coverage report of all instrumented files into <code>directory</code>. 
If <code>directory</code> does not exist, it will be created. The main report will be
printed to the file cover-index.html. The external format of the source
files can be specified with the <code>external-format</code> parameter.

        </p><p>If the keyword argument <code>form-mode</code> has the value <code>:car</code>, the annotations in
the coverage report will be placed on the CARs of any cons-forms, while if
it has the value <code>:whole</code> the whole form will be annotated (the default). 
The former mode shows explicitly which forms were instrumented, while the
latter mode is generally easier to read. 
</p></blockquote></div>

   <p><a name="Function-sb_002dcover_003areset_002dcoverage"></a>

</p><div class="defun">
— Function: <b>reset-coverage [sb-cover]</b><var><a name="index-g_t_0040sbcover_007breset_002dcoverage_007d-636"></a></var><br>
<blockquote><p>Reset all coverage data back to the `Not executed` state. 
</p></blockquote></div>

   <p><a name="Function-sb_002dcover_003aclear_002dcoverage"></a>

</p><div class="defun">
— Function: <b>clear-coverage [sb-cover]</b><var><a name="index-g_t_0040sbcover_007bclear_002dcoverage_007d-637"></a></var><br>
<blockquote><p>Clear all files from the coverage database. The files will be re-entered
into the database when the <code>fasl</code> files (produced by compiling
<code>store-coverage-data</code> optimization policy set to 3) are loaded again into the
image. 
</p></blockquote></div>

   <p><a name="Function-sb_002dcover_003asave_002dcoverage"></a>

</p><div class="defun">
— Function: <b>save-coverage [sb-cover]</b><var><a name="index-g_t_0040sbcover_007bsave_002dcoverage_007d-638"></a></var><br>
<blockquote><p>Returns an opaque representation of the current code coverage state. 
The only operation that may be done on the state is passing it to
<code>restore-coverage</code>. The representation is guaranteed to be readably printable. 
A representation that has been printed and read back will work identically
in <code>restore-coverage</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dcover_003asave_002dcoverage_002din_002dfile"></a>

</p><div class="defun">
— Function: <b>save-coverage-in-file [sb-cover]</b><var> pathname<a name="index-g_t_0040sbcover_007bsave_002dcoverage_002din_002dfile_007d-639"></a></var><br>
<blockquote><p>Call <code>save-coverage</code> and write the results of that operation into the
file designated by <code>pathname</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dcover_003arestore_002dcoverage"></a>

</p><div class="defun">
— Function: <b>restore-coverage [sb-cover]</b><var> coverage-state<a name="index-g_t_0040sbcover_007brestore_002dcoverage_007d-640"></a></var><br>
<blockquote><p>Restore the code coverage data back to an earlier state produced by
<code>save-coverage</code>. 
</p></blockquote></div>

   <p><a name="Function-sb_002dcover_003arestore_002dcoverage_002dfrom_002dfile"></a>

</p><div class="defun">
— Function: <b>restore-coverage-from-file [sb-cover]</b><var> pathname<a name="index-g_t_0040sbcover_007brestore_002dcoverage_002dfrom_002dfile_007d-641"></a></var><br>
<blockquote><p><code>read</code> the contents of the file designated by <code>pathname</code> and pass the
result to <code>restore-coverage</code>. 
</p></blockquote></div>

<div class="node">
<a name="sb-grovel"></a>
<a name="sb_002dgrovel"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002dmd5">sb-md5</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002dcover">sb-cover</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.4 sb-grovel</h3>

<p><a name="index-Foreign-Function-Interface_002c-generation-642"></a>
The <code>sb-grovel</code> module helps in generation of foreign function
interfaces. It aids in extracting constants' values from the C
compiler and in generating SB-ALIEN structure and union types,
see <a href="#Defining-Foreign-Types">Defining Foreign Types</a>.

   </p><p>The ASDF(<a href="http://www.cliki.net/ASDF">http://www.cliki.net/ASDF</a>) component type
GROVEL-CONSTANTS-FILE has its PERFORM
<!-- @xref for PERFORM when asdf manual is included? -->
operation defined to write out a C source file, compile it, and run
it.  The output from this program is Lisp, which is then itself
compiled and loaded.

   </p><p>sb-grovel is used in a few contributed modules, and it is currently
compatible only to SBCL. However, if you want to use it, here are a
few directions.

</p><h4 class="subsection">16.4.1 Using sb-grovel in your own ASDF system</h4>

     <ol start="1" type="1">

     <li>Create a Lisp package for the foreign constants/functions to go into.

     </li><li>Make your system depend on the 'sb-grovel system.

     </li><li>Create a grovel-constants data file - for an example, see
example-constants.lisp in the contrib/sb-grovel/ directory in the SBCL
source distribution.

     </li><li>Add it as a component in your system. e.g.

     <pre class="lisp">          (eval-when (:compile-toplevel :load-toplevel :execute)
            (require :sb-grovel))
          
          (defpackage :example-package.system
                      (:use :cl :asdf :sb-grovel :sb-alien))
          
          (in-package :example-package.system)
          
          (defsystem example-system
              :depends-on (sb-grovel)
              :components
              ((:module "sbcl"
                        :components
                        ((:file "defpackage")
                         (grovel-constants-file "example-constants"
                                                :package :example-package)))))
</pre>
     <p>Make sure to specify the package you chose in step 1

     </p></li><li>Build stuff.

     </li></ol>

<h4 class="subsection">16.4.2 Contents of a grovel-constants-file</h4>

<p>The grovel-constants-file, typically named <code>constants.lisp</code>,
comprises lisp expressions describing the foreign things that you want
to grovel for. A <code>constants.lisp</code> file contains two sections:

     </p><ul>
<li>a list of headers to include in the C program, for example:
     <pre class="lisp">          ("sys/types.h" "sys/socket.h" "sys/stat.h" "unistd.h" "sys/un.h"
           "netinet/in.h" "netinet/in_systm.h" "netinet/ip.h" "net/if.h"
           "netdb.h" "errno.h" "netinet/tcp.h" "fcntl.h" "signal.h" )
</pre>
     </li><li>A list of sb-grovel clauses describing the things you want to grovel
from the C compiler, for example:
     <pre class="lisp">          ((:integer af-local
                     #+(or sunos solaris) "AF_UNIX"
                     #-(or sunos solaris) "AF_LOCAL"
                     "Local to host (pipes and file-domain).")
           (:structure stat ("struct stat"
                             (integer dev "dev_t" "st_dev")
                             (integer atime "time_t" "st_atime")))
           (:function getpid ("getpid" int )))
</pre>
     </li></ul>

   <p>There are two types of things that sb-grovel can sensibly extract from
the C compiler: constant integers and structure layouts. It is also
possible to define foreign functions in the constants.lisp file, but
these definitions don't use any information from the C program; they
expand directly to <code>sb-alien:define-alien-routine</code>
(see <a href="#The-define_002dalien_002droutine-Macro">The define-alien-routine Macro</a>) forms.

   </p><p>Here's how to use the grovel clauses:

     </p><ul>
<li><code>:integer</code> - constant expressions in C. Used in this form:
     <pre class="lisp">           (:integer lisp-variable-name "C expression" &amp;optional doc export)
</pre>
     <p><code>"C expression"</code> will be typically be the name of a constant. But
other forms are possible.

     </p></li><li><code>:enum</code>
     <pre class="lisp">           (:enum lisp-type-name ((lisp-enumerated-name c-enumerated-name) ...)))
</pre>
     <p>An <code>sb-alien:enum</code> type with name <code>lisp-type-name</code> will be defined. 
The symbols are the <code>lisp-enumerated-name</code>s, and the values
are grovelled from the <code>c-enumerated-name</code>s.

     </p></li><li><code>:structure</code> - alien structure definitions look like this:
     <pre class="lisp">           (:structure lisp-struct-name ("struct c_structure"
                                         (type-designator lisp-element-name
                                          "c_element_type" "c_element_name"
                                          :distrust-length nil)
                                         ; ...
                                         ))
</pre>
     <p><code>type-designator</code> is a reference to a type whose size (and type
constraints) will be groveled for. sb-grovel accepts a form of type
designator that doesn't quite conform to either lisp nor sb-alien's
type specifiers. Here's a list of type designators that sb-grovel
currently accepts:
          </p><ul>
<li><code>integer</code> - a C integral type; sb-grovel will infer the exact
type from size information extracted from the C program. All common C
integer types can be grovelled for with this type designator, but it
is not possible to grovel for bit fields yet.

          </li><li><code>(unsigned n)</code> - an unsigned integer variable that is <code>n</code>
bytes long. No size information from the C program will be used. 
</li><li><code>(signed n)</code> - an signed integer variable that is <code>n</code> bytes
long. No size information from the C program will be used.

          </li><li><code>c-string</code> - an array of <code>char</code> in the structure. sb-grovel
will use the array's length from the C program, unless you pass it the
<code>:distrust-length</code> keyword argument with non-<code>nil</code> value
(this might be required for structures such as solaris's <code>struct
dirent</code>).

          </li><li><code>c-string-pointer</code> - a pointer to a C string, corresponding to
the <code>sb-alien:c-string</code> type (see <a href="#Foreign-Type-Specifiers">Foreign Type Specifiers</a>). 
</li><li><code>(array alien-type)</code> - An array of the previously-declared alien
type. The array's size will be determined from the output of the C
program and the alien type's size. 
</li><li><code>(array alien-type n)</code> - An array of the previously-declared alien
type. The array's size will be assumed as being <code>n</code>. 
</li></ul>

     <p>Note that <code>c-string</code> and <code>c-string-pointer</code> do not have the
same meaning. If you declare that an element is of type
<code>c-string</code>, it will be treated as if the string is a part of the
structure, whereas if you declare that the element is of type
<code>c-string-pointer</code>, a <em>pointer to a string</em> will be the
structure member.

     </p></li><li><code>:function</code> - alien function definitions are similar to
<code>define-alien-routine</code> definitions, because they expand to such
forms when the lisp program is loaded. See <a href="#Foreign-Function-Calls">Foreign Function Calls</a>.

     <pre class="lisp">          (:function lisp-function-name ("alien_function_name" alien-return-type
                                                               (argument alien-type)
                                                               (argument2 alien-type)))
</pre>
     </li></ul>

<h4 class="subsection">16.4.3 Programming with sb-grovel's structure types</h4>

<p>Let us assume that you have a grovelled structure definition:
</p><pre class="lisp">      (:structure mystruct ("struct my_structure"
                            (integer myint "int" "st_int")
                            (c-string mystring "char[]" "st_str")))
</pre>
   <p>What can you do with it? Here's a short interface document:

     </p><ul>
<li>Creating and destroying objects:
          <ul>
<li>Function <code>(allocate-mystruct)</code> - allocates an object of type <code>mystruct</code>and
returns a system area pointer to it. 
</li><li>Function <code>(free-mystruct var)</code> - frees the alien object pointed to by
<var>var</var>. 
</li><li>Macro <code>(with-mystruct var ((member init) [...]) &amp;body body)</code> -
allocates an object of type <code>mystruct</code> that is valid in
<var>body</var>. If <var>body</var> terminates or control unwinds out of
<var>body</var>, the object pointed to by <var>var</var> will be deallocated. 
</li></ul>

     </li><li>Accessing structure members:
          <ul>
<li><code>(mystruct-myint var)</code> and <code>(mystruct-mystring var)</code> return
the value of the respective fields in <code>mystruct</code>. 
</li><li><code>(setf (mystruct-myint var) new-val)</code> and
<code>(setf (mystruct-mystring var) new-val)</code> sets the value of the respective
structure member to the value of <var>new-val</var>. Notice that in
<code>(setf (mystruct-mystring var) new-val)</code>'s case, new-val is a lisp
string. 
</li></ul>
     </li></ul>

<h5 class="subsubsection">16.4.3.1 Traps and Pitfalls</h5>

<p>Basically, you can treat functions and data structure definitions that
sb-grovel spits out as if they were alien routines and types. This has
a few implications that might not be immediately obvious (especially
if you have programmed in a previous version of sb-grovel that didn't
use alien types):

     </p><ul>
<li>You must take care of grovel-allocated structures yourself. They are
alien types, so the garbage collector will not collect them when you
drop the last reference.

     </li><li>If you use the <code>with-mystruct</code> macro, be sure that no references
to the variable thus allocated leaks out. It will be deallocated when
the block exits. 
</li></ul>

<div class="node">
<a name="sb-md5"></a>
<a name="sb_002dmd5"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002dposix">sb-posix</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002dgrovel">sb-grovel</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.5 sb-md5</h3>

<p><a name="index-Hashing_002c-cryptographic-643"></a>
The <code>sb-md5</code> module implements the RFC1321 MD5 Message Digest
Algorithm. [FIXME cite]

   </p><p><a name="Function-sb_002dmd5_003amd5sum_002dfile"></a>

</p><div class="defun">
— Function: <b>md5sum-file [sb-md5]</b><var> pathname<a name="index-g_t_0040sbmd_007bmd5sum_002dfile_007d-644"></a></var><br>
<blockquote><p>Calculate the MD5 message-digest of the file specified by `pathname'. 
</p></blockquote></div>

   <p><a name="Function-sb_002dmd5_003amd5sum_002dsequence"></a>

</p><div class="defun">
— Function: <b>md5sum-sequence [sb-md5]</b><var> sequence &amp;key start end<a name="index-g_t_0040sbmd_007bmd5sum_002dsequence_007d-645"></a></var><br>
<blockquote><p>Calculate the MD5 message-digest of data in `sequence', which should
be a 1d simple-array with element type (unsigned-byte 8).  On <code>cmu</code> <code>cl</code>
and <code>sbcl</code> non-simple and non-1d arrays with this element-type are also
supported.  Use with strings is <code>deprecated</code>, since this will not work
correctly on implementations with `char-code-limit' &gt; 256 and ignores
character-coding issues.  Use md5sum-string instead, or convert to the
required (unsigned-byte 8) format through other means before-hand. 
</p></blockquote></div>

   <p><a name="Function-sb_002dmd5_003amd5sum_002dstream"></a>

</p><div class="defun">
— Function: <b>md5sum-stream [sb-md5]</b><var> stream<a name="index-g_t_0040sbmd_007bmd5sum_002dstream_007d-646"></a></var><br>
<blockquote><p>Calculate an MD5 message-digest of the contents of `stream'.  Its
element-type has to be (unsigned-byte 8). Use on character streams is
<code>deprecated</code>, as this will not work correctly on implementations with
`char-code-limit' &gt; 256 and ignores character coding issues. 
</p></blockquote></div>

   <p><a name="Function-sb_002dmd5_003amd5sum_002dstring"></a>

</p><div class="defun">
— Function: <b>md5sum-string [sb-md5]</b><var> string &amp;key external-format start end<a name="index-g_t_0040sbmd_007bmd5sum_002dstring_007d-647"></a></var><br>
<blockquote><p>Calculate the MD5 message-digest of the binary representation of
`string' (as octets) in the external format specified by
`external-format'. The boundaries `start' and `end' refer to character
positions in the string, not to octets in the resulting binary
representation.  The permissible external format specifiers are
determined by the underlying implementation. 
</p></blockquote></div>

<h4 class="subsection">16.5.1 Credits</h4>

<p>The implementation for CMUCL was largely done by Pierre Mai, with help
from members of the <code>cmucl-help</code> mailing list.  Since CMUCL and
SBCL are similar in many respects, it was not too difficult to extend
the low-level implementation optimizations for CMUCL to SBCL. 
Following this, SBCL's compiler was extended to implement efficient
compilation of modular arithmetic (see <a href="#Modular-arithmetic">Modular arithmetic</a>), which
enabled the implementation to be expressed in portable arithmetical
terms, apart from the use of <code>rotate-byte</code> for bitwise rotation. 
<a name="index-g_t_0040sbrotatebyte_007brotate_002dbyte_007d-648"></a>

</p><div class="node">
<a name="sb-posix"></a>
<a name="sb_002dposix"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002dqueue">sb-queue</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002dmd5">sb-md5</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.6 sb-posix</h3>

<p><a name="index-Operating-System-Interface-649"></a><a name="index-System-Calls-650"></a><a name="index-Posix-651"></a>
Sb-posix is the supported interface for calling out to the operating
system.<a rel="footnote" href="#fn-10" name="fnd-10"><sup>10</sup></a>

   </p><p>The scope of this interface is “operating system calls on a typical
Unixlike platform”.  This is section 2 of the Unix manual, plus section
3 calls that are (a) typically found in libc, but (b) not part of the C
standard.  For example, we intend to provide support for
<code>opendir()</code> and <code>readdir()</code>, but not for <code>printf()</code>. 
That said, if your favourite system call is not included yet, you are
encouraged to submit a patch to the SBCL mailing list.

   </p><p>Some facilities are omitted where they offer absolutely no additional
use over some portable function, or would be actively dangerous to the
consistency of Lisp.  Not all functions are available on all
platforms.

</p><ul class="menu">
<li><a accesskey="1" href="#Lisp-names-for-C-names">Lisp names for C names</a>
</li><li><a accesskey="2" href="#Types">Types</a>
</li><li><a accesskey="3" href="#Function-Parameters">Function Parameters</a>
</li><li><a accesskey="4" href="#Function-Return-Values">Function Return Values</a>
</li><li><a accesskey="5" href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a>
</li><li><a accesskey="6" href="#Functions-with-idiosyncratic-bindings">Functions with idiosyncratic bindings</a>
</li></ul>

<div class="node">
<a name="Lisp-names-for-C-names"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Types">Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#sb_002dposix">sb-posix</a>

</div>

<h4 class="subsection">16.6.1 Lisp names for C names</h4>

<p>All symbols are in the <code>SB-POSIX</code> package.  This package contains a
Lisp function for each supported Unix system call or function, a
variable or constant for each supported Unix constant, an object type
for each supported Unix structure type, and a slot name for each
supported Unix structure member.  A symbol name is derived from the C
binding's name, by (a) uppercasing, then (b) removing leading
underscores (<code>#\_</code>) then replacing remaining underscore characters
with the hyphen (<code>#\-</code>). The requirement to uppercase is so that in
a standard upcasing reader the user may write <code>sb-posix:creat</code>
instead of <code>sb-posix:|creat|</code> as would otherise be required.

   </p><p>No other changes to “Lispify” symbol names are made, so <code>creat()</code>
becomes <code>CREAT</code>, not <code>CREATE</code>.

   </p><p>The user is encouraged not to <code>(USE-PACKAGE :SB-POSIX)</code> but instead
to use the <code>SB-POSIX:</code> prefix on all references, as some of the
symbols symbols contained in the SB-POSIX package have the same name as
CL symbols (<code>OPEN</code>, <code>CLOSE</code>, <code>SIGNAL</code> etc).

</p><div class="node">
<a name="Types"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Function-Parameters">Function Parameters</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Lisp-names-for-C-names">Lisp names for C names</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#sb_002dposix">sb-posix</a>

</div>

<h4 class="subsection">16.6.2 Types</h4>

<p>Generally, marshalling between Lisp and C data types is done using
SBCL's FFI. See <a href="#Foreign-Function-Interface">Foreign Function Interface</a>.

   </p><p>Some functions accept objects such as filenames or file descriptors.  In
the C binding to POSIX these are represented as strings and small
integers respectively. For the Lisp programmer's convenience we
introduce designators such that CL pathnames or open streams can be
passed to these functions.  For example, <code>rename</code> accepts both
pathnames and strings as its arguments.

</p><ul class="menu">
<li><a accesskey="1" href="#File_002ddescriptors">File-descriptors</a>
</li><li><a accesskey="2" href="#Filenames">Filenames</a>
</li></ul>

<div class="node">
<a name="File-descriptors"></a>
<a name="File_002ddescriptors"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Filenames">Filenames</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Types">Types</a>

</div>

<h5 class="subsubsection">16.6.2.1 File-descriptors</h5>

<p><a name="Type-sb_002dposix_003afile_002ddescriptor"></a>

</p><div class="defun">
— Type: <b>file-descriptor [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bfile_002ddescriptor_007d-652"></a></var><br>
<blockquote><p>A <code>fixnum</code> designating a native file descriptor.

        </p><p><code>sb-sys:make-fd-stream</code> can be used to construct a <code>file-stream</code> associated with a
native file descriptor.

        </p><p>Note that mixing I/O operations on a <code>file-stream</code> with operations directly on its
descriptor may produce unexpected results if the stream is buffered. 
</p></blockquote></div>

   <p><a name="Type-sb_002dposix_003afile_002ddescriptor_002ddesignator"></a>

</p><div class="defun">
— Type: <b>file-descriptor-designator [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bfile_002ddescriptor_002ddesignator_007d-653"></a></var><br>
<blockquote><p>Designator for a <code>file-descriptor:</code> either a fixnum designating itself, or
a <code>file-stream</code> designating the underlying file-descriptor. 
</p></blockquote></div>

   <p><a name="Function-sb_002dposix_003afile_002ddescriptor"></a>

</p><div class="defun">
— Function: <b>file-descriptor [sb-posix]</b><var> file-descriptor<a name="index-g_t_0040sbposix_007bfile_002ddescriptor_007d-654"></a></var><br>
<blockquote><p>Converts <code>file-descriptor-designator</code> into a <code>file-descriptor</code>. 
</p></blockquote></div>

<div class="node">
<a name="Filenames"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#File_002ddescriptors">File-descriptors</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Types">Types</a>

</div>

<h5 class="subsubsection">16.6.2.2 Filenames</h5>

<p><a name="Type-sb_002dposix_003afilename"></a>

</p><div class="defun">
— Type: <b>filename [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bfilename_007d-655"></a></var><br>
<blockquote><p>A <code>string</code> designating a filename in native namestring syntax.

        </p><p>Note that native namestring syntax is distinct from Lisp namestring syntax:

     </p><pre class="lisp">            (pathname "/foo*/bar")
</pre>
        <p>is a wild pathname with a pattern-matching directory component. 
<code>sb-ext:parse-native-namestring</code> may be used to construct Lisp pathnames that
denote <code>posix</code> filenames as understood by system calls, and
<code>sb-ext:native-namestring</code> can be used to coerce them into strings in the native
namestring syntax.

        </p><p>Note also that <code>posix</code> filename syntax does not distinguish the names of files
from the names of directories: in order to parse the name of a directory in
<code>posix</code> filename syntax into a pathname <code>my-defaults</code> for which

     </p><pre class="lisp">            (merge-pathnames (make-pathname :name "FOO" :case :common)
                              my-defaults)
</pre>
        <p>returns a pathname that denotes a file in the directory, supply a true
<code>:as-directory</code> argument to <code>sb-ext:parse-native-namestring</code>. Likewise, to supply
the name of a directory to a <code>posix</code> function in non-directory syntax, supply a
true <code>:as-file</code> argument to <code>sb-ext:native-namestring</code>. 
</p></blockquote></div>

   <p><a name="Type-sb_002dposix_003afilename_002ddesignator"></a>

</p><div class="defun">
— Type: <b>filename-designator [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bfilename_002ddesignator_007d-656"></a></var><br>
<blockquote><p>Designator for a <code>filename:</code> a <code>string</code> designating itself, or a
designator for a <code>pathname</code> designating the corresponding native namestring. 
</p></blockquote></div>

   <p><a name="Function-sb_002dposix_003afilename"></a>

</p><div class="defun">
— Function: <b>filename [sb-posix]</b><var> filename<a name="index-g_t_0040sbposix_007bfilename_007d-657"></a></var><br>
<blockquote><p>Converts <code>filename-designator</code> into a <code>filename</code>. 
</p></blockquote></div>

<div class="node">
<a name="Function-Parameters"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Function-Return-Values">Function Return Values</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Types">Types</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#sb_002dposix">sb-posix</a>

</div>

<h4 class="subsection">16.6.3 Function Parameters</h4>

<p>The calling convention is modelled after that of CMUCL's <code>UNIX</code>
package: in particular, it's like the C interface except that:

     </p><ol start="1" type="a">
<li>Length arguments are omitted or optional where the sensible value
is obvious.  For example, <code>read</code> would be defined this way:

     <pre class="lisp">          (read fd buffer &amp;optional (length (length buffer))) =&gt; bytes-read
</pre>
     </li><li>Where C simulates “out” parameters using pointers (for instance, in
<code>pipe()</code> or <code>socketpair()</code>) these may be optional or omitted
in the Lisp interface: if not provided, appropriate objects will be
allocated and returned (using multiple return values if necessary).

     </li><li>Some functions accept objects such as filenames or file descriptors. 
Wherever these are specified as such in the C bindings, the Lisp
interface accepts designators for them as specified in the 'Types'
section above.

     </li><li>A few functions have been included in sb-posix that do not correspond
exactly with their C counterparts.  These are described in
See <a href="#Functions-with-idiosyncratic-bindings">Functions with idiosyncratic bindings</a>.

        </li></ol>

<div class="node">
<a name="Function-Return-Values"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Function-Parameters">Function Parameters</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#sb_002dposix">sb-posix</a>

</div>

<h4 class="subsection">16.6.4 Function Return Values</h4>

<p>The return value is usually the same as for the C binding, except in
error cases: where the C function is defined as returning some sentinel
value and setting <code>errno</code> on error, we instead signal an error of
type <code>SYSCALL-ERROR</code>.  The actual error value (<code>errno</code>) is
stored in this condition and can be accessed with <code>SYSCALL-ERRNO</code>.

   </p><p>We do not automatically translate the returned value into “Lispy”
objects – for example, <code>SB-POSIX:OPEN</code> returns a small integer,
not a stream.  Exception: boolean-returning functions (or, more
commonly, macros) do not return a C integer, but instead a Lisp
boolean.

</p><div class="node">
<a name="Lisp-objects-and-C-structures"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Functions-with-idiosyncratic-bindings">Functions with idiosyncratic bindings</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Function-Return-Values">Function Return Values</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#sb_002dposix">sb-posix</a>

</div>

<h4 class="subsection">16.6.5 Lisp objects and C structures</h4>

<p>Sb-posix provides various Lisp object types to stand in for C
structures in the POSIX library.  Lisp bindings to C functions that
accept, manipulate, or return C structures accept, manipulate, or
return instances of these Lisp types instead of instances of alien
types.

   </p><p>The names of the Lisp types are chosen according to the general rules
described above.  For example Lisp objects of type <code>STAT</code> stand
in for C structures of type <code>struct stat</code>.

   </p><p>Accessors are provided for each standard field in the structure. These
are named <var>structure-name</var><code>-</code><var>field-name</var> where the two
components are chosen according to the general name conversion rules,
with the exception that in cases where all fields in a given structure
have a common prefix, that prefix is omitted. For example,
<code>stat.st_dev</code> in C becomes <code>STAT-DEV</code> in Lisp.

<!-- This was in the README, but it proves to be false about sb-posix. -->
   </p><p>Because sb-posix might not support all semi-standard or
implementation-dependent members of all structure types on your system
(patches welcome), here is an enumeration of all supported Lisp
objects corresponding to supported POSIX structures, and the supported
slots for those structures.

     </p><ul>
<li>flock
<a name="Class-sb_002dposix_003aflock"></a>

     <div class="defun">
— Class: <b>flock [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bflock_007d-658"></a></var><br>
<blockquote> <p>Class precedence list: <code>flock, standard-object, t</code>

             </p><p>Slots:
               </p><ul>
<li><code>type</code> — initarg: <code>:type<!-- /@w --></code>; reader: <code>sb-posix:flock-type<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:flock-type)<!-- /@w --></code>

               <p>Type of lock; F_RDLCK, F_WRLCK, F_UNLCK. 
</p></li><li><code>whence</code> — initarg: <code>:whence<!-- /@w --></code>; reader: <code>sb-posix:flock-whence<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:flock-whence)<!-- /@w --></code>

               <p>Flag for starting offset. 
</p></li><li><code>start</code> — initarg: <code>:start<!-- /@w --></code>; reader: <code>sb-posix:flock-start<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:flock-start)<!-- /@w --></code>

               <p>Relative offset in bytes. 
</p></li><li><code>len</code> — initarg: <code>:len<!-- /@w --></code>; reader: <code>sb-posix:flock-len<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:flock-len)<!-- /@w --></code>

               <p>Size; if 0 then until <code>eof</code>. 
</p></li><li><code>pid</code> — reader: <code>sb-posix:flock-pid<!-- /@w --></code>

               <p>Process <code>id</code> of the process holding the lock; returned with F_GETLK. 
</p></li></ul>

             <p>Class representing locks used in fcntl(2). 
</p></blockquote></div>

     </li><li>passwd
<a name="Class-sb_002dposix_003apasswd"></a>

     <div class="defun">
— Class: <b>passwd [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bpasswd_007d-659"></a></var><br>
<blockquote> <p>Class precedence list: <code>passwd, standard-object, t</code>

             </p><p>Slots:
               </p><ul>
<li><code>name</code> — initarg: <code>:name<!-- /@w --></code>; reader: <code>sb-posix:passwd-name<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-name)<!-- /@w --></code>

               <p>User's login name. 
</p></li><li><code>passwd</code> — initarg: <code>:passwd<!-- /@w --></code>; reader: <code>sb-posix:passwd-passwd<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-passwd)<!-- /@w --></code>

               <p>The account's encrypted password. 
</p></li><li><code>uid</code> — initarg: <code>:uid<!-- /@w --></code>; reader: <code>sb-posix:passwd-uid<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-uid)<!-- /@w --></code>

               <p>Numerical user <code>id</code>. 
</p></li><li><code>gid</code> — initarg: <code>:gid<!-- /@w --></code>; reader: <code>sb-posix:passwd-gid<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-gid)<!-- /@w --></code>

               <p>Numerical group <code>id</code>. 
</p></li><li><code>gecos</code> — initarg: <code>:gecos<!-- /@w --></code>; reader: <code>sb-posix:passwd-gecos<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-gecos)<!-- /@w --></code>

               <p>User's name or comment field. 
</p></li><li><code>dir</code> — initarg: <code>:dir<!-- /@w --></code>; reader: <code>sb-posix:passwd-dir<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-dir)<!-- /@w --></code>

               <p>Initial working directory. 
</p></li><li><code>shell</code> — initarg: <code>:shell<!-- /@w --></code>; reader: <code>sb-posix:passwd-shell<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:passwd-shell)<!-- /@w --></code>

               <p>Program to use as shell. 
</p></li></ul>

             <p>Instances of this class represent entries in the system's user database. 
</p></blockquote></div>

     </li><li>stat
<a name="Class-sb_002dposix_003astat"></a>

     <div class="defun">
— Class: <b>stat [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bstat_007d-660"></a></var><br>
<blockquote> <p>Class precedence list: <code>stat, standard-object, t</code>

             </p><p>Slots:
               </p><ul>
<li><code>mode</code> — initarg: <code>:mode<!-- /@w --></code>; reader: <code>sb-posix:stat-mode<!-- /@w --></code>

               <p>Mode of file. 
</p></li><li><code>ino</code> — initarg: <code>:ino<!-- /@w --></code>; reader: <code>sb-posix:stat-ino<!-- /@w --></code>

               <p>File serial number. 
</p></li><li><code>dev</code> — initarg: <code>:dev<!-- /@w --></code>; reader: <code>sb-posix:stat-dev<!-- /@w --></code>

               <p>Device <code>id</code> of device containing file. 
</p></li><li><code>nlink</code> — initarg: <code>:nlink<!-- /@w --></code>; reader: <code>sb-posix:stat-nlink<!-- /@w --></code>

               <p>Number of hard links to the file. 
</p></li><li><code>uid</code> — initarg: <code>:uid<!-- /@w --></code>; reader: <code>sb-posix:stat-uid<!-- /@w --></code>

               <p>User <code>id</code> of file. 
</p></li><li><code>gid</code> — initarg: <code>:gid<!-- /@w --></code>; reader: <code>sb-posix:stat-gid<!-- /@w --></code>

               <p>Group <code>id</code> of file. 
</p></li><li><code>size</code> — initarg: <code>:size<!-- /@w --></code>; reader: <code>sb-posix:stat-size<!-- /@w --></code>

               <p>For regular files, the file size in
                         bytes.  For symbolic links, the length
                         in bytes of the filename contained in
                         the symbolic link. 
</p></li><li><code>rdev</code> — initarg: <code>:rdev<!-- /@w --></code>; reader: <code>sb-posix:stat-rdev<!-- /@w --></code>

               <p>For devices the device number. 
</p></li><li><code>atime</code> — initarg: <code>:atime<!-- /@w --></code>; reader: <code>sb-posix:stat-atime<!-- /@w --></code>

               <p>Time of last access. 
</p></li><li><code>mtime</code> — initarg: <code>:mtime<!-- /@w --></code>; reader: <code>sb-posix:stat-mtime<!-- /@w --></code>

               <p>Time of last data modification. 
</p></li><li><code>ctime</code> — initarg: <code>:ctime<!-- /@w --></code>; reader: <code>sb-posix:stat-ctime<!-- /@w --></code>

               <p>Time of last status change. 
</p></li></ul>

             <p>Instances of this class represent <code>posix</code> file metadata. 
</p></blockquote></div>

     </li><li>termios
<a name="Class-sb_002dposix_003atermios"></a>

     <div class="defun">
— Class: <b>termios [sb-posix]</b><var><a name="index-g_t_0040sbposix_007btermios_007d-661"></a></var><br>
<blockquote> <p>Class precedence list: <code>termios, standard-object, t</code>

             </p><p>Slots:
               </p><ul>
<li><code>iflag</code> — initarg: <code>:iflag<!-- /@w --></code>; reader: <code>sb-posix:termios-iflag<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:termios-iflag)<!-- /@w --></code>

               <p>Input modes. 
</p></li><li><code>oflag</code> — initarg: <code>:oflag<!-- /@w --></code>; reader: <code>sb-posix:termios-oflag<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:termios-oflag)<!-- /@w --></code>

               <p>Output modes. 
</p></li><li><code>cflag</code> — initarg: <code>:cflag<!-- /@w --></code>; reader: <code>sb-posix:termios-cflag<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:termios-cflag)<!-- /@w --></code>

               <p>Control modes. 
</p></li><li><code>lflag</code> — initarg: <code>:lflag<!-- /@w --></code>; reader: <code>sb-posix:termios-lflag<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:termios-lflag)<!-- /@w --></code>

               <p>Local modes. 
</p></li><li><code>cc</code> — initarg: <code>:cc<!-- /@w --></code>; reader: <code>sb-posix:termios-cc<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:termios-cc)<!-- /@w --></code>

               <p>Control characters. 
</p></li></ul>

             <p>Instances of this class represent I/O characteristics of the terminal. 
</p></blockquote></div>

     </li><li>timeval
<a name="Class-sb_002dposix_003atimeval"></a>

     <div class="defun">
— Class: <b>timeval [sb-posix]</b><var><a name="index-g_t_0040sbposix_007btimeval_007d-662"></a></var><br>
<blockquote> <p>Class precedence list: <code>timeval, standard-object, t</code>

             </p><p>Slots:
               </p><ul>
<li><code>sec</code> — initarg: <code>:tv-sec<!-- /@w --></code>; reader: <code>sb-posix:timeval-sec<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:timeval-sec)<!-- /@w --></code>

               <p>Seconds. 
</p></li><li><code>usec</code> — initarg: <code>:tv-usec<!-- /@w --></code>; reader: <code>sb-posix:timeval-usec<!-- /@w --></code>; writer: <code>(setf&nbsp;sb-posix:timeval-usec)<!-- /@w --></code>

               <p>Microseconds. 
</p></li></ul>

             <p>Instances of this class represent time values. 
</p></blockquote></div>
     </li></ul>

<div class="node">
<a name="Functions-with-idiosyncratic-bindings"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#sb_002dposix">sb-posix</a>

</div>

<h4 class="subsection">16.6.6 Functions with idiosyncratic bindings</h4>

<p>A few functions in sb-posix don't correspond directly to their C
counterparts.

     </p><ul>
<li>getcwd
<a name="Function-sb_002dposix_003agetcwd"></a>

     <div class="defun">
— Function: <b>getcwd [sb-posix]</b><var><a name="index-g_t_0040sbposix_007bgetcwd_007d-663"></a></var><br>
<blockquote> <p>Returns the process's current working directory as a string. 
</p></blockquote></div>
     </li><li>readlink
<a name="Function-sb_002dposix_003areadlink"></a>

     <div class="defun">
— Function: <b>readlink [sb-posix]</b><var> pathspec<a name="index-g_t_0040sbposix_007breadlink_007d-664"></a></var><br>
<blockquote> <p>Returns the resolved target of a symbolic link as a string. 
</p></blockquote></div>
     </li><li>syslog
<a name="Function-sb_002dposix_003asyslog"></a>

     <div class="defun">
— Function: <b>syslog [sb-posix]</b><var> priority format &amp;rest args<a name="index-g_t_0040sbposix_007bsyslog_007d-665"></a></var><br>
<blockquote> <p>Send a message to the syslog facility, with severity level
<code>priority</code>.  The message will be formatted as by <code>cl:format</code> (rather
than C's printf) with format string <code>format</code> and arguments <code>args</code>. 
</p></blockquote></div>
     </li></ul>

<div class="node">
<a name="sb-queue"></a>
<a name="sb_002dqueue"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#sb_002drotate_002dbyte">sb-rotate-byte</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002dposix">sb-posix</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.7 sb-queue</h3>

<p><a name="index-Queue_002c-FIFO-666"></a>
Since SBCL 1.0.38, the <code>sb-queue</code> module has been merged into the
<code>sb-concurrency</code> module (see <a href="#sb_002dconcurrency">sb-concurrency</a>.)

</p><div class="node">
<a name="sb-rotate-byte"></a>
<a name="sb_002drotate_002dbyte"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#sb_002dqueue">sb-queue</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Contributed-Modules">Contributed Modules</a>

</div>

<h3 class="section">16.8 sb-rotate-byte</h3>

<p><a name="index-Modular-arithmetic-667"></a><a name="index-Arithmetic_002c-modular-668"></a><a name="index-Arithmetic_002c-hardware-669"></a>
The <code>sb-rotate-byte</code> module offers an interface to bitwise
rotation, with an efficient implementation for operations which can be
performed directly using the platform's arithmetic routines.  It
implements the specification at
<a href="http://www.cliki.net/ROTATE-BYTE">http://www.cliki.net/ROTATE-BYTE</a>. 
<!-- FIXME: except when someone scribbles all over it.  Hmm. -->

   </p><p>Bitwise rotation is a component of various cryptographic or hashing
algorithms: MD5, SHA-1, etc.; often these algorithms are specified on
32-bit rings.  [FIXME cite cite cite].

   </p><p><a name="Function-sb_002drotate_002dbyte_003arotate_002dbyte"></a>

</p><div class="defun">
— Function: <b>rotate-byte [sb-rotate-byte]</b><var> count bytespec integer<a name="index-g_t_0040sbrotatebyte_007brotate_002dbyte_007d-670"></a></var><br>
<blockquote><p>Rotates a field of bits within <code>integer</code>; specifically, returns an
integer that contains the bits of <code>integer</code> rotated <code>count</code> times
leftwards within the byte specified by <code>bytespec</code>, and elsewhere
contains the bits of <code>integer</code>. 
</p></blockquote></div>

<div class="node">
<a name="Deprecation"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Concept-Index">Concept Index</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Contributed-Modules">Contributed Modules</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="chapter">17 Deprecation</h2>

<p>In order to support evolution of interfaces in SBCL as well as in user
code, SBCL allows declaring functions, variables and types as
deprecated. Users of deprecated things are notified by means of warnings
while the deprecated thing in question is still available.

   </p><p>This chapter documents the interfaces for being notified when using
deprecated thing and declaring things as deprecated, the deprecation
process used for SBCL interfaces, and lists legacy interfaces in various
stages of deprecation.

   </p><p><dfn>Deprecation</dfn> in this context should not be confused with those
things the ANSI Common Lisp standard calls <dfn>deprecated</dfn>: the
entirety of ANSI CL is supported by SBCL, and none of those interfaces
are subject to censure.

</p><ul class="menu">
<li><a accesskey="1" href="#Why-Deprecate_003f">Why Deprecate?</a>
</li><li><a accesskey="2" href="#The-Deprecation-Pipeline">The Deprecation Pipeline</a>
</li><li><a accesskey="3" href="#Deprecation-Conditions">Deprecation Conditions</a>
</li><li><a accesskey="4" href="#Introspecting-Deprecation-Information">Introspecting Deprecation Information</a>
</li><li><a accesskey="5" href="#Deprecation-Declaration">Deprecation Declaration</a>
</li><li><a accesskey="6" href="#Deprecation-Examples">Deprecation Examples</a>
</li><li><a accesskey="7" href="#Deprecated-Interfaces-in-SBCL">Deprecated Interfaces in SBCL</a>
</li></ul>

<div class="node">
<a name="Why-Deprecate?"></a>
<a name="Why-Deprecate_003f"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#The-Deprecation-Pipeline">The Deprecation Pipeline</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.1 Why Deprecate?</h3>

<p><a name="index-Why-Deprecate_003f-671"></a>
While generally speaking we try to keep SBCL changes as backwards
compatible as feasible, there are situations when existing interfaces
are deprecated:

     </p><ul>
<li><strong>Broken Interfaces</strong>

     <p>Sometimes it turns out that an interface is sufficiently misdesigned
that fixing it would be worse than deprecating it and replacing it
with another.

     </p><p>This is typically the case when fixing the interface would change its
semantics in ways that could break user code subtly: in such cases we
may end up considering the obvious breakage caused by deprecation to
be preferable.

     </p><p>Another example are functions or macros whose current signature makes
them hard or impossible to extend in the future: backwards compatible
extensions would either make the interface intolerably hairy, or are
sometimes outright impossible.

     </p></li><li><strong>Internal Interfaces</strong>

     <p>SBCL has several internal interfaces that were never meant to be used
in user code – or at least never meant to be used in user code
unwilling to track changes to SBCL internals.

     </p><p>Ideally we'd like to be free to refactor our own internals as we
please, without even going through the hassle of deprecating things. 
Sometimes, however, it turns out that our internal interfaces have
several external users who aren't using them advisedly, but due to
misunderstandings regarding their status or stability.

     </p><p>Consider a deprecated internal interface a reminder for SBCL
maintainers not to delete the thing just yet, even though it is seems
unused – because it has external users.

     </p><p>When internal interfaces are deprecated we try our best to provide
supported alternatives.

     </p></li><li><strong>Aesthetics &amp; Ease of Maintenance</strong>

     <p>Sometimes an interface isn't broken or internal, but just inconsistent
somehow.

     </p><p>This mostly happens only with historical interfaces inherited from
CMUCL which often haven't been officially supported in SBCL before, or
with new extensions to SBCL that haven't been around for very long in
the first place.

     </p><p>The alternative would be to keep the suboptimal version around
forever, possibly alongside an improved version. Sometimes we may do
just that, but because every line of code comes with a maintenance
cost, sometimes we opt to deprecate the suboptimal version instead:
SBCL doesn't have infinite developer resources.

     </p><p>We also believe that sometimes cleaning out legacy interfaces helps
keep the whole system more comprehensible to users, and makes
introspective tools such as <code>apropos</code> more useful.

   </p></li></ul>

<div class="node">
<a name="The-Deprecation-Pipeline"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Deprecation-Conditions">Deprecation Conditions</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Why-Deprecate_003f">Why Deprecate?</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.2 The Deprecation Pipeline</h3>

<p><a name="index-The-Deprecation-Pipeline-672"></a>
SBCL uses a <dfn>deprecation pipeline</dfn> with multiple stages: as time
goes by, deprecated things move from earlier stages of deprecation to
later stages before finally being removed. The intention is making users
aware of necessary changes early but allowing a migration to new
interfaces at a reasonable pace.

   </p><p>Deprecation proceeds in three stages, each lasting approximately a
year. In some cases it might move slower or faster, but one year per
stage is what we aim at in general. During each stage warnings (and
errors) of increasing severity are signaled, which note that the
interface is deprecated, and point users towards any replacements when
applicable.

     </p><ol start="1" type="1">

     <li><strong>Early Deprecation</strong>

     <p>During early deprecation the interface is kept in working
condition. However, when a thing in this deprecation stage is used, an
early-deprecation-warning [sb-ext], which is a style-warning [cl], is
signaled at compile-time.

     </p><p>The internals may change at this stage: typically because the interface
is re-implemented on top of its successor. While we try to keep things
as backwards-compatible as feasible (taking maintenance costs into account),
sometimes semantics change slightly.

     </p><p>For example, when the spinlock API was deprecated, spinlock objects ceased
to exist, and the whole spinlock API became a synonym for the mutex
API – so code using the spinlock API continued working, but silently
switched to mutexes instead. However, if someone relied on

     </p><p><code>(typep lock 'spinlock)</code>

     </p><p>returning <code>NIL</code> for a mutexes, trouble could ensue.

     </p></li><li><strong>Late Deprecation</strong>

     <p>During late deprecation the interface remains as it was during early
deprecation, but the compile-time warning is upgraded: when a thing in
this deprecation stage is used, a late-deprecation-warning [sb-ext],
which is a full warning [cl], is signaled at compile-time.

     </p></li><li><strong>Final Deprecation</strong>

     <p>During final deprecation the symbols still exist. However, when a thing
in this deprecation stage is used, a final-deprecation-warning [sb-ext],
which is a full warning [cl], is signaled at compile-time and an
error [cl] is signaled at run-time.

     </p></li><li><strong>After Final Deprecation</strong>

     <p>The interface is deleted entirely.

        </p></li></ol>

<div class="node">
<a name="Deprecation-Conditions"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Introspecting-Deprecation-Information">Introspecting Deprecation Information</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#The-Deprecation-Pipeline">The Deprecation Pipeline</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.3 Deprecation Conditions</h3>

<p><a name="index-Deprecation-Conditions-673"></a>
deprecation-condition [sb-ext] is the superclass of all
deprecation-related warning and error conditions. All common slots and
readers are defined in this condition class.

   </p><p><a name="Condition-sb_002dext_003adeprecation_002dcondition"></a>

</p><div class="defun">
— Condition: <b>deprecation-condition [sb-ext]</b><var><a name="index-g_t_0040sbext_007bdeprecation_002dcondition_007d-674"></a></var><br>
<blockquote><p>Class precedence list: <code>deprecation-condition, condition, t</code>

        </p><p>Superclass for deprecation-related error and warning
conditions. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003aearly_002ddeprecation_002dwarning"></a>

</p><div class="defun">
— Condition: <b>early-deprecation-warning [sb-ext]</b><var><a name="index-g_t_0040sbext_007bearly_002ddeprecation_002dwarning_007d-675"></a></var><br>
<blockquote><p>Class precedence list: <code>early-deprecation-warning, style-warning, warning, deprecation-condition, condition, t</code>

        </p><p>This warning is signaled when the use of a variable,
function, type, etc. in <code>:early</code> deprecation is detected at
compile-time. The use will work at run-time with no warning or
error. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003alate_002ddeprecation_002dwarning"></a>

</p><div class="defun">
— Condition: <b>late-deprecation-warning [sb-ext]</b><var><a name="index-g_t_0040sbext_007blate_002ddeprecation_002dwarning_007d-676"></a></var><br>
<blockquote><p>Class precedence list: <code>late-deprecation-warning, warning, deprecation-condition, condition, t</code>

        </p><p>This warning is signaled when the use of a variable,
function, type, etc. in <code>:late</code> deprecation is detected at
compile-time. The use will work at run-time with no warning or
error. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003afinal_002ddeprecation_002dwarning"></a>

</p><div class="defun">
— Condition: <b>final-deprecation-warning [sb-ext]</b><var><a name="index-g_t_0040sbext_007bfinal_002ddeprecation_002dwarning_007d-677"></a></var><br>
<blockquote><p>Class precedence list: <code>final-deprecation-warning, warning, deprecation-condition, condition, t</code>

        </p><p>This warning is signaled when the use of a variable,
function, type, etc. in <code>:final</code> deprecation is detected at
compile-time. An error will be signaled at run-time. 
</p></blockquote></div>

   <p><a name="Condition-sb_002dext_003adeprecation_002derror"></a>

</p><div class="defun">
— Condition: <b>deprecation-error [sb-ext]</b><var><a name="index-g_t_0040sbext_007bdeprecation_002derror_007d-678"></a></var><br>
<blockquote><p>Class precedence list: <code>deprecation-error, error, serious-condition, deprecation-condition, condition, t</code>

        </p><p>This error is signaled at run-time when an attempt is made to use
a thing that is in <code>:final</code> deprecation, i.e. call a function or access
a variable. 
</p></blockquote></div>

<div class="node">
<a name="Introspecting-Deprecation-Information"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Deprecation-Declaration">Deprecation Declaration</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Deprecation-Conditions">Deprecation Conditions</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.4 Introspecting Deprecation Information</h3>

<p><a name="index-Introspecting-Deprecation-Information-679"></a><!-- TODO @findex @sbcltl{function-information} -->
<!-- TODO @findex @sbcltl{variable-information} -->

   </p><p>The deprecation status of functions and variables can be inspected using
the <code>sb-cltl2:function-information</code> and
<code>sb-cltl2:variable-information</code> functions provided by the
<code>sb-cltl2</code> contributed module.

</p><div class="node">
<a name="Deprecation-Declaration"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Deprecation-Examples">Deprecation Examples</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Introspecting-Deprecation-Information">Introspecting Deprecation Information</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.5 Deprecation Declaration</h3>

<p><a name="index-Deprecation-Declaration-680"></a><a name="index-g_t_0040sbext_007bdeprecated_007d-681"></a>
The <code>sb-ext:deprecated</code> declaration can be used to declare objects
in various namespaces<a rel="footnote" href="#fn-11" name="fnd-11"><sup>11</sup></a> as deprecated.

</p><div class="defun">
— Declaration: <b>deprecated [sb-ext]</b><var><a name="index-g_t_0040sbext_007bdeprecated_007d-682"></a></var><br>
<blockquote>
        <p>Syntax:
     </p><pre class="example">          <code>sb-ext:deprecated</code> stage since {object-clause}*
          
          stage ::= {:early | :late | :final}
          
          since ::= {<var>version</var> | (<var>software</var> <var>version</var>)}
          
          object-clause ::= (namespace <var>name</var> [:replacement <var>replacement</var>])
          
          namespace ::= {cl:variable | cl:function | cl:type}
</pre>
        <p class="noindent">were <var>name</var> is the name of the deprecated thing,
<var>version</var> and <var>software</var> are strings describing the version in
which the thing has been deprecated and <var>replacement</var> is a name or a
list of names designating things that should be used instead of the
deprecated thing.

        </p><p>Currently the following namespaces are supported:

          </p><dl>
<dt><code>cl:function</code></dt><dd>Declare functions, compiler-macros or macros as deprecated.

          <blockquote>
<b>note:</b> When declaring a function to be in <code>:final</code> deprecation, there
should be no actual definition of the function as the declaration emits
a stub function that signals a deprecation-error [sb-ext] at run-time
when called. 
</blockquote>

          <br></dd><dt><code>cl:variable</code></dt><dd>Declare special and global variables, constants and symbol-macros as
deprecated.

          <blockquote>
<b>note:</b> When declaring a variable to be in <code>:final</code> deprecation, there
should be no actual definition of the variable as the declaration emits
a symbol-macro that signals a <code>sb-ext:deprecation-error</code> at
run-time when accessed. 
</blockquote>

          <br></dd><dt><code>cl:type</code></dt><dd>Declare named types (i.e. defined via <code>deftype</code>), standard classes,
structure classes and condition classes as deprecated.

        </dd></dl>
        <p></p></blockquote></div>

<div class="node">
<a name="Deprecation-Examples"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Deprecated-Interfaces-in-SBCL">Deprecated Interfaces in SBCL</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Deprecation-Declaration">Deprecation Declaration</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.6 Deprecation Examples</h3>

<p><a name="index-Deprecation-Examples-683"></a>
Marking functions as deprecated:
</p><pre class="lisp">     (defun foo ())
     (defun bar ())
     (declaim (deprecated :early ("my-system" "1.2.3")
                          (function foo :replacement bar)))
     
     ;; Remember: do not define the actual function or variable in case of
     ;; :final deprecation:
     (declaim (deprecated :final ("my-system" "1.2.3")
                          (function fez :replacement whoop)))
</pre>
   <p class="noindent">Attempting to use the deprecated functions:
</p><pre class="lisp">     (defun baz ()
       (foo))
     | STYLE-WARNING: The function CL-USER::FOO has been deprecated...
     =&gt; BAZ
     (baz)
     =&gt; NIL ; no error
     
     (defun danger ()
       (fez))
     | WARNING: The function CL-USER::FEZ has been deprecated...
     =&gt; DANGER
     (danger)
     |- ERROR: The function CL-USER::FEZ has been deprecated...
</pre>
   <div class="node">
<a name="Deprecated-Interfaces-in-SBCL"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Deprecation-Examples">Deprecation Examples</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Deprecation">Deprecation</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h3 class="section">17.7 Deprecated Interfaces in SBCL</h3>

<p>This sections lists legacy interfaces in various stages of deprecation.

</p><h4 class="subsection">17.7.1 List of Deprecated Interfaces</h4>

<h5 class="subsubsection">17.7.1.1 Early Deprecation</h5>

     <ul>
<li><strong>SOCKINT::WIN32-*</strong>

     <p>Deprecated in favor of the corresponding prefix-less functions
(e.g. <code>sockint::bind</code> replaces <code>sockint::win32-bind</code>) as of
1.2.10 in March 2015. Expected to move into late deprecation in August
2015.

     </p></li><li><strong>SB-EXT:QUIT</strong>

     <p>Deprecated in favor of <code>sb-ext:exit</code> as of 1.0.56.55 in May 2012. 
Expected to move into late deprecation in May 2013.

     </p><p>The design of <code>sb-ext:quit</code> proved too broken to fix in a
backwards-compatible manner, so it had to be deprecated and replaced.

     </p><p>Problems with it were manifold: when called in the main thread it
cause the entire process to exit. When called in another thread with
<code>:recklessly-p</code> it also caused the entire process to exit. 
However, when called in another thread without <code>:recklessly-p</code> it
instead caused that thread to terminate abnormally without terminating
the process. Its behaviour versus other threads than the one it was
called in was also underspecified, and dependent on things such as the
current session. Any conceivable change that would have made it sane
would also have silently broken code that depended on the old
behaviour.

     </p><p><strong>Remedy</strong>

     </p><p>For code needing to work with legacy SBCLs, if you were calling
<code>quit</code> with <code>:recklessly-p t</code>, use

     </p><pre class="sp">     
     </pre>
     <pre class="lisp">          (defun system-exit (&amp;optional (code 0))
            (alien-funcall (extern-alien "exit" (function void int)) code))
</pre>
     <pre class="sp">     
     </pre>
     
instead. In modern SBCLs simply call either <code>sb-posix:exit</code> or
<code>sb-ext:exit</code>.

     <p>If you were calling it without <code>:recklessly-p</code>, be advised
that your code may not function as expected when called from threads
other than the main one (see above) – in any case, you can support
legacy SBCLs using the following conditionalization:

     </p><pre class="sp">     
     </pre>
     <pre class="lisp">          (defun lisp-exit (&amp;key (code 0) abort)
            #+#.(cl:if (cl:find-symbol "EXIT" :sb-ext) '(and) '(or))
            ;; Assuming process exit is what is desired -- if thread termination
            ;; is intended, use SB-THREAD:ABORT-THREAD instead.
            (sb-ext:exit :code code :abort abort)
            #-#.(cl:if (cl:find-symbol "EXIT" :sb-ext) '(and) '(or))
            (sb-ext:quit :unix-status code :recklessly-p abort))
</pre>
     <pre class="sp">     
     </pre>
     <pre class="sp">     
     </pre>
     </li><li><strong>SB-UNIX:UNIX-EXIT</strong>

     <p>Deprecated as of 1.0.56.55 in May 2012. Expected to move into late
deprecation in May 2013.

     </p><p>When the SBCL process termination was refactored as part of changes that
led to <code>sb-ext:quit</code> being deprecated, <code>sb-unix:unix-exit</code>
ceased to be used internally. Since <code>SB-UNIX</code> is an internal package
not intended for user code to use, and since we're slowly in the process
of refactoring things to be less Unix-oriented, <code>sb-unix:unix-exit</code>
was initially deleted as it was no longer used. Unfortunately it became
apparent that it was used by several external users, so it was re-instated
in deprecated form.

     </p><p>While the cost of keeping <code>sb-unix:unix-exit</code> indefinitely is
trivial, the ability to refactor our internals is important, so its
deprecation was taken as an opportunity to highlight that
<code>SB-UNIX</code> is an internal package and <code>SB-POSIX</code> should be
used by user-programs instead – or alternatively calling the foreign
function directly if the desired interface doesn't for some reason
exist in <code>SB-POSIX</code>.

     </p><p><strong>Remedy</strong>

     </p><p>For code needing to work with legacy SBCLs, use e.g. <code>system-exit</code>
as show above in remedies for <code>sb-ext:quit</code>. In modern SBCLs
simply call either <code>sb-posix:exit</code> or <code>sb-ext:exit</code> with
appropriate arguments.

     </p><pre class="sp">     
     </pre>
     </li><li><strong>SB-C::MERGE-TAIL-CALLS Compiler Policy</strong>

     <p>Deprecated as of 1.0.53.74 in November 2011. Expected to move into
late deprecation in November 2012.

     </p><p>This compiler policy was never functional: SBCL has always merged tail
calls when it could, regardless of this policy setting. (It was also
never officially supported, but several code-bases have historically
used it.)

     </p><p><strong>Remedy</strong>

     </p><p>Simply remove the policy declarations. They were never necessary: SBCL
always merged tail-calls when possible. To disable tail merging,
structure the code to avoid the tail position instead.

     </p><pre class="sp">     
     </pre>
     </li><li><strong>Spinlock API</strong>

     <p>Deprecated as of 1.0.53.11 in August 2011. Expected to move into late
deprecation in August 2012.

     </p><p>Spinlocks were an internal interface, but had a number of external users
and were hence deprecated instead of being simply deleted.

     </p><p>Affected symbols: <code>sb-thread::spinlock</code>,
<code>sb-thread::make-spinlock</code>, <code>sb-thread::with-spinlock</code>,
<code>sb-thread::with-recursive-spinlock</code>,
<code>sb-thread::get-spinlock</code>, <code>sb-thread::release-spinlock</code>,
<code>sb-thread::spinlock-value</code>, and <code>sb-thread::spinlock-name</code>.

     </p><p><strong>Remedy</strong>

     </p><p>Use the mutex API instead, or implement spinlocks suiting your needs
on top of <code>sb-ext:compare-and-swap</code>,
<code>sb-ext:spin-loop-hint</code>, etc.

     </p></li><li><strong>SOCKINT::HANDLE-&gt;FD</strong>, <strong>SOCKINT::FD-&gt;HANDLE</strong>

     <p>Internally deprecated in 2012. Declared deprecated as of 1.2.10 in March
2015. Expected to move into final deprecation in August 2015.

</p></li></ul>

<h5 class="subsubsection">17.7.1.2 Late Deprecation</h5>

     <ul>
<li><strong>SB-THREAD:JOIN-THREAD-ERROR-THREAD and SB-THREAD:INTERRUPT-THREAD-ERROR-THREAD</strong>

     <p>Deprecated in favor of <code>sb-thread:thread-error-thread</code> as of
1.0.29.17 in June 2009. Expected to move into final deprecation in
June 2012.

     </p><p><strong>Remedy</strong>

     </p><p>For code that needs to support legacy SBCLs, use e.g.:

     </p><pre class="sp">     
     </pre>
     <pre class="lisp">          (defun get-thread-error-thread (condition)
            #+#.(cl:if (cl:find-symbol "THREAD-ERROR-THREAD" :sb-thread)
                       '(and) '(or))
            (sb-thread:thread-error-thread condition)
            #-#.(cl:if (cl:find-symbol "THREAD-ERROR-THREAD" :sb-thread)
                       '(and) '(or))
            (etypecase condition
             (sb-thread:join-thread-error
              (sb-thread:join-thread-error-thread condition))
             (sb-thread:interrupt-thread-error
              (sb-thread:interrupt-thread-error-thread condition))))
</pre>
     <pre class="sp">     
     </pre>
     <pre class="sp">     
     </pre>
     </li><li><strong>SB-INTROSPECT:FUNCTION-ARGLIST</strong>

     <p>Deprecated in favor of <code>sb-introspect:function-lambda-list</code> as of
1.0.24.5 in January 2009. Expected to move into final deprecation in
January 2012.

     </p><p>Renamed for consistency and aesthetics. Functions have lambda-lists,
not arglists.

     </p><p><strong>Remedy</strong>

     </p><p>For code that needs to support legacy SBCLs, use e.g.:

     </p><pre class="sp">     
     </pre>
     <pre class="lisp">          (defun get-function-lambda-list (function)
            #+#.(cl:if (cl:find-symbol "FUNCTION-LAMBDA-LIST" :sb-introspect)
                       '(and) '(or))
            (sb-introspect:function-lambda-list function)
            #-#.(cl:if (cl:find-symbol "FUNCTION-LAMBDA-LIST" :sb-introspect)
                       '(and) '(or))
            (sb-introspect:function-arglist function))
</pre>
     <pre class="sp">     
     </pre>
     <pre class="sp">     
     </pre>
     </li><li><strong>Stack Allocation Policies</strong>

     <p>Deprecated in favor of <code>sb-ext:*stack-allocate-dynamic-extent*</code>
as of 1.0.19.7 in August 2008, and are expected to be removed in
August 2012.

     </p><p>Affected symbols: <code>sb-c::stack-allocate-dynamic-extent</code>,
<code>sb-c::stack-allocate-vector</code>, and
<code>sb-c::stack-allocate-value-cells</code>.

     </p><p>These compiler policies were never officially supported, and turned
out the be a flawed design.

     </p><p><strong>Remedy</strong>

     </p><p>For code that needs stack-allocation in legacy SBCLs, conditionalize
using:

     </p><pre class="sp">     
     </pre>
     <pre class="lisp">          #-#.(cl:if (cl:find-symbol "*STACK-ALLOCATE-DYNAMIC-EXTENT*" :sb-ext)
                     '(and) '(or))
          (declare (optimize sb-c::stack-allocate-dynamic-extent))
</pre>
     <pre class="sp">     
     </pre>
     
However, unless stack allocation is essential, we recommend simply
removing these declarations. Refer to documentation on
<code>sb-ext:*stack-allocate-dynamic*</code> for details on stack allocation
control in modern SBCLs.

     <pre class="sp">     
     </pre>
     </li><li><strong>SB-SYS:OUTPUT-RAW-BYTES</strong>

     <p>Deprecated as of 1.0.8.16 in June 2007. Expected to move into final
deprecation in June 2012.

     </p><p>Internal interface with some external users. Never officially
supported, deemed unnecessary in presence of <code>write-sequence</code> and
bivalent streams.

     </p><p><strong>Remedy</strong>

     </p><p>Use streams with element-type <code>(unsigned-byte 8)</code>
or <code>:default</code> – the latter allowing both binary and
character IO – in conjunction with <code>write-sequence</code>.

</p></li></ul>

<h5 class="subsubsection">17.7.1.3 Final Deprecation</h5>

<p>No interfaces are currently in final deprecation.

</p><h4 class="subsection">17.7.2 Historical Interfaces</h4>

<p>The following is a partial list of interfaces present in historical
versions of SBCL, which have since then been deleted.

     </p><ul>
<li><strong>SB-KERNEL:INSTANCE-LAMBDA</strong>

     <p>Historically needed for CLOS code. Deprecated as of 0.9.3.32 in August
2005. Deleted as of 1.0.47.8 in April 2011. Plain <code>lambda</code> can be
used where <code>sb-kernel:instance-lambda</code> used to be needed.

     </p><pre class="sp">     
     </pre>
     </li><li><strong>SB-ALIEN:DEF-ALIEN-ROUTINE, SB-ALIEN:DEF-ALIEN-VARIABLE, SB-ALIEN:DEF-ALIEN-TYPE</strong>

     <p>Inherited from CMUCL, naming convention not consistent with preferred
SBCL style. Deprecated as of 0.pre7.90 in December 2001. Deleted as of
1.0.9.17 in September 2007. Replaced by
<code>sb-alien:define-alien-routine</code>,
<code>sb-alien:define-alien-variable</code>, and
<code>sb-alien:define-alien-type</code>.

   </p></li></ul>

<div class="node">
<a name="Concept-Index"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Function-Index">Function Index</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Deprecation">Deprecation</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="appendix">Appendix A Concept Index</h2>

<ul class="index-cp" compact="compact">
<li><a href="#index-Actual-Source-37">Actual Source</a>: <a href="#The-Original-and-Actual-Source">The Original and Actual Source</a></li>
<li><a href="#index-Actual-Source-35">Actual Source</a>: <a href="#The-Parts-of-a-Compiler-Diagnostic">The Parts of a Compiler Diagnostic</a></li>
<li><a href="#index-Arithmetic_002c-hardware-669">Arithmetic, hardware</a>: <a href="#sb_002drotate_002dbyte">sb-rotate-byte</a></li>
<li><a href="#index-Arithmetic_002c-hardware-152">Arithmetic, hardware</a>: <a href="#Modular-arithmetic">Modular arithmetic</a></li>
<li><a href="#index-Arithmetic_002c-modular-668">Arithmetic, modular</a>: <a href="#sb_002drotate_002dbyte">sb-rotate-byte</a></li>
<li><a href="#index-Arithmetic_002c-modular-151">Arithmetic, modular</a>: <a href="#Modular-arithmetic">Modular arithmetic</a></li>
<li><a href="#index-Availability-of-debug-variables-87">Availability of debug variables</a>: <a href="#Variable-Value-Availability">Variable Value Availability</a></li>
<li><a href="#index-Block-compilation_002c-debugger-implications-73">Block compilation, debugger implications</a>: <a href="#Entry-Point-Details">Entry Point Details</a></li>
<li><a href="#index-Block_002c-basic-93">Block, basic</a>: <a href="#Source-Location-Availability">Source Location Availability</a></li>
<li><a href="#index-Block_002c-start-location-94">Block, start location</a>: <a href="#Source-Location-Availability">Source Location Availability</a></li>
<li><a href="#index-Cleanup_002c-stack-frame-kind-76">Cleanup, stack frame kind</a>: <a href="#Entry-Point-Details">Entry Point Details</a></li>
<li><a href="#index-Code-Coverage-634">Code Coverage</a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-Compatibility-with-other-Lisps-47">Compatibility with other Lisps</a>: <a href="#Getting-Existing-Programs-to-Run">Getting Existing Programs to Run</a></li>
<li><a href="#index-Compile-time-type-errors-51">Compile time type errors</a>: <a href="#Type-Errors-at-Compile-Time">Type Errors at Compile Time</a></li>
<li><a href="#index-Compiler-Diagnostic-Severity-24">Compiler Diagnostic Severity</a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
<li><a href="#index-Compiler-messages-19">Compiler messages</a>: <a href="#Diagnostic-Messages">Diagnostic Messages</a></li>
<li><a href="#index-Concurrency-590">Concurrency</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Debug-optimization-quality-96">Debug optimization quality</a>: <a href="#Debugger-Policy-Control">Debugger Policy Control</a></li>
<li><a href="#index-Debug-optimization-quality-92">Debug optimization quality</a>: <a href="#Source-Location-Availability">Source Location Availability</a></li>
<li><a href="#index-Debug-optimization-quality-89">Debug optimization quality</a>: <a href="#Variable-Value-Availability">Variable Value Availability</a></li>
<li><a href="#index-Debug-variables-83">Debug variables</a>: <a href="#Variable-Access">Variable Access</a></li>
<li><a href="#index-Debugger-62">Debugger</a>: <a href="#Debugger">Debugger</a></li>
<li><a href="#index-debugger_002c-disabling-128">debugger, disabling</a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-debugger_002c-enabling-127">debugger, enabling</a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-declaration_002c-_0040code_007bdynamic_002dextent_007d-138">declaration, <code>dynamic-extent</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-Declarations-453">Declarations</a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-Deprecation-Conditions-673">Deprecation Conditions</a>: <a href="#Deprecation-Conditions">Deprecation Conditions</a></li>
<li><a href="#index-Deprecation-Declaration-680">Deprecation Declaration</a>: <a href="#Deprecation-Declaration">Deprecation Declaration</a></li>
<li><a href="#index-Deprecation-Examples-683">Deprecation Examples</a>: <a href="#Deprecation-Examples">Deprecation Examples</a></li>
<li><a href="#index-disabling-debugger-129">disabling debugger</a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-disabling-ldb-132">disabling ldb</a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-disabling-ldb-14">disabling ldb</a>: <a href="#Runtime-Options">Runtime Options</a></li>
<li><a href="#index-g_t_0040code_007bdynamic_002dextent_007d-declaration-137"><code>dynamic-extent</code> declaration</a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-Efficiency-135">Efficiency</a>: <a href="#Efficiency">Efficiency</a></li>
<li><a href="#index-Entry-points_002c-external-72">Entry points, external</a>: <a href="#Entry-Point-Details">Entry Point Details</a></li>
<li><a href="#index-Errors_002c-run_002dtime-82">Errors, run-time</a>: <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a></li>
<li><a href="#index-Existing-programs_002c-to-run-45">Existing programs, to run</a>: <a href="#Getting-Existing-Programs-to-Run">Getting Existing Programs to Run</a></li>
<li><a href="#index-External-entry-points-71">External entry points</a>: <a href="#Entry-Point-Details">Entry Point Details</a></li>
<li><a href="#index-External-formats-401">External formats</a>: <a href="#External-Formats">External Formats</a></li>
<li><a href="#index-External-formats-371">External formats</a>: <a href="#Foreign-Type-Specifiers">Foreign Type Specifiers</a></li>
<li><a href="#index-External_002c-stack-frame-kind-74">External, stack frame kind</a>: <a href="#Entry-Point-Details">Entry Point Details</a></li>
<li><a href="#index-Fast-Read-Lock-624">Fast Read Lock</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Finalization-175">Finalization</a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-Foreign-Function-Interface_002c-generation-642">Foreign Function Interface, generation</a>: <a href="#sb_002dgrovel">sb-grovel</a></li>
<li><a href="#index-Frlock-623">Frlock</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Function_002c-tracing-113">Function, tracing</a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-Garbage-collection-172">Garbage collection</a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-Garbage-Collection_002c-conservative-4">Garbage Collection, conservative</a>: <a href="#History-and-Implementation-of-SBCL">History and Implementation of SBCL</a></li>
<li><a href="#index-Garbage-Collection_002c-generational-3">Garbage Collection, generational</a>: <a href="#History-and-Implementation-of-SBCL">History and Implementation of SBCL</a></li>
<li><a href="#index-Gate-614">Gate</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Hash-tables-356">Hash tables</a>: <a href="#Hash-Table-Extensions">Hash Table Extensions</a></li>
<li><a href="#index-Hashing_002c-cryptographic-643">Hashing, cryptographic</a>: <a href="#sb_002dmd5">sb-md5</a></li>
<li><a href="#index-Inline-expansion-98">Inline expansion</a>: <a href="#Debugger-Policy-Control">Debugger Policy Control</a></li>
<li><a href="#index-Inline-expansion-56">Inline expansion</a>: <a href="#Open-Coding-and-Inline-Expansion">Open Coding and Inline Expansion</a></li>
<li><a href="#index-Interpreter-58">Interpreter</a>: <a href="#Interpreter">Interpreter</a></li>
<li><a href="#index-Interrupts-81">Interrupts</a>: <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a></li>
<li><a href="#index-Introspecting-Deprecation-Information-679">Introspecting Deprecation Information</a>: <a href="#Introspecting-Deprecation-Information">Introspecting Deprecation Information</a></li>
<li><a href="#index-ldb-12">ldb</a>: <a href="#Runtime-Options">Runtime Options</a></li>
<li><a href="#index-ldb-1">ldb</a>: <a href="#Reporting-Bugs">Reporting Bugs</a></li>
<li><a href="#index-ldb_002c-disabling-131">ldb, disabling</a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-ldb_002c-disabling-13">ldb, disabling</a>: <a href="#Runtime-Options">Runtime Options</a></li>
<li><a href="#index-ldb_002c-enabling-130">ldb, enabling</a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-Locations_002c-unknown-80">Locations, unknown</a>: <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a></li>
<li><a href="#index-Logical-pathnames-393">Logical pathnames</a>: <a href="#Lisp-Pathnames">Lisp Pathnames</a></li>
<li><a href="#index-Macroexpansion-39">Macroexpansion</a>: <a href="#The-Processing-Path">The Processing Path</a></li>
<li><a href="#index-Macroexpansion_002c-errors-during-53">Macroexpansion, errors during</a>: <a href="#Errors-During-Macroexpansion">Errors During Macroexpansion</a></li>
<li><a href="#index-Mailbox_002c-lock_002dfree-602">Mailbox, lock-free</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Messages_002c-Compiler-18">Messages, Compiler</a>: <a href="#Diagnostic-Messages">Diagnostic Messages</a></li>
<li><a href="#index-Modular-arithmetic-667">Modular arithmetic</a>: <a href="#sb_002drotate_002dbyte">sb-rotate-byte</a></li>
<li><a href="#index-Modular-arithmetic-150">Modular arithmetic</a>: <a href="#Modular-arithmetic">Modular arithmetic</a></li>
<li><a href="#index-Open_002dcoding-55">Open-coding</a>: <a href="#Open-Coding-and-Inline-Expansion">Open Coding and Inline Expansion</a></li>
<li><a href="#index-Operating-System-Interface-649">Operating System Interface</a>: <a href="#sb_002dposix">sb-posix</a></li>
<li><a href="#index-optimization-quality_002c-_0040code_007bsafety_007d-149">optimization quality, <code>safety</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-Optimize-declaration-97">Optimize declaration</a>: <a href="#Debugger-Policy-Control">Debugger Policy Control</a></li>
<li><a href="#index-Optional_002c-stack-frame-kind-75">Optional, stack frame kind</a>: <a href="#Entry-Point-Details">Entry Point Details</a></li>
<li><a href="#index-Original-Source-36">Original Source</a>: <a href="#The-Original-and-Actual-Source">The Original and Actual Source</a></li>
<li><a href="#index-Original-Source-33">Original Source</a>: <a href="#The-Parts-of-a-Compiler-Diagnostic">The Parts of a Compiler Diagnostic</a></li>
<li><a href="#index-Package_002dLocal-Nicknames-164">Package-Local Nicknames</a>: <a href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a></li>
<li><a href="#index-Packages_002c-locked-439">Packages, locked</a>: <a href="#Package-Locks">Package Locks</a></li>
<li><a href="#index-Pathnames-392">Pathnames</a>: <a href="#Pathnames">Pathnames</a></li>
<li><a href="#index-Pathnames_002c-logical-394">Pathnames, logical</a>: <a href="#Lisp-Pathnames">Lisp Pathnames</a></li>
<li><a href="#index-Policy_002c-debugger-95">Policy, debugger</a>: <a href="#Debugger-Policy-Control">Debugger Policy Control</a></li>
<li><a href="#index-Posix-651">Posix</a>: <a href="#sb_002dposix">sb-posix</a></li>
<li><a href="#index-Precise-type-checking-43">Precise type checking</a>: <a href="#Precise-Type-Checking">Precise Type Checking</a></li>
<li><a href="#index-Processing-Path-38">Processing Path</a>: <a href="#The-Processing-Path">The Processing Path</a></li>
<li><a href="#index-Processing-Path-34">Processing Path</a>: <a href="#The-Parts-of-a-Compiler-Diagnostic">The Parts of a Compiler Diagnostic</a></li>
<li><a href="#index-Profiling-571">Profiling</a>: <a href="#Profiling">Profiling</a></li>
<li><a href="#index-Profiling_002c-deterministic-572">Profiling, deterministic</a>: <a href="#Deterministic-Profiler">Deterministic Profiler</a></li>
<li><a href="#index-Profiling_002c-statistical-577">Profiling, statistical</a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-Queue_002c-FIFO-666">Queue, FIFO</a>: <a href="#sb_002dqueue">sb-queue</a></li>
<li><a href="#index-Queue_002c-lock_002dfree-592">Queue, lock-free</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Random-Number-Generation-362">Random Number Generation</a>: <a href="#Random-Number-Generation">Random Number Generation</a></li>
<li><a href="#index-Read-errors_002c-compiler-54">Read errors, compiler</a>: <a href="#Read-Errors">Read Errors</a></li>
<li><a href="#index-Read_002dEval_002dPrint-Loop-588">Read-Eval-Print Loop</a>: <a href="#sb_002daclrepl">sb-aclrepl</a></li>
<li><a href="#index-Reader-Extensions-161">Reader Extensions</a>: <a href="#Reader-Extensions">Reader Extensions</a></li>
<li><a href="#index-Recursion_002c-tail-78">Recursion, tail</a>: <a href="#Debug-Tail-Recursion">Debug Tail Recursion</a></li>
<li><a href="#index-REPL-589">REPL</a>: <a href="#sb_002daclrepl">sb-aclrepl</a></li>
<li><a href="#index-g_t_0040code_007bsafety_007d-optimization-quality-148"><code>safety</code> optimization quality</a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-Safety-optimization-quality-145">Safety optimization quality</a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-Safety-optimization-quality-42">Safety optimization quality</a>: <a href="#Declarations-as-Assertions">Declarations as Assertions</a></li>
<li><a href="#index-Sb_002dconcurrency-591">Sb-concurrency</a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-Semi_002dinline-expansion-99">Semi-inline expansion</a>: <a href="#Debugger-Policy-Control">Debugger Policy Control</a></li>
<li><a href="#index-Severity-of-compiler-messages-23">Severity of compiler messages</a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
<li><a href="#index-Single-Stepping-120">Single Stepping</a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-Slot-access-136">Slot access</a>: <a href="#Slot-access">Slot access</a></li>
<li><a href="#index-Sockets_002c-Networking-535">Sockets, Networking</a>: <a href="#Networking">Networking</a></li>
<li><a href="#index-Source-location-printing_002c-debugger-90">Source location printing, debugger</a>: <a href="#Source-Location-Printing">Source Location Printing</a></li>
<li><a href="#index-Source_002dto_002dsource-transformation-40">Source-to-source transformation</a>: <a href="#The-Processing-Path">The Processing Path</a></li>
<li><a href="#index-Stack-frames-65">Stack frames</a>: <a href="#Stack-Frames">Stack Frames</a></li>
<li><a href="#index-Static-functions-57">Static functions</a>: <a href="#Open-Coding-and-Inline-Expansion">Open Coding and Inline Expansion</a></li>
<li><a href="#index-Stepper-119">Stepper</a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-System-Calls-650">System Calls</a>: <a href="#sb_002dposix">sb-posix</a></li>
<li><a href="#index-Tail-recursion-77">Tail recursion</a>: <a href="#Debug-Tail-Recursion">Debug Tail Recursion</a></li>
<li><a href="#index-The-Deprecation-Pipeline-672">The Deprecation Pipeline</a>: <a href="#The-Deprecation-Pipeline">The Deprecation Pipeline</a></li>
<li><a href="#index-Tracing-112">Tracing</a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-Type-checking_002c-at-compile-time-52">Type checking, at compile time</a>: <a href="#Type-Errors-at-Compile-Time">Type Errors at Compile Time</a></li>
<li><a href="#index-Type-checking_002c-precise-44">Type checking, precise</a>: <a href="#Precise-Type-Checking">Precise Type Checking</a></li>
<li><a href="#index-Types_002c-portability-46">Types, portability</a>: <a href="#Getting-Existing-Programs-to-Run">Getting Existing Programs to Run</a></li>
<li><a href="#index-Unknown-code-locations-79">Unknown code locations</a>: <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a></li>
<li><a href="#index-Validity-of-debug-variables-88">Validity of debug variables</a>: <a href="#Variable-Value-Availability">Variable Value Availability</a></li>
<li><a href="#index-Variables_002c-debugger-access-84">Variables, debugger access</a>: <a href="#Variable-Access">Variable Access</a></li>
<li><a href="#index-Weak-pointers-178">Weak pointers</a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-Why-Deprecate_003f-671">Why Deprecate?</a>: <a href="#Why-Deprecate_003f">Why Deprecate?</a></li>
   </ul><div class="node">
<a name="Function-Index"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Variable-Index">Variable Index</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Concept-Index">Concept Index</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="appendix">Appendix B Function Index</h2>



<ul class="index-fn" compact="compact">
<li><a href="#index-g_t_0040setf_007b_0040sequence_007belt_007d_007d-248"><code>(setf elt [sb-sequence])</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040setf_007b_0040sequence_007biterator_002delement_007d_007d-279"><code>(setf iterator-element [sb-sequence])</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040setf_007b_0040cl_007blogical_002dpathname_002dtranslations_007d_007d-396"><code>(setf logical-pathname-translations [cl])</code></a>: <a href="#Lisp-Pathnames">Lisp Pathnames</a></li>
<li><a href="#index-g_t_0040setf_007b_0040sbmop_007bslot_002dvalue_002dusing_002dclass_007d_007d-211"><code>(setf slot-value-using-class [sb-mop])</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040nopkg_007b_003f_007d-107"><code>?</code></a>: <a href="#Information-Commands">Information Commands</a></li>
<li><a href="#index-g_t_0040nopkg_007babort_007d-103"><code>abort</code></a>: <a href="#Exiting-Commands">Exiting Commands</a></li>
<li><a href="#index-g_t_0040sbthread_007babort_002dthread_007d-481"><code>abort-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007badd_002dimplementation_002dpackage_007d-467"><code>add-implementation-package [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007badd_002dpackage_002dlocal_002dnickname_007d-169"><code>add-package-local-nickname [sb-ext]</code></a>: <a href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a></li>
<li><a href="#index-g_t_0040sbalien_007baddr_007d-377"><code>addr [sb-alien]</code></a>: <a href="#Coercing-Foreign-Values">Coercing Foreign Values</a></li>
<li><a href="#index-g_t_0040sequence_007badjust_002dsequence_007d-249"><code>adjust-sequence [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbunicode_007bage_007d-305"><code>age [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbalien_007balien_002dfuncall_007d-390"><code>alien-funcall [sb-alien]</code></a>: <a href="#The-alien_002dfuncall-Primitive">The alien-funcall Primitive</a></li>
<li><a href="#index-g_t_0040sbalien_007balien_002dsap_007d-380"><code>alien-sap [sb-alien]</code></a>: <a href="#Coercing-Foreign-Values">Coercing Foreign Values</a></li>
<li><a href="#index-g_t_0040sbunicode_007balphabetic_002dp_007d-316"><code>alphabetic-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007balways_002dbound_007d-156"><code>always-bound [sb-ext]</code></a>: <a href="#Global-and-Always_002dBound-variables">Global and Always-Bound variables</a></li>
<li><a href="#index-g_t_0040sbext_007barray_002dstorage_002dvector_007d-364"><code>array-storage-vector [sb-ext]</code></a>: <a href="#Miscellaneous-Extensions">Miscellaneous Extensions</a></li>
<li><a href="#index-g_t_0040sbext_007bassert_002dversion_002d_003e_003d_007d-368"><code>assert-version-&gt;= [sb-ext]</code></a>: <a href="#Miscellaneous-Extensions">Miscellaneous Extensions</a></li>
<li><a href="#index-g_t_0040sbext_007batomic_002ddecf_007d-491"><code>atomic-decf [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbext_007batomic_002dincf_007d-492"><code>atomic-incf [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbext_007batomic_002dpop_007d-493"><code>atomic-pop [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbext_007batomic_002dpush_007d-494"><code>atomic-push [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbext_007batomic_002dupdate_007d-495"><code>atomic-update [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040nopkg_007bbacktrace_007d-111"><code>backtrace</code></a>: <a href="#Information-Commands">Information Commands</a></li>
<li><a href="#index-g_t_0040sbthread_007bbarrier_007d-527"><code>barrier [sb-thread]</code></a>: <a href="#Barriers">Barriers</a></li>
<li><a href="#index-g_t_0040sbunicode_007bbidi_002dclass_007d-298"><code>bidi-class [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bbidi_002dmirroring_002dglyph_007d-304"><code>bidi-mirroring-glyph [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bboth_002dcase_002dp_007d-335"><code>both-case-p [cl]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040nopkg_007bbottom_007d-69"><code>bottom</code></a>: <a href="#Stack-Motion">Stack Motion</a></li>
<li><a href="#index-g_t_0040sbext_007bbytes_002dconsed_002dbetween_002dgcs_007d-182"><code>bytes-consed-between-gcs [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bcancel_002dfinalization_007d-177"><code>cancel-finalization [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bcas_007d-497"><code>cas [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbunicode_007bcase_002dignorable_002dp_007d-315"><code>case-ignorable-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bcased_002dp_007d-314"><code>cased-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bcasefold_007d-332"><code>casefold [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbalien_007bcast_007d-378"><code>cast [sb-alien]</code></a>: <a href="#Coercing-Foreign-Values">Coercing Foreign Values</a></li>
<li><a href="#index-g_t_0040sbunicode_007bchar_002dblock_007d-309"><code>char-block [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bchar_002ddowncase_007d-334"><code>char-downcase [cl]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bclass_002dname_007d-217"><code>class-name [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bclass_002dof_007d-207"><code>class-of [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbmop_007bclass_002dprototype_007d-205"><code>class-prototype [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbcover_007bclear_002dcoverage_007d-637"><code>clear-coverage [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040sbthread_007bclear_002dsemaphore_002dnotification_007d-520"><code>clear-semaphore-notification [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040cl_007bclose_007d-415"><code>close [cl]</code></a>: <a href="#Methods-common-to-all-streams">Methods common to all streams</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bclose_002dgate_007d-616"><code>close-gate [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040cl_007bcoerce_007d-240"><code>coerce [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbunicode_007bcombining_002dclass_007d-299"><code>combining-class [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bcompare_002dand_002dswap_007d-496"><code>compare-and-swap [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbmop_007bcompute_002deffective_002dmethod_007d-192"><code>compute-effective-method [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007bconcatenate_007d-259"><code>concatenate [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbthread_007bcondition_002dbroadcast_007d-526"><code>condition-broadcast [sb-thread]</code></a>: <a href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a></li>
<li><a href="#index-g_t_0040sbthread_007bcondition_002dnotify_007d-525"><code>condition-notify [sb-thread]</code></a>: <a href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a></li>
<li><a href="#index-g_t_0040sbthread_007bcondition_002dwait_007d-524"><code>condition-wait [sb-thread]</code></a>: <a href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a></li>
<li><a href="#index-g_t_0040sbunicode_007bconfusable_002dp_007d-342"><code>confusable-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bcons_007d-140"><code>cons [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040nopkg_007bcontinue_007d-102"><code>continue</code></a>: <a href="#Exiting-Commands">Exiting Commands</a></li>
<li><a href="#index-g_t_0040code_007bcopy-function_007d-269"><code>copy function</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bcopy_002dseq_007d-254"><code>copy-seq [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbunicode_007bdecimal_002dvalue_007d-300"><code>decimal-value [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bdeclare_007d-452"><code>declare [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040sbunicode_007bdefault_002dignorable_002dp_007d-322"><code>default-ignorable-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bdefcas_007d-499"><code>defcas [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040cl_007bdefclass_007d-213"><code>defclass [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bdefconstant_007d-2"><code>defconstant [cl]</code></a>: <a href="#Defining-Constants">Defining Constants</a></li>
<li><a href="#index-g_t_0040sbext_007bdefglobal_007d-154"><code>defglobal [sb-ext]</code></a>: <a href="#Global-and-Always_002dBound-variables">Global and Always-Bound variables</a></li>
<li><a href="#index-g_t_0040sbalien_007bdefine_002dalien_002droutine_007d-391"><code>define-alien-routine [sb-alien]</code></a>: <a href="#The-define_002dalien_002droutine-Macro">The define-alien-routine Macro</a></li>
<li><a href="#index-g_t_0040sbalien_007bdefine_002dalien_002dvariable_007d-385"><code>define-alien-variable [sb-alien]</code></a>: <a href="#External-Foreign-Variables">External Foreign Variables</a></li>
<li><a href="#index-g_t_0040sbext_007bdefine_002dcas_002dexpander_007d-498"><code>define-cas-expander [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbext_007bdefine_002dhash_002dtable_002dtest_007d-358"><code>define-hash-table-test [sb-ext]</code></a>: <a href="#Hash-Table-Extensions">Hash Table Extensions</a></li>
<li><a href="#index-g_t_0040cl_007bdefmethod_007d-225"><code>defmethod [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bdefpackage_007d-471"><code>defpackage [cl]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040cl_007bdefpackage_007d-441"><code>defpackage [cl]</code></a>: <a href="#Implementation-Packages">Implementation Packages</a></li>
<li><a href="#index-g_t_0040cl_007bdefpackage_007d-165"><code>defpackage [cl]</code></a>: <a href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a></li>
<li><a href="#index-g_t_0040cl_007bdefstruct_007d-220"><code>defstruct [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbext_007bdelete_002ddirectory_007d-365"><code>delete-directory [sb-ext]</code></a>: <a href="#Miscellaneous-Extensions">Miscellaneous Extensions</a></li>
<li><a href="#index-g_t_0040sbext_007bdeprecated_007d-681"><code>deprecated [sb-ext]</code></a>: <a href="#Deprecation-Declaration">Deprecation Declaration</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bdequeue_007d-594"><code>dequeue [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbalien_007bderef_007d-372"><code>deref [sb-alien]</code></a>: <a href="#Accessing-Foreign-Values">Accessing Foreign Values</a></li>
<li><a href="#index-g_t_0040nopkg_007bdescribe_007d-108"><code>describe</code></a>: <a href="#Information-Commands">Information Commands</a></li>
<li><a href="#index-g_t_0040sbext_007bdescribe_002dcompiler_002dpolicy_007d-48"><code>describe-compiler-policy [sb-ext]</code></a>: <a href="#Compiler-Policy">Compiler Policy</a></li>
<li><a href="#index-g_t_0040sbunicode_007bdigit_002dvalue_007d-301"><code>digit-value [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bdisable_002ddebugger_007d-133"><code>disable-debugger [sb-ext]</code></a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-g_t_0040sbext_007bdisable_002dpackage_002dlocks_007d-456"><code>disable-package-locks [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bdisable_002dpackage_002dlocks_007d-454"><code>disable-package-locks [sb-ext]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040cl_007bdolist_007d-261"><code>dolist [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sequence_007bdosequence_007d-262"><code>dosequence [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040nopkg_007bdown_007d-67"><code>down</code></a>: <a href="#Stack-Motion">Stack Motion</a></li>
<li><a href="#index-g_t_0040sbext_007bdynamic_002dspace_002dsize_007d-183"><code>dynamic-space-size [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbunicode_007beast_002dasian_002dwidth_007d-307"><code>east-asian-width [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bed_007d-349"><code>ed [cl]</code></a>: <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a></li>
<li><a href="#index-g_t_0040code_007belement-function_007d-266"><code>element function</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007belt_007d-247"><code>elt [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sequence_007bemptyp_007d-257"><code>emptyp [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbext_007benable_002ddebugger_007d-134"><code>enable-debugger [sb-ext]</code></a>: <a href="#Enabling-and-Disabling-the-Debugger">Enabling and Disabling the Debugger</a></li>
<li><a href="#index-g_t_0040sbext_007benable_002dpackage_002dlocks_007d-457"><code>enable-package-locks [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007benable_002dpackage_002dlocks_007d-455"><code>enable-package-locks [sb-ext]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040code_007bendp-function_007d-265"><code>endp function</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007benqueue_007d-595"><code>enqueue [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbmop_007bensure_002dclass_007d-214"><code>ensure-class [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbmop_007bensure_002dclass_002dusing_002dclass_007d-215"><code>ensure-class-using-class [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bensure_002dgeneric_002dfunction_007d-198"><code>ensure-generic-function [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040nopkg_007berror_007d-110"><code>error</code></a>: <a href="#Information-Commands">Information Commands</a></li>
<li><a href="#index-g_t_0040cl_007beval_007d-59"><code>eval [cl]</code></a>: <a href="#Interpreter">Interpreter</a></li>
<li><a href="#index-g_t_0040sbext_007bexit_007d-6"><code>exit [sb-ext]</code></a>: <a href="#Exit">Exit</a></li>
<li><a href="#index-g_t_0040sbalien_007bextern_002dalien_007d-387"><code>extern-alien [sb-alien]</code></a>: <a href="#External-Foreign-Variables">External Foreign Variables</a></li>
<li><a href="#index-g_t_0040sbposix_007bfile_002ddescriptor_007d-654"><code>file-descriptor [sb-posix]</code></a>: <a href="#File_002ddescriptors">File-descriptors</a></li>
<li><a href="#index-g_t_0040sbposix_007bfilename_007d-657"><code>filename [sb-posix]</code></a>: <a href="#Filenames">Filenames</a></li>
<li><a href="#index-g_t_0040sbext_007bfinalize_007d-176"><code>finalize [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbmop_007bfinalize_002dinheritance_007d-201"><code>finalize-inheritance [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bfind_007d-238"><code>find [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040cl_007bfind_002dclass_007d-216"><code>find-class [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bfind_002dmethod_007d-230"><code>find-method [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bflet_007d-448"><code>flet [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040cl_007bflet_007d-146"><code>flet [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040nopkg_007bframe_007d-70"><code>frame</code></a>: <a href="#Stack-Motion">Stack Motion</a></li>
<li><a href="#index-g_t_0040sbalien_007bfree_002dalien_007d-383"><code>free-alien [sb-alien]</code></a>: <a href="#Foreign-Dynamic-Allocation">Foreign Dynamic Allocation</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bfrlock_002dname_007d-629"><code>frlock-name [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bfrlock_002dread_007d-626"><code>frlock-read [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bfrlock_002dread_002dbegin_007d-630"><code>frlock-read-begin [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bfrlock_002dread_002dend_007d-631"><code>frlock-read-end [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bfrlock_002dwrite_007d-627"><code>frlock-write [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbmop_007bfuncallable_002dstandard_002dinstance_002daccess_007d-235"><code>funcallable-standard-instance-access [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bgate_002dname_007d-617"><code>gate-name [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bgate_002dopen_002dp_007d-618"><code>gate-open-p [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bgatep_007d-619"><code>gatep [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbext_007bgc_007d-174"><code>gc [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bgc_002dlogfile_007d-185"><code>gc-logfile [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbunicode_007bgeneral_002dcategory_007d-297"><code>general-category [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bgeneration_002daverage_002dage_007d-186"><code>generation-average-age [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bgeneration_002dbytes_002dallocated_007d-187"><code>generation-bytes-allocated [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bgeneration_002dbytes_002dconsed_002dbetween_002dgcs_007d-188"><code>generation-bytes-consed-between-gcs [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bgeneration_002dminimum_002dage_002dbefore_002dgc_007d-189"><code>generation-minimum-age-before-gc [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bgeneration_002dnumber_002dof_002dgcs_007d-191"><code>generation-number-of-gcs [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bgeneration_002dnumber_002dof_002dgcs_002dbefore_002dpromotion_007d-190"><code>generation-number-of-gcs-before-promotion [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbmop_007bgeneric_002dfunction_002ddeclarations_007d-199"><code>generic-function-declarations [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbext_007bget_002dbytes_002dconsed_007d-184"><code>get-bytes-consed [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007bget_002dcas_002dexpansion_007d-500"><code>get-cas-expansion [sb-ext]</code></a>: <a href="#Atomic-Operations">Atomic Operations</a></li>
<li><a href="#index-g_t_0040sbalien_007bget_002derrno_007d-386"><code>get-errno [sb-alien]</code></a>: <a href="#External-Foreign-Variables">External Foreign Variables</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bget_002dhost_002dby_002daddress_007d-569"><code>get-host-by-address [sb-bsd-sockets]</code></a>: <a href="#Name-Service">Name Service</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bget_002dhost_002dby_002dname_007d-568"><code>get-host-by-name [sb-bsd-sockets]</code></a>: <a href="#Name-Service">Name Service</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bget_002dprotocol_002dby_002dname_007d-565"><code>get-protocol-by-name [sb-bsd-sockets]</code></a>: <a href="#INET-Domain-Sockets">INET Domain Sockets</a></li>
<li><a href="#index-g_t_0040sbext_007bget_002dtime_002dof_002dday_007d-366"><code>get-time-of-day [sb-ext]</code></a>: <a href="#Miscellaneous-Extensions">Miscellaneous Extensions</a></li>
<li><a href="#index-g_t_0040sbposix_007bgetcwd_007d-663"><code>getcwd [sb-posix]</code></a>: <a href="#Functions-with-idiosyncratic-bindings">Functions with idiosyncratic bindings</a></li>
<li><a href="#index-g_t_0040sbext_007bglobal_007d-155"><code>global [sb-ext]</code></a>: <a href="#Global-and-Always_002dBound-variables">Global and Always-Bound variables</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bgrab_002dfrlock_002dwrite_002dlock_007d-632"><code>grab-frlock-write-lock [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007bgrab_002dmutex_007d-508"><code>grab-mutex [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bgrapheme_002dbreak_002dclass_007d-323"><code>grapheme-break-class [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bgraphemes_007d-343"><code>graphemes [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bhangul_002dsyllable_002dtype_007d-306"><code>hangul-syllable-type [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bhash_002dtable_002dsynchronized_002dp_007d-360"><code>hash-table-synchronized-p [sb-ext]</code></a>: <a href="#Hash-Table-Extensions">Hash Table Extensions</a></li>
<li><a href="#index-g_t_0040sbext_007bhash_002dtable_002dweakness_007d-361"><code>hash-table-weakness [sb-ext]</code></a>: <a href="#Hash-Table-Extensions">Hash Table Extensions</a></li>
<li><a href="#index-g_t_0040nopkg_007bhelp_007d-106"><code>help</code></a>: <a href="#Information-Commands">Information Commands</a></li>
<li><a href="#index-g_t_0040sbunicode_007bhex_002ddigit_002dp_007d-321"><code>hex-digit-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bhost_002dent_002daddress_007d-570"><code>host-ent-address [sb-bsd-sockets]</code></a>: <a href="#Name-Service">Name Service</a></li>
<li><a href="#index-g_t_0040sbunicode_007bideographic_002dp_007d-317"><code>ideographic-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040code_007bindex-function_007d-268"><code>index function</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040cl_007binspect_007d-353"><code>inspect [cl]</code></a>: <a href="#Tools-To-Help-Developers">Tools To Help Developers</a></li>
<li><a href="#index-g_t_0040sbsys_007bint_002dsap_007d-374"><code>int-sap [sb-sys]</code></a>: <a href="#Accessing-Foreign-Values">Accessing Foreign Values</a></li>
<li><a href="#index-g_t_0040cl_007bintern_007d-163"><code>intern [cl]</code></a>: <a href="#Reader-Extensions">Reader Extensions</a></li>
<li><a href="#index-g_t_0040sbmop_007bintern_002deql_002dspecializer_007d-227"><code>intern-eql-specializer [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbthread_007binterrupt_002dthread_007d-484"><code>interrupt-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sequence_007biterator_002dcopy_007d-281"><code>iterator-copy [sb-sequence]</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007biterator_002delement_007d-278"><code>iterator-element [sb-sequence]</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007biterator_002dendp_007d-277"><code>iterator-endp [sb-sequence]</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007biterator_002dindex_007d-280"><code>iterator-index [sb-sequence]</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007biterator_002dstep_007d-276"><code>iterator-step [sb-sequence]</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sbthread_007bjoin_002dthread_007d-482"><code>join-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040cl_007blabels_007d-449"><code>labels [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040cl_007blabels_007d-147"><code>labels [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040sequence_007blength_007d-246"><code>length [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040cl_007blet_007d-446"><code>let [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040cl_007blet_007d-157"><code>let [cl]</code></a>: <a href="#Miscellaneous-Efficiency-Issues">Miscellaneous Efficiency Issues</a></li>
<li><a href="#index-g_t_0040cl_007blet_002a_007d-447"><code>let* [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040cl_007blet_002a_007d-158"><code>let* [cl]</code></a>: <a href="#Miscellaneous-Efficiency-Issues">Miscellaneous Efficiency Issues</a></li>
<li><a href="#index-g_t_0040sbunicode_007bline_002dbreak_002dclass_007d-326"><code>line-break-class [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007blines_007d-346"><code>lines [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007blist_007d-141"><code>list [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040cl_007blist_002a_007d-142"><code>list* [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040sbthread_007blist_002dall_002dthreads_007d-474"><code>list-all-threads [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007blist_002dall_002dtimers_007d-534"><code>list-all-timers [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040nopkg_007blist_002dlocals_007d-85"><code>list-locals</code></a>: <a href="#Variable-Access">Variable Access</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007blist_002dmailbox_002dmessages_007d-604"><code>list-mailbox-messages [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007blist_002dqueue_002dcontents_007d-596"><code>list-queue-contents [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbalien_007bload_002dshared_002dobject_007d-388"><code>load-shared-object [sb-alien]</code></a>: <a href="#Loading-Shared-Object-Files">Loading Shared Object Files</a></li>
<li><a href="#index-g_t_0040sbext_007block_002dpackage_007d-463"><code>lock-package [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040cl_007blogand_007d-153"><code>logand [cl]</code></a>: <a href="#Modular-arithmetic">Modular arithmetic</a></li>
<li><a href="#index-g_t_0040cl_007blogical_002dpathname_002dtranslations_007d-395"><code>logical-pathname-translations [cl]</code></a>: <a href="#Lisp-Pathnames">Lisp Pathnames</a></li>
<li><a href="#index-g_t_0040sbunicode_007blowercase_007d-330"><code>lowercase [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007blowercase_002dp_007d-313"><code>lowercase-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bmacrolet_007d-450"><code>macrolet [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmailbox_002dcount_007d-605"><code>mailbox-count [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmailbox_002dempty_002dp_007d-606"><code>mailbox-empty-p [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmailbox_002dname_007d-607"><code>mailbox-name [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmailboxp_007d-608"><code>mailboxp [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007bmain_002dthread_007d-478"><code>main-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bmain_002dthread_002dp_007d-477"><code>main-thread-p [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbalien_007bmake_002dalien_007d-381"><code>make-alien [sb-alien]</code></a>: <a href="#Foreign-Dynamic-Allocation">Foreign Dynamic Allocation</a></li>
<li><a href="#index-g_t_0040sbalien_007bmake_002dalien_002dstring_007d-382"><code>make-alien-string [sb-alien]</code></a>: <a href="#Foreign-Dynamic-Allocation">Foreign Dynamic Allocation</a></li>
<li><a href="#index-g_t_0040cl_007bmake_002darray_007d-144"><code>make-array [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmake_002dfrlock_007d-628"><code>make-frlock [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmake_002dgate_007d-620"><code>make-gate [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040cl_007bmake_002dhash_002dtable_007d-357"><code>make-hash-table [cl]</code></a>: <a href="#Hash-Table-Extensions">Hash Table Extensions</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bmake_002dinet_002daddress_007d-563"><code>make-inet-address [sb-bsd-sockets]</code></a>: <a href="#INET-Domain-Sockets">INET Domain Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bmake_002dinet6_002daddress_007d-564"><code>make-inet6-address [sb-bsd-sockets]</code></a>: <a href="#INET-Domain-Sockets">INET Domain Sockets</a></li>
<li><a href="#index-g_t_0040cl_007bmake_002dinstance_007d-242"><code>make-instance [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmake_002dmailbox_007d-609"><code>make-mailbox [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbmop_007bmake_002dmethod_002dlambda_007d-229"><code>make-method-lambda [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbpcl_007bmake_002dmethod_002dspecializers_002dform_007d-228"><code>make-method-specializers-form [sb-pcl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbthread_007bmake_002dmutex_007d-504"><code>make-mutex [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmake_002dqueue_007d-597"><code>make-queue [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007bmake_002dsemaphore_007d-511"><code>make-semaphore [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbthread_007bmake_002dsemaphore_002dnotification_007d-518"><code>make-semaphore-notification [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sequence_007bmake_002dsequence_002diterator_007d-263"><code>make-sequence-iterator [sb-sequence]</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007bmake_002dsequence_002dlike_007d-250"><code>make-sequence-like [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sequence_007bmake_002dsimple_002dsequence_002diterator_007d-282"><code>make-simple-sequence-iterator [sb-sequence]</code></a>: <a href="#Simple-Iterator-Protocol">Simple Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007bmake_002dsimple_002dsequence_002diterator_007d-272"><code>make-simple-sequence-iterator [sb-sequence]</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sbthread_007bmake_002dthread_007d-479"><code>make-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007bmake_002dtimer_007d-529"><code>make-timer [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040sbthread_007bmake_002dwaitqueue_007d-522"><code>make-waitqueue [sb-thread]</code></a>: <a href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a></li>
<li><a href="#index-g_t_0040sbext_007bmake_002dweak_002dpointer_007d-179"><code>make-weak-pointer [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sequence_007bmap_007d-258"><code>map [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbunicode_007bmath_002dp_007d-318"><code>math-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbmd_007bmd5sum_002dfile_007d-644"><code>md5sum-file [sb-md5]</code></a>: <a href="#sb_002dmd5">sb-md5</a></li>
<li><a href="#index-g_t_0040sbmd_007bmd5sum_002dsequence_007d-645"><code>md5sum-sequence [sb-md5]</code></a>: <a href="#sb_002dmd5">sb-md5</a></li>
<li><a href="#index-g_t_0040sbmd_007bmd5sum_002dstream_007d-646"><code>md5sum-stream [sb-md5]</code></a>: <a href="#sb_002dmd5">sb-md5</a></li>
<li><a href="#index-g_t_0040sbmd_007bmd5sum_002dstring_007d-647"><code>md5sum-string [sb-md5]</code></a>: <a href="#sb_002dmd5">sb-md5</a></li>
<li><a href="#index-g_t_0040sequence_007bmerge_007d-260"><code>merge [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbunicode_007bmirrored_002dp_007d-303"><code>mirrored-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bmuffle_002dconditions_007d-20"><code>muffle-conditions [sb-ext]</code></a>: <a href="#Controlling-Verbosity">Controlling Verbosity</a></li>
<li><a href="#index-g_t_0040sbthread_007bmutex_002dname_007d-505"><code>mutex-name [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbthread_007bmutex_002downer_007d-506"><code>mutex-owner [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbthread_007bmutex_002dvalue_007d-507"><code>mutex-value [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbext_007bname_002dconflict_002dsymbols_007d-355"><code>name-conflict-symbols [sb-ext]</code></a>: <a href="#Resolution-of-Name-Conflicts">Resolution of Name Conflicts</a></li>
<li><a href="#index-g_t_0040sbext_007bnative_002dnamestring_007d-400"><code>native-namestring [sb-ext]</code></a>: <a href="#Native-Filenames">Native Filenames</a></li>
<li><a href="#index-g_t_0040sbext_007bnative_002dpathname_007d-399"><code>native-pathname [sb-ext]</code></a>: <a href="#Native-Filenames">Native Filenames</a></li>
<li><a href="#index-g_t_0040nopkg_007bnext_007d-123"><code>next</code></a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bnon_002dblocking_002dmode_007d-551"><code>non-blocking-mode [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbunicode_007bnormalize_002dstring_007d-327"><code>normalize-string [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bnormalized_002dp_007d-328"><code>normalized-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bnumeric_002dvalue_007d-302"><code>numeric-value [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bopen_007d-403"><code>open [cl]</code></a>: <a href="#External-Formats">External Formats</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bopen_002dgate_007d-621"><code>open-gate [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040nopkg_007bout_007d-124"><code>out</code></a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dimplemented_002dby_002dlist_007d-465"><code>package-implemented-by-list [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dimplements_002dlist_007d-466"><code>package-implements-list [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlocal_002dnicknames_007d-167"><code>package-local-nicknames [sb-ext]</code></a>: <a href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlocally_002dnicknamed_002dby_002dlist_007d-168"><code>package-locally-nicknamed-by-list [sb-ext]</code></a>: <a href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlocked_002derror_002dsymbol_007d-461"><code>package-locked-error-symbol [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlocked_002dp_007d-462"><code>package-locked-p [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bparse_002dnative_002dnamestring_007d-398"><code>parse-native-namestring [sb-ext]</code></a>: <a href="#Native-Filenames">Native Filenames</a></li>
<li><a href="#index-g_t_0040sbpcl_007bparse_002dspecializer_002dusing_002dclass_007d-231"><code>parse-specializer-using-class [sb-pcl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbext_007bposix_002dgetenv_007d-284"><code>posix-getenv [sb-ext]</code></a>: <a href="#Querying-the-process-environment">Querying the process environment</a></li>
<li><a href="#index-g_t_0040nopkg_007bprint_007d-109"><code>print</code></a>: <a href="#Information-Commands">Information Commands</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dalive_002dp_007d-290"><code>process-alive-p [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dclose_007d-295"><code>process-close [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dcore_002ddumped_007d-294"><code>process-core-dumped [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002derror_007d-289"><code>process-error [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dexit_002dcode_007d-293"><code>process-exit-code [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dinput_007d-287"><code>process-input [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dkill_007d-296"><code>process-kill [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002doutput_007d-288"><code>process-output [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dp_007d-286"><code>process-p [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dstatus_007d-291"><code>process-status [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbext_007bprocess_002dwait_007d-292"><code>process-wait [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbprofile_007bprofile_007d-573"><code>profile [sb-profile]</code></a>: <a href="#Deterministic-Profiler">Deterministic Profiler</a></li>
<li><a href="#index-g_t_0040sbsprof_007bprofile_002dcall_002dcounts_007d-584"><code>profile-call-counts [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbunicode_007bproplist_002dp_007d-311"><code>proplist-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bpurify_007d-369"><code>purify [sb-ext]</code></a>: <a href="#Efficiency-Hacks">Efficiency Hacks</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bqueue_002dcount_007d-598"><code>queue-count [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bqueue_002dempty_002dp_007d-599"><code>queue-empty-p [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bqueue_002dname_007d-600"><code>queue-name [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bqueuep_007d-601"><code>queuep [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbposix_007breadlink_007d-664"><code>readlink [sb-posix]</code></a>: <a href="#Functions-with-idiosyncratic-bindings">Functions with idiosyncratic bindings</a></li>
<li><a href="#index-g_t_0040sbext_007breadtable_002dnormalization_007d-162"><code>readtable-normalization [sb-ext]</code></a>: <a href="#Reader-Extensions">Reader Extensions</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007breceive_002dmessage_007d-610"><code>receive-message [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007breceive_002dmessage_002dno_002dhang_007d-611"><code>receive-message-no-hang [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007breceive_002dpending_002dmessages_007d-612"><code>receive-pending-messages [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007brelease_002dfrlock_002dwrite_002dlock_007d-633"><code>release-frlock-write-lock [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007brelease_002dmutex_007d-509"><code>release-mutex [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbext_007bremove_002dimplementation_002dpackage_007d-468"><code>remove-implementation-package [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bremove_002dpackage_002dlocal_002dnickname_007d-170"><code>remove-package-local-nickname [sb-ext]</code></a>: <a href="#Package_002dLocal-Nicknames">Package-Local Nicknames</a></li>
<li><a href="#index-g_t_0040sbcover_007breport_007d-635"><code>report [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040sbprofile_007breport_007d-575"><code>report [sb-profile]</code></a>: <a href="#Deterministic-Profiler">Deterministic Profiler</a></li>
<li><a href="#index-g_t_0040sbsprof_007breport_007d-580"><code>report [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040cl_007brequire_007d-347"><code>require [cl]</code></a>: <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a></li>
<li><a href="#index-g_t_0040sbprofile_007breset_007d-576"><code>reset [sb-profile]</code></a>: <a href="#Deterministic-Profiler">Deterministic Profiler</a></li>
<li><a href="#index-g_t_0040sbsprof_007breset_007d-581"><code>reset [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbcover_007breset_002dcoverage_007d-636"><code>reset-coverage [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040nopkg_007brestart_007d-101"><code>restart</code></a>: <a href="#Exiting-Commands">Exiting Commands</a></li>
<li><a href="#index-g_t_0040nopkg_007brestart_002dframe_007d-105"><code>restart-frame</code></a>: <a href="#Exiting-Commands">Exiting Commands</a></li>
<li><a href="#index-g_t_0040sbcover_007brestore_002dcoverage_007d-640"><code>restore-coverage [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040sbcover_007brestore_002dcoverage_002dfrom_002dfile_007d-641"><code>restore-coverage-from-file [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040sbext_007brestrict_002dcompiler_002dpolicy_007d-49"><code>restrict-compiler-policy [sb-ext]</code></a>: <a href="#Compiler-Policy">Compiler Policy</a></li>
<li><a href="#index-g_t_0040nopkg_007breturn_007d-104"><code>return</code></a>: <a href="#Exiting-Commands">Exiting Commands</a></li>
<li><a href="#index-g_t_0040sbthread_007breturn_002dfrom_002dthread_007d-480"><code>return-from-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbrotatebyte_007brotate_002dbyte_007d-670"><code>rotate-byte [sb-rotate-byte]</code></a>: <a href="#sb_002drotate_002dbyte">sb-rotate-byte</a></li>
<li><a href="#index-g_t_0040sbrotatebyte_007brotate_002dbyte_007d-648"><code>rotate-byte [sb-rotate-byte]</code></a>: <a href="#sb_002dmd5">sb-md5</a></li>
<li><a href="#index-g_t_0040sbext_007brun_002dprogram_007d-285"><code>run-program [sb-ext]</code></a>: <a href="#Running-external-programs">Running external programs</a></li>
<li><a href="#index-g_t_0040sbalien_007bsap_002dalien_007d-379"><code>sap-alien [sb-alien]</code></a>: <a href="#Coercing-Foreign-Values">Coercing Foreign Values</a></li>
<li><a href="#index-g_t_0040sbsys_007bsap_002dref_002d32_007d-375"><code>sap-ref-32 [sb-sys]</code></a>: <a href="#Accessing-Foreign-Values">Accessing Foreign Values</a></li>
<li><a href="#index-g_t_0040sbsys_007bsap_003d_007d-376"><code>sap= [sb-sys]</code></a>: <a href="#Accessing-Foreign-Values">Accessing Foreign Values</a></li>
<li><a href="#index-g_t_0040cl_007bsatisfies_007d-41"><code>satisfies [cl]</code></a>: <a href="#Handling-of-Types">Handling of Types</a></li>
<li><a href="#index-g_t_0040sbcover_007bsave_002dcoverage_007d-638"><code>save-coverage [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040sbcover_007bsave_002dcoverage_002din_002dfile_007d-639"><code>save-coverage-in-file [sb-cover]</code></a>: <a href="#sb_002dcover">sb-cover</a></li>
<li><a href="#index-g_t_0040sbext_007bsave_002dlisp_002dand_002ddie_007d-7"><code>save-lisp-and-die [sb-ext]</code></a>: <a href="#Saving-a-Core-Image">Saving a Core Image</a></li>
<li><a href="#index-g_t_0040sbext_007bschedule_002dtimer_007d-532"><code>schedule-timer [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040sbunicode_007bscript_007d-308"><code>script [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bseed_002drandom_002dstate_007d-363"><code>seed-random-state [sb-ext]</code></a>: <a href="#Random-Number-Generation">Random Number Generation</a></li>
<li><a href="#index-g_t_0040sbthread_007bsemaphore_002dcount_007d-515"><code>semaphore-count [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbthread_007bsemaphore_002dname_007d-516"><code>semaphore-name [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbthread_007bsemaphore_002dnotification_002dstatus_007d-519"><code>semaphore-notification-status [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bsend_002dmessage_007d-613"><code>send-message [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbunicode_007bsentence_002dbreak_002dclass_007d-325"><code>sentence-break-class [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bsentences_007d-345"><code>sentences [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbext_007bset_002dsbcl_002dsource_002dlocation_007d-397"><code>set-sbcl-source-location [sb-ext]</code></a>: <a href="#Lisp-Pathnames">Lisp Pathnames</a></li>
<li><a href="#index-g_t_0040cl_007bsetf_007d-160"><code>setf [cl]</code></a>: <a href="#Miscellaneous-Efficiency-Issues">Miscellaneous Efficiency Issues</a></li>
<li><a href="#index-g_t_0040code_007bsetf-element-function_007d-267"><code>setf element function</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bsetq_007d-159"><code>setq [cl]</code></a>: <a href="#Miscellaneous-Efficiency-Issues">Miscellaneous Efficiency Issues</a></li>
<li><a href="#index-g_t_0040sbthread_007bsignal_002dsemaphore_007d-512"><code>signal-semaphore [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbalien_007bslot_007d-373"><code>slot [sb-alien]</code></a>: <a href="#Accessing-Foreign-Values">Accessing Foreign Values</a></li>
<li><a href="#index-g_t_0040sbmop_007bslot_002dboundp_002dusing_002dclass_007d-212"><code>slot-boundp-using-class [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbmop_007bslot_002ddefinition_002dname_007d-218"><code>slot-definition-name [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbmop_007bslot_002dvalue_002dusing_002dclass_007d-210"><code>slot-value-using-class [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002daccept_007d-538"><code>socket-accept [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dbind_007d-537"><code>socket-bind [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dclose_007d-546"><code>socket-close [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dconnect_007d-539"><code>socket-connect [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002derror_007d-550"><code>socket-error [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dlisten_007d-544"><code>socket-listen [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dmake_002dstream_007d-548"><code>socket-make-stream [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dname_007d-541"><code>socket-name [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dopen_002dp_007d-545"><code>socket-open-p [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dpeername_007d-540"><code>socket-peername [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dreceive_007d-542"><code>socket-receive [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dsend_007d-543"><code>socket-send [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_002dshutdown_007d-547"><code>socket-shutdown [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002dbroadcast_007d-559"><code>sockopt-broadcast [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002dbsd_002dcompatible_007d-555"><code>sockopt-bsd-compatible [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002ddebug_007d-557"><code>sockopt-debug [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002ddont_002droute_007d-558"><code>sockopt-dont-route [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002dkeep_002dalive_007d-553"><code>sockopt-keep-alive [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002doob_002dinline_007d-554"><code>sockopt-oob-inline [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002dpass_002dcredentials_007d-556"><code>sockopt-pass-credentials [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002dreuse_002daddress_007d-552"><code>sockopt-reuse-address [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsockopt_002dtcp_002dnodelay_007d-560"><code>sockopt-tcp-nodelay [sb-bsd-sockets]</code></a>: <a href="#Socket-Options">Socket Options</a></li>
<li><a href="#index-g_t_0040sbunicode_007bsoft_002ddotted_002dp_007d-320"><code>soft-dotted-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040nopkg_007bsource_007d-91"><code>source</code></a>: <a href="#Source-Location-Printing">Source Location Printing</a></li>
<li><a href="#index-g_t_0040sbmop_007bstandard_002dinstance_002daccess_007d-234"><code>standard-instance-access [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040nopkg_007bstart_007d-121"><code>start</code></a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-g_t_0040sbsprof_007bstart_002dprofiling_007d-582"><code>start-profiling [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040nopkg_007bstep_007d-122"><code>step</code></a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-g_t_0040cl_007bstep_007d-126"><code>step [cl]</code></a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-g_t_0040code_007bstep-function_007d-264"><code>step function</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040nopkg_007bstop_007d-125"><code>stop</code></a>: <a href="#Single-Stepping">Single Stepping</a></li>
<li><a href="#index-g_t_0040sbsprof_007bstop_002dprofiling_007d-583"><code>stop-profiling [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dadvance_002dto_002dcolumn_007d-429"><code>stream-advance-to-column [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dclear_002dinput_007d-417"><code>stream-clear-input [sb-gray]</code></a>: <a href="#Input-stream-methods">Input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dclear_002doutput_007d-425"><code>stream-clear-output [sb-gray]</code></a>: <a href="#Output-stream-methods">Output stream methods</a></li>
<li><a href="#index-g_t_0040cl_007bstream_002delement_002dtype_007d-414"><code>stream-element-type [cl]</code></a>: <a href="#Methods-common-to-all-streams">Methods common to all streams</a></li>
<li><a href="#index-g_t_0040cl_007bstream_002dexternal_002dformat_007d-402"><code>stream-external-format [cl]</code></a>: <a href="#External-Formats">External Formats</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dfile_002dposition_007d-416"><code>stream-file-position [sb-gray]</code></a>: <a href="#Methods-common-to-all-streams">Methods common to all streams</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dfinish_002doutput_007d-426"><code>stream-finish-output [sb-gray]</code></a>: <a href="#Output-stream-methods">Output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dforce_002doutput_007d-427"><code>stream-force-output [sb-gray]</code></a>: <a href="#Output-stream-methods">Output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dfresh_002dline_007d-430"><code>stream-fresh-line [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dline_002dcolumn_007d-431"><code>stream-line-column [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dline_002dlength_007d-432"><code>stream-line-length [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dlisten_007d-423"><code>stream-listen [sb-gray]</code></a>: <a href="#Character-input-stream-methods">Character input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dpeek_002dchar_007d-419"><code>stream-peek-char [sb-gray]</code></a>: <a href="#Character-input-stream-methods">Character input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dread_002dbyte_007d-437"><code>stream-read-byte [sb-gray]</code></a>: <a href="#Binary-stream-methods">Binary stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dread_002dchar_007d-421"><code>stream-read-char [sb-gray]</code></a>: <a href="#Character-input-stream-methods">Character input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dread_002dchar_002dno_002dhang_007d-420"><code>stream-read-char-no-hang [sb-gray]</code></a>: <a href="#Character-input-stream-methods">Character input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dread_002dline_007d-422"><code>stream-read-line [sb-gray]</code></a>: <a href="#Character-input-stream-methods">Character input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dread_002dsequence_007d-418"><code>stream-read-sequence [sb-gray]</code></a>: <a href="#Input-stream-methods">Input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dstart_002dline_002dp_007d-433"><code>stream-start-line-p [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dterpri_007d-434"><code>stream-terpri [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dunread_002dchar_007d-424"><code>stream-unread-char [sb-gray]</code></a>: <a href="#Character-input-stream-methods">Character input stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dwrite_002dbyte_007d-438"><code>stream-write-byte [sb-gray]</code></a>: <a href="#Binary-stream-methods">Binary stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dwrite_002dchar_007d-435"><code>stream-write-char [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dwrite_002dsequence_007d-428"><code>stream-write-sequence [sb-gray]</code></a>: <a href="#Output-stream-methods">Output stream methods</a></li>
<li><a href="#index-g_t_0040sbgray_007bstream_002dwrite_002dstring_007d-436"><code>stream-write-string [sb-gray]</code></a>: <a href="#Character-output-stream-methods">Character output stream methods</a></li>
<li><a href="#index-g_t_0040cl_007bstring_002dupcase_007d-333"><code>string-upcase [cl]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040cl_007bsubseq_007d-239"><code>subseq [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040cl_007bsubtypep_007d-208"><code>subtypep [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bsymbol_002dmacrolet_007d-451"><code>symbol-macrolet [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040sbthread_007bsymbol_002dvalue_002din_002dthread_007d-486"><code>symbol-value-in-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbposix_007bsyslog_007d-665"><code>syslog [sb-posix]</code></a>: <a href="#Functions-with-idiosyncratic-bindings">Functions with idiosyncratic bindings</a></li>
<li><a href="#index-g_t_0040sbthread_007bterminate_002dthread_007d-485"><code>terminate-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bthread_002dalive_002dp_007d-475"><code>thread-alive-p [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bthread_002derror_002dthread_007d-488"><code>thread-error-thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bthread_002dname_007d-476"><code>thread-name [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bthread_002dyield_007d-483"><code>thread-yield [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007btimer_002dname_007d-530"><code>timer-name [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040sbext_007btimer_002dscheduled_002dp_007d-531"><code>timer-scheduled-p [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040sbunicode_007btitlecase_007d-331"><code>titlecase [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040nopkg_007btop_007d-68"><code>top</code></a>: <a href="#Stack-Motion">Stack Motion</a></li>
<li><a href="#index-g_t_0040nopkg_007btoplevel_007d-100"><code>toplevel</code></a>: <a href="#Exiting-Commands">Exiting Commands</a></li>
<li><a href="#index-g_t_0040cl_007btrace_007d-352"><code>trace [cl]</code></a>: <a href="#Tools-To-Help-Developers">Tools To Help Developers</a></li>
<li><a href="#index-g_t_0040cl_007btrace_007d-114"><code>trace [cl]</code></a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-g_t_0040sbext_007btruly_002dthe_007d-370"><code>truly-the [sb-ext]</code></a>: <a href="#Efficiency-Hacks">Efficiency Hacks</a></li>
<li><a href="#index-g_t_0040sbthread_007btry_002dsemaphore_007d-514"><code>try-semaphore [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040cl_007btypep_007d-206"><code>typep [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_002d1_002dname_007d-310"><code>unicode-1-name [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_002dequal_007d-338"><code>unicode-equal [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_003c_007d-336"><code>unicode&lt; [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_003c_003d_007d-339"><code>unicode&lt;= [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_003d_007d-337"><code>unicode= [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_003e_007d-340"><code>unicode&gt; [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bunicode_003e_003d_007d-341"><code>unicode&gt;= [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbalien_007bunload_002dshared_002dobject_007d-389"><code>unload-shared-object [sb-alien]</code></a>: <a href="#Loading-Shared-Object-Files">Loading Shared Object Files</a></li>
<li><a href="#index-g_t_0040sbext_007bunlock_002dpackage_007d-464"><code>unlock-package [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bunmuffle_002dconditions_007d-21"><code>unmuffle-conditions [sb-ext]</code></a>: <a href="#Controlling-Verbosity">Controlling Verbosity</a></li>
<li><a href="#index-g_t_0040sbpcl_007bunparse_002dspecializer_002dusing_002dclass_007d-232"><code>unparse-specializer-using-class [sb-pcl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbprofile_007bunprofile_007d-574"><code>unprofile [sb-profile]</code></a>: <a href="#Deterministic-Profiler">Deterministic Profiler</a></li>
<li><a href="#index-g_t_0040sbsprof_007bunprofile_002dcall_002dcounts_007d-585"><code>unprofile-call-counts [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbext_007bunschedule_002dtimer_007d-533"><code>unschedule-timer [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040cl_007buntrace_007d-115"><code>untrace [cl]</code></a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-g_t_0040nopkg_007bup_007d-66"><code>up</code></a>: <a href="#Stack-Motion">Stack Motion</a></li>
<li><a href="#index-g_t_0040sbunicode_007buppercase_007d-329"><code>uppercase [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007buppercase_002dp_007d-312"><code>uppercase-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbmop_007bvalidate_002dsuperclass_007d-200"><code>validate-superclass [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbdebug_007bvar_007d-86"><code>var [sb-debug]</code></a>: <a href="#Variable-Access">Variable Access</a></li>
<li><a href="#index-g_t_0040cl_007bvector_007d-143"><code>vector [cl]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040sbext_007bwait_002dfor_007d-367"><code>wait-for [sb-ext]</code></a>: <a href="#Miscellaneous-Extensions">Miscellaneous Extensions</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bwait_002don_002dgate_007d-622"><code>wait-on-gate [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007bwait_002don_002dsemaphore_007d-513"><code>wait-on-semaphore [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbthread_007bwaitqueue_002dname_007d-523"><code>waitqueue-name [sb-thread]</code></a>: <a href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a></li>
<li><a href="#index-g_t_0040sbext_007bweak_002dpointer_002dvalue_007d-180"><code>weak-pointer-value [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbunicode_007bwhitespace_002dp_007d-319"><code>whitespace-p [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbalien_007bwith_002dalien_007d-384"><code>with-alien [sb-alien]</code></a>: <a href="#Local-Foreign-Variables">Local Foreign Variables</a></li>
<li><a href="#index-g_t_0040cl_007bwith_002dcompilation_002dunit_007d-50"><code>with-compilation-unit [cl]</code></a>: <a href="#Compiler-Policy">Compiler Policy</a></li>
<li><a href="#index-g_t_0040cl_007bwith_002dcompilation_002dunit_007d-32"><code>with-compilation-unit [cl]</code></a>: <a href="#The-Parts-of-a-Compiler-Diagnostic">The Parts of a Compiler Diagnostic</a></li>
<li><a href="#index-g_t_0040sbext_007bwith_002dlocked_002dhash_002dtable_007d-359"><code>with-locked-hash-table [sb-ext]</code></a>: <a href="#Hash-Table-Extensions">Hash Table Extensions</a></li>
<li><a href="#index-g_t_0040sbthread_007bwith_002dmutex_007d-502"><code>with-mutex [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040cl_007bwith_002dopen_002dfile_007d-404"><code>with-open-file [cl]</code></a>: <a href="#External-Formats">External Formats</a></li>
<li><a href="#index-g_t_0040sbsprof_007bwith_002dprofiling_007d-578"><code>with-profiling [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbthread_007bwith_002drecursive_002dlock_007d-503"><code>with-recursive-lock [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbsprof_007bwith_002dsampling_007d-579"><code>with-sampling [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sequence_007bwith_002dsequence_002diterator_007d-274"><code>with-sequence-iterator [sb-sequence]</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sequence_007bwith_002dsequence_002diterator_002dfunctions_007d-275"><code>with-sequence-iterator-functions [sb-sequence]</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040sbext_007bwith_002dunlocked_002dpackages_007d-470"><code>with-unlocked-packages [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bwithout_002dpackage_002dlocks_007d-469"><code>without-package-locks [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbunicode_007bword_002dbreak_002dclass_007d-324"><code>word-break-class [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
<li><a href="#index-g_t_0040sbunicode_007bwords_007d-344"><code>words [sb-unicode]</code></a>: <a href="#Unicode-Support">Unicode Support</a></li>
   </ul><div class="node">
<a name="Variable-Index"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Type-Index">Type Index</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Function-Index">Function Index</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="appendix">Appendix C Variable Index</h2>



<ul class="index-vr" compact="compact">
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bafter_002dgc_002dhooks_007d_007d-173"><code>*after-gc-hooks* [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bcompiler_002dprint_002dvariable_002dalist_007d_007d-22"><code>*compiler-print-variable-alist* [sb-ext]</code></a>: <a href="#Controlling-Verbosity">Controlling Verbosity</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bcore_002dpathname_007d_007d-11"><code>*core-pathname* [sb-ext]</code></a>: <a href="#Saving-a-Core-Image">Saving a Core Image</a></li>
<li><a href="#index-g_t_0040sbthread_007b_0040earmuffs_007bcurrent_002dthread_007d_007d-473"><code>*current-thread* [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bdebug_002dprint_002dvariable_002dalist_007d_007d-64"><code>*debug-print-variable-alist* [sb-ext]</code></a>: <a href="#Debugger-Command-Loop">Debugger Command Loop</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bed_002dfunctions_007d_007d-350"><code>*ed-functions* [sb-ext]</code></a>: <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bevaluator_002dmode_007d_007d-60"><code>*evaluator-mode* [sb-ext]</code></a>: <a href="#Interpreter">Interpreter</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bexit_002dhooks_007d_007d-17"><code>*exit-hooks* [sb-ext]</code></a>: <a href="#Initialization-and-Exit-Hooks">Initialization and Exit Hooks</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bgc_002drun_002dtime_007d_007d-181"><code>*gc-run-time* [sb-ext]</code></a>: <a href="#Garbage-Collection">Garbage Collection</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007binit_002dhooks_007d_007d-16"><code>*init-hooks* [sb-ext]</code></a>: <a href="#Initialization-and-Exit-Hooks">Initialization and Exit Hooks</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007binvoke_002ddebugger_002dhook_007d_007d-63"><code>*invoke-debugger-hook* [sb-ext]</code></a>: <a href="#Debugger-Invocation">Debugger Invocation</a></li>
<li><a href="#index-g_t_0040sbsprof_007b_0040earmuffs_007bmax_002dsamples_007d_007d-586"><code>*max-samples* [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbdebug_007b_0040earmuffs_007bmax_002dtrace_002dindentation_007d_007d-117"><code>*max-trace-indentation* [sb-debug]</code></a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bmodule_002dprovider_002dfunctions_007d_007d-348"><code>*module-provider-functions* [sb-ext]</code></a>: <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bmuffled_002dwarnings_007d_007d-351"><code>*muffled-warnings* [sb-ext]</code></a>: <a href="#Customization-Hooks-for-Users">Customization Hooks for Users</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bon_002dpackage_002dvariance_007d_007d-171"><code>*on-package-variance* [sb-ext]</code></a>: <a href="#Package-Variance">Package Variance</a></li>
<li><a href="#index-g_t_0040cl_007b_0040earmuffs_007bpackage_007d_007d-440"><code>*package* [cl]</code></a>: <a href="#Implementation-Packages">Implementation Packages</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bposix_002dargv_007d_007d-283"><code>*posix-argv* [sb-ext]</code></a>: <a href="#Command_002dline-arguments">Command-line arguments</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bposix_002dargv_007d_007d-5"><code>*posix-argv* [sb-ext]</code></a>: <a href="#Shebang-Scripts">Shebang Scripts</a></li>
<li><a href="#index-g_t_0040sbsprof_007b_0040earmuffs_007bsample_002dinterval_007d_007d-587"><code>*sample-interval* [sb-sprof]</code></a>: <a href="#Statistical-Profiler">Statistical Profiler</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bsave_002dhooks_007d_007d-8"><code>*save-hooks* [sb-ext]</code></a>: <a href="#Saving-a-Core-Image">Saving a Core Image</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bstack_002dallocate_002ddynamic_002dextent_007d_007d-139"><code>*stack-allocate-dynamic-extent* [sb-ext]</code></a>: <a href="#Dynamic_002dextent-allocation">Dynamic-extent allocation</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007bsysinit_002dpathname_002dfunction_007d_007d-9"><code>*sysinit-pathname-function* [sb-ext]</code></a>: <a href="#Saving-a-Core-Image">Saving a Core Image</a></li>
<li><a href="#index-g_t_0040sbdebug_007b_0040earmuffs_007btrace_002dencapsulate_002ddefault_007d_007d-118"><code>*trace-encapsulate-default* [sb-debug]</code></a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-g_t_0040sbdebug_007b_0040earmuffs_007btrace_002dindentation_002dstep_007d_007d-116"><code>*trace-indentation-step* [sb-debug]</code></a>: <a href="#Function-Tracing">Function Tracing</a></li>
<li><a href="#index-g_t_0040sbext_007b_0040earmuffs_007buserinit_002dpathname_002dfunction_007d_007d-10"><code>*userinit-pathname-function* [sb-ext]</code></a>: <a href="#Saving-a-Core-Image">Saving a Core Image</a></li>
<li><a href="#index-g_t_0040sbpcl_007b_002bslot_002dunbound_002b_007d-233"><code>+slot-unbound+ [sb-pcl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
   </ul><div class="node">
<a name="Type-Index"></a>
<p></p><hr>
Next:&nbsp;<a rel="next" accesskey="n" href="#Colophon">Colophon</a>,
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Variable-Index">Variable Index</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="appendix">Appendix D Type Index</h2>



<ul class="index-tp" compact="compact">
<li><a href="#index-g_t_0040cl_007bbuilt_002din_002dclass_007d-222"><code>built-in-class [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbext_007bcode_002ddeletion_002dnote_007d-29"><code>code-deletion-note [sb-ext]</code></a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
<li><a href="#index-g_t_0040sbext_007bcompiler_002dnote_007d-28"><code>compiler-note [sb-ext]</code></a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
<li><a href="#index-g_t_0040sbext_007bdeprecation_002dcondition_007d-674"><code>deprecation-condition [sb-ext]</code></a>: <a href="#Deprecation-Conditions">Deprecation Conditions</a></li>
<li><a href="#index-g_t_0040sbext_007bdeprecation_002derror_007d-678"><code>deprecation-error [sb-ext]</code></a>: <a href="#Deprecation-Conditions">Deprecation Conditions</a></li>
<li><a href="#index-g_t_0040sbext_007bearly_002ddeprecation_002dwarning_007d-675"><code>early-deprecation-warning [sb-ext]</code></a>: <a href="#Deprecation-Conditions">Deprecation Conditions</a></li>
<li><a href="#index-g_t_0040cl_007berror_007d-25"><code>error [cl]</code></a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
<li><a href="#index-g_t_0040sbposix_007bfile_002ddescriptor_007d-652"><code>file-descriptor [sb-posix]</code></a>: <a href="#File_002ddescriptors">File-descriptors</a></li>
<li><a href="#index-g_t_0040sbposix_007bfile_002ddescriptor_002ddesignator_007d-653"><code>file-descriptor-designator [sb-posix]</code></a>: <a href="#File_002ddescriptors">File-descriptors</a></li>
<li><a href="#index-g_t_0040sbposix_007bfilename_007d-655"><code>filename [sb-posix]</code></a>: <a href="#Filenames">Filenames</a></li>
<li><a href="#index-g_t_0040sbposix_007bfilename_002ddesignator_007d-656"><code>filename-designator [sb-posix]</code></a>: <a href="#Filenames">Filenames</a></li>
<li><a href="#index-g_t_0040sbext_007bfinal_002ddeprecation_002dwarning_007d-677"><code>final-deprecation-warning [sb-ext]</code></a>: <a href="#Deprecation-Conditions">Deprecation Conditions</a></li>
<li><a href="#index-g_t_0040sbposix_007bflock_007d-658"><code>flock [sb-posix]</code></a>: <a href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bfrlock_007d-625"><code>frlock [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbmop_007bfuncallable_002dstandard_002dclass_007d-203"><code>funcallable-standard-class [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbmop_007bfuncallable_002dstandard_002dobject_007d-195"><code>funcallable-standard-object [sb-mop]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bfunction_007d-197"><code>function [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dbinary_002dinput_002dstream_007d-410"><code>fundamental-binary-input-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dbinary_002doutput_002dstream_007d-411"><code>fundamental-binary-output-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dbinary_002dstream_007d-408"><code>fundamental-binary-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dcharacter_002dinput_002dstream_007d-412"><code>fundamental-character-input-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dcharacter_002doutput_002dstream_007d-413"><code>fundamental-character-output-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dcharacter_002dstream_007d-409"><code>fundamental-character-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dinput_002dstream_007d-406"><code>fundamental-input-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002doutput_002dstream_007d-407"><code>fundamental-output-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbgray_007bfundamental_002dstream_007d-405"><code>fundamental-stream [sb-gray]</code></a>: <a href="#Gray-Streams-classes">Gray Streams classes</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bgate_007d-615"><code>gate [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040cl_007bgeneric_002dfunction_007d-193"><code>generic-function [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bhost_002dent_007d-567"><code>host-ent [sb-bsd-sockets]</code></a>: <a href="#Name-Service">Name Service</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007binet_002dsocket_007d-561"><code>inet-socket [sb-bsd-sockets]</code></a>: <a href="#INET-Domain-Sockets">INET Domain Sockets</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007binet6_002dsocket_007d-562"><code>inet6-socket [sb-bsd-sockets]</code></a>: <a href="#INET-Domain-Sockets">INET Domain Sockets</a></li>
<li><a href="#index-g_t_0040sbthread_007binterrupt_002dthread_002derror_007d-489"><code>interrupt-thread-error [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bjoin_002dthread_002derror_007d-490"><code>join-thread-error [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007blate_002ddeprecation_002dwarning_007d-676"><code>late-deprecation-warning [sb-ext]</code></a>: <a href="#Deprecation-Conditions">Deprecation Conditions</a></li>
<li><a href="#index-g_t_0040cl_007blist_007d-243"><code>list [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007blocal_002dsocket_007d-566"><code>local-socket [sb-bsd-sockets]</code></a>: <a href="#Local-_0028Unix_0029-Domain-Sockets">Local (Unix) Domain Sockets</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bmailbox_007d-603"><code>mailbox [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007bmutex_007d-501"><code>mutex [sb-thread]</code></a>: <a href="#Mutex-Support">Mutex Support</a></li>
<li><a href="#index-g_t_0040sbext_007bname_002dconflict_007d-354"><code>name-conflict [sb-ext]</code></a>: <a href="#Resolution-of-Name-Conflicts">Resolution of Name Conflicts</a></li>
<li><a href="#index-g_t_0040cl_007bpackage_002derror_007d-445"><code>package-error [cl]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlock_002dviolation_007d-458"><code>package-lock-violation [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlock_002dviolation_007d-442"><code>package-lock-violation [sb-ext]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlocked_002derror_007d-459"><code>package-locked-error [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bpackage_002dlocked_002derror_007d-443"><code>package-locked-error [sb-ext]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040sbposix_007bpasswd_007d-659"><code>passwd [sb-posix]</code></a>: <a href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a></li>
<li><a href="#index-g_t_0040sequence_007bprotocol_002dunimplemented_007d-256"><code>protocol-unimplemented [sb-sequence]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbconcurrency_007bqueue_007d-593"><code>queue [sb-concurrency]</code></a>: <a href="#sb_002dconcurrency">sb-concurrency</a></li>
<li><a href="#index-g_t_0040sbthread_007bsemaphore_007d-510"><code>semaphore [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040sbthread_007bsemaphore_002dnotification_007d-517"><code>semaphore-notification [sb-thread]</code></a>: <a href="#Semaphores">Semaphores</a></li>
<li><a href="#index-g_t_0040cl_007bsequence_007d-273"><code>sequence [cl]</code></a>: <a href="#Iterator-Protocol">Iterator Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bsequence_007d-236"><code>sequence [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbbsdsockets_007bsocket_007d-536"><code>socket [sb-bsd-sockets]</code></a>: <a href="#General-Sockets">General Sockets</a></li>
<li><a href="#index-g_t_0040cl_007bstandard_002dclass_007d-202"><code>standard-class [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bstandard_002dgeneric_002dfunction_007d-194"><code>standard-generic-function [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bstandard_002dobject_007d-245"><code>standard-object [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040cl_007bstandard_002dobject_007d-196"><code>standard-object [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbposix_007bstat_007d-660"><code>stat [sb-posix]</code></a>: <a href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a></li>
<li><a href="#index-g_t_0040cl_007bstructure_002dclass_007d-219"><code>structure-class [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040cl_007bstyle_002dwarning_007d-27"><code>style-warning [cl]</code></a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
<li><a href="#index-g_t_0040sbext_007bsymbol_002dpackage_002dlocked_002derror_007d-460"><code>symbol-package-locked-error [sb-ext]</code></a>: <a href="#Package-Lock-Dictionary">Package Lock Dictionary</a></li>
<li><a href="#index-g_t_0040sbext_007bsymbol_002dpackage_002dlocked_002derror_007d-444"><code>symbol-package-locked-error [sb-ext]</code></a>: <a href="#Package-Lock-Violations">Package Lock Violations</a></li>
<li><a href="#index-g_t_0040cl_007bt_007d-221"><code>t [cl]</code></a>: <a href="#Metaobject-Protocol">Metaobject Protocol</a></li>
<li><a href="#index-g_t_0040sbposix_007btermios_007d-661"><code>termios [sb-posix]</code></a>: <a href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a></li>
<li><a href="#index-g_t_0040sbthread_007bthread_007d-472"><code>thread [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbthread_007bthread_002derror_007d-487"><code>thread-error [sb-thread]</code></a>: <a href="#Threading-basics">Threading basics</a></li>
<li><a href="#index-g_t_0040sbext_007btimer_007d-528"><code>timer [sb-ext]</code></a>: <a href="#Timers">Timers</a></li>
<li><a href="#index-g_t_0040sbposix_007btimeval_007d-662"><code>timeval [sb-posix]</code></a>: <a href="#Lisp-objects-and-C-structures">Lisp objects and C structures</a></li>
<li><a href="#index-g_t_0040cl_007bvector_007d-237"><code>vector [cl]</code></a>: <a href="#Extensible-Sequences">Extensible Sequences</a></li>
<li><a href="#index-g_t_0040sbthread_007bwaitqueue_007d-521"><code>waitqueue [sb-thread]</code></a>: <a href="#Waitqueue_002fcondition-variables">Waitqueue/condition variables</a></li>
<li><a href="#index-g_t_0040cl_007bwarning_007d-26"><code>warning [cl]</code></a>: <a href="#Diagnostic-Severity">Diagnostic Severity</a></li>
   </ul><div class="node">
<a name="Colophon"></a>
<p></p><hr>
Previous:&nbsp;<a rel="previous" accesskey="p" href="#Type-Index">Type Index</a>,
Up:&nbsp;<a rel="up" accesskey="u" href="#Top">Top</a>

</div>

<!-- node-name,  next,  previous,  up -->
<h2 class="unnumbered">Colophon</h2>

<p>This manual is maintained in Texinfo, and automatically translated
into other forms (e.g. HTML or pdf). If you're <em>reading</em> this
manual in one of these non-Texinfo translated forms, that's fine, but
if you want to <em>modify</em> this manual, you are strongly advised to
seek out a Texinfo version and modify that instead of modifying a
translated version. Even better might be to seek out <em>the</em>
Texinfo version (maintained at the time of this writing as part of the
SBCL project at <a href="http://sbcl.sourceforge.net/">http://sbcl.sourceforge.net/</a>) and submit a
patch.

   </p><div class="footnote">
<hr>
<a name="texinfo-footnotes-in-document"></a><h4>Footnotes</h4><p class="footnote"><small>[<a name="fn-1" href="#fnd-1">1</a>]</small> Historically, the ILISP package at
<a href="http://ilisp.cons.org/">http://ilisp.cons.org/</a> provided similar functionality, but it
does not support modern SBCL versions.</p>

   <p class="footnote"><small>[<a name="fn-2" href="#fnd-2">2</a>]</small> Actually, this declaration is unnecessary in
SBCL, since it already knows that <code>position</code> returns a
non-negative <code>fixnum</code> or <code>nil</code>.</p>

   <p class="footnote"><small>[<a name="fn-3" href="#fnd-3">3</a>]</small> A deprecated
extension <code>sb-ext:inhibit-warnings</code> is still supported, but
liable to go away at any time.</p>

   <p class="footnote"><small>[<a name="fn-4" href="#fnd-4">4</a>]</small> Since the location of an interrupt or hardware
error will always be an unknown location, non-argument variable values
will never be available in the interrupted frame.  See <a href="#Unknown-Locations-and-Interrupts">Unknown Locations and Interrupts</a>.</p>

   <p class="footnote"><small>[<a name="fn-5" href="#fnd-5">5</a>]</small> The variable bindings are actually created
using the Lisp <code>symbol-macrolet</code> special form.</p>

   <p class="footnote"><small>[<a name="fn-6" href="#fnd-6">6</a>]</small> A motivation, rationale and additional examples for the design
of this extension can be found in the paper <cite>Rhodes, Christophe
(2007): User-extensible sequences in Common Lisp</cite> available for download
at
<a href="http://www.doc.gold.ac.uk/%7Emas01cr/papers/ilc2007/sequences-20070301.pdf">http://www.doc.gold.ac.uk/~mas01cr/papers/ilc2007/sequences-20070301.pdf</a>.</p>

   <p class="footnote"><small>[<a name="fn-7" href="#fnd-7">7</a>]</small> In SBCL versions prior to 1.0.13, <code>sb-ext:run-program</code>
searched for executables in a manner somewhat incompatible with other
languages.  As of this version, SBCL uses the system library routine
<code>execvp(3)</code>, and no longer contains the function,
<code>find-executable-in-search-path</code>, which implemented the old
search.  Users who need this function may find it
in <samp><span class="file">run-program.lisp</span></samp> versions 1.67 and earlier in SBCL's CVS
repository here
<a href="http://sbcl.cvs.sourceforge.net/sbcl/sbcl/src/code/run-program.lisp?view=log">http://sbcl.cvs.sourceforge.net/sbcl/sbcl/src/code/run-program.lisp?view=log</a>. However,
we caution such users that this search routine finds executables that
system library routines do not.</p>

   <p class="footnote"><small>[<a name="fn-8" href="#fnd-8">8</a>]</small> Please
note that the codepoint U+1F5CF (PAGE) introduced in Unicode 7.0 is
named <code>UNICODE_PAGE</code>, since the name “Page” is required to be
assigned to form-feed (U+0C) by the ANSI standard.</p>

   <p class="footnote"><small>[<a name="fn-9" href="#fnd-9">9</a>]</small> See chapter 7 "Testing widely used RNGs" in
<cite>TestU01: A C Library for Empirical Testing of Random Number
Generators</cite> by Pierre L'Ecuyer and Richard Simard, ACM Transactions on
Mathematical Software, Vol. 33, article 22, 2007.</p>

   <p class="footnote"><small>[<a name="fn-10" href="#fnd-10">10</a>]</small> The functionality contained in the package
<code>SB-UNIX</code> is for SBCL internal use only; its contents are likely to
change from version to version.</p>

   <p class="footnote"><small>[<a name="fn-11" href="#fnd-11">11</a>]</small> See “namespace” entry in the glossary
of the Common Lisp Hyperspec.</p>

   <hr></div>




</body></html>
<!--

Local Variables:
coding: utf-8
End:

-->