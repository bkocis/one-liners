#### small one-liners using awk 

- calculate the sum of a chocen column in a textfile of numbers 
	- `awk '{x += $3} END {print x}' textfile.txt` will return the sum of the third column 

- unzip mulitple zip files each to a separate folder 
	- `find . *zip | awk -F '.zip' '{print "unzip "$0" -d "$1"}' | sh`

- count elements from the end backwards 
	- `awk '{print $(NF-1)}'`i

- concatenate two text files as a two column "table", line-by-line.
	- `awk 'BEGIN {OFS=" "}{getline line < "file_2"; print $0,line}' file_1`

- example of searching for pattern "Loading" and taking the second last and last column, with string cleaning of column values 
 	- `awk  '/Loading/{print $(NF-2) ";" substr($(NF-0), 1, length($(NF-0))-1)  }' GRAYLOG_EXPORT.csv`


Do some basic arithmetic on floats extracted by string search:

```bash 
#!/bin/bash

# cli version of the command 
# LC_NUMERIC="C" awk  '/TIMING/{ print $(NF-1) ; sum += $(NF-1) ; n++ } END { print sum ; print n ; print sum/n }' model_elastic_net_05Super_02.txt

FILENAME=$1
STRING_TO_MATCH=$2
COLUMN_FROM_END=$3

echo $FILENAME
echo $STRING_TO_MATCH
echo $COLUMN_FROM_END

# use variable passing to awk from bash with the `-v` flag
# use the `$0 ~` to pass the sting to awk
# local setting for handling commas and dot for floats
LC_NUMERIC="C" awk -v search="$STRING_TO_MATCH" -v nc="$COLUMN_FROM_END" '$0 ~ search{ print $(NF-nc) ; sum += $(NF-nc) ; n++ } END { print sum ; print n ; print sum/n }' $FILENAME

```
