Voxer Nagios Plugins
====================

Plugins for nagios used by [Voxer][0], made specifically for [SmartOS][1]

Plugins
-------

### check_svcs

Check for services in SMF that are not functioning properly

    ~ $ ./check_svcs
    ok: all services are online

### check_hard_errors

Check kstat for hard errors - useful for identifying failing hardware

    ~ $ ./check_hard_errors
    ok: no hard errors found

### check_mem

Like `check_disk` for memory usage using kstat to calculate used memory

    ~ $ ./check_mem -w 90 -c 95
    ok: 4% used (warning=90%, critical=95%)

### check_disk_busy

Like `check_mem` for disk utilization

    ~ $ ./check_disk_busy -w 90 -c 95 sd1
    ok: disk 20% busy (warning=90%, critical=95%, disk=sd1)

The final argument is the disk name to check (defaults to `sd1`), if
you supply an invalid name, a list of all disks will be printed to
stderr.

### check_proc_count

Count and alert on the number of running processes.  The benefit of this check
over the built-in `check_proc` is that this script only does process count, so
it is fast, and also does not require escalated privileges.

    ~ $ ./check_proc_count -w 200 -c 400
    ok: 30 processes running

### check_proc_owners

Look for running processes with an invalid or removed UID.  This is usually
a sign that an automatically generated user from something like `pkgin` has
been clobbered by configuration management software.

    ~ $ ./check_proc_owners
    critical: 2 processes found without valid UIDs
    ~ $ ./check_proc_owners -v
    critical: 2 processes found without valid UIDs
    pid 47247 (uid 2033): sh
    pid 47251 (uid 2033): node server.js v

Supply `-v` for verbose output, suitable for interactive use.

Notes
-----

Some of the plugins rely on GNU grep being present.
You can install it with `pkgin in ggrep`, and then just make sure that
`/opt/local/bin` is in your PATH. The following list is the plugins that
require GNU grep being present.

* check_svcs

License
-------

LICENSE - "MIT License"
Copyright (c) 2012 Voxer LLC. All rights reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[0]: http://voxer.com
[1]: http://smartos.org
