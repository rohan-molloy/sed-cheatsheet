---


---

<h1 id="find-and-replace">Find and replace</h1>
<h2 id="find-and-replace-any-match-anywhere-in-the-file">Find and replace any match anywhere in the file</h2>
<pre><code>sed 's/'$find'/'$replace'/g'
</code></pre>
<h2 id="find-and-replace-on-lines-containing-pattern">Find and replace on lines containing pattern</h2>
<pre><code>sed '/'$pattern'/'$find'/'$replace'/g'
</code></pre>
<h2 id="find-and-replace-the-first-match">Find and replace the first match</h2>
<pre><code>sed 's/'$find'/'$replace'/'
</code></pre>
<h2 id="find-and-replace-only-on-the-last-match">Find and replace only on the last match</h2>
<pre><code>sed 's/\(.*\)'$find'/'$replace'/'
</code></pre>
<h2 id="find-and-replace-inside-a-range-of-lines">Find and replace inside a range of lines</h2>
<pre><code>sed '$range s/'$find'/'$replace'/g' 
</code></pre>
<h2 id="find-and-replace-outside-a-range-of-lines">Find and replace outside a range of lines</h2>
<pre><code>sed '$range !s/'$find'/'$replace'/g' 
</code></pre>
<h2 id="find-and-replace-the-nth-instance-in-a-line">Find and replace the nth instance in a line</h2>
<pre><code>sed 's/'$find'/'$replace'/$nth_instance''
</code></pre>
<h2 id="find-and-replace-if-within-matching-start-and-end-pattern">Find and replace if within matching $start and $end pattern</h2>
<pre><code>sed -e '/'$start'/,/^'$end'/s/'$find'/'$replace'/g' 
</code></pre>
<h2 id="print-every-5th-line-starting-with-the-second">Print every 5th line starting with the second</h2>
<pre><code>sed -n '2~5p' 
</code></pre>
<h2 id="print-paragraphs-only-if-they-contain-pattern">Print paragraphs only if they contain pattern</h2>
<pre><code>sed '/./{H;$!d;};x;/'$pattern'/!d'
</code></pre>
<h1 id="translations">Translations</h1>
<h2 id="comment-lines-from-start-to-end">Comment lines from $start to $end</h2>
<pre><code>sed "$start,$end {s/^/#/}"  
</code></pre>
<h2 id="change-word-to-uppercase-uppercase-if-matching-pattern">Change word to uppercase uppercase if matching pattern</h2>
<pre><code>sed -r "s/\&lt;'$pattern'[a-z]+/\U&amp;/g"   
</code></pre>
<h2 id="join-two-lines-if-the-first-ends-in-a-backslash">Join two lines if the first ends in a backslash</h2>
<pre><code>sed ':a; /\$/N; s/\\n//; ta'  
</code></pre>
<h2 id="remove-characters-in-set-from-lines">Remove characters in set from lines</h2>
<pre><code>set="[0-9]"
sed 's/'$set'//g' 
</code></pre>
<h2 id="read-lines-from-bottom-to-top-tac">Read lines from bottom-to-top (tac)</h2>
<pre><code>sed '1!G;h;$!d' 
</code></pre>
<h2 id="read-lines-from-right-to-left-rev">Read lines from right to left (rev)</h2>
<pre><code>sed '/\n/!G;s/\(.\)\(.*\n\)/&amp;\
/;//D;s/.//'
</code></pre>
<h2 id="remove-html-tags">Remove HTML tags</h2>
<pre><code>sed -e :a -e 's/&lt;[^&gt;]*&gt;//g;/&lt;/N;//ba'
</code></pre>
<h2 id="sort-paragraphs-alphabetically">Sort paragraphs alphabetically</h2>
<pre><code>(sed '/./{H;d;};x;s/\n/={NL}=/g'| sort | sed '1s/={NL}=//;s/={NL}=/\n/g')
</code></pre>
<h2 id="insert-strings-before-and-after-to-lines-matching-pattern">Insert strings $before and $after to lines matching pattern</h2>
<pre><code>sed '/'$pattern'/s@^.*$@'$before'&amp;'$after'@g'
</code></pre>
<h2 id="join-a-relative-and-absolute-path">Join a relative and absolute path</h2>
<pre><code>sed 's@'$pathAbsolute'@&amp;'/$pathRelative'@g'
</code></pre>
<h1 id="printing-lines-matching-patterns">Printing lines matching patterns</h1>
<h2 id="print-the-line-matching-a-pattern">Print the line matching a pattern</h2>
<pre><code>sed '/'$pattern'/!d' 
</code></pre>
<h2 id="print-the-line-immediately-before-pattern">Print the line immediately before pattern</h2>
<pre><code>sed -n '/'$pattern'/{g;1!p;};h' 
</code></pre>
<h2 id="print-the-line-immediately-after-pattern">Print the line immediately after pattern</h2>
<pre><code>sed -n '/'$pattern'/{n;p;}' 
</code></pre>
<h2 id="print-the-line-matching-pattern-and-all-subsequent-lines">Print the line matching pattern and all subsequent lines</h2>
<pre><code>sed '/'$pattern'/,$!d
</code></pre>
<h2 id="print-lines-matching-a-pattern-and-give-context-and-position">Print lines matching a pattern and give context and position</h2>
<pre><code>sed -n -e '/'$pattern'/{=;x;1!p;g;$!N;p;D;}'
</code></pre>
<h2 id="print-lines-matching-multiple-patterns-in-any-order">Print lines matching multiple patterns in any order</h2>
<pre><code>sed '/'$pattern3'/!d; /'$pattern1'/!d; /'$pattern2'/!d' 
</code></pre>
<h2 id="print-lines-matching-multiple-patterns-in-a-specific-order">Print lines matching multiple patterns in a specific order</h2>
<pre><code>sed '/'$pattern1'.*'$pattern2'.*'$pattern3'/!d' 
</code></pre>
<h2 id="print-lines-matching-a-minimum-number-characters">Print lines matching a minimum number characters</h2>
<pre><code>sed -n '/^.\{$n\}/p' 
</code></pre>
<h2 id="print-lines-matching-a-maximum-number-characters">Print lines matching a maximum number characters</h2>
<pre><code>sed -n '/^.\{$n\}/!p' 
</code></pre>
<h1 id="deleting-lines-with-sed">Deleting lines with sed</h1>
<h2 id="delete-lines-matching-pattern">Delete lines matching pattern</h2>
<pre><code>sed '/'$pattern'/d' 
</code></pre>
<h2 id="delete-all-blank-lines">Delete all blank lines</h2>
<pre><code>sed '/./!d' 
</code></pre>
<h2 id="delete-all-blankwhitespace-lines">Delete all blank/whitespace lines</h2>
<pre><code>sed "/^\s*$/d"
</code></pre>
<h2 id="delete-all-consecutive-blank-lines-except-for-end">Delete all consecutive blank lines except for end</h2>
<pre><code>sed '/./,/^$/!d' 
</code></pre>
<h2 id="delete-all-consecutive-blank-lines-except-start">Delete all consecutive blank lines except start</h2>
<pre><code>sed '/^$/N;/\n$/D' 
</code></pre>
<h2 id="delete-all-consecutive-blank-lines-except-for-the-first-two">Delete all consecutive blank lines except for the first two</h2>
<pre><code>sed '/^$/N;/\n$/N;//D' 
</code></pre>
<h2 id="delete-all-leading-blank-lines">Delete all leading blank lines</h2>
<pre><code>sed '/./,$!d' 
</code></pre>
<h2 id="delete-all-trailing-blank-lines">Delete all trailing blank lines</h2>
<pre><code>sed -e :a -e '/^\n*$/{$d;N;};/\n$/ba' 
</code></pre>
<h2 id="delete-every-nth-line-after-start">Delete every nth line after $start</h2>
<pre><code>sed '"$start"~"$nth"d' 
</code></pre>
<h2 id="delete-the-last-line-of-each-paragraph">Delete the last line of each paragraph</h2>
<pre><code>sed-n '/^$/{p;h;};/./{x;/./p;}'
</code></pre>
<h2 id="insert-blank-line-below-lines-that-match-pattern">Insert blank line below lines that match pattern</h2>
<pre><code>sed '/'$pattern'/G' 
</code></pre>
<h2 id="insert-blank-line-above-lines-that-match-pattern">Insert blank line above lines that match pattern</h2>
<pre><code>sed '/'$pattern'/{x;p;x;}'
</code></pre>
<h2 id="insert-blank-line-above-and-below-matching-lines">Insert blank line above and below matching lines</h2>
<pre><code>sed '/'$pattern'/{x;p;x;G;}'
</code></pre>
<h2 id="number-lines---delimiting-with-tab">Number lines - delimiting with tab</h2>
<pre><code>sed = \ | sed 'N;s/\n/\t/') 
</code></pre>
