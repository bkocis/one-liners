# One-liners
Gnu/Linux command line "one-liners"

Based on the excellent summary of command line tools by jlevy 
https://github.com/bkocis/the-art-of-command-line

Here are some extended versions of the "one-liners" from the mentioned repository. The following solutions are specific cases that I encountered; it is probable that you have found similar solutions.  

- Reverse the content of all specified text files using `find` and `vi` commands 

	- `find . -iname '*.DPT' -exec vi '{}' -c ':g/^/m0' -c ':wq' \;`

- Copy one file into all subfolders in the current working directory 

	- `find . -type d -exec cp file.name '{}' \;`

- swap a file using `find`, `cp` and `rename` (in two steps) in case two files are in separate folders or subfolders. The 'old.f' content and filename is swaped to 'new.f'. 
	- `find . -iname '*.f' -exec cp ./path-to-file/new.f '{}' \;`
	- `find . -iname 'new.f' -exec rename 's/old.f/new.f/' '{}' \;`

- a compillation of sed one-liners 
	- http://sed.sourceforge.net/sed1line.txt

- search files inbetween specific date
	- using `find`
		- `find . -newermt '2015-03-03' ! -newermt '2015-03-04'` 
		- `find . -newermt 'Nov 11 03:56' ! -newermt 'Nov 11 03:59' -printf '%Tc %p\n'`

			where `-printf '%Tc %p\n'` will print out the exact date 

			adding `| sort -n` to the end will do the evident sorting

	- using `ls` and `awk`
		- `ls -ltr | grep 'Nov.*5.*10' | awk '{print $NF}'`

		and copy them to another folder:

		- `ls -ltr | grep 'Nov.*5.*10' | awk '{print $NF}' | xargs -i cp '{}' folder`

- find and subfolder depth control 
	- `find . '*.py* -maxdepth 1 -not -path './*' ` 

# Disclaimer 

The fact you can do something in Bash doesn't necessarily mean you should! ;)

### Worth to check out 
https://unix-shell.zeef.com/caleb.xu
