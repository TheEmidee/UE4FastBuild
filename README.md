# UE4FastBuild

This is a fixed version of the *FASTBuild.cs* file you can find [here](https://github.com/ClxS/FASTBuild-UE4) and [here](https://github.com/liamkf/Unreal_FASTBuild/), for UE 4.20 and the windows SDK 10.

Please note also that only VS2017 is supported.

You will have to update a few other files from the UnrealBuildTool project, as stated [here](https://github.com/ClxS/FASTBuild-UE4).

You will have to update the contents of the function *AppendCLArguments_Global* of the file *VCToolChain.cs* to be able to build with VS2017:

````C++
if(WindowsPlatform.bUseVCCompilerArgs && CompileEnvironment.bEnableUndefinedIdentifierWarnings)
{
    if (CompileEnvironment.bUndefinedIdentifierWarningsAsErrors)
    {
        if (Target.WindowsPlatform.Compiler == WindowsCompiler.VisualStudio2015 )
        {
            Arguments.Add("/we4668"); 
        }
        else if (Target.WindowsPlatform.Compiler == WindowsCompiler.VisualStudio2017)
        {
            Arguments.Add("/wd4668");
        }
    }
    else
    {
        Arguments.Add("/w44668");
    }
}
````

## Do I have to compile the full source of UE4 to use FASTBuild?

Luckily no :)

All you need to do is:
* open the project file *UnrealBuildTool.csproj* in *UE_INSTALL_FOLDER}\Engine\Source\Programs\UnrealBuildTool\*
* Add the *FASTBuild.cs* file
* Update the other files accordingly
* Build in Release: the project is pre-configured to output the binary in the correct folder
* Enjoy :)