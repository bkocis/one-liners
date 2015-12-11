#### small one-liners using awk 

- calculate the sum of a chocen column in a textfile of numbers 
	- `awk '{x += $3} END {print x}' textfile.txt` will return the sum of the third column 

- unzip mulitple zip files each to a separate folder 
	- `find . *zip | awk -F '.zip' '{print "unzip "$0" -d "$1"}' | sh`
