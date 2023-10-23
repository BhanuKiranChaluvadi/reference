# Building a .NET Project from Command Line on Windows

This guide provides steps to build a .NET project from the command line using the .NET CLI (Command Line Interface) on Windows.

## Prerequisites

- .NET SDK installed on your machine.
- A .NET project with a `.csproj` file.

## Steps

1. **Open Command Prompt or Windows Terminal**:
   - Press `Win` + `R`, type `cmd` or `wt` (for Windows Terminal), and press `Enter`.

2. **Navigate to the Project Directory**:
   - Use the `cd` command to navigate to the directory containing your `.csproj` file.
     ```plaintext
     cd path\to\your\project
     ```

3. **Build the Project**:
   - Use the `dotnet build` command to build your project.
     ```plaintext
     dotnet build
     ```

4. **(Optional) Specify Configuration and Output Directory**:
   - You can specify a configuration (e.g., Debug or Release) and an output directory for the build.
     ```plaintext
     dotnet build -c Release -o out
     ```
     - `-c Release`: Specifies that the project should be built with the Release configuration.
     - `-o out`: Specifies that the build output should be placed in a directory named `out`.

5. **(Optional) Build for a Specific Runtime**:
   - If you need to build your project for a specific runtime, you can use the `--runtime` option.
     ```plaintext
     dotnet build --runtime win-x64
     ```

6. **(Optional) Build a Specific Project**:
   - If you have multiple projects in a solution and want to build a specific one, specify the path to the `.csproj` or `.sln` file.
     ```plaintext
     dotnet build path\to\your\project.csproj
     ```

7. **Check the Build Output**:
   - After the build completes, you'll find the build output in the specified directory or, if you didn't specify an output directory, in the `bin` directory under your project directory.

8. **(Optional) Publish the Project**:
   - If you want to create a package for deployment, use the `dotnet publish` command.
     ```plaintext
     dotnet publish -c Release -o publish
     ```

## Additional Resources

- [Official .NET CLI documentation](https://docs.microsoft.com/en-us/dotnet/core/tools/)

