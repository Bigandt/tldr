# ksh

> Korn Shell.
> `bash` and `sh`-compatible command line interpreter.
> More information: <http://kornshell.com>.

- Start interactive command line interpreter:

`ksh`

- Execute a command:

`ksh -c {{command}}`

- Run commands from a file:

`ksh {{file}}`

- Run commands from a file and print them as they are executed:

`ksh -x {{file}}`

- Template:

```
#!/bin/ksh

if [[ -z $1 ]]
then
	echo "Not input argument found"
	echo "Exiting"
	exit
fi

for var in "$@"
do
	echo "Read argument '$var'"
done 

```