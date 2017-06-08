---
layout: post
title: 'Squirrel.Windows - Installer and Updater'
tags: ['C#', '.NET', 'Squirrel']
category: 'C#'
date: '2017-01-21 12:24'
author: 'GaryNg'
---
# Squirrel.Windows
GitHub: https://github.com/Squirrel/Squirrel.Windows

Documentation: https://github.com/Squirrel/Squirrel.Windows/blob/master/docs/readme.md

## Deploying from GitHub
Refer to [Using GitHub](https://github.com/Squirrel/Squirrel.Windows/blob/master/docs/using/github.md)

## NuGet
[NuGet Package Metadata](https://github.com/Squirrel/Squirrel.Windows/blob/master/docs/using/nuget-package-metadata.md)

Use [NuGetPackageExplorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) to package files for creating the installer, but **Cake** is the recommended way of doing this.

### Create .nuspec for MSBuild/Cake
Refer to [Example .nuspec file for MyApp](https://github.com/Squirrel/Squirrel.Windows/blob/master/docs/using/visual-studio-packaging.md#example-nuspec-file-for-myapp)

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
  <metadata>
    <id>MyApp</id>
    <!-- version will be replaced by MSBuild -->
    <version>0.0.0.0</version>
    <title>title</title>
    <authors>authors</authors>
    <description>description</description>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <copyright>Copyright 2016</copyright>
    <dependencies />
  </metadata>
  <files>
    <file src="*.*" target="lib\net45\" exclude="*.pdb;*.nupkg;*.vshost.*"/>
  </files>
</package>
```

Note: Install `NuGet.CommandLine` tool via NuGet to provide `nuget.exe` for `squirrel`
```
Install-Package NuGet.CommandLine
```
