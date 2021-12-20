#!/bin/bash

pause=0.2
file="${@: -1}"

while getopts ":f:s:n:" opt; do
	case "$opt" in
		f) file=$OPTARG ;;
		s) pause=$OPTARG ;;
		n) numstart="$OPTARG" ;;
	esac
done

pusher() {
	while IFS= read -r word; do
		clear;
		tput cup $(( $(tput lines)/2 )) $(( $(tput cols)/2 - ( ${#word}/2 ) )) ;
		printf "$word"
		sleep $pause;
	done
}

tput civis; trap "tput cnorm; clear" 2 #SIGINT
[[ ! -f $file ]] && echo "Error, this file does't support." && tput cnorm && exit 1

case "$file" in
	*.pdf) pdftotext "$file" - | tr -s '[:blank:]' '[\n*]' | pusher ;;
	*) tr -s '[:blank:]' '[\n*]' < "$file" | pusher ;;
esac

tput cnorm
exit 0
