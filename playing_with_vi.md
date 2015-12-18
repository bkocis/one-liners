####Vi text editor commands examples

- set up the `.vimrc` file [rc files](https://github.com/bkocis/linux_rc-s/blob/master/vimrc/)

- `g/^/m0` to reverse the content of a file, for example lines 1-2-3 to 3-2-1

- `setlocal spell` to get highlighted spell check. Choose from offered correction with typing `z=` at the misspelled word. 

- find and replace characters, words by using `:``%s/something/new/g`

- remove all white space (unknown amount) 
	-`%s/[^ ]\zs \+/ /g` 	where `\zs` means the required result starts after the `[^ ]` (lines that start with a whitespace) 

