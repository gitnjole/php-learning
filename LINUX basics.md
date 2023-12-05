#linux #programming
# Permissions

r = 4
w = 2
x = 1

```bash
drwxr-xr-x 4 njole njole 4096 Nov 30 15:52 Desktop
```
	d - directory
	rwx - user
	r-x - group
	r-x - other
	njole - user
	njole - group
	4096 - file size(?)
## CHMOD
change mode

```bash
chmod u+w file.file
```
	->chmod naredba
	-> u/g/o user group ili other
	->+/- dodavanje ili micanje ovlasti
	->file.file ime datoteke ili direktorija
>[!info] korisnik i dodavanje ovlasti moraju biti pisani zajedno, npr u+r, o-x, g+w

```bash
chmod 770 file.file 
```
	-> all permissions for user
	-> all permissions for group
	-> *no* permissions for other

```bash
chmod 725 file.file
```
	-> all permissions for user
	-> write permissions for group
	-> read and execute permissions for other

-R changes permissions for all files and directories inside
```bash
chmod -R 600 Downloads
```
	-> read and write permission for anything inside Downloads directory

## CHOWN
change ownership

```bash
chown -R user2 Downloads/
```
	-> change ownership of Downloads directory to user2

drwxr-xr-x 4 user2 njole 4096 Nov 30 15:52 Downloads


# Usage

## CP
copy

```bash
cp ...file/source destination 
```


```bash
cp ./DirectoryA_1/README.txt ./DirectoryA_2
```

## GREP

Search for the given string in a single file
```bash
grep "literal_string" filename
```

Case insensitive search using grep -i
```bash
grep -i "string" FILE
```

Search through all files within a directory
```bash
grep -r "string" *
```

Count number of lines matched
```bash
grep -c "string" demo_text
```

## TOP

task manager, write out all processes 

## PS

write out all processes started by user