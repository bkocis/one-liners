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

- a compilation of sed one-liners 
	- http://sed.sourceforge.net/sed1line.txt

- search files in-between specific date
	- using `find`
		- `find . -newermt '2015-03-03' ! -newermt '2015-03-04'` 
		- `find . -newermt 'Nov 11 03:56' ! -newermt 'Nov 11 03:59' -printf '%Tc %p\n'`

			where `-printf '%Tc %p\n'` will print out the exact date 

			adding `| sort -n` to the end will do the evident sorting

	- using `ls` and `awk`
		- `ls -ltr | grep 'Nov.*5.*10' | awk '{print $NF}'`

		and copy them to another folder:

		- `ls -ltr | grep 'Nov.*5.*10' | awk '{print $NF}' | xargs -i cp '{}' folder`

- find and sub folder depth control and skip folders/subfolders 
	- `find . '*.py* -maxdepth 1 -not -path './*' ` 



- remove files but skip some
	- `rm * !(*.zip)` or `rm *.* !(*.zip|*.dat)`
	- `rm -r */` to remove only folders 


- sorting using `sort`
	- `sort -k 2,2n -k 3 file.txt`

		where `-k 2,2n -k 3` means to sort data using the given column number. First, it will sort 2nd column (date dd field) and then 3rd column (time). Found [here](http://www.cyberciti.biz/faq/linux-unix-sort-date-data-using-sortcommand/)





####related
[vi commands](https://github.com/bkocis/linux_rc-s/blob/master/playing_with_vi/)

[awk stuff](https://github.com/bkocis/linux_rc-s/blob/master/playing_with_awk/)

# Disclaimer 

The fact you can do something in Bash doesn't necessarily mean you should! ;)

### Worth to check out 

[jlevy's art-of-command-line](https://github.com/jlevy/the-art-of-command-line)  
 
[zeef/caleb.xu](https://unix-shell.zeef.com/caleb.xu)
