ssh on Windows
==============

https://www.howtogeek.com/336775/how-to-enable-and-use-windows-10s-built-in-ssh-commands/

PuTTY
-----

Putty has better color support. The links by default are a lighter blue with is readable.
If that fails, there is an option for "use system colors" which in my case gave a white
background and all the links were easy to read.

Recommended: 14 point font.


OpenSSH via Windows PowerShell
------------------------------

Search Bar "powershell" to find Windows PowerShell

    ssh ubuntu@xxx


If OpenSSH Not Already Installed
--------------------------------

Settings -> Search "manage optional" -> Manage Optional Feautures


Find "OpenSSH Client" in the list
(Mine was already installed)

If it's not on the list, click the "+" to add one.
