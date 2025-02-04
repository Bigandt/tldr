# sed

> Edit text in a scriptable manner.

- Replace the first occurrence of a regular expression in each line of a file, and print the result:

`sed 's/{{regex}}/{{replace}}/' {{filename}}`

- Replace all occurrences of an extended regular expression in a file, and print the result:

`sed -r 's/{{regex}}/{{replace}}/g' {{filename}}`

- Replace all occurrences of a string in a file, overwriting the file (i.e. in-place):

`sed -i 's/{{find}}/{{replace}}/g' {{filename}}`

- Replace only on lines matching the line pattern:

`sed '/{{line_pattern}}/s/{{find}}/{{replace}}/' {{filename}}`

- Delete lines matching the line pattern:

`sed '/{{line_pattern}}/d' {{filename}}`

- Print only text between n-th line till the next empty line:

`sed -n '{{n}},/^$/p' {{filename}}`

- Apply multiple find-replace expressions to a file:

`sed -e 's/{{find}}/{{replace}}/' -e 's/{{find}}/{{replace}}/' {{filename}}`

- Replace separator / by any other character not used in the find or replace patterns, e.g., #:

`sed 's#{{find}}#{{replace}}#' {{filename}}`

- Print only the n-th line of a file:

`sed '{{n}}q;d' {{filename}}`

- Format error.log i terminal

`tail -f /var/log/apache2/error.log | sed \"s/\\\\\\n/\\\\n/g\" `

- Print log between timestamps. Prints from first match of first regex til first match of second regex 

`sed -nE '/^foo/,/^bar/p' file.log`

`sed -nE '/^03\/22 08:53:52/,/^03\/22 08:54:24/p' file.log > newfile.log`