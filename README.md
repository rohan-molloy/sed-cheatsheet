
# Sed examples

A collection based mostly on stackexchange posts along with a few I threw together myself. Later, I will have a `.bashrc` file that contains a collection of regex patterns 


# Find and replace

## Find and replace any match anywhere in the file

	find_and_replace(){
	sed 's/'$find'/'$replace'/g' $@
	}

## Find and replace on lines containing pattern
	find_and_replace_on_lines() {
	sed '/'$pattern'/'$find'/'$replace'/g' $@
	}
## Find and replace the first match
	find_and_replace_first_match(){
	sed 's/'$find'/'$replace'/'
	}
## Find and replace only on the last match
	find_and_replace_last_match() {
	sed 's/\(.*\)'$find'/'$replace'/' $@
	}
## Find and replace inside a range of lines
	find_and_replace_inside_range() {
	sed '$range s/'$find'/'$replace'/g' $@
	} 

## Find and replace outside a range of lines
	find_and_replace_outside_range(){
	sed '$range !s/'$find'/'$replace'/g' $@
	}

## Find and replace the nth instance in a line
	find_and_replace_nth_instance(){
	sed 's/'$find'/'$replace'/'$nth_instance'' $@
	}
## Find and replace if within matching $start and $end pattern
	find_and_replace_within_start_end(){
	sed -e '/'$start'/,/^'$end'/s/'$find'/'$replace'/g' $@
	}
# Printing lines based on pattern

## Print the line matching a pattern
	print_line_matching_pattern(){
	sed '/'$pattern'/!d' $@
	}
## Print the line immediately before pattern
	print_line_preceeding_pattern() {
	sed -n '/'$pattern'/{g;1!p;};h' $@ 
	}
## Print the line immediately after pattern
	print_line_suceeding_pattern(){
	sed -n '/'$pattern'/{n;p;}' 
	}
## Print the line matching pattern and all subsequent lines
	print_line_matching_p
	sed '/'$pattern'/,$!d

## Print lines matching a pattern and give context and position

	sed -n -e '/'$pattern'/{=;x;1!p;g;$!N;p;D;}'

## Print lines matching multiple patterns in any order

	sed '/'$pattern3'/!d; /'$pattern1'/!d; /'$pattern2'/!d' 

## Print lines matching multiple patterns in a specific order

	sed '/'$pattern1'.*'$pattern2'.*'$pattern3'/!d' 

## Print lines matching a minimum number characters

	sed -n '/^.\{$n\}/p' 

## Print lines matching a maximum number characters

	sed -n '/^.\{$n\}/!p' 

## Print substring of a line after matching a section

	sed -n -e 's/^.*'$word' //p' 

# Translation/Refactoring

## Comment lines from $start to $end

	sed "$start,$end {s/^/#/}"  

## Uncomment lines from $start to $end

	sed "$start,$end {s/'^#'//}"  

## Uncomment lines matching pattern 

	sed '/'$pattern'/s/^/#/g'

## Uncomment lines matching pattern 

	sed '/'$pattern'/s/^#//g' 

## Change word to uppercase uppercase if matching pattern

	sed -r "s/\<'$pattern'[a-z]+/\U&/g"   

## Join two lines if the first ends in a backslash

	sed ':a; /\$/N; s/\\n//; ta'  

## Remove characters in set from lines

	set="[0-9]"
	sed 's/'$set'//g' 

## Remove HTML tags

	sed -e :a -e 's/<[^>]*>//g;/</N;//ba'
	
## Insert strings $before and $after to lines matching pattern

	sed '/'$pattern'/s@^.*$@'$before'&'$after'@g'

## Join a relative and absolute path

	sed 's@'$pathAbsolute'@&'/$pathRelative'@g'

# Paragraphing

## Sort paragraphs alphabetically

	(sed '/./{H;d;};x;s/\n/={NL}=/g'| sort | sed '1s/={NL}=//;s/={NL}=/\n/g')

## Print paragraphs only if they contain pattern

	sed '/./{H;$!d;};x;/'$pattern'/!d'

## Insert blank line below lines that match pattern

	sed '/'$pattern'/G' 

## Insert blank line above lines that match pattern

	sed '/'$pattern'/{x;p;x;}'

## Insert blank line above and below matching lines

	sed '/'$pattern'/{x;p;x;G;}'

## Delete the last line of each paragraph

	sed-n '/^$/{p;h;};/./{x;/./p;}'

## Print every nth line starting with x

	sed -n '$n~$xp' 

# Deleting lines 

## Delete lines matching pattern

	sed '/'$pattern'/d' 

## Delete all blank lines

	sed '/./!d' 

## Delete all blank/whitespace lines

	sed "/^\s*$/d"

## Delete all consecutive blank lines except for end

	sed '/./,/^$/!d' 

## Delete all consecutive blank lines except start

	sed '/^$/N;/\n$/D' 

## Delete all consecutive blank lines except for the first two

	sed '/^$/N;/\n$/N;//D' 

## Delete all trailing blank lines

	sed -e :a -e '/^\n*$/{$d;N;};/\n$/ba' 

## Delete every nth line after $start

	sed '"$start"~"$nth"d' 

## Delete all leading blank lines

	sed '/./,$!d' 

# Miscellaneous 

## Read lines from bottom-to-top (tac)

	sed '1!G;h;$!d' 

## Read lines from right to left (rev)

	sed '/\n/!G;s/\(.\)\(.*\n\)/&/;//D;s/.//'

## Number lines - delimiting with tab

	sed = \ | sed 'N;s/\n/\t/') 


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNjc3ODQ3NTIsLTE2OTk3NTE0NDVdfQ
==
-->