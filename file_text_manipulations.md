## Working with files, merging, cutting, concatenating etc. 

- concatenate two text files as a two column "table", line-by-line.
	- `paste file1 file2 > file_12`
	or using `awk`
	- `awk 'BEGIN {OFS=" "}{getline line < "file_2"; print $0,line}' file_1`

- filtering out duplicate lines
	- `sort -u` will leave one of each duplicate 
	- `sort | uniq -u` will delete all duplicates 
	or using `awk`
	- `awk '!x[$0]++' file` will keep the order and the first occurance of and delete further duplicates
		- The command controls what will be printed out. `$0` is the whole line, and using the square brackets gives array access. For each node of the array `x` is incrementad and the line printed if the content of that node was not previously set (by using `!`)
	
	

## CSV or other tabular type data 

- show nice table representation of csv files using `column` command: 

	- `column -tns, training_metrics.csv | less -#2NS`
	
	with the comma `,` as separator
	
- or using the escape character in case the delimiter is ";"

	- `column -ts\; category_metrics.csv | less -#2NS`
	

- the `less` command helps in navigating in bigger files 

- on mac
	- `column -t -s, FILENAME.csv | less -#2NS`
