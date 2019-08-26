# Find all Excel files by Filename - Open -> Save -> Close

`
\\HOST-NAME\FOLDER\*\2019\
`
>
```*``` = any foldername

```
$Files = Dir '\\HOST-NAME\FOLDER\*\2019\' -Recurse | ? {$_.Name -eq "FILE-NAME.xlsx"} | Select -ExpandProperty FullName
$excl=New-Object -ComObject "Excel.Application"
foreach ($file in $Files)
{
$wrkb=$excl.Workbooks.Open($file)
$excl.DisplayAlerts = $FALSE
$wrkb.Save()
$wrkb.Close()
}
$excl.Quit()
```
