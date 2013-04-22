Coursera Downloader
===================

[![Build Status](https://travis-ci.org/nonsleepr/coursera.png?branch=master)](https://travis-ci.org/nonsleepr/coursera)

[Coursera][1] is arguably the leader in *massive open online courses* (MOOC) 
with a selection of more than 300 classes from 62 different institutions [as of 
February 2013][13]. Generous contributions by educators and institutions are 
making excellent education available to many who could not afford it otherwise. 
There are even non-profits with "feet on the ground" in remote areas of the
world who are helping spread the wealth (see the feedback below from [Tunapanda][14]).

This script makes it easier to batch download lecture resources (e.g., videos, ppt,
etc) for Coursera classes.  Given one or more class names and account credentials, 
it obtains week and class names from the *lectures* page, and then downloads 
the related materials into appropriately named files and directories.

Why is this helpful?  A utility like [`wget`][2] can work, but has the
following limitations:

1. Video names have a number in them, but this does not correspond to the
   actual order.  Manually renaming them is a pain.
2. Using names from the syllabus page provides more informative names.
3. Using a wget in a for loop picks up extra videos which are not
   posted/linked, and these are sometimes duplicates.

*DownloadThemAll* is another possiblity, but this script provides more features such
as appropriately named files.

This work was originally inspired in part by [youtube-dl][3] by which 
I've downloaded many other good videos such as those from Khan Academy.


Features
--------

  * Intentionally detailed names, so that it will display and sort properly
    on most interfaces (e.g., MX Video on Android phone).
  * Regex-based section (week) and lecture name filters to download only
    certain resources.
  * File format extension filter to grab resource types you want.
  * Login credentials accepted on command-line or from `.netrc` file
  * Core functionality tested on Linux, Mac and Windows.


Directions
----------

Requires Python 3.3 (or newer) and a free Coursera account enrolled in
the class of interest.

1\. Install any missing dependencies.

If you are using pip, you can directly install all the dependencies from the
requirements file using `pip install -r requirements.txt`.

2\. Create a Coursera.org account and enroll in a class.
e.g. http://saas-class.org

3\. Run the script to download the materials by providing your Coursera
account (e.g., email address), password (or a `~/.netrc` file), the class names

    General:                     coursera-dl -u <user> -p <pass> saas
    Multiple classes:            coursera-dl -u <user> -p <pass> saas nlp proglang-2012-001
    Filter by section name:      coursera-dl -u <user> -p <pass> -sf "Chapter_Four" saas
    Filter by lecture name:      coursera-dl -u <user> -p <pass> -lf "3.1_" saas
    Download only ppt files:     coursera-dl -u <user> -p <pass> -f "ppt" saas
    Use a ~/.netrc file (will be used automatically, if user/pass are not specified):
                                 coursera-dl saas
    Specify download path:       coursera-dl --path="C:\Coursera\Classes\" saas
    
    Maintain a list of classes in a dir:
      Initialize:              mkdir -p CURRENT/{class1,class2,..classN}
      Update:                  coursera-dl -n --path CURRENT `ls CURRENT`

On \*nix platforms\*, the use of a `~/.netrc` file is a good alternative to
specifying both your username and password every time on the command
line. To use it, simply add a line like the one below to a file named
`.netrc` in your home directory (or the [equivalent][8], if you are using
Windows) with contents like:

    machine coursera-dl login <user> password <pass>

Create the file if it doesn't exist yet.  From then on, you can switch from
using `-u` and `-p` to simply call `coursera-dl` with the option `-n`
instead.  This is especially convenient, as typing usernames and passwords
directly on the command line can get tiresome (even more if you happened to
choose a "strong" password).

\* if this works on Windows, please add additional instructions for it if
any are needed.

Troubleshooting
---------------

* When reporting bugs against `coursera-dl`, please don't forget to include
  enough information so that you can help us help you:
    * Is the problem happening with the latest version of the script?
    * What is the course that you are trying to access:
    * What is the precise command line that you are using (feel free to hide
      your username and password with asterisks, but leave all other
      information untouched).
    * What are the precise messages that you get? Please, copy and past them.
      Don't reword the messages.

* Make sure the classname you are using corresponds to the resource name used in
  the URL for that class:
    `https://class.coursera.org/<CLASS_NAME>/class/index`

* Previously one could export a Netscape-style cookies file with a browser
  extension ([1][9], [2][10]) for use with the `-c` option, but this
  approach does not appear to work with recent classes. Use the `-u` and
  `-p` flags instead or use the `-n` flag.

* If results show 0 sections, you most likely have provided invalid
  credentials (username and/or password in the command line or in your
  `.netrc` file).


Feedback
--------

I enjoy getting feedback. Here are a few of the comments I've received:

* "Thanks for the good job! Knowledge will flood the World a little more thanks
  to your script!"
  <br>Guillaume V. 11/8/2012
  
* "Just wanted to send you props for your Python script to download Coursera
  courses. I've been using it in Kenya for my non-profit to get online courses
  to places where internet is really expensive and unreliable. Mostly kids here
  can't afford high school, and downloading one of these classes by the usual
  means would cost more than the average family earns in one week. Thanks!"
  <br>Jay L., [Tunapanda][14] 3/20/2013

  
* "I am a big fan of Coursera and attend lots of different courses. Time
  constraints don't allow me to attend all the courses I want at the same time.
  I came across your script, and I am very happily using it!  Great stuff and
  thanks for making this available on Github - well done!"
  <br>William G.  2/18/2013
  
* "This script is awesome! I was painstakingly downloading each and every video
  and ppt by hand -- looked into wget but ran into wildcard issues with HTML,
  and then.. I came across your script.  Can't tell you how many hours you've
  just saved me :) If you're ever in Paris / Stockholm, it is absolutely
  mandatory that I buy you a beer :)"
  <br>Razvan T. 11/26/2012


Contact
-------

Post bugs and issues on [github][11]. Send other comments to John Lehmann:
first last at geemail dotcom or [@jplehmann][12]

[1]: https://www.coursera.org
[2]: http://sourceforge.net/projects/gnuwin32/files/wget/1.11.4-1/wget-1.11.4-1-setup.exe
[3]: https://rg3.github.com/youtube-dl
[4]: http://www.crummy.com/software/BeautifulSoup/bs3
[5]: http://www.crummy.com/software/BeautifulSoup
[6]: http://pypi.python.org/pypi/argparse
[7]: http://pypi.python.org/pypi/setuptools
[8]: http://stackoverflow.com/a/6031266/962311
[9]: https://chrome.google.com/webstore/detail/lopabhfecdfhgogdbojmaicoicjekelh
[10]: https://addons.mozilla.org/en-US/firefox/addon/export-cookies
[11]: https://github.com/jplehmann/coursera/issues
[12]: https://twitter.com/jplehmann
[13]: http://techcrunch.com/2013/02/20/coursera-adds-29-schools-90-courses-and-4-new-languages-to-its-online-learning-platform
[14]: http://www.tunapanda.org
