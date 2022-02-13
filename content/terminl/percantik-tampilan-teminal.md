---
draft: false 
date: 2022-02-13T09:10:53+08:00
title: "Memodifikasi Tampilan Teminal Ubuntu"
description:
slug: percantik-tampilan-teminal
type: blog
author: ari
tags:
    - terminal 

categories:
    - terminal 

---
Assalamualaikum warahmatullahi wabarakaatuh.

Pada artikel kali ini kita akan membahas cara memodifikasi terminal di ubuntu, langsung saja kita langsung praktikan.

##### Membuat File Konfigurasinya
buat file .bash_prompt, ketik perintah berikut ini di terminal:

```shell
touch .bash_prompt
vim .bash_prompt
```
setelah itu tulis kode berikut ini pada file .bash_prompt:

```shell
red="\[$(tput setaf 21)\]"
bright_red="\[$(tput setaf 196)\]"
light_purple="\[$(tput setaf 60)\]"
orange="\[$(tput setaf 172)\]"
blue="\[$(tput setaf 46)\]"
light_blue="\[$(tput setaf 46)\]"
bold="\[$(tput bold)\]"
reset="\[$(tput sgr0)\]"

# Define basic colors to be used in prompt
## The color for username (light_blue, for root user: bright_red)
username_color="${reset}${bold}${light_blue}\$([[ \${EUID} == 0 ]] && echo \"${bright_red}\")";
## Color of @ and ✗ symbols (orange)
at_color=$reset$bold$orange
## Color of host/pc-name (blue)
host_color=$reset$bold$blue
## Color of current working directory (light_purple)
directory_color=$reset$light_purple
## Color for other characters (like the arrow)
etc_color=$reset$red
# If last operation did not succeded, add [✗]- to the prompt
on_error="\$([[ \$? != 0 ]] && echo \"${etc_color}[${at_color}✗${etc_color}]─\")"
# The last symbol in prompt ($, for root user: #)
symbol="${reset}${bold}${bright_red}$(if [[ ${EUID} == 0 ]]; then echo '#'; else echo '$'; fi)"


# Setup the prompt/prefix for linux terminal
PS1="${etc_color}┌─${on_error}[";
PS1+="${username_color}\u"; # \u=Username
PS1+="${at_color}@";
PS1+="${host_color}\h" #\h=Host
PS1+="${etc_color}]-[";
PS1+="${directory_color}\w"; # \w=Working directory
PS1+="${etc_color}]\n| "; # \n=New Line
PS1+="${etc_color}\n└──╼ "; # \n=New Line
PS1+="${symbol}${reset}";

export PS1
```
setelah itu edit file .bashrc ketik pada terminal:
```shell
vim .bashrc
```
setelah itu ketik skript berikut ini pada akhir kode pada file .bashrc:
```shell
# Use custom bash prompt (will execute .bash_prompt script)
if [ -f ~/.bash_prompt ]; then
  . ~/.bash_prompt
fi 
```
maka tampilan terminalnya akan seperti ini:

![terminal ubuntu](https://lh3.googleusercontent.com/r4sGLJSYEXBuoCeOnk7pHfd_FKJJK5Gf3oX5oasqpvzxMOHjZFiD9hydgjI352sG5InsfWwpSUXlc90wnyhlrLjxg1qtb4s3Lv-8mGSqn3DLPXsB7WISUUAnjwJzzngDGDO0MlUwdgKae1G44twa4OLYfO_1V0yvYkxoF705zzq7QDp46FruA2fXzFTsNDgb62gLJbL7bPk3K3rtbqiYQBb7LktPsY69ctl32As1c-2c4OlPnsPcIcLeUBK-Btnz-kAFzcKBNzybYuUXKrWZgrPhDwHdxE6X7LfTqdT7-8NBiX2qfz2l6mCASNXD41hI7saJke3hS5hp-l5s9Zqsnb4kBZA9tJ41aY47DZGJkMPsp9yW2N0HYG05nTDx8ZWdjmdX4_mPw-GWMlFw4Q4EogmWRcXbDtrDTKX_V_htHwYjV2zQywq6QNuYFuXw-eE16p7QH6c3U6qkw6DWNl6vNKBMpcit0GqMdAzD1eyKrxni6pTOMlMbryGcieeqVotLpjNj0jyQlRkzvTIRufpUPKfEviXw6fhsYEfsfp3De3tbIizqaNghcNjLQhUpJcELdrI0ezObe6WLGJj4TUsZF0L24vtDivkNQf5G2BmTs6EdZU4QvroehiCwZ-h3tHtV7gxnWikCYERy53AzTlY7YnvUmwuYrNrLPDr2u0t9Jnmfz39x9tEYSKxEDVZlo3kkVV3oicVi6Y8XpAV9axrq0cgZ=w719-h370-no?authuser=0)










