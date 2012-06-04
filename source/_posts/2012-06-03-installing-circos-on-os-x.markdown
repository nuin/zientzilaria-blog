---
layout: post
title: "Installing Circos on OS X"
date: 2012-06-03 19:40
comments: true
categories: tutorial
---


I think one the main topics in the Circos discussion group is how to install it, especially as it requires some specific Perl and C libraries to be in place. This short tutorial gives a step-by-step overview on how to make Circos work on OS X, but it should be similar to other *nix flavours. I just installed on my Mountain Lion box, but, again, it should be identical to previous versions of OS X.

My Circos is installed on

``` bash Circos location
/Applications/circos-0.55/
```

and if we try running it

``` bash Circos trial run
$ perl /Applications/circos-0.55/bin/circos
```

I get this error, initially

```bash Circos runtime error
Can't locate Config/General.pm in @INC (@INC contains: /Applications/circos-0.55/bin/lib /Applications/circos-0.55/bin/../lib
 /Applications/circos-0.55/bin /Library/Perl/5.12/darwin-thread-multi-2level /Library/Perl/5.12
 /Network/Library/Perl/5.12/darwin-thread-multi-2level /Network/Library/Perl/5.12
 /Library/Perl/Updates/5.12.4/darwin-thread-multi-2level /Library/Perl/Updates/5.12.4
 /System/Library/Perl/5.12/darwin-thread-multi-2level /System/Library/Perl/5.12
 /System/Library/Perl/Extras/5.12/darwin-thread-multi-2level /System/Library/Perl/Extras/5.12 .) at
 /Applications/circos-0.55/bin/../lib/Circos.pm line 53.
BEGIN failed--compilation aborted at /Applications/circos-0.55/bin/../lib/Circos.pm line 53.
Compilation failed in require at /Applications/circos-0.55/bin/circos line 184.
BEGIN failed--compilation aborted at /Applications/circos-0.55/bin/circos line 184.
```

So, a lot of things going wrong, we need to check what is missing and install. Circos has a couple of commands bundled in its package that help us working through the errors. Best way to run them is to cd into Circos bin directory

``` bash Circos: checking modules
$ cd /Applications/circos-0.55/bin/
/Applications/circos-0.55/bin$ ./list.modules
```

In my case, running this script gave me a list of the required modules for Circos 

``` bash Circos requirements
Carp
Config::General
Data::Dumper
Digest::MD5
File::Basename
File::Spec::Functions
FindBin
GD
GD::Polyline
Getopt::Long
Graphics::ColorObject
IO::File
List::MoreUtils
List::Util
Math::Bezier
Math::BigFloat
Math::Round
Math::VecStat
Memoize
POSIX
Params::Validate
Pod::Usage
Readonly
Regexp::Common
Set::IntSpan
Storable
Time::HiRes
```

Another script checks for the current status of each module (still from the same dir)

``` bash Circos checking modules
/Applications/circos-0.55/bin$ ./test.modules
```

and this finally gives me a list of the current status of each one of the required modules

``` bash Circos: requirements
ok   Carp
fail Config::General is not usable (it or a sub-module is missing)
ok   Data::Dumper
ok   Digest::MD5
ok   File::Basename
ok   File::Spec::Functions
ok   FindBin
fail GD is not usable (it or a sub-module is missing)
fail GD::Polyline is not usable (it or a sub-module is missing)
ok   Getopt::Long
fail Graphics::ColorObject is not usable (it or a sub-module is missing)
ok   IO::File
ok   List::MoreUtils
ok   List::Util
fail Math::Bezier is not usable (it or a sub-module is missing)
ok   Math::BigFloat
ok   Math::Round
fail Math::VecStat is not usable (it or a sub-module is missing)
ok   Memoize
ok   POSIX
ok   Params::Validate
ok   Pod::Usage
fail Readonly is not usable (it or a sub-module is missing)
ok   Regexp::Common
fail Set::IntSpan is not usable (it or a sub-module is missing)
ok   Storable
ok   Time::HiRes
```

We have to address everything that failed in the test. In this case, *GD*, *Graphics::ColorObjects*, *Math::VecStat*, *Readonly* and *Set::IntSpan*. We leave GD behind for a moment and focus on the other modules (this list might vary for each Perl installation, so you might need to install more or less modules, but the commands are similar).

The easiest way to install module in Perl is to use *cpan*, the repository of Perl modules. It has an interactive shell that we can use, and we will see how to do that. In order to make sure our installation works we use *sudo* and call *cpan* (from any directory)

``` bash
$ sudo cpan
```

If this is the first time you are running it, just answer **yes** to all config questions and you are good to go. Now we have to install the five modules required. By using the command *install*, that can be achieved

``` bash
cpan$ install Config::General
-output omitted-

cpan$ install Graphics::ColorObject
-output omitted-

cpan$ install Math::Bezier
-output omitted-

cpan$ install Math::VecStat
-output omitted-

cpan$ install Readonly
-output omitted-

cpan$ install Set::IntSpan
-output omitted-
```

Now, we deal with the last module and usually the most labourious to install, *GD*. Ideally you should have all possible library support for *GD* and for this you have to install additional libraries. We are going to start with two of the most common and see if we need anything else. Usually **libjpeg** and **libpng** are required by *GD*. So, let's download both of them

``` bash Downloading and install libjpeg and libpng
$ mkdir srctemp
$ cd srctemp
srctemp$ curl -O http://www.ijg.org/files/jpegsrc.v8d.tar.gz
srctemp$ tar -xzvf jpegsrc.v8d.tar.gz
srctemp$ cd jpeg-8d
srctemp/jpeg-8d$ ./configure
srctemp/jpeg-8d$ make
srctemp/jpeg-8d$ sudo make install

srctemp/jpeg-8d$ cd ..
srctemp$ curl -O ftp://ftp.simplesystems.org/pub/libpng/png/src/libpng-1.5.10.tar.gz
srctemp$ tar -xzvf libpng-1.5.10.tar.gz
srctemp$ cd libpng-1.5.10
srctemp/libpng-1.5.10$ ./configure
srctemp/libpng-1.5.10$ make
srctemp/libpng-1.5.10$ sudo make install
```

That should do it for now. We will download *GD* and check if the configuration we have so far is enough. *GD*'s website is still down, but we can get the source from Bitbucket and use identical commands to install is

``` bash Installing GD
srctemp$ curl -O https://bitbucket.org/pierrejoye/gd-libgd/get/GD_2_0_33.tar.gz
srctemp$ tar -xzvf GD_2_0_33.tar.gz
srctemp$ cd pierrejoye-gd-libgd-5551f61978e3/src
srctemp/pierrejoye-gd-libgd-5551f61978e3/src$ ./configure
```

At the end of the configuration run, you should see something like this

``` bash
** Configuration summary for gd 2.0.33:

   Support for PNG library:          yes
   Support for JPEG library:         yes
   Support for Freetype 2.x library: yes
   Support for Fontconfig library:   yes
   Support for Xpm library:          no
   Support for pthreads:             yes
```

In my case, I'm good to go. But if in your case *Freetype* and *Fontconfig* are missing, you would have to download, configure, make and install them, just like *libpng* and *libjpeg*. So now 

``` bash
srctemp/pierrejoye-gd-libgd-5551f61978e3/src$ make
srctemp/pierrejoye-gd-libgd-5551f61978e3/src$ sudo make install
```

We are almost there. The last step is to install *GD* in Perl. Normally, if we use *cpan* to install it on OS X, it fails. So, we will have to do it by hand. We go to CPAN website and download the latest Perl's *GD* implementation and with similar commands to above we install it.

``` bash Installing GD on perl
srctemp$ curl -O http://search.cpan.org/CPAN/authors/id/L/LD/LDS/GD-2.46.tar.gz (if curl fails copy and past on your browser)
srctemp$ tar -xzvf GD-2.46.tar.gz
srctemp$ cd GD-2.46
srctemp/GD-2.46$ perl Makefile.PL
srctemp/GD-2.46$ make
srctemp/GD-2.46$ sudo make install
```

you should see some output, maybe some warnings, but if you followed all the steps above the installation worked. You can run the *test.modules* script in order to check.

Leave a comment, if you get any errors, or send me an email.

