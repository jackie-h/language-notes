Current state of Timezone updates in different programming languages

Python:
Proposal to add support for IANA/Olsen timezones to the standard library
http://pyfound.blogspot.com/2019/05/paul-ganssle-time-zones-in-standard.html
Current options are this:
https://pypi.org/project/pytz/

Java:
Includes IANA and a timezone updater
https://www.oracle.com/technetwork/java/javase/documentation/tzupdater-readme-136440.html

C++:
Proposal for C++ 20 to add to the standard library
https://mariusbancila.ro/blog/2018/03/27/cpp20-calendars-and-time-zones/

NodeJS:
https://github.com/nodejs/help/issues/1843
Uses ICU (C++)


ICU - 
http://site.icu-project.org/
ICU is a mature, widely used set of C/C++ and Java libraries providing Unicode and Globalization support for software applications. ICU is widely portable and gives applications the same results on all platforms and between C/C++ and Java software.

Operating systems:
Linux - includes IANA
MacOS - includes IANA
Windows - Microsoft Timezone 
