####Vi text editor commands examples

- set up the `.vimrc` file [rc files](https://github.com/bkocis/linux_rc-s/blob/master/vimrc/)

- `:setlocal spell` to get highlighted spell check. Choose from offered correction by typing `z=` at the misspelled word. 

- `:g/^/m0` to reverse the content of a file, for example lines 1-2-3 to 3-2-1

- simple find and replace anything in whole file `:%s/something/new/g`

- remove all white space (unknown amount) 
	`:%s/[^ ]\zs \+/ /g` 	where `\zs` means the required result starts after the `[^ ]` (lines that start with a whitespace) 
- replace occurance of a character in selected lines and selected number of occurances in a line
 
	`:g/^/let i=0 | where i<1 | s/a/b/ | let i+=1 | endwhile` - first occurances of a is replaced by b in all lines (g)
	`:12:28/^/let i=0 | where i<1 | s/a/b/ | let i+=1 | endwhile` - first occurance of a is replaced by b in lines 12 to 28
