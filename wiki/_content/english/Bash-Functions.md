[Bash](/index.php/Bash "Bash") also supports functions. Add the functions to `~/.bashrc`, or a separate file which is [sourced](/index.php/Source "Source") from `~/.bashrc`. More Bash function examples can be found in [BBS#30155](https://bbs.archlinux.org/viewtopic.php?id=30155).

## Contents

*   [1 Display error codes](#Display_error_codes)
*   [2 Compile and execute a C source on the fly](#Compile_and_execute_a_C_source_on_the_fly)
*   [3 Extract](#Extract)
*   [4 cd and ls in one](#cd_and_ls_in_one)
*   [5 Simple note taker](#Simple_note_taker)
*   [6 Simple task utility](#Simple_task_utility)
*   [7 Calculator](#Calculator)
*   [8 Kingbash](#Kingbash)
*   [9 IP info](#IP_info)

## Display error codes

To set `trap` to intercept a non-zero return code of the last program run:

```
EC() {
	echo -e '\e[1;33m'code $?'\e[m
'
}
trap EC ERR

```

## Compile and execute a C source on the fly

The following function will compile (within the `/tmp/` directory) and execute the [C](https://en.wikipedia.org/wiki/C_(programming_language) source argument on the fly (and the execution will be without arguments). And finally, after program terminates, will remove the compiled file.

```
# Compile and execute a C source on the fly
csource() {
	[[ $1 ]]    || { echo "Missing operand" >&2; return 1; }
	[[ -r $1 ]] || { printf "File %s does not exist or is not readable
" "$1" >&2; return 1; }
	local output_path=${TMPDIR:-/tmp}/${1##*/};
	gcc "$1" -o "$output_path" && "$output_path";
	rm "$output_path";
	return 0;
}
```

## Extract

The following function will extract a wide range of compressed file types. and use it with the syntax `extract <file1> <file2> ...`

```
extract() {
    local c e i

    (($#)) || return

    for i; do
        c=''
        e=1

        if [[ ! -r $i ]]; then
            echo "$0: file is unreadable: \`$i'" >&2
            continue
        fi

        case $i in
            *.t@(gz|lz|xz|b@(2|z?(2))|a@(z|r?(.@(Z|bz?(2)|gz|lzma|xz)))))
                   c=(bsdtar xvf);;
            *.7z)  c=(7z x);;
            *.Z)   c=(uncompress);;
            *.bz2) c=(bunzip2);;
            *.exe) c=(cabextract);;
            *.gz)  c=(gunzip);;
            *.rar) c=(unrar x);;
            *.xz)  c=(unxz);;
            *.zip) c=(unzip);;
            *)     echo "$0: unrecognized file extension: \`$i'" >&2
                   continue;;
        esac

        command "${c[@]}" "$i"
        ((e = e || $?))
    done
    return "$e"
}

```

**Note:** Make sure `extglob` is enabled: `shopt -s extglob`, by adding it to the `~/.bashrc` (see [gregswiki:glob#Options_which_change_globbing_behavior](https://mywiki.wooledge.org/glob#Options_which_change_globbing_behavior "gregswiki:glob")).

Another way to do this is to install a specialized package, see [Archiving and compression tools#Convenience tools](/index.php/Archiving_and_compression_tools#Convenience_tools "Archiving and compression tools").

## cd and ls in one

Very often changing to a directory is followed by the `ls` command to list its contents. Therefore it is helpful to have a second function doing both at once. In this example we will name it `cl` (change list) and show an error message if the specified directory does not exist.

```
cl() {
	local dir="$1"
	local dir="${dir:=$HOME}"
	if [[ -d "$dir" ]]; then
		cd "$dir" >/dev/null; ls
	else
		echo "bash: cl: $dir: Directory not found"
	fi
}

```

Of course the *ls* command can be altered to fit your needs, for example `ls -hall --color=auto`.

## Simple note taker

```
note () {
    # if file doesn't exist, create it
    if [[ ! -f $HOME/.notes ]]; then
        touch "$HOME/.notes"
    fi

    if ! (($#)); then
        # no arguments, print file
        cat "$HOME/.notes"
    elif [[ "$1" == "-c" ]]; then
        # clear file
        printf "%s" > "$HOME/.notes"
    else
        # add all arguments to file
        printf "%s
" "$*" >> "$HOME/.notes"
    fi
}

```

## Simple task utility

Inspired by [#Simple note taker](#Simple_note_taker)

```
todo() {
    if [[ ! -f $HOME/.todo ]]; then
        touch "$HOME/.todo"
    fi

    if ! (($#)); then
        cat "$HOME/.todo"
    elif [[ "$1" == "-l" ]]; then
        nl -b a "$HOME/.todo"
    elif [[ "$1" == "-c" ]]; then
        > $HOME/.todo
    elif [[ "$1" == "-r" ]]; then
        nl -b a "$HOME/.todo"
        eval printf %.0s- '{1..'"${COLUMNS:-$(tput cols)}"\}; echo
        read -p "Type a number to remove: " number
        sed -i ${number}d $HOME/.todo "$HOME/.todo"
    else
        printf "%s
" "$*" >> "$HOME/.todo"
    fi
}

```

## Calculator

```
calc() {
    echo "scale=3;$@" | bc -l
}

```

## Kingbash

Kingbash - menu driven auto-completion (see [BBS#101010](https://bbs.archlinux.org/viewtopic.php?id=101010)).

[Install](/index.php/Install "Install") [kingbash-gb-git](https://aur.archlinux.org/packages/kingbash-gb-git/) from the [AUR](/index.php/AUR "AUR"), then insert the following into your `~/.bashrc`:

```
function kingbash.fn() {
    echo -n "KingBash> $READLINE_LINE" #Where "KingBash> " looks best if it resembles your PS1, at least in length.
    OUTPUT=$(/usr/bin/kingbash "$(compgen -ab -A function)")
    READLINE_POINT=$(echo "$OUTPUT" | tail -n 1)
    READLINE_LINE=$(echo "$OUTPUT" | head -n -1)
    echo -ne "\r\e[2K"
}
bind -x '"\t":kingbash.fn'

```

## IP info

Detailed information on an IP address or hostname in bash via [http://ipinfo.io](http://ipinfo.io):

```
ipif() { 
    if grep -P "(([1-9]\d{0,2})\.){3}(?2)" <<< "$1"; then
	 curl ipinfo.io/"$1"
    else
	ipawk=($(host "$1" | awk '/address/ { print $NF }'))
	curl ipinfo.io/${ipawk[1]}
    fi
    echo
}

```

**Note:** Bash is limited to extended regular expressions; this example uses perl regular expressions with *grep*. [[1]](http://unix.stackexchange.com/questions/84477/forcing-bash-to-use-perl-regex-engine)