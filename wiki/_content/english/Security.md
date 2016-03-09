This article contains recommendations and best practices for hardening an Arch Linux system.

## Contents

*   [1 Concepts](#Concepts)
*   [2 Passwords](#Passwords)
    *   [2.1 Choosing secure passwords](#Choosing_secure_passwords)
    *   [2.2 Maintaining passwords](#Maintaining_passwords)
    *   [2.3 Password hashes](#Password_hashes)
    *   [2.4 Enforcing strong passwords using pam_cracklib](#Enforcing_strong_passwords_using_pam_cracklib)
*   [3 Storage](#Storage)
    *   [3.1 Disk encryption](#Disk_encryption)
    *   [3.2 File systems](#File_systems)
        *   [3.2.1 Mount options](#Mount_options)
    *   [3.3 File access permissions](#File_access_permissions)
*   [4 User setup](#User_setup)
    *   [4.1 Lockout user after three failed login attempts](#Lockout_user_after_three_failed_login_attempts)
    *   [4.2 Limit amount of processes](#Limit_amount_of_processes)
*   [5 Restricting root](#Restricting_root)
    *   [5.1 Use sudo instead of su](#Use_sudo_instead_of_su)
        *   [5.1.1 Editing files using sudo](#Editing_files_using_sudo)
    *   [5.2 Restricting root login](#Restricting_root_login)
        *   [5.2.1 Allow only certain users](#Allow_only_certain_users)
        *   [5.2.2 Denying ssh login](#Denying_ssh_login)
*   [6 Mandatory access control](#Mandatory_access_control)
    *   [6.1 Pathname MAC](#Pathname_MAC)
    *   [6.2 Role-based access control](#Role-based_access_control)
    *   [6.3 Labels MAC](#Labels_MAC)
    *   [6.4 Access Control Lists](#Access_Control_Lists)
*   [7 Kernel hardening](#Kernel_hardening)
    *   [7.1 Restricting access to kernel logs](#Restricting_access_to_kernel_logs)
    *   [7.2 Restricting access to kernel pointers in the proc filesystem](#Restricting_access_to_kernel_pointers_in_the_proc_filesystem)
    *   [7.3 Keep BPF JIT compiler disabled](#Keep_BPF_JIT_compiler_disabled)
    *   [7.4 ptrace scope](#ptrace_scope)
        *   [7.4.1 Examples of broken functionality](#Examples_of_broken_functionality)
    *   [7.5 hidepid](#hidepid)
    *   [7.6 grsecurity](#grsecurity)
*   [8 Sandboxing applications](#Sandboxing_applications)
    *   [8.1 Firejail](#Firejail)
    *   [8.2 chroots](#chroots)
    *   [8.3 Linux containers](#Linux_containers)
    *   [8.4 Other virtualization options](#Other_virtualization_options)
*   [9 Network and firewalls](#Network_and_firewalls)
    *   [9.1 Firewalls](#Firewalls)
    *   [9.2 Kernel parameters](#Kernel_parameters)
    *   [9.3 SSH](#SSH)
    *   [9.4 DNS](#DNS)
    *   [9.5 Proxies](#Proxies)
*   [10 Authenticating packages](#Authenticating_packages)
*   [11 Follow NVD/CVE alerts](#Follow_NVD.2FCVE_alerts)
*   [12 Physical security](#Physical_security)
    *   [12.1 Locking down BIOS](#Locking_down_BIOS)
    *   [12.2 Bootloaders](#Bootloaders)
        *   [12.2.1 Syslinux](#Syslinux)
        *   [12.2.2 GRUB](#GRUB)
    *   [12.3 Denying console login as root](#Denying_console_login_as_root)
    *   [12.4 Automatic logout](#Automatic_logout)
*   [13 See also](#See_also)

## Concepts

*   It *is* possible to tighten the security so much as to make your system unusable. The trick is to secure it without overdoing it.
*   There are many other things that can be done to heighten the security, but the biggest threat is, and will always be, the user. When you think security, you have to think layers. When one layer is breached, another should stop the attack. But you can never make the system 100% secure unless you unplug the machine from all networks, lock it in a safe and never use it.
*   Be a little paranoid. It helps. And be suspicious. If anything sounds too good to be true, it probably is!
*   The [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege "wikipedia:Principle of least privilege"): each part of a system should only be able to access what is required to use it, and nothing more.

## Passwords

Passwords are key to a secure linux system. They secure your [user accounts](/index.php/Users_and_groups "Users and groups"), [encrypted filesystems](/index.php/Disk_encryption "Disk encryption"), and [SSH](/index.php/SSH_keys "SSH keys")/[GPG](/index.php/GPG "GPG") keys. They are the main way a computer chooses to trust the person using it, so a big part of security is just about picking secure passwords and protecting them.

### Choosing secure passwords

When relying on a passphrase, it must be complex enough to not be easily guessed from e.g. personal information, or [cracked](https://en.wikipedia.org/wiki/Password_cracking "wikipedia:Password cracking") using e.g. brute-force attacks. The tenets of strong passphrases are based on *length* and *randomness*. In cryptography the quality of a passphrase is referred to as its [Wikipedia:Entropic security](https://en.wikipedia.org/wiki/Entropic_security "wikipedia:Entropic security").

Insecure passwords include those containing:

*   Personally identifiable information (e.g., your dog's name, date of birth, area code, favorite video game)
*   Simple character substitutions on words (e.g., `k1araj0hns0n`)
*   Root "words" or common strings followed or preceded by added numbers, symbols, or characters (e.g., `DG091101%`)
*   Common phrases or short phrases of grammatically related words (e.g. `all of the lights`), and even with character substitution.

The right choice for a password is something long (8-20 characters, depending on importance) and seemingly completely random. A good technique for building secure, seemingly random passwords is to base them on characters from every word in a sentence. Take for instance “the girl is walking down the rainy street” could be translated to `t6!WdtR5` or, less simply, `t&6!RrlW@dtR,57`. This approach could make it easier to remember a password, but note that the the various letters have very different probabilities of being found at the start of words ([Wikipedia:Letter frequency](https://en.wikipedia.org/wiki/Letter_frequency#Relative_frequencies_of_the_first_letters_of_a_word_in_the_English_language "wikipedia:Letter frequency")).

A better approach is to generate pseudo-random passwords with tools like [pwgen](https://www.archlinux.org/packages/?name=pwgen) or [apg](https://www.archlinux.org/packages/?name=apg): for memorizing them, one technique (for ones typed often) is to generate a long password and memorize a minimally secure number of characters, temporarily writing down the full generated string. Over time, increase the number of characters typed - until the password is ingrained in muscle memory and need not be remembered. This technique is more difficult, but can provide confidence that a password will not turn up in wordlists or "intelligent" brute force attacks that combine words and substitute characters.

It is also very effective to combine these two techniques by saving long, complex random passwords with a [password manager](/index.php/List_of_applications/Security#Password_managers "List of applications/Security"), which will be in turn accessed with a mnemonic password that will have to be used only for that purpose, especially avoiding to ever transmit it over any kind of network. This method of course limits the use of the stored passwords to the terminals where the database is available for reading (which on the other hand could be seen as an added security feature).

Also consider the [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html) method, using a sufficient number of words.

See Bruce Schneier's article [Choosing Secure Passwords](https://www.schneier.com/blog/archives/2014/03/choosing_secure_1.html) or [The passphrase FAQ](http://www.iusmentis.com/security/passphrasefaq/) for some additional background. Also, you can check entropy level of your chosen passphrase [here](http://rumkin.com/tools/password/passchk.php), or consulting [Wikipedia:Password strength](https://en.wikipedia.org/wiki/Password_strength "wikipedia:Password strength").

### Maintaining passwords

Once you pick a strong password, be sure to keep it safe. Watch out for [manipulation](https://en.wikipedia.org/wiki/Social_engineering_(security) "wikipedia:Social engineering (security)"), [shoulder surfing](https://en.wikipedia.org/wiki/Shoulder_surfing_(computer_security) "wikipedia:Shoulder surfing (computer security)"), and avoid reusing passwords so insecure servers cannot leak more information than necessary. [Password managers](/index.php/List_of_applications/Security#Password_managers "List of applications/Security") can help manage large numbers of complex passwords: if you are copy-pasting the stored passwords from the manager to the applications that need them, make sure to clear the copy buffer every time, and ensure they are not saved in any kind of log (e.g. do not paste them in plain terminal commands, which would store them in files like `.bash_history`). [Lastpass](https://en.wikipedia.org/wiki/LastPass_Password_Manager "wikipedia:LastPass Password Manager") is a service that stores encrypted passwords online for synchronization between devices, but requires that you trust both closed-source code and an external corporation.

As a rule, do not pick insecure passwords just because secure ones are harder to remember. Passwords are a balancing act. It is better to have an encrypted database of secure passwords, guarded behind a key and one strong master password, than it is to have many similar weak passwords. Writing passwords down is perhaps equally effective[[1]](https://www.schneier.com/blog/archives/2005/06/write_down_your.html), avoiding potential vulnerabilities in software solutions while requiring physical security.

Another aspect of the strength of the passphrase is that it must not be easily recoverable from other places. If you use the same passphrase for disk encryption as you use for your login password (useful e.g. to auto-mount the encrypted partition or folder on login), make sure that `/etc/shadow` either also ends up on an encrypted partition, or uses a strong hash algorithm (i.e. sha512/bcrypt, not md5) for the stored password hash (see [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes") for more info).

### Password hashes

By default, Arch stores the hashed user passwords in the root-only-readable `/etc/shadow` file, separated from the other user parameters stored in the world-readable `/etc/passwd` file, see [Users and groups#User database](/index.php/Users_and_groups#User_database "Users and groups"). See also [#Restricting root](#Restricting_root).

Passwords are set with the **passwd** command, which [stretches](https://en.wikipedia.org/wiki/Key_stretching function and then saves them in `/etc/shadow`. See also [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes"). The passwords are also [salted](https://en.wikipedia.org/wiki/Salt_(cryptography) in order to defend them against [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table "wikipedia:Rainbow table") attacks.

See also [How are passwords stored in Linux (Understanding hashing with shadow utils)](http://www.slashroot.in/how-are-passwords-stored-linux-understanding-hashing-shadow-utils).

### Enforcing strong passwords using pam_cracklib

*pam_cracklib* provides protection against [Dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack "wikipedia:Dictionary attack") and helps configure a password policy that can be enforced throughout the system.

**Warning:** The *root* account is not affected by this policy.

**Note:** You can use the *root* account to set a password for a user that bypasses the desired/configured policy. This is useful when setting temporary passwords.

If for example you want to enforce this policy:

*   prompt 2 times for password in case of an error
*   10 characters minimum length (minlen option)
*   at least 6 characters should be different from old password when entering a new one (difok option)
*   at least 1 digit (dcredit option)
*   at least 1 uppercase (ucredit option)
*   at least 1 other character (ocredit option)
*   at least 1 lowercase (lcredit option)

Edit the `/etc/pam.d/passwd` file to read as:

```
#%PAM-1.0
password required pam_cracklib.so retry=2 minlen=10 difok=6 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=-1
password required pam_unix.so use_authtok sha512 shadow
```

The `password required pam_unix.so use_authtok` instructs the *pam_unix* module to not prompt for a password but rather to use the one provided by *pam_cracklib*.

You can refer to the pam_cracklib(8) and pam_unix(8) man pages for more information.

## Storage

### Disk encryption

[Disk encryption](/index.php/Disk_encryption "Disk encryption"), preferably full disk encryption with a [strong passphrase](#Passwords), is the only way to guard data against physical recovery. This provides complete security when the computer is turned off or the disks in question are unmounted.

Once the computer is powered on and the drive is mounted, however, its data becomes just as vulnerable as an unencrypted drive. It is therefore best practice to unmount data partitions as soon as they are no longer needed.

Certain programs, like [Dm-crypt](/index.php/Dm-crypt "Dm-crypt"), allow the user to encrypt a loop file as a virtual volume. This is a reasonable alternative to full disk encryption when only certain parts of the system need be secure.

### File systems

The kernel now prevents security issues related to hardlinks and symlinks if the `fs.protected_hardlinks` and `fs.protected_symlinks` sysctl switches are enabled, so there is no longer a major security benefit from separating out world-writable directories.

Partitions containing world-writable directories can still be kept separate as a coarse way of limiting the damage from disk space exhaustion. However, filling a partition like `/var` or `/tmp` is enough to take down services. More flexible mechanisms for dealing with this concern exist (like quotas), and some filesystems include related features themselves (btrfs has quotas on subvolumes).

#### Mount options

Following the principle of least privilege, partitions should be mounted with the most restrictive mount options possible (without losing functionality).

Relevant mount options are:

*   `nodev`: Do not interpret character or block special devices on the file system.
*   `nosuid`: Do not allow set-user-identifier or set-group-identifier bits to take effect.
*   `noexec`: Do not allow direct execution of any binaries on the mounted filesystem.

Data partitions should always be mounted with `nodev`, `nosuid`, `noexec`. Potential usage is presented in the table below.

| **Partition** | `nodev` | `nosuid` | `noexec` |
| `/var` | yes | yes | yes  |
| `/home` | yes | yes | yes, if you do not code, use wine or steam |
| `/dev/shm` | yes | yes | yes |
| `/tmp` | yes | yes | maybe, breaks compiling packages and various other things |
| `/boot` | yes | yes | yes |

 Note that some packages (building [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) for example) may require `exec` on `/var`.

### File access permissions

The default [file permissions](/index.php/File_permissions "File permissions") allow read access to almost everything and changing the permissions can hide valuable information from an attacker who gains access to a non-root account such as the `http` or `nobody` users.

For example:

```
# chmod 700 /boot /etc/{iptables,arptables}

```

The default [Umask](/index.php/Umask "Umask") can be changed to improve security for newly created files. The [NSA RHEL5 Security Guide](http://www.nsa.gov/ia/_files/os/redhat/rhel5-guide-i731.pdf) suggests a umask of `077` for maximum security, which makes new files not readable by users other than the owner. To change this, see [Umask#Setting the umask](/index.php/Umask#Setting_the_umask "Umask").

## User setup

After installation make a normal user for daily use. Do not use the root user for daily use.

### Lockout user after three failed login attempts

To further heighten the security it is possible to lockout a user after a specified number of failed login attempts. The user account can either be locked until the root user unlocks it, or automatically be unlocked after a set time. To lockout a user for ten minutes after three failed login attempts you have to modify `/etc/pam.d/system-login`:

 `/etc/pam.d/system-login` 
```
auth required pam_tally.so deny=2 unlock_time=600 onerr=succeed file=/var/log/faillog
#auth required pam_tally.so onerr=succeed file=/var/log/faillog
```

If you do not comment the second line every failed login attempt will be counted twice. That is all there is to it. If you feel adventurous, make three failed login attempts. Then you can see for yourself what happens. To unlock a user manually do:

```
# pam_tally --user *username* --reset

```

If you want to permanently lockout a user after 3 failed login attempts remove the `unlock_time` part of the line. The user can then not login until root unlocks the account.

### Limit amount of processes

On systems with many, or untrusted users, it is important to limit the number of processes each can run at once, therefore preventing [fork bombs](https://en.wikipedia.org/wiki/Fork_bomb "wikipedia:Fork bomb") and other denial of service attacks. `/etc/security/limits.conf` determines how many processes each user, or group can have open, and is empty (except for useful comments) by default. adding the following lines to this file will limit all users to 100 active processes, unless they use the ulimit command to explicitly raise their maximum to 200 for one session. These values can be changed according to the appropriate number of processes a user should have running, or the hardware of the box you are administrating.

```
* soft nproc 100
* hard nproc 200

```

## Restricting root

The root user is, by definition, the most powerful user on a system. Because of this, there are a number of ways to keep the power of the root user while limiting its ability to cause harm, or at least to make root user actions more traceable.

### Use sudo instead of su

Using [sudo](/index.php/Sudo "Sudo") for privileged access is preferable to [su](/index.php/Su "Su") for [a number of reasons](/index.php/Su#Security "Su").

*   It keeps a log of which normal privilege user has run each privileged command.
*   The root user password need not be given out to each user who requires root access.
*   `sudo` prevents users from accidentally running commands as *root* that do not need root access, because a full root terminal is not created. This aligns with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege "wikipedia:Principle of least privilege").
*   Individual programs may be enabled per user, instead of offering complete root access just to run one command. For example, to give the user *alice* access to a particular program:

```
# visudo

```
 `/etc/sudoers`  `alice ALL = NOPASSWD: /path/to/program` 

Or, individual commands can be allowed for all users. To mount Samba shares from a server as a regular user:

```
%users ALL=/sbin/mount.cifs,/sbin/umount.cifs

```

This allows all users who are members of the group users to run the commands `/sbin/mount.cifs` and `/sbin/umount.cifs` from any machine (ALL).

**Tip:**

To use `nano` instead of `vi` with `visudo`,

 `/etc/sudoers`  `Defaults editor=/usr/bin/rnano` 

Exporting `# EDITOR=nano visudo` is regarded as a severe security risk since everything can be used as an `EDITOR`.

#### Editing files using sudo

Running a text editor as root can be a security vulnerability as many editors can run arbitrary shell commands or affect files other than the one you intend to edit. To avoid this, use `sudoedit filename` (equivalently, `sudo -e filename`) to edit files. This edits a copy of the file using your normal user privileges and then overwrites the original using sudo only after the editor is closed. You can change the editor this uses by setting the `SUDO_EDITOR` environment variable:

```
export SUDO_EDITOR=vim

```

Alternatively, use an editor like `rvim` which has restricted capabilities in order to be safe to run as root.

### Restricting root login

Once [sudo](/index.php/Sudo "Sudo") is properly configured, full root access can be heavily restricted or denied without losing much usability.

#### Allow only certain users

The [PAM](https://en.wikipedia.org/wiki/Pluggable_authentication_module "wikipedia:Pluggable authentication module") `pam_wheel.so` lets you allow only users in the group `wheel` to login using `su`. Edit both `/etc/pam.d/su` and `/etc/pam.d/su-l`, then uncomment the line:

```
# Uncomment the following line to require a user to be in the "wheel" group.
auth		required	pam_wheel.so use_uid

```

This means only users who are already able to run privileged commands may login as root.

#### Denying ssh login

Even if you do not wish to deny root login for local users, it is always good practice to [deny root login via SSH](/index.php/Ssh#Deny "Ssh"). The purpose of this is to add an additional layer of security before a user can completely compromise your system remotely.

## Mandatory access control

[Mandatory access control](https://en.wikipedia.org/wiki/Mandatory_Access_Control "wikipedia:Mandatory Access Control") (MAC) is a type of security policy that differs significantly from the [discretionary access control](https://en.wikipedia.org/wiki/Discretionary_Access_Control "wikipedia:Discretionary Access Control") (DAC) used by default in Arch and most Linux distributions. MAC essentially means that every action a program could perform that affects the system in any way is checked against a security ruleset. This ruleset, in contrast to DAC methods, cannot be modified by users. Using virtually any mandatory access control system will significantly improve the security of your computer, although there are differences in how it can be implemented.

### Pathname MAC

Pathname-based access control is a simple form of access control that offers permissions based on the path of a given file. The downside to this style of access control is that permissions are not carried with files if they are moved about the system. On the positive side, pathname-based MAC can be implemented on a much wider range of filesystems, unlike labels-based alternatives.

*   [AppArmor](/index.php/AppArmor "AppArmor") is a [Canonical](https://en.wikipedia.org/wiki/Canonical "wikipedia:Canonical")-maintained MAC implementation seen as an "easier" alternative to SELinux.
*   [Tomoyo](/index.php/Tomoyo "Tomoyo") is another simple, easy-to-use system offering mandatory access control. It is designed to be both simple in usage and in implementation, requiring very few dependencies.

### Role-based access control

The MAC implementation grsecurity supports is called role-based access control. RBAC associates roles with each user. Each role defines what operations can be performed on certain objects. Given a well-written collection of roles and operations your users will be restricted to perform only those tasks that you tell them they can do. The default "deny-all" ensures you that a user cannot perform an action you have not thought of.

*   [Grsecurity RBAC](/index.php/Grsecurity#RBAC "Grsecurity") has a learning mode like AppArmor for easy configuration
*   [Grsecurity RBAC](/index.php/Grsecurity#RBAC "Grsecurity") does not rely on extra meta-data like SELinux. RBAC is significantly faster then SELinux.

### Labels MAC

Labels-based access control means the extended attributes of a file are used to govern its security permissions. While this system is arguably more flexible in its security offerings than pathname-based MAC, it only works on filesystems that support these extended attributes.

*   [SELinux](/index.php/SELinux "SELinux"), based on a [NSA](https://en.wikipedia.org/wiki/NSA "wikipedia:NSA") project to improve Linux security, implements MAC completely separate from system users and roles. It offers an extremely robust multi-level MAC policy implementation that can easily maintain control of a system that grows and changes past its original configuration.

### Access Control Lists

[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") (ACLs) are an alternative to attaching rules directly to the filesystem in some way. ACLs implement access control by checking program actions against a list of permitted behavior.

*   [grsecurity](/index.php/Grsecurity "Grsecurity") implements ACL access control, as well as a complete kernel patchset focused on improving security. Its changes extend to control of memory allocation, improved chroot restrictions, and rules involving specific network behavior.

## Kernel hardening

### Restricting access to kernel logs

The kernel logs contain useful information for an attacker trying to exploit kernel vulnerabilities, such as sensitive memory addresses. The `kernel.dmesg_restrict` flag was to forbid access to the logs without the `CAP_SYS_ADMIN` capability (which only processes running as root have by default).

 `/etc/sysctl.d/50-dmesg-restrict.conf`  `kernel.dmesg_restrict = 1` 

### Restricting access to kernel pointers in the proc filesystem

Enabling `kernel.kptr_restrict` will hide kernel symbol addresses in `/proc/kallsyms` from regular users without `CAP_SYSLOG`, making it more difficult for kernel exploits to resolve addresses/symbols dynamically. This will not help that much on a pre-compiled Arch Linux kernel, since a determined attacker could just download the kernel package and get the symbols manually from there, but if you're compiling your own kernel, this can help mitigating local root exploits. This will break some [perf](https://www.archlinux.org/packages/?name=perf) commands when used by non-root users (but many [perf](https://www.archlinux.org/packages/?name=perf) features require root access anyway). See [FS#34323](https://bugs.archlinux.org/task/34323) for more information.

 `/etc/sysctl.d/50-kptr-restrict.conf`  `kernel.kptr_restrict = 1` 

### Keep BPF JIT compiler disabled

The Linux kernel includes the ability to compile BPF/Seccomp rule sets to native code as a performance optimization. The `net.core.bpf_jit_enable` flag should be left at 0 for a maximum level of security.

This can be helpful in specific domains, but is not usually useful. A JIT compiler opens up the possibility for an attacker to perform a heap spraying attack, where they fill the kernel's heap with malicious code. This code can then potentially be executed via another exploit, like an incorrect function pointer dereference.

**Note:** [grsecurity](/index.php/Grsecurity "Grsecurity") includes JIT hardening for the BPF JIT compiler, greatly reducing the risk of exploitation.

### ptrace scope

Arch enables the Yama LSM by default, providing a `kernel.yama.ptrace_scope` flag. This flag is enabled by default and prevents processes from performing a `ptrace` call on other processes outside of their scope without `CAP_SYS_PTRACE`. While many debugging tools require this for some of their functionality, it is a significant improvement in security. Without this feature, there is essentially no separation between processes running as the same user without applying extra layers like namespaces. The ability to attach a debugger to an existing process is a demonstration of this weakness.

**Note:** In [grsecurity](/index.php/Grsecurity "Grsecurity"), this protection is toggled via the `kernel.grsecurity.harden_ptrace` flag instead.

#### Examples of broken functionality

**Note:** You can still execute these commands as root (such as allowing them through [sudo](/index.php/Sudo "Sudo") for certain users, with or without a password), or enable ptrace selectively through `setcap cap_sys_ptrace=eip */path/to/program*`.

*   `gdb -p $PID`
*   `strace -p $PID`
*   `perf trace -p $PID`
*   `reptyr $PID`

### hidepid

The kernel has the ability to hide other users' processes from unprivileged users by mounting the `proc` filesystem with `hidepid=1` or `hidepid=2`. This can be automated with the [hidepid](https://www.archlinux.org/packages/?name=hidepid) package. It will install polkit and systemd-logind exceptions and make sure `/proc` is mounted with `hidepid=2,gid=26`.

### grsecurity

The [grsecurity](/index.php/Grsecurity "Grsecurity") kernel provides many security-related improvements. It hardens both the kernel and userspace against common memory corruption vulnerabilities, along with providing many miscellaneous features and a role-based access control system. It is the only way to secure the kernel itself against exploitation, which is the most important improvement for a system already making good use of user isolation, containers/chroots and sandboxes.

## Sandboxing applications

### Firejail

[Firejail](/index.php/Firejail "Firejail") is an easy to use and simple tool for sandboxing applications and servers alike. Firejail is suggested for browsers and internet facing applications, as well as any servers you may be running. Firejail is further enhanced when used with Grsecurity.

### chroots

Manual [chroot](/index.php/Chroot "Chroot") jails can also be constructed.

### Linux containers

[Linux Containers](/index.php/Linux_Containers "Linux Containers") are another good option when you need more separation than the other options (short of KVM and Virtualbox) provide. LXC's run on top of the existing kernel in a pseudo-chroot with their own virtual hardware.

### Other virtualization options

Using other, more full virtualization options such as [VirtualBox](/index.php/VirtualBox "VirtualBox"), [KVM](/index.php/KVM "KVM"), or [Xen](/index.php/Xen "Xen") can also improve security in the event you plan on running risky applications or browsing dangerous websites.

## Network and firewalls

### Firewalls

While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables"), it is not enabled by default. It is highly recommended to set up some form of firewall to protect the services running on the system. Many resources (including ArchWiki) do not state explicitly which services are worth protecting, so enabling a firewall is a good precaution.

*   See [iptables](/index.php/Iptables "Iptables") for general info.
*   See [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") for a guide on setting up an iptables firewall.
*   See [Firewalls](/index.php/Firewalls "Firewalls") for other ways of setting up netfilter.
*   See [Ipset](/index.php/Ipset "Ipset") for blocking lists of ip addresses, such as those from Bluetack.

### Kernel parameters

Kernel parameters which affect networking can be set using [Sysctl](/index.php/Sysctl "Sysctl"). For how to do this, see [Sysctl#TCP/IP stack hardening](/index.php/Sysctl#TCP.2FIP_stack_hardening "Sysctl").

### SSH

Avoid using [Secure Shell](/index.php/Secure_Shell "Secure Shell") without [requiring SSH keys](/index.php/Secure_Shell#Force_public_key_authentication "Secure Shell"). This prevents [brute-force attacks](https://en.wikipedia.org/wiki/Brute-force_attack "wikipedia:Brute-force attack"). Alternatively [Fail2ban](/index.php/Fail2ban "Fail2ban") or [Sshguard](/index.php/Sshguard "Sshguard") offer lesser forms of protection by monitoring logs and writing [iptables rules](/index.php/Iptables "Iptables") but open up the potential for a denial of serving, since an attacker can spoof packets as if they came from the administrator after identifying their address.

[Denying root login](/index.php/Secure_Shell#Deny "Secure Shell") is good practice, both for tracing intrusions and adding an additional layer of security before root access.

### DNS

See [DNSSEC](/index.php/DNSSEC "DNSSEC") and [DNSCrypt](/index.php/DNSCrypt "DNSCrypt").

### Proxies

Proxies are commonly used as an extra layer between applications and the network, sanitizing data from untrusted sources. The attack surface of a small proxy running with lower privileges is significantly smaller than a complex application running with the end user privileges.

For example the DNS resolver is implemented in [glibc](https://www.archlinux.org/packages/?name=glibc), that is linked with the application (that may be running as root), so a bug in the DNS resolver might lead to a remote code execution. This can be prevented by installing a DNS caching server, such as [Dnsmasq](/index.php/Dnsmasq "Dnsmasq"), which acts as a proxy. [[2]](https://googleonlinesecurity.blogspot.it/2016/02/cve-2015-7547-glibc-getaddrinfo-stack.html)

## Authenticating packages

[Attacks on package managers](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#overview) are possible without proper use of package signing, and can affect even package managers with [proper signature systems](http://www.cs.arizona.edu/stork/packagemanagersecurity/faq.html). Arch uses package signing by default and relies on a web of trust from 5 trusted master keys. See [Pacman-key](/index.php/Pacman-key "Pacman-key") for details.

## Follow NVD/CVE alerts

Subscribe to the Common Vulnerabilities and Exposure Security Alert updates, made available by National Vulnerability Database, and found on the [NVD Download webpage](http://nvd.nist.gov/download.cfm). See also [Arch CVE Monitoring Team](/index.php/Arch_CVE_Monitoring_Team "Arch CVE Monitoring Team") and [CVE](/index.php/CVE "CVE").

**Warning:** Do not be tempted to perform [partial upgrades](/index.php/Partial_upgrades "Partial upgrades"), as they are not supported by Arch Linux and may cause instability: the whole system should be upgraded when upgrading a component. Also note that infrequent system updates can complicate the update process.

## Physical security

**Note:** You can ignore this section if you just want to secure your computer against remote threats.

Physical access to a computer is root access given enough time and resources. However, a high *practical* level of security can be obtained by putting up enough barriers.

An attacker can gain full control of your computer on the next boot by simply attaching a malicious IEEE 1394 (FireWire), Thunderbolt or PCI Express device as they are given full memory access.[[3]](http://www.breaknenter.org/projects/inception/) There is little you can do from preventing this, or modification of the hardware itself - such as flashing malicious firmware onto a drive. However, the vast majority of attackers will not be this knowledgeable and determined.

[#Disk encryption](#Disk_encryption) will prevent access to your data if the computer is stolen, but malicious firmware can be installed to obtain this data upon your next log in by a resourceful attacker.

### Locking down BIOS

Adding a password to the BIOS prevents someone from booting into removable media, which is basically the same as having root access to your computer. You should make sure your drive is first in the boot order and disable the other drives from being bootable if you can.

### Bootloaders

It is highly important to protect your bootloader. There is a magic kernel parameter called `init=/bin/sh`. This makes any user/login restrictions totally useless.

#### Syslinux

Syslinux supports [password-protecting your bootloader](/index.php/Syslinux#Security "Syslinux"). It allows you to set either a per-menu-item password or a global bootloader password.

#### GRUB

[GRUB](/index.php/GRUB "GRUB") supports bootloader passwords as well. See [GRUB/Tips and tricks#Password protection of GRUB menu](/index.php/GRUB/Tips_and_tricks#Password_protection_of_GRUB_menu "GRUB/Tips and tricks") for details. It also has support for [encrypted boot partitions](/index.php/GRUB#Boot_partition "GRUB"), which only leaves some parts of the bootloader code unencrypted. GRUB's configuration, [kernel](/index.php/Kernel "Kernel") and [initramfs](/index.php/Initramfs "Initramfs") are encrypted.

### Denying console login as root

Changing the configuration to disallow root to login from the console makes it harder for an intruder to gain access to the system. The intruder would have to guess both a user-name that exists on the system and that users password. When root is allowed to log in via the console, an intruder only needs to guess a password. Blocking root login at the console is done by commenting out the tty lines in `/etc/securetty`.

 `/etc/securetty` 
```
#tty1

```

Repeat for any tty you wish to block. To check the effect of this change, start by commenting out only one line and go to that particular console and try to login as root. You will be greeted by the message `Login incorrect`. Now that we are sure it works, go back and comment out the rest of the tty lines.

**Note:** If you see `ttyS0` this is for a serial console. Similarly, on Xen virtualized systems `hvc0` is for the administrator.

### Automatic logout

If you are using [Bash](/index.php/Bash "Bash") or [Zsh](/index.php/Zsh "Zsh"), you can set `TMOUT` for an automatic logout from shells after a timeout.

For example, the following will automatically log out from virtual consoles (but not terminal emulators in X11):

 `/etc/profile.d/shell-timeout.sh` 
```
TMOUT="$(( 60*10 ))";
[ -z "$DISPLAY" ] && export TMOUT;
case $( /usr/bin/tty ) in
	/dev/tty[0-9]*) export TMOUT;;
esac

```

If you really want EVERY Bash/Zsh prompt (even within X) to timeout, use:

```
$ export TMOUT="$(( 60*10 ))";

```

Note that this will not work if there is some command running in the shell (eg.: an SSH session or other shell without `TMOUT` support). But if you are using VC mostly for restarting frozen GDM/Xorg as root, then this is very usefull.

## See also

*   [DeveloperWiki:Security](/index.php/DeveloperWiki:Security "DeveloperWiki:Security")
*   ArchWiki's Current list of security applications: [Lists of Applications: Security](/index.php/List_of_applications/Security "List of applications/Security")
*   [Securing and Hardening Red Hat Linux Production Systems](http://www.puschitz.com/SecuringLinux.shtml)
*   [Hardening the linux desktop](http://www.ibm.com/developerworks/linux/tutorials/l-harden-desktop/index.html)
*   [Hardening the linux server](http://www.ibm.com/developerworks/linux/tutorials/l-harden-server/index.html)
*   [Securing and Optimizing Linux](http://www.faqs.org/docs/securing/index.html)
*   [UNIX and Linux Security Checklist v3.0](http://www.auscert.org.au/5816)
*   [CentOS Wiki: OS Protection](http://wiki.centos.org/HowTos/OS_Protection)
*   [Hardening Debian (pdf)](http://www.debian.org/doc/manuals/securing-debian-howto/securing-debian-howto.en.pdf)
*   [The paranoid #! Security Guide](http://crunchbang.org/forums/viewtopic.php?id=24722)
*   [Linux Foundation's Linux workstation security checklist](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md)
*   [privacytools.io](https://www.privacytools.io/)