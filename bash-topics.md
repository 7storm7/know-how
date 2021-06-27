# Here-document (Heredoc)

__Syntax:__
~~~
[COMMAND] <<[-] 'DELIMITER'
  HERE-DOCUMENT
DELIMITER
~~~
__Definition:__
Used to pass a multiline block of text or code to an interactive command, such as tee , cat, or sftp.

* The first line starts with an optional command followed by the special redirection operator __<<__ and the delimiting identifier.
  You can use any string as a delimiting identifier, the most commonly used are EOF or END.
* If the delimiting identifier is unquoted, the shell will substitute all variables, commands and special characters before passing the here-document lines to the command.
Appending a minus sign to the redirection operator __<<-__, will cause all leading tab characters to be ignored. This allows you to use __indentation__ when writing here-documents in shell scripts. Leading whitespace characters are __not allowed__, only tab.
* The here-document block can contain strings, variables, commands and any other type of input.
* The last line ends with the delimiting identifier. White space in front of the delimiter is __not allowed__.

__Samples:__

1.
~~~
cat << EOF
The current working directory is: $PWD
You are logged in as: $(whoami)
EOF
~~~
Output:
~~~
The current working directory is: /home/linuxize
You are logged in as: linuxize
~~~

2. If we enclose the delimiter in single or double quotes.

~~~
cat <<- "EOF"
The current working directory is: $PWD
You are logged in as: $(whoami)
EOF
~~~
Output:
~~~
The current working directory is: $PWD
You are logged in as: $(whoami)
~~~~

__Ref:__ https://linuxize.com/post/bash-heredoc/

---


# Extended Globbing

If you use switch/case conditions and want to use the content of a variable as alternating ("|") patterns.

__Samples:__

~~~
shopt -s extglob

string='@(foo|bar)'

read choice
    case $choice in
        $string )      printf 'String  choice %-20s' "$choice"; ;;&
        $s1|$s2 )      printf 'Two val choice %-20s' "$choice"; ;;
        *)             printf 'A Bad  choice! %-20s' "$choice"; ;;
    esac
echo
~~~


__Ref:__ 
https://unix.stackexchange.com/questions/234264/how-can-i-use-a-variable-as-a-case-condition
http://mywiki.wooledge.org/glob

---
