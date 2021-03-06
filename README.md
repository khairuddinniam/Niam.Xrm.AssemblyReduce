# Niam.XRM.AssemblyReduce
Reduce the size of Dynamics CRM plugin assembly by removing unused methods and properties! Starting from plugin type (IPlugin) as entry point, system will scanning all the types and check for unsed to be removed in the result dll.

## How to Use From Command Prompt
1. Copy all the references dll in the same folder (input folder).
1. Open Command Prompt, change directory to the exe file (Niam.Xrm.AssemblyReduce.exe).
1. Run this code in the command prompt:
```
Niam.Xrm.AssemblyReduce.exe -i="input\LeadPlugin.dll" [-o="output\LeadPlugin.dll"] -snk="input\key.snk" 
[-k="namespacedll1.*, namespacedll2.subnamespace"]
```
Let the program run and check the result in the output folder.

| Param         | Description                   | Example Value       |
| ------------- |:-----------------------------:|-------------------|
| -i            | The dll input path     | "input\LeadPlugin.dll" |
| -o            | The dll result path (optional)     |   "output\LeadPlugin.dll"|
| -k | The namespace you want to keep (optional)     |    "Niam.Xrm.Framework.* , SimpleJson" |

For the -o param, if you not put this param. Then the original input dll will be replaced with the result dll.

For the -k param, these param will help you to keep this namespace. For example if you put Niam.Xrm.Framework.* this param will giving flag to the system to keep all the types inside the namespace of Niam.Xrm.Framework.

## How to Use From Nuget Package
Install from Package Manager Console (First time only) in Project that implement IPlugin:
```
Install-Package Niam.Xrm.AssemblyReduce
```
In old csproj file, add this command:
```
<Target Name="AfterBuild">
	<Exec Command="$(AssemblyReduce) -input=$(TargetPath) -snk=$(ProjectDir)key.snk" />
</Target>
```

For new (.net core) csproj:
```
<Target Name="PostBuild" AfterTargets="PostBuildEvent">
	<Exec Command="$(AssemblyReduce) -input=$(TargetPath) -snk=$(ProjectDir)key.snk" />
</Target>
```
