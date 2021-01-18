# JDB
> 
> 
> https://ethangmt.github.io/2017/08/19/java-debugging.html
> https://www.tutorialspoint.com/jdb/jdb_quick_guide.htm

- Debug program with source code available:

`jdb -sourcepath C:\Users\jeab\eclipse-workspace\test\test\src\test\java test.TestMain`

- Gradle compile with -g option (debug):

`
compileJava {
    options.warnings = true
    options.compilerArgs += ["-g"]
}
`