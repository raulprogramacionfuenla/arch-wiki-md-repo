The Arch Security Team is a group of volunteers whose goal is to track security issues with Arch Linux packages. All issues are tracked on the [Arch Linux security tracker](https://security.archlinux.org/).

It was formerly known as the Arch CVE Monitoring Team.

## Contents

*   [1 Contribute](#Contribute)
*   [2 Guidelines](#Guidelines)
*   [3 Procedure](#Procedure)
*   [4 Resources](#Resources)
    *   [4.1 RSS](#RSS)
    *   [4.2 Mailing Lists](#Mailing_Lists)
    *   [4.3 Other Distributions](#Other_Distributions)
    *   [4.4 Other](#Other)
    *   [4.5 More](#More)
*   [5 Team Members](#Team_Members)

## Contribute

Anyone can contribute to the Security Team and improve the security of Arch Linux. The most important job is to find and track issues assigned a [Common Vulnerabilites and Exposure](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "wikipedia:Common Vulnerabilities and Exposures") (CVE) number. Following the recommended mailing lists for new CVEs, along with other sources if required, is a good idea to stay updated on new issues.

Advisories are published on the IRC channel for peer-review, and needs two acknowledgments from team members before being published. We encourage volunteers in the channel to look over the advisories for mistakes, questions, or comments about the advisory.

The Arch Linux security tracker is a platform used by the Security Team to track packages, add CVEs and generate advisory text. Contributing code to the [project](https://github.com/archlinux/arch-security-tracker) is a great way to contribute to the team.

Derivative distributions that rely on Arch Linux package repositories are encouraged to contribute. This helps the security of all the users.

## Guidelines

Follow the [#archlinux-security](irc://irc.freenode.net/archlinux-security) IRC channel.

Subscribe to the following mailing lists:

*   [arch-security](https://lists.archlinux.org/listinfo/arch-security)
*   [oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security)

Packages qualified for an advisory has to be part of the following repositories:

*   *core*
*   *extra*
*   *community*
*   *multilib*

## Procedure

A security vulnerability has been found in a software package within the Arch Linux official repositories. A Security Team member picks up this information.

*   In order to assure vulnerability, verify the report against the current package version (including possible patches), and collect as much information (also via search engines) as possible.
    *   Enter the IRC channel if you need help verifying the security issue.
*   If upstream released a new version that corrects the issue, the Security Team member should flag the package out-of-date.
    *   If the package has not been updated after a long delay, a bug report should be filed about the vulnerability.
    *   If this is an important (critical) security issue, a bug report must be filed immediately after flagging the package out-of-date.
    *   If there is no upstream release available, a bug report must be filed including the patches for mitigation.
*   If a bug report has been created, the following information is mandatory:
    *   Description about the security issue and its impact
    *   Links to the CVE-IDs and (upstream) report
    *   If no release is available, links to the upstream patches (or attachments) that mitigate the issue
*   A team member will create an advisory on the [security tracker](https://security.archlinux.org/) and add the CVEs for tracking.
*   A team member with access to [arch-security](https://lists.archlinux.org/listinfo/arch-security) will generate an ASA from the tracker and publish it.

If you have a private bug to report, contact [security@archlinux.org](https://mailman.archlinux.org/pipermail/arch-security/2014-June/000088.html). Please note that the address for private bug reporting is *security*, not *arch-security*. A private bug is one that is too sensitive to post where anyone can read and exploit it, e.g. vulnerabilities in the Arch Linux infrastructure.

## Resources

### RSS

	National Vulnerability Database (NVD)

	All CVE vulnerabilites: [https://nvd.nist.gov/download/nvd-rss.xml](https://nvd.nist.gov/download/nvd-rss.xml)

	All fully analyzed CVE vulnerabilities: [https://nvd.nist.gov/download/nvd-rss-analyzed.xml](https://nvd.nist.gov/download/nvd-rss-analyzed.xml)

### Mailing Lists

	oss-sec

	Main list dealing with security of free software, a lot of CVE attributions happen here, required if you wish to follow security news.

	Info: [http://oss-security.openwall.org/wiki/mailing-lists/oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security)

	Subscribe: oss-security-subscribe(at)lists.openwall.com

	Archive: [http://www.openwall.com/lists/oss-security/](http://www.openwall.com/lists/oss-security/)

	BugTraq

	A full disclosure moderated mailing list (noisy).

	Info: [http://www.securityfocus.com/archive/1/description](http://www.securityfocus.com/archive/1/description)

	Subscribe: bugtraq-subscribe(at)securityfocus.com

	Full-disclosure

	Another full-disclosure mailing-list (noisy).

	Info: [http://lists.grok.org.uk/full-disclosure-charter.html](http://lists.grok.org.uk/full-disclosure-charter.html)

	Subscribe: full-disclosure-request(at)lists.grok.org.uk

Also consider following the mailing lists for specific packages, such as LibreOffice, X.org, Puppetlabs, ISC, etc.

### Other Distributions

Resources of other distributions (to look for CVE, patch, comments etc.):

	RedHat and Fedora

	Advisories feed: [https://bodhi.fedoraproject.org/rss/updates/?type=security](https://bodhi.fedoraproject.org/rss/updates/?type=security)

	CVE tracker: [https://access.redhat.com/security/cve/](https://access.redhat.com/security/cve/)<CVE-ID>

	Bug tracker: [https://bugzilla.redhat.com/show_bug.cgi?id=](https://bugzilla.redhat.com/show_bug.cgi?id=)<CVE-ID>

	Ubuntu

	Advisories feed: [https://www.ubuntu.com/usn/atom.xml](https://www.ubuntu.com/usn/atom.xml)

	CVE tracker: [https://people.canonical.com/~ubuntu-security/cve/?cve=](https://people.canonical.com/~ubuntu-security/cve/?cve=)<CVE-ID>

	Database: [https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master](https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master)

	Debian

	CVE tracker: [https://security-tracker.debian.org/tracker/](https://security-tracker.debian.org/tracker/)<CVE-ID>/

	Patch tracker: [https://tracker.debian.org/pkg/patch](https://tracker.debian.org/pkg/patch)

	Database: [https://anonscm.debian.org/viewvc/secure-testing/data/](https://anonscm.debian.org/viewvc/secure-testing/data/)

	OpenSUSE

	CVE tracker: [https://www.suse.com/security/cve/](https://www.suse.com/security/cve/)<CVE-ID>/

### Other

	Mitre and NVD links for CVE's

	[https://cve.mitre.org/cgi-bin/cvename.cgi?name=](https://cve.mitre.org/cgi-bin/cvename.cgi?name=)<CVE-ID>

	[https://web.nvd.nist.gov/view/vuln/detail?vulnId=](https://web.nvd.nist.gov/view/vuln/detail?vulnId=)<CVE-ID>

NVD and Mitre do not necessarily fill their CVE entry immediately after attribution, so it is not always relevant for Arch. The CVE-ID and the "Date Entry Created" fields do not have particular meaning. CVE are attributed by CVE Numbering Authorities (CNA), and each CNA obtain CVE blocks from Mitre when needed/asked, so the CVE ID is not linked to the attribution date. The "Date Entry Created" field often only indicates when the CVE block was given to the CNA, nothing more.

	Linux Weekly News

	LWN provides a daily notice of security updates for various distributions.

	[https://lwn.net/headlines/newrss](https://lwn.net/headlines/newrss)

### More

For more resources, please see the OpenWall's [Open Source Software Security Wiki](http://oss-security.openwall.org/wiki/).

## Team Members

**Note:** Run `!pingsec <msg>` in [IRC channels](/index.php/IRC_channels "IRC channels") to hilight all current security team members.

*   [Levente Polyak](/index.php/User:Anthraxx "User:Anthraxx")
*   [Remi Gacogne](/index.php/User:Rgacogne "User:Rgacogne")
*   [Christian Rebischke](/index.php/User:Shibumi "User:Shibumi")
*   [Jelle van der Waa](/index.php/User:Jelly "User:Jelly")
*   [Santiago Torres-Arias](/index.php/User:Sangy "User:Sangy")
*   [Jonathan Roemer](/index.php/User:Pid1 "User:Pid1")
*   [Morten Linderud](/index.php/User:Foxboron "User:Foxboron")