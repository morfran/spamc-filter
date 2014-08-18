spamc-filter
============

A pipeline for integrating spamc, spamassassin SQL user prefs and Postfix.

Usage
-----

     spamc-filter --sender=[sender] --recipient=[recipient]

spamc-filter is called with two mandatory arguments, the sender and recipient(s) of the email to be piped to spamc.  The filter attempts to work out the most appropriate user to run spamc as before passing the message on.

Knowing the user allows spamc to fetch the user settings from the SQL source.

Typically this can be used by adding the following line to your Postfix configuration in /etc/postfix/master.cf:

     spamassassin unix -     n       n       -       -       pipe user=spamd argv=/usr/local/bin/spamc-filter --sender=${sender} --recipient=${recipient}

It is also recommended to set the maximum recipients to 1 in /etc/postfix/main.cf:

     spamassassin_destination_recipient_limit=1

Acknowledgements
----------------

This is based on the code and concepts documented on the SpamAssassin wiki in the section on [Using SQL](http://wiki.apache.org/spamassassin/UsingSQL)

License
-------

Copyright 2014 Matthew Hunt

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.
 
You should have received a copy of the GNU General Public License along with this program; if not, write to the Free Software Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
