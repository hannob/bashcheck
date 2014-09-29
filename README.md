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

Not yet published parser bug by Michal Zalewski (lcamtuf).

* http://lcamtuf.blogspot.de/2014/09/bash-bug-apply-unofficial-patch-now.html
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6277

CVE-2014-6278
=============

Another not yet published parser bug by Michal Zalewski (lcamtuf).

* http://lcamtuf.blogspot.de/2014/09/bash-bug-apply-unofficial-patch-now.html
* https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6278
