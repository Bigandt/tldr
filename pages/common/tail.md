# tail

> Display the last part of a file.

- Show last 'num' lines in file:

`tail -n {{num}} {{file}}`

- Show all file since line 'num':

`tail -n +{{num}} {{file}}`

- Show last 'num' bytes in file:

`tail -c {{num}} {{file}}`

- Keep reading file until `Ctrl + C`:

`tail -f {{file}}`

- Keep reading file until `Ctrl + C`, even if the file is rotated:

`tail -F {{file}}`

Extract middle section of a text file. Invoke tail using a line-count from the beginning, not the end.

`tail -n +{{from_line}_number} {{file}} | head -{{number_of_lines_to_see}}`

Example below

`cat -n myfile.txt | tail -n +150000 | head -100 | less`