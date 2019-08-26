# Continuous image upload to FTP with temporary file creation and replacement

```
while($true)
{
    $i++
$source = "http://URL/image.jpg"
$destination = "ftp://username:password@web-page.com/location/temp"

$webclient = New-Object System.Net.WebClient

$webclient.DownloadFile($source, "this.jpg")
$webclient.UploadFile($destination, "this.jpg")

$ftp = [System.Net.FtpWebRequest]::Create("ftp://username:password@web-page.com/location/temp")
$ftp.KeepAlive = $true
$ftp.UsePassive = $false
$ftp.Method = "Rename"
$ftp.RenameTo = "/location/image.jpg"
$ftp.UseBinary = $true
$response = [System.Net.FtpWebResponse] $ftp.GetResponse()
}
```
