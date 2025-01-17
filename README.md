# Elk
![Elk logo](https://raw.githubusercontent.com/rockola/elk-scheme/master/doc/elk-logo.png)

This fork is based on Elk 3.99.8, a pre-release of Elk 4.0, the
Extension Language Kit.

## Build
Tested on Ubuntu 22.04.
```
autoreconf -i
./configure
make
```
Install `elk` in `/usr/local/bin`, man pages in `/usr/local/share/man`, and 
libraries in `/usr/local/lib`:
```
sudo make install
sudo ldconfig
```

## What is Elk?

Elk is an implementation of the Scheme programming language.  In
contrast to existing, stand-alone Scheme systems Elk has been designed
specifically as an embeddable, reusable extension language subsystem
for applications written in C or C++.

Developers using Elk can deliver applications with different components
written in different languages, such as an efficient core written in
C or C++ and an extensible user interface layer implemented in Scheme.
To help building hybrid application architectures, Elk supports a
tightly-knit interworking of the C/C++ parts of applications with
Scheme code.

Elk is also useful as a stand-alone Scheme implementation, in particular
as a platform for rapid prototyping of X11-based Scheme programs.

The Elk project was started in 1987 to support ISOTEXT, a multimedia
document editor that has been developed at the Technical University of
Berlin.  The first freely available version, Elk 1.0, was published in
USENET in September 1989.  Since then, Elk has been successfully used as
the extension language framework for numerous applications (commercial
products as well as free software projects).


## Getting Elk

https://github.com/rockola/elk-scheme

A non-trivial example application using Elk as its extension language
is available as source (`unroff` is a troff
translator with back-ends for HTML and the -ms and -man macros):

http://github.com/rockola/unroff


### Original v3.99

Elk 3.99.8 is mirrored on GitHub at https://github.com/cellularmitosis/elk-scheme-mirror

You can obtain the Elk 3.99 distribution as well as additional information
about Elk at http://sam.zoy.org/elk/


## Elk features

###  Full incremental, dynamic loading

This facility enables Scheme code to load compiled Scheme extensions
into the running interpreter (or into the application) on demand.
Complex Elk-based applications can be decomposed into dynamically
loadable components to avoid large, monolithic executables.
Furthermore, user-supplied extension need not be written entirely in
Scheme; they may include an efficient, low-level layer written in C or
C++.

Dynamic loading in Elk is supported on many platforms and is not
restricted to a dlopen() interface.  Elk provides automatic
initialization of dynamically loaded extensions and takes care of C++
static constructors/destructors embedded in object files.

###  Freezing of fully customized applications into executable files

Elk provides a new Scheme primitive `dump` which freezes the dynamic
runtime image of the Scheme interpreter into an executable file
(including an enclosing application if present).  This facility
resembles `unexec()` in Emacs, but the new executable resumes
execution by returning from the call to `dump` by which that
executable was created (not unlike `fork()` in UNIX).  Dynamic loading
and `dump` increase the usability of Elk as the backbone of complex
applications.

###  Powerful C/C++ interface for language interoperability

Elk provides for a tight integration of the C/C++ core of applications
(or extensions) with the extension language.  Applications can define
their own Scheme primitives (three calling disciplines are supported),
define application-specific first-class Scheme types with customized
print and read functions, convert objects between Scheme types and
C/C++ types in various ways, implement weak data structures, raise
Scheme errors, define Scheme variables and symbols, evaluate
S-expressions encoded as C strings, and utilize the garbage collector.

### Full Scheme bindings for X11 and Motif

Several dynamically loadable extensions provide full Scheme access to
the X11/OpenWindows Xlib, to the application programmer interface of
the Xt intrinsics, and to the Athena and OSF/Motif widget sets.  Using
these extensions, the graphical user-interfaces of Elk-based
applications can be built entirely in the extension language.

###  UNIX interface

Elk provides Scheme access to most UNIX system calls and common C
library functions.  The UNIX extension supports a wide range of
different UNIX platforms without restricting its functionality to the
lowest common denominator or to the POSIX 1003.1 functions.

###  Stop-and-copy and generational, incremental garbage collection

Elk employs two garbage collection strategies selectable at compile
time: a traditional stop-and-copy garbage collector and a generational
garbage collector which is more efficient and thus reduces the time
the application is disrupted by a garbage collection.  On platforms
with advanced memory management, "incremental" mode can be enabled for
the generational garbage collector to further reduce wait times.

###  Non-standard Scheme features

In addition to the standard Scheme core, Elk supports first-class
environments, error handling, provide/require and autoloading, fluid
bindings and dynamic-wind, simple `eval-twice`-style macros, property
lists, string ports and bidirectional ports, shell-style "tilde
expansion" in filenames, an interactive top-level written in Scheme, a
Scheme debugger and a pretty printer, arbitrary length bitstrings, and
Scheme records.

###  Comprehensive documentation

The distribution includes 230+ pages of fully indexed documentation.
All manuals exist as troff input files which can be translated to
HTML (with [`unroff`](https://github.com/rockola/unroff)) for online
browsing in addition to producing typeset- quality printed versions.

###  Distributed in legally unencumbered form

The copyright/license agreement permits free redistribution and use
of Elk in commercial products.

## Why is Elk using Scheme?

As extensions can get as large and complex as freestanding programs,
extension language programmers (usually the users of the application)
deserve the same language features that other programmers are
accustomed to.  By using a general-purpose programming language rather
than a specialized scripting language, non-trivial extensions can
benefit from the structuring functionality inherent in real programming
languages (such as Lisp).

Members of the Lisp language family are particularly suitable as an
extension language:  Lisp has a simple syntax but powerful semantics,
it allows for small implementations, and its interactive nature
supports rapid prototyping and encourages users to explore and test
solutions to problems in an incremental way.

Consequently, Lisp has become increasingly popular for this purpose, to
the point where the abundance of different dialects has grown into a
problem.  Of the standardized dialects of Lisp, only Scheme is suitably
modest, yet sufficiently general, to serve as a reusable extension
language for a wide range of applications.  Scheme is orthogonal and
well-defined, and it is small enough to not dominate the application it
serves and to be fully understood with acceptable effort.


## The Elk distribution

Here is a brief roadmap for the subdirectories and files included in
the distribution.

* [`README`](README.md) Explains the purpose and release status of Elk
* [`CHANGES`](CHANGES) Lists the changes between this and earlier
  releases of Elk
* [`MIGRATE`](MIGRATE) Explains how C/C++ code (applications or
  extensions) written for older versions of Elk may have to be
  modified to make it work with this version
* [`INSTALL`](INSTALL) Instructions for configuring, compiling, and
  installing Elk; a brief description of the files that get installed
  in the process; and a description of the structure of the Makefiles
  and the purpose of Makefile.local and `build` in each source
  directory
* [`MACHINES`](MACHINES) Additional, platform-specific advice for
  installing and using Elk, such as compiler bugs, unsupported
  features, problems with older OS versions and other pitfalls
* [`BUGS`](BUGS)        Information about known problems with this release
* [`TODO`](TODO)        Ideas, improvements and projects for future releases
* [`COPYING`](COPYING)  License (BSD-ish); The copyright status of the distribution
* [`AUTHORS`](AUTHORS) A list of people who have contributed
  significantly to Elk; acknowledgments and credits

* `include/` The include files to be `#include`d by applications that
  use Elk as their extension language, and by extensions to Elk.
  Including `scheme.h` from this directory causes all the other `.h`
  files to be included in the right order.  The include files may or
  may not use ANSI/ISO-C prototypes, depending on the config file you
  have chosen.
* `src/`        The C source files of the Scheme interpreter
* `scm/` Scheme files that are loaded during runtime.  These are
  copied to a destination directory specified in config/site when Elk
  is installed.
* `lib/` This directory tree holds the C source for various Elk
  extensions that can be loaded into the Scheme interpreter or linked
  with an application
  * `xlib/`  The C source files of the X11 Xlib extension
  * `xt/`    The C source files of the Xt (X11 Toolkit Intrinsics) extension
  * `xaw/` The Scheme interfaces to the X11 Athena widgets.  There is
    one `.d` file for each widget class.  Each of these is compiled into
    a C source file when running `make` and then compiled into a
    dynamically loadable object.
  * `xm/`  The .d files for the Motif widgets
  * `unix/`  The C source files of the UNIX extension
  * `misc/` The C source files of the record extension, the bitstring
    extension, the regular expression extension, and various other
    dynamically loadable Elk extensions
* `doc/` The directory tree holding the documentation for
  Elk as troff input files and pre-generated
  PostScript files.  See [`doc/README`](doc/README.md) for a roadmap
  of the `doc` tree.
* `examples/` A collection of demonstration programs for Elk
  and the various extensions (mostly in Scheme)
  * `scheme/`  Basic Scheme demos (collected from USENET and other sources)
  * `xlib/`    Programs demonstrating the Xlib extension
  * `xaw/` Programs demonstrating the Athena extension
  * `xm/` Programs demonstrating the Motif extension
  * `unix/` Example programs for the UNIX extension
  * `regexp/`  A demonstration of the regexp extension
  * `c++/` A few simple C++ programs demonstrating use of Elk with C++
    applications (see README in this directory)
* `util/` Various utilities, some of which may aid in preparing a
  config file for an as yet unsupported platform.
