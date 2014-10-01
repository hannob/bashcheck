bashcheck
=========

Test script for Shellshock and related vulnerabilities

background
==========

The Bash vulnerability that is now known as Shellshock had an incomplete
fix at first. There are currently 4 public and one supposedly non-public
vulnerability.

usage
=====

Just run script:
 `./bashcheck`

CVE-2014-6271
=============

The original vulnerability.

* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271

CVE-2014-7169
=============

Further parser error, found by Tavis Ormandy (taviso).

* https://twitter.com/taviso/status/514887394294652929
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-7169

CVE-2014-7186
=============

Out of bound memory read error in redir_stack.

* http://seclists.org/oss-sec/2014/q3/712
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-7186

CVE-2014-7187
=============

Off-by-one error in nested loops.
(check only works when Bash is built with -fsanitize=address)

* http://seclists.org/oss-sec/2014/q3/712
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-7187

CVE-2014-6277
=============

Uninitialized Memory use in make_redirect(), found by
Michal Zalewski (lcamtuf).

* http://lcamtuf.blogspot.de/2014/10/bash-bug-how-we-finally-cracked.html
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6277

CVE-2014-6278
=============

Another parser bug, analysis still incomplete, also found
by Michal Zalewski (lcamtuf).

* http://lcamtuf.blogspot.de/2014/10/bash-bug-how-we-finally-cracked.html
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6278

Patch recommendation
====================

Latest upstream patches (4.3 patchlevel 028, 4.2 patchleven 051) now
include all fixes except for the latest lcamtuf issue.

They also add prefixing to variable functions (a variant of Florian
Weimer's patch) and thus although two known (and some possibly unknown)
parser bugs are still unfixed they should not be exploitable.

My current recommendation: Use latest upstream patches.
