# lame-bulk-convert
A Bash script designed to bulk-convert files to mp3-320kbps format.

This was written purely based on an immediate need, but could be improved in the future.

```
#!/bin/bash
# lame-bulk-convert
# Written by Captain Couch
# Jan. 4 2022
# Last Updated: Jan. 4 2022
# Purpose: Bulk convert all audio files in a directory to 320kbps MP3 using
#	   the LAME mp3 encoder as a prerequisite.

# Set the $SAVEIFS variable as the global Internal Field Separator character.
# This preserves the original global $IFS variable to change it back later.

SAVEIFS=$IFS

# Set the $IFS variable to a space character using substitution escape sequence 
# for the space character.

IFS=$(echo -en "\n\b")

# Create a new directory for the newly-converted files, if not already existing.

mkdir -p ./converted-mp3

# Loop and convert each file "i" to mp3. Quotation marks are used to account for
# spaces and illegal characters. The files are placed in ./converted-mp3/filename.mp3.

for i in $(ls)
do
	# Set a variable "c" containing the filename with the ".ext" extension removed.
	# For example, "sound.wav" would become "sound", and "sound.foo.wav" would
	# become "sound.foo".

	c="${i%.*}"
	lame -V2 "$i" -h -b 320 "./converted-mp3/$c.mp3"
done	

# Set the $IFS variable back to previous value, using the value stored in $SAVEIFS
# for safekeeping.

IFS=$SAVEIFS
```
