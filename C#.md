## Create Project

To create a project, you can use the following commands in the terminal:

### List Templates

To list all available templates:

```bash
dotnet new list
```

### Create a Console Application

To create a new console application with .NET 6.0:
```bash
dotnet new console -n microsoft.botsay -f net6.0
```

### Create a Windows Forms Application

To create a new Windows Forms application with .NET 6.0:
```bash
dotnet new winforms -n HelloWorld -f net6.0
```

## Create Solution

```bash
dotnet new sln -n YourSolutionName
```
```bash
dotnet new classlib -n YourLibraryName
```

```bash
dotnet new console -n YourConsoleAppName
```
```bash
dotnet sln YourSolutionName.sln add YourLibraryName/YourLibraryName.csproj
dotnet sln YourSolutionName.sln add YourConsoleAppName/YourConsoleAppName.csproj
```

```bash
cd YourConsoleAppName
dotnet add reference ../YourLibraryName/YourLibraryName.csproj
```
```bash
dotnet build
```
```bash
dotnet run --project YourConsoleAppName
```

```bash
dotnet add package Newtonsoft.Json
dotnet add package Beckhoff.TwinCAT.Ads
```

## dependency tree walker
Download it from the readme "Download here".  After which you can run "Dependencies.Gui"
```bash
https://github.com/lucasg/Dependencies?tab=readme-ov-file
```
