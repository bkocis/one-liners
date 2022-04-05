# One-liners
Gnu/Linux command line "one-liners"

Most probably you are pondering how to solve a specific problem using the command line. The following solutions are specific cases that I encountered; it is most likely that you have found similar solutions. The purpose of this repository is to represent an on-line substitution of my paper-notebook of one-liners.

- Reverse the content of all specified text files using `find` and `vi` commands 

	- `find . -iname '*.DPT' -exec vi '{}' -c ':g/^/m0' -c ':wq' \;`

- Copy one file into all sub folders in the current working directory 

	- `find . -type d -exec cp file.name '{}' \;`

- swap a file using `find`, `cp` and `rename` (in two steps) in case two files are in separate folders or sub folders. The 'old.f' content and filename is swapped to 'new.f'. 
	- `find . -iname '*.f' -exec cp ./path-to-file/new.f '{}' \;`
	- `find . -iname 'new.f' -exec rename 's/old.f/new.f/' '{}' \;`


- search files in-between specific date
	- using `find`
		- `find . -newermt '2015-03-03' ! -newermt '2015-03-04'` 
		- `find . -newermt 'Nov 11 03:56' ! -newermt 'Nov 11 03:59' -printf '%Tc %p\n'`

			where `-printf '%Tc %p\n'` will print out the exact date 
			
			to be more specific use: `-printf '%TY-%Tm-%Td--%TH:%TM:%TS'`

			`%p` prints out the path

			adding `| sort -n` to the end will do the evident sorting

	- using `ls` and `awk`
		- `ls -ltr | grep 'Nov.*5.*10' | awk '{print $NF}'`

		and copy them to another folder:

		- `ls -ltr | grep 'Nov.*5.*10' | awk '{print $NF}' | xargs -i cp '{}' folder`


- returning path string with find:

	- ``find `pwd` ....`` will return the absolute path, since find is giving output relative to the input 

	- `find . .....` 

	- `find . -iname '*x' -printf '%p\n' ` will print out the filename only without the path 


- find with subfolder depth control
	- `find . -maxdepth 1 -iname '*.py*` 

- find partial path and file 

	- `find -path '*.git/logs/HEAD'`  using `iname` instead of `path` does not work

- excluding folders from find 
	- `find . -path ./some/path -prune -o -iname '*some*' -print`

	or without `-prune`

	- `find . -iname '*some*' -not -path "./some_path/*"` 
	
	the `*` is very much needed, otherwise it will exclude only the given path and not all paths below

	- in addition one can exclude a given folder at any level by 
	- `find . -iname '*some*' -not path "*/some_path/*"`
	

- combining regular expression with `find`. For example find all filenames that are longer then 5 characters
	- `find -regextype posix-egrep -regex '.*[^/]{5}'`

- multiple find ; to use logical operators with `find` through regular expression 
	- `find . -regextype posix-egrep -regex "(.*bgg.*\.*add.*)"`  AND
	- `find . -regextype posix-egrep -regex "(.*bgg.*|.*add.*)"`  OR


- chaining commands inside `find`, for example rename specific files and move them to another folder 
	- `find . -iname '*.dat' -exec rename 's/dat/DPT/' '{}' \; -exec mv '{}' ~/home/somewhere \;`

- remove files but skip some
	- `rm !(*.zip)` or `rm !(*.zip|*.dat)`
	- `rm -r */` to remove only folders 

- cleaning git repo
	- `find . -name "*.pyc" -exec git rm {} \;`

- sorting using `sort`
	- `sort -k 2,2n -k 3 file.txt`

		where `-k 2,2n -k 3` means to sort data using the given column number. First, it will sort 2nd column (date dd field) and then 3rd column (time). Found [here](http://www.cyberciti.biz/faq/linux-unix-sort-date-data-using-sortcommand/)



- a compilation of sed one-liners 
	- http://sed.sourceforge.net/sed1line.txt


- networking using `nmcli`
	- Connect to netwrok `nmcli device wifi connect <SSID> password <password> `
	- connect to netwrok `nmcli con up id <SSID>`
	- check available devices `nmcli d`
	- check all wifi networks in the area with signal strength `nmcli d wifi`
	



## Related:

[vi commands](https://github.com/bkocis/one-liners/blob/master/playing_with_vi.md)

[awk stuff](https://github.com/bkocis/one-liners/blob/master/playing_with_awk.md)

[file text manipulations](https://github.com/bkocis/one-liners/blob/master/file_text_manipulations.md)

## Disclaimer 

The fact you can do something doesn't necessarily mean you should! ;)

## Worth checking out: 

[jlevy's art-of-command-line](https://github.com/jlevy/the-art-of-command-line)  
 
[zeef/caleb.xu](https://unix-shell.zeef.com/caleb.xu)

+++
