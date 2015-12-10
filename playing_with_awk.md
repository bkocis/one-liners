## small one-liners using awk 

- unzip mulitple zip files each to a separate folder 
	- `find . *zip | awk -F '.zip' '{print "unzip "$0" -d "$1"} ' | sh`
