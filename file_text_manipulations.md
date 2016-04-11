## Working with files, merging, cutting, concatenating etc. 

- concatenate two text files as a two column "table", line-by-line.
	- `paste file1 file2 > file_12`
	or using `awk`
	- `awk 'BEGIN {OFS=" "}{getline line < "file_2"; print $0,line}' file_1`

- filtering out duplicate lines
	- `sort -u` 
	or using `awk`
	- `awk '!x[$0]++' file`
		- where `$0` is the whole line, and using the square brackets gives array access. For each each node of the array `x` is incrementad and the line printed if the content of that node was not previously set (by using `!`)
	
	

