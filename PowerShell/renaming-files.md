---
layout: post
title: 'Renaming files'
tags: ['PowerShell']
categories: ['PowerShell']
date: '2017-02-02 20:08'
author: 'GaryNg'
---

# Renaming Files
```powershell
Get-ChildItem -Filter *.mp3 | Rename-Item -NewName { $_.Name -replace '\.mp3','.tmp' }
```
> `\` is for escaping the dot (otherwise it is considered as regex)

## Getting Filename without Extensions
Use `$_.BaseName`  
```powershell
dir *.xml | Rename-Item -NewName {$_.BaseName + ".tmp"}
```

or use `[System.IO.Path]::GetFileNameWithoutExtension()`
```powershell
Rename-Item -NewName {[System.IO.Path]::GetFileNameWithoutExtension($_.fullname) + ".tmp"
```

# Reference
SO: [How can I bulk rename files in PowerShell?](http://stackoverflow.com/questions/13382638/how-can-i-bulk-rename-files-in-powershell)

# Off-topic
I was downloading [this playlist from soundcloud](https://soundcloud.com/pianoman_weddings/sets/piano-instrumental-all) using [youtube-dl](https://rg3.github.io/youtube-dl/), all the files downloaded are named like:
```
A STEP YOU CAN'T TAKE BACK (MOVIE BEGIN AGAIN) KEIRA KNIGHTLEY-182809059.mp3
ADELE - ALL I ASK (piano instrumental cover)-246176513.mp3
ADELE - HELLO (piano instrumental cover)-229785698.mp3
ADELE - REMEDY (piano instrumental cover)-235144565.mp3
ADELE - SOMEONE LIKE YOU (piano instrumental cover)-54692939.mp3
ADELE - WHEN WE WERE YOUNG (piano instrumental cover)-234015646.mp3
AL GREEN - LET'S STICK TOGETHER (piano instrumental cover)-144633620.mp3
ANDREA BOCELLI - TIME TO SAY GOODBYE (piano instrumental cover)-232869491.mp3
ANGUS AND JULIA STONE - BIG JET PLANE-61542958.mp3
BEATLES - HERE COMES THE SUN-53333775.mp3
BEAUTY AND THE BEAST (piano instrumental)-153192892.mp3
BEN FOLDS - THE LUCKIEST-53334850.mp3
...
```

wrote a simple script to rename all the files to  
(remove `(piano instrumental cover)` and the trailing random number, then convert to Title Case)
```
1927 - If I Could.mp3
A Step You Can't Take Back Keira Knightley.mp3
Adele - All I Ask.mp3
Adele - Hello.mp3
Adele - Remedy.mp3
Adele - Someone Like You.mp3
Adele - When We Were Young.mp3
Al Green - Let's Stick Together.mp3
Andrea Bocelli - Time To Say Goodbye.mp3
Angus And Julia Stone - Big Jet Plane.mp3
Beatles - Here Comes The Sun.mp3
Beauty And The Beast.mp3
Ben Folds - The Luckiest.mp3
Ben Folds Five - Sky High.mp3
Beyonce - If I Were A Boy.mp3
Billy Joel - She's Always A Woman.mp3
...
```

```powershell
Get-ChildItem -Filter *.mp3 | Rename-Item -NewName {
$name = $_.Name -replace '(\s\(.*\)|-\d+)+',''
return (Get-Culture).TextInfo.ToTitleCase([System.IO.Path]::GetFileNameWithoutExtension($name).ToLower()) + ".mp3"
}
```

[mp3tag](http://www.mp3tag.de/en/) is then used to bulk add Artist (Benny Martin Piano), Album (Benny Martin Piano) and Cover photo (https://i1.sndcdn.com/avatars-000040739168-0afczo-t500x500.jpg)
