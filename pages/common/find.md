# find

> Find files or directories under the given directory tree, recursively.

- Find files by extension:

`find {{root_path}} -name '{{*.ext}}'`

- Find files by matching multiple patterns:

`find {{root_path}} -name '{{*pattern_1*}}' -or -name '{{*pattern_2*}}'`

- Find directories matching a given name, in case-insensitive mode:

`find {{root_path}} -type d -iname {{*lib*}}`

- Find files matching a path pattern:

`find {{root_path}} -path '{{**/lib/**/*.ext}}'`

- Find files matching a given pattern, excluding specific paths:

`find {{root_path}} -name '{{*.py}}' -not -path '{{*/site-packages/*}}'`

- Find files matching a given size range:

`find {{root_path}} -size {{+500k}} -size {{-10M}}`

- Run a command for each file (use `{}` within the command to access the filename):

`find {{root_path}} -name '{{*.ext}}' -exec {{wc -l {} }}\;`

- Example below

`find ./ -maxdepth 1 -type f -name 'testfile' -exec wc -l {} \;`

- Find files modified in the last 7 days, and delete them:

`find {{root_path}} -mtime {{-7}} -delete`

- Find files and remove lines containing 'Permission denied' (or any other string):

`sudo find {{root_path}} -name '{{filename.*}}' 2>&1 | grep -v 'Permission denied'`

- Find filenames for XML files older than 5 minutes and bigger than 0 bytes:

`find {{root_path}} -maxdepth 1 -mmin +1 -type f -size +0c -printf "%f\n"`

- Find files bigger than 4096 bytes. (https://superuser.com/questions/204564/how-can-i-find-files-that-are-bigger-smaller-than-x-bytes):

`find {{root_path}} -type f -size +4096c`

- Find files smaller than 4096 bytes. (https://superuser.com/questions/204564/how-can-i-find-files-that-are-bigger-smaller-than-x-bytes):

`find {{root_path}} -type f -size -4096c`
