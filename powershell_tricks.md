# Powershell

## Base64 + Gzip Encode / Decode

```powershell
function Base64_Gzip_Encode() {
    param (
        $StringToEncode
    )
    
    $ms = New-Object System.IO.MemoryStream
    $cs = New-Object System.IO.Compression.GZipStream($ms, [System.IO.Compression.CompressionMode]::Compress)
    $sw = New-Object System.IO.StreamWriter($cs)
    $sw.Write($StringToEncode)
    $sw.Close();
    $StringToEncode = [System.Convert]::ToBase64String($ms.ToArray())
    return $StringToEncode
}
    
    
function Base64_Gzip_Decode() {
    param ($StringToDecode
    )
    
    $data = [System.Convert]::FromBase64String($StringToDecode)
    $ms = New-Object System.IO.MemoryStream
    $ms.Write($data, 0, $data.Length)
    $ms.Seek(0, 0) | Out-Null
    $sr = New-Object System.IO.StreamReader(New-Object System.IO.Compression.GZipStream($ms, [System.IO.Compression.CompressionMode]::Decompress))
    $string = $sr.ReadToEnd()
    return $string
}
    
$res = Base64_Gzip_Encode "Hello World"
$decoded = Base64_Gzip_Decode "$res"
    
    
Write-Host "Result: $res"
Write-Host "Decoded Result: $decoded"
```
