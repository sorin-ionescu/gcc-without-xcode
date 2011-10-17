# GCC Without Xcode

For a decade, Mac OS X web developers have been asking for the ability to install [GCC](http://gcc.gnu.org) without [Xcode](http://developer.apple.com/technologies/tools/) to compile command line programs from package mangers, such as [MacPorts](http://www.macports.org) and [Homebrew](http://mxcl.github.com/homebrew/), and programming language modules, such as Ruby [gems](http://rubygems.org) and Python [eggs](http://pypi.python.org). 

This project provides a script that will reduce [Install Xcode.app](http://itunes.apple.com/us/app/xcode/id448457090?mt=12) of 3.19 GB to a compressed archive of 284.5 MB (.cpio.gz) or 78.3 MB (.cpio.xz), if [XZ Utils](http://tukaani.org/xz/) are installed, of only the necessary GCC without Xcode files and two convenience scripts to install and uninstall said files.

## Install

Download [Install Xcode.app](http://itunes.apple.com/us/app/xcode/id448457090?mt=12) from the Mac App Store.

![Get Xcode from the App Store](http://i.imgur.com/zcRkN.jpg)

Download this project and copy the scripts somewhere in the `PATH` or leave them where they are and amend it.

    export PATH=$HOME/Downloads/gcc-without-xcode:$PATH.

Execute `sudo make-gcc-without-xcode` (root privileges are necessary to retain file ownership and permissions). 

![make-gcc-without-xcode Screenshot](http://i.imgur.com/snjn8.png)

Install the archive by copying and pasting the displayed installation command, which will be similar to the line bellow.

    cd / && gzcat < '/path/to/gcc-without-xcode-4.1.1-mac-os-x-10.7.cpio.gz' | sudo cpio -idmv

Alternatively, install the archive with the convenience script. 

    sudo install-gcc-without-xcode '/path/to/gcc-without-xcode-4.1.1-mac-os-x-10.7.cpio.gz' /

### Smaller Archive

To create the 72.47% smaller, but less portable, _.cpio.xz_ archive, download [XZ Utils](http://afb.users.sourceforge.net/xz/). Do not download XZ.dmg, which contains an installer that will install the utilities in /usr/local. This is unnecessary since XZ can be installed later from MacPorts or Homebrew. Instead, download **XZ.tbz**, which contains binaries that can be simply extracted. Amend the `PATH` with the location to the XZ Utils.

    export PATH=$HOME/Downloads/XZ/bin:$PATH

  The make script will automatically detect XZ and use it instead of gzip. Replace .gz with .xz in the above installation instructions.

## Uninstall

Use the convenience script to uninstall the archive.

    sudo uninstall-gcc-without-xcode '/path/to/gcc-without-xcode-4.1.1-mac-os-x-10.7.cpio.gz' /

## Caveats

Mac OS X has an atrocious packaging system. Apple packages overwrite files installed by other packages. While the install script does not overwrite existing files, the uninstall script does not check if a file has been overwritten by an Apple package, and therefore, is still needed. It is possible to list all the files in the package receipt database and check if a file that is about to be deleted is still needed by another package and skip it. The uninstall script may be amended in the future to do so at the expense of speed.

To install a new major version of the developer tools, it will be necessary to first uninstall, then create a new archive from the new Xcode Install.app, and then reinstall.

## License

(The MIT License)

Copyright (c) 2011 Sorin Ionescu

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

