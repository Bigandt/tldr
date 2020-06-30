# cmd

> The Windows command interpreter.
> More information: <https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/cmd>.

- Start a new instance of the command interpreter:

`cmd`

- Run the specified command and then exit:

`cmd /c "{{command}}"`

- Run the specified command and then enter an interactive shell:

`cmd /k "{{command}}"`

- Disable the usage of `echo` in command output:

`cmd /q`

- Enable or disable command extensions:

`cmd /e:{{on|off}}`

- Enable or disable file or directory autocompletion:

`cmd /f:{{on|off}}`

- Enable or disable environment variable expansion:

`cmd /v:{{on|off}}`

- Force output to use unicode encoding:

`cmd /u`

```
@echo off

set LOCAL_JAVA="C:\Program Files\OpenJDK\jdk-8.0.242.08-hotspot\bin"

rem Switch to E: and the application directory
C:
cd C:\applications

%LOCAL_JAVA%\java -Dlogback.configurationFile=logback.xml -jar prog.jar -propertiesFile prop.properties
```