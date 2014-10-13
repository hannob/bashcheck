#!/bin/bash

warn() {
	if [ "$scary" == "1" ]; then
		echo -e "\033[91mVulnerable to $1\033[39m"
	else
		echo -e "\033[93mFound non-exploitable $1\033[39m"
	fi
}

good() {
	echo -e "\033[92mNot vulnerable to $1\033[39m"
}

tmpdir=`mktemp -d -t tmp.XXXXXXXX`

[ -n "$1" ] && bash=$(which $1) || bash=$(which bash)
echo -e "\033[95mTesting $bash ..."
$bash -c 'echo "Bash version $BASH_VERSION"'
echo -e "\033[39m"

#r=`a="() { echo x;}" $bash -c a 2>/dev/null`
if [ -n "$(env 'a'="() { echo x;}" $bash -c a 2>/dev/null)" ]; then
	echo -e "\033[91mVariable function parser active, maybe vulnerable to unknown parser bugs\033[39m"
	scary=1
elif [ -n "$(env 'BASH_FUNC_a%%'="() { echo x;}" $bash -c a 2>/dev/null)" ]; then
	echo -e "\033[92mVariable function parser pre/suffixed [%%, upstream], bugs not exploitable\033[39m"
	scary=0
elif [ -n "$(env 'BASH_FUNC_a()'="() { echo x;}" $bash -c a 2>/dev/null)" ]; then
	echo -e "\033[92mVariable function parser pre/suffixed [(), redhat], bugs not exploitable\033[39m"
	scary=0
elif [ -n "$(env '__BASH_FUNC<a>()'="() { echo x;}" $bash -c a 2>/dev/null)" ]; then
	echo -e "\033[92mVariable function parser pre/suffixed [__BASH_FUNC<..>(), apple], bugs not exploitable\033[39m"
	scary=0
else
	echo -e "\033[92mVariable function parser inactive, bugs not exploitable\033[39m"
	scary=0
fi


r=`env x="() { :; }; echo x" $bash -c "" 2>/dev/null`
if [ -n "$r" ]; then
	warn "CVE-2014-6271 (original shellshock)"
else
	good "CVE-2014-6271 (original shellshock)"
fi

pushd $tmpdir > /dev/null
env x='() { function a a>\' $bash -c echo 2>/dev/null > /dev/null
if [ -e echo ]; then
	warn "CVE-2014-7169 (taviso bug)"
else
	good "CVE-2014-7169 (taviso bug)"
fi
popd > /dev/null

$($bash -c "true $(printf '<<EOF %.0s' {1..80})" 2>$tmpdir/bashcheck.tmp)
ret=$?
grep AddressSanitizer $tmpdir/bashcheck.tmp > /dev/null
if [ $? == 0 ] || [ $ret == 139 ]; then
	warn "CVE-2014-7186 (redir_stack bug)"
else
	good "CVE-2014-7186 (redir_stack bug)"
fi


$bash -c "`for i in {1..200}; do echo -n "for x$i in; do :;"; done; for i in {1..200}; do echo -n "done;";done`" 2>/dev/null
if [ $? != 0 ]; then
	warn "CVE-2014-7187 (nested loops off by one)"
else
	echo -e "\033[96mTest for CVE-2014-7187 not reliable without address sanitizer\033[39m"
fi

$($bash -c "f(){ x(){ _;};x(){ _;}<<a;}" 2>/dev/null)
if [ $? != 0 ]; then
	warn "CVE-2014-6277 (lcamtuf bug #1)"
else
	good "CVE-2014-6277 (lcamtuf bug #1)"
fi

if [ -n "$(env x='() { _;}>_[$($())] { echo x;}' $bash -c : 2>/dev/null)" ]; then
	warn "CVE-2014-6278 (lcamtuf bug #2)"
elif [ -n "$(env BASH_FUNC_x%%='() { _;}>_[$($())] { echo x;}' $bash -c : 2>/dev/null)" ]; then
	warn "CVE-2014-6278 (lcamtuf bug #2)"
elif [ -n "$(env 'BASH_FUNC_x()'='() { _;}>_[$($())] { echo x;}' $bash -c : 2>/dev/null)" ]; then
	warn "CVE-2014-6278 (lcamtuf bug #2)"
else
	good "CVE-2014-6278 (lcamtuf bug #2)"
fi

rm -rf $tmpdir
