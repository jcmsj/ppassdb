# `ppassdb`
- It is POSIX compliant shell script that manages encrypted text files.
- It is another alternative of [password-store](https://www.passwordstore.org/).
- It uses `gpg` to encrypt files.
- Aims for portability.
- Designed to work on most Operating Systems including Android and Windows.
- It encrypts text files and encrypts them indivdually or with a key pair .
- It mainly puts the encrypted text to clipboard after decryption.
- If the script doesn't support the clipboard, there is an option to
use the web browser instead.

# `dpassmenu`
- A simple dmenu script that decrypts files to clipboard with
ppassdb that I definitely not copied from the [password-store](https://www.passwordstore.org/)
devs.
- Very powerful script especially if binded on a keyboard

## Table of Contents
- [Depedencies](#Depedencies)
	- [Optional](#Optional)
	- [GNU/Linux](#gnu-linux)
	- [Windows](#Windows)
	- [Android](#Android)
- [Installation](#Installation)
	- [ppassdb](#install-ppassdb)
	- [dpassmenu](#install-dpassmenu)
- [Uninstallation](#Uninstallation)
	- [Remove encrypted all files](#remove-encrypted-files)
	- [Uninstall ppassdb](#uninstall-ppassdb)
	- [Uninstall dpassmenu](#uninstall-dpassmenu)
- [Manual](#Manual)
	- [ppassdb](#ppassdb-manual)
		- [Usage](#Usage-ppassdb)
		- [Operations](#Operations-ppassdb)
		- [Options](#Options-ppassdb)
			- [Specific for `-E` only](#e-only-ppassdb)
			- [Specific to both `-D` and `-E`](#d-and-e-ppassdb)
		- [Examples](#Examples)
			- [Lists all encrypted file](#example-1-ppassdb)
			- [Encrypt a text](#example-2-ppassdb)
			- [Decrypts the password and put it into the system clipboard and clears for a period of time](#example-3-ppassdb)
	- [dpassmenu](#dpassmenu-manual)
		- [Usage](#Usage-dpassmenu)
		- [Options](#Options-dpassmenu)
- [Directory location](#directory-location)
	- [Priorities for searching existed directories](#search-directory) 
	- [Priorities for initializing directories](#initialize-directory) 
	- [Changing Directory Locations](#change-directory) 

## Depedencies
- `gpg`
- `oauthtool` (For OTP codes)

### Optional:
- `tree`
- `notify-send`

### <a name=gnu-linux></a> GNU/Linux:
- `xclip` or `wl-copy`
- `dmenu` (`dpassmenu`)

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

Give execution permissions:
```
chmod +x ./ppassdb
```

For system-wide installation, put the script to `/usr/local/bin` (Need root privileges in Linux):
```
cp ppassdb /usr/local/bin
```
### <a name=install-dpassmenu></a>`dpassmenu`:
```
curl -LO  https://raw.githubusercontent.com/jamez2128/ppassdb/master/dpassmenu
```

Give execution permissions:
```
chmod +x ./dpassmenu
```

For installation, same thing above:

```
cp dpassmenu /usr/local/bin
```

## Uninstallation
If you want to know where the script saves the files and you want to delete it, run this command:
```
ppassdb -P
```
If you think that it is safe to delete, run this command:
### <a name="remove-encrypted-files"></a> Remove all encrypted files:
```
rm -r "$(ppassdb -P)"
```
### <a name="uninstall-ppassdb"></a>Uninstall `ppassdb`:
```
rm  /usr/local/bin/ppassdb
```
### <a name=uninstall-dpassmenu></a> Uninstall `dpassmenu`:
```
rm /usr/local/bin/dpassmenu
```
## Manual
### <a name="ppassdb-manual"></a>`ppassdb`
#### <a name="Usage-ppassdb">Usage
```
ppassdb <operation> [options] <filename>
```

#### <a name="Operations-ppassdb">Operations
- `-h`, `--help`	To shows this help message
- `-E`		For adding and encrypting text files.
- `-D`		For decrypting text file.
- `-L`		Lists all the added encrypted text files. If -i
		is not specified, it will list all encrypted files
		from all groups.
- `-P`		Outputs the path to where all the encrypted
		files will be stored.

#### <a name="Options-ppassdb"></a>Options
- `-n`      Pushes feedback messages to notifications (Only works on Linux)

##### <a name="e-only-ppassdb"></a>Specific for `-E` only:
- `-g`       Auto generates a random string and encrypts it.
- `-a`	Specify the number of characters to randomly generate.
- `-t`	Specify the type of characters to randomly generate.
	- `[:graph:]` - All printable characters, except whitespace
	- `[:alnum:]` - All letters and numbers
	- `[:alpha:]` - Letters only
	- `[:lower:]` - Capital letters only
	- `[:upper:]` - Small letters only 
	- `[:digit:]` - Numbers only
	- For more options, refer to the `tr` manual
- `-r`	Encrypts it with a existing user ID name made with a key pair.
	Without this option, it will use symetric encryption instead.
- `-m`	Encrypts a multi-line text instead of a single line.
- `-o`	For decryption, it converts the OTP URL to OTP code. For
	encryption, it verifies and tell information about the
	OTP URL to encrypt so to know whether the URL is valid
	for code generation.

##### <a name="d-and-e-ppassdb"></a>Specific to both `-D` and `-E`:
- `-d`	This option will not attempt to copy to clipboard.
- `-c`      Clears the clipboard after a period of time.
- `-f`      This will be the input file name. `/` are not allowed in this 
        option and will be replaced with `_` if present.
- `-i`      An identifier to group encrypted files. This is optional and if 
        this option is not called, it will use the default folder.
- `-s`      Shows the text. This will return a successful exit status even if 
        the clipboard failed.
- `-j`      Puts text to the generated html to copy it from the web browser.
- `-k`	Forgets password after an operation was performed

#### Examples
##### <a name="example-1-ppassdb"></a> Lists all encrypted file:
```
ppassdb -L
```

##### <a name="example-2-ppassdb"></a>Encrypt a text:
```
ppassdb -E -i "username" -f "website.pass" 
```

##### <a name="example-3-ppassdb"></a>Decrypts the password and put it into the system clipboard and clears for a period of time:
```
ppassdb -Dc -i "username" -f "website.pass"
```

### <a name="dpassmenu-manual"></a>`dpassmenu`

A simple dmenu script for ppassdb

#### <a name="Usage-dpassmenu"></a>Usage
```
dpassmenu [options]
```

#### <a name="Options-dpassmenu"></a>Options
- `--help`		To show this help message
- `--otp`		Generate an OTP code instead of the
		encrypted text. All files without the
		.otp at the end are hidden unless
		if --show-all is specified.
- `--show-all`	Show all files even if otp is specified.
- `--sort`		Sort all files and folders together

##  <a name="directory-location"></a>Directory Location
If you want to know where the script saves the files, run this command:
```
ppassdb -P
```
If you want to know all the possible locations, it is listed below

###  <a name="search-directory"></a>Priorities for searching existed directories:
- `/storage/emulated/0/ppassdb`
- `%APPDATA%\ppassdb`
- `~/Library/Application Support/ppassdb`
- `~/.ppassdb`
- `~/.local/share/ppassdb`
- `$XDG_DATA_HOME/ppassdb`

###  <a name="initialize-directory"></a>Priorities for initializing directories:
- `/storage/emulated/0/ppassdb`
- `%APPDATA%\ppassdb`
- `~/Library/Application Support/ppassdb`
- `$XDG_DATA_HOME/ppassdb`
- `~/.local/share/ppassdb`
- `~/.ppassdb`
- Current directory

### <a name="change-directory"></a> Changing Directory Locations:
If you wish to change the location, you can do so by editing directly in
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
for directories everytime the script runs. You have to suffix an empty directory
or the directory that has files already made by the script. If you plan to change it,
make sure to move it to desired directory first before setting an environmental variable.
