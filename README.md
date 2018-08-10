# HPSS Wrapper

The HLRS (Höchstleistungsrechenzentrum Stuttgart) has a tape archive system as
usual. The unusual thing is that one can only access it via an FTP connection.
Also it uses a special `pftp_client` which transfers file in a parallel fashion
for more bandwidth. Usability is horrible as one has to enter username and
password and then type `GET` and `PUT` commands for each file that one wants to
transfer.

Documentation can be found in these places:

- https://wickie.hlrs.de/platforms/index.php/HPSS_Introduction
- https://wickie.hlrs.de/platforms/index.php/HPSS_User_Access

This script is a wrapper for the FTP connection to allow doing actual work
instead of monkey work. Previously it had been implemented in Python 2 with the
`pexpect` library and the `pftp_client`, now it uses Python 3 and the `ftplib`
of the standard library and setting the “class of service” to the appropriate
number.

## Usage

Only work with the `start-hpss-agent` program as that loads the needed modules
on Hazel Hen.

First you need to set it up with your username and password. For this call:

    ./start-hpss-agent setup

You will be promted to enter username and password.

To transfer files, use the `put` and `get` subcommands:

    ./start-hpss-agent put FILENAME
    ./start-hpss-agent get FILENAME

In order to get help on all the arguments, use one of the following:

    ./start-hpss-agent -h
    ./start-hpss-agent get -h
    ./start-hpss-agent put -h
