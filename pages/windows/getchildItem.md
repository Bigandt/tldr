# Get-ChildItem

- Get all files/folders in directory with given filter:

`Get-ChildItem -Filter "2020-01*"`

- Get all files/folders in directory with given filter and delete them:

`Get-ChildItem -Filter "2020-01*" | %{ Remove-Item -LiteralPath $_.FullName -Force -Recurse }`