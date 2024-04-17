# Software-version-testing-script
$file=Start-Transcript;
$FileName=$file -replace('Transcript started, output file is ','');
$SearchSoftware = {Get-WmiObject Win32_Product | Where Name -ilike '*.NET*' |Format-Table Name,version,installdate};;
$hostnames = gc hostnames.txt; ;write-host "`n`n Checking the given software product on the hosts..." -foregroundcolor cyan;;
foreach($computer in $hostnames){write-host "`n #### $computer : #### `n" -foregroundcolor yellow;
invoke-command -computername $computer -scriptblock $SearchSoftware;
write-host "`n ---------------------------------------------------- `n" -foregroundcolor yellow;};Stop-Transcript;
write-host "`n Opening the Output file...`n" -foregroundcolor cyan;sleep 2;
invoke-item $FileName;

