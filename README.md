## Sample NuGet Package including any files which consequently are copied to consuming project's output directory with preserved folder structure

### How to build the sample package
Run `dotnet pack --no-build`  or `nuget pack My.Package.nuspec`

As this sample does not contain any C# code that should be built, nor do we want to build anything, we need to specify `--no-build` to prevent `dotnet pack` from trying to build anything. The build **would** fail anyway, as we have `<DisableImplicitFrameworkReferences>` set to true in the .csproj file. We also have specified that any potential build output should **not** be included in the NuGet package, through the use of `<IncludeBuildOutput>false</IncludeBuildOutput>`. These could be removed to allow code to be built and output included in the package, if that is what you wish to achieve. 

The `My.Package.nuspec` file defines the properties for the NuGet package itself. Here we also manually specify what "extra" files we want included in the package. In this example, we say that all files and folders found in the `content/` folder should be included in the NuGet package, with preserved folder structure.

The `build/My.Package.targets` file includes the magic that makes the included files copy to the output directory of the consuming project with preserved folder structure. This file must have the same name as the package id and be found under the `build/` subdirectory (unless manually specified in the .csproj).

The produced NuGet package can be found in the `bin/Release/` folder. Point your Visual Studio to this directory as a local source to test install your package locally in any project.