# ppassdb
- It is posix compliant shell script that manages encrypted single line text files.
- It is a discount, inferior, and a rip-off version of [password-store](https://www.passwordstore.org/).
- It uses `gpg` to encrypt files.
- Aims for portability so you can store them in a USB drive
- Designed to work on most Operating Systems including Android
- It encrypts indivdual text files in a single line and encrypts them
indivdually. meaning every file can have different master passwords and
it is not required to create a `gpg` keypair
- Puts the encrypted text to clipboard after decryption
- If the script doesn't support the clipboard, there is an option to
use the web browser instead.

## Table of Contents
- [Depedencies](#Depedencies)
	- [Optional](#Optional)
	- [GNU/Linux](#GNU/Linux)
	- [Windows](#Windows)
	- [Android](#Android)
	- [Installation](Installation)
- [Installation](#Installation)
	- [ppassdb](#install-ppassdb)
- [Uninstallation](#Uninstallation)
	- [Remove encrypted all files](#remove-enrypted-files)
	- [Uninstall ppassdb](#uninstall-ppassdb)
- [Run](#Run)
	- [Usage](#Usage)
	- [Operations](#Operations)
	- [Options](#Options)
		- [Specific for `-E` only](#e-only)
		- [Specific to both `-D` and `-E`](#d-and-e)
	- [Examples](#Examples)
		- [Lists all encrypted file:](#example-1)
		- [Encrypt a text](#example-2)
		- [Decrypts the password and put it into the system clipboard and clears for a period of time](#example-3)
- [Directory location](#directory-location)
	- [Priorities for searching existed directories](#search-directory) 
	- [Priorities for initializing directories](#initialize-directory) 
	- [Changing Directory Locations](#change-directory) 

## Depedencies
- `gpg`

### Optional:
- `tree`
- `notify-send`

### GNU/Linux:
- `xclip` or `wl-copy`

### Windows:
- `Bash` (Either `Git bash` or `WSL`)

### Android:
- `Termux`
- `Termux: API`

## Installation
### <a name=install-ppassdb></a> `ppassdb`:
```
curl -LO  https://raw.githubusercontent.com/jamez2128/ppassdb/master/ppassdb
```
For system-wide installation, put the script to `/usr/local/bin` (Need root privileges in Linux):
```
cp ppassdb /usr/local/bin
```

If the script doesn't run, make sure that you that the file has
permissions to run. To give it execution permissions:
```
chmod +x ./ppassdb
```

## Uninstallation
If you want to know where the script saves the files and you want to delete it, run this command:
```
ppassdb -L | sed -n 2p
```
If you think that it is safe to delete, run this command:
### <a name="remove-enrypted-files"></a> Remove encrypted all files:
```
rm -r "$(ppassdb -L | sed -n 2p)"
```
### <a name="uninstall-ppassdb"></a>Uninstall ppassdb:
```
rm ppassdb /usr/local/bin
```
## Run
### Usage
```
ppassdb <operation> [options] <filename>
```

### Operations
- `-h`, `--help`      To shows this help message
- `-E`              For adding and encryting text files.
- `-D`              For decrypting text file.
- `-L`              Lists all the added encrypted text files.

### Options
- `-n`      Pushes feedback messages to notifications (Only works on Linux)

#### <a name="e-only"></a>Specific for `-E` only:
- `-g`       Auto generates a random string and encrypts it.

#### <a name="d-and-e"></a>Specific to both `-D` and `-E`:
- `-c`      Clears the clipboard after a period of time.
- `-f`      This will be the input file name. "/" are not allowed in this 
        option and will be replaced with "_" if present.
- `-i`      An identifier to group encrypted files. This is optional and if 
        this option is not called, it will use the default folder.
- `-s`      Shows the text. This will return a successful exit status even if 
        the clipboard failed.
- `-j`      Puts text to the generated html to copy it from the web browser.

### Examples
#### <a name="example-1"></a> Lists all encrypted file:
```
ppassdb -L
```

#### <a name="example-2"></a>Encrypt a text:
```
ppassdb -E -i "username" -f "website.pass" 
```

#### <a name="example-3"></a>Decrypts the password and put it into the system clipboard and clears for a period of time:
```
ppassdb -Dc -i "username" -f "website.pass"
```

##  <a name="directory-location"></a>Directory Location
If you want to know where the script saves the files, run this command:
```
ppassdb -L | sed -n 2p
```
If you want to know all the possible locations, it is listed below

###  <a name="search-directory"></a>Priorities for searching existed directories:
- `/storage/emulated/0/ppassdb`
- `$APPDATA/ppassdb`
- `~/Library/Application Support/ppassdb`
- `~/.ppassdb`
- `~/.local/share/ppassdb`
- `$XDG_DATA_HOME/ppassdb`

###  <a name="initialize-directory"></a>Priorities for initializing directories:
- `/storage/emulated/0/ppassdb`
- `$APPDATA/ppassdb`
- `~/Library/Application Support/ppassdb`
- `$XDG_DATA_HOME/ppassdb`
- `~/.local/share/ppassdb`
- `~/.ppassdb`
- Current directory

### <a name="change-directory"></a> Changing Directory Locations:
You also change the location of the script by editing directly in
the script's variable in the Configuration part, or exporting "PPASSDB_HOME" as 
an environmental variable. For example:
- Change to Home Directory:
```
export PPASSDB_HOME="$HOME/.ppassdb"
```

- Change to XDG Base Directory
```
export PPASSDB_HOME="$HOME/.local/share/ppassdb"
```

or this (Must have XDG_DATA_HOME defined)
```
export PPASSDB_HOME="$XDG_DATA_HOME/ppassdb"
```
It is recommended to set the environmental variable so it does need to check
for directories evertime the script runs. You have to suffix an empty directory
or the directory that has files made by the script.
