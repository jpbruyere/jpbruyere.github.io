---
layout: post
title: Ship files with NuGet package
tags: [nuget,c#]
---

The problem when including custom files into a nuget package is that their are effectively copied into the user project only if you use visual studio.

Here is an example to ship a `.dll.config` file with a nuget package and have it copied into the destination build directory.

Nuget has a special folder called `build` where you may put only two files: a `ProjectName.props` or a `ProjectName.targets`.

Those files will be processed like any props or targets during the build of the destination project.

First include the file to be copied into the nuget package (ProjectName.csproj):

```xml
<ItemGroup>
	<None Include="ProjectName.dll.config" Pack="true" PackagePath="content" />    
</ItemGroup>
```

Then create a `ProjectName.targets` to process this file during build.
```danger
Note that the `.target` file's name MUST be the same that your project name!
```

```xml
<Project>
	<ItemGroup>
		<Content Include="$(MSBuildThisFileDirectory)\..\content\glfw-sharp.dll.config">
			<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
		</Content>
	</ItemGroup>
</Project>
```
Finaly include this `.target` into the `build\` directory of the package(project.csproj):

```xml
<ItemGroup>
	<None Include="glfw-sharp.targets" Pack="true" PackagePath="build"/>
</ItemGroup>

```
That's it, now when you include ProjectName nuget package in a project, `ProjectName.config` will be copied to the output directory.
