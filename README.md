zCompile is a simple build tool for windows that allows you to compile multi language projects into executables
<br>If you plan to distribute your project in any way please read the section under "Licensing"
# Setting up your project
Create a folder for your project and in that folder make
<br>The file "app.xml"
<br>The folder "src"
## app.xml
This will be formatted like an xml file
<br>You must format it like this
```xml
<app> <!-- Use the app tag to define your app -->
	<app id="nameofexe">app.py</app> <!-- The app tag will define an exe, this one is called nameofexe.exe (or the os equivelant) and will run app.py -->
	<app id="nameofexe2">path/to/app.js</app> <!-- You may have multiple exes, they can be in subdirectories and can be in any supported language -->
	<lib id="nameoflib">lib.py<app> <!-- The lib tag will define a library which can be called by other languages using their built in library system -->
</app>
```
If you end a script path with a / you can have multifile scripts
<br>These can be maven projects, or java projects using a manifest.txt
<br>For every script the id tag is required as an identifier however you can also have other tags
### Tags
#### Runtime
You can set runtime to runtimename@runtimeversion or runtimename if versionless to set a custom runtime (runtimename must be lowercase)
<br>For most scripts you dont need this as it automatically picks the most common one for you but it is required in multifile scripts
#### Ui
You can set ui to console to show a console or to none to show none which is useful for background tasks or guis (app tag only)
#### Lib
Space seperated values of libraries to install using a package manager
<br>Pip for winpython, Npm for node, Cargo for rustc
<br>If using cargo you can add optional symbols and declare it like libraryname@libraryversion$feature1$feature2
## src
This folder will contain all your source code and all file references in app.xml will reference the root of this folder
## doc
Optionally you can have a folder called doc in your project root and all files here will be copied into the root of dst
# Using libs
If you set a script as a lib you will be able to call it from other scripts
<br>You will be able to communicate via the basic std operations. stdarg, stdin, stdout, stdexit
<br>Below are examples for each language that supports calling others
## Node
```javascript
const libname = require("libname");

const proc = libname(["argv1", "argv2"]) // returns ChildProcess object
```
## Python, Winpython
```python
import libname

proc = libname(["argv1", "argv2"]) # returns subprocess.Popen object
```
# Installing modules
In module.html you will find a list of modules you can install
<br>To install a module click install on one of the modules and extract the downloaded file
<br>Find which folder is required, either the same folder as the one extracted or if theres only one folder inside and nothing else, choose that folder
<br>The module you clicked will be labeled as modulename moduleversion with modulename capitalized but from now on its important you make it lowercase only
<br>Rename that folder to the version of the module and in the same folder as zComp.exe go to module/(modulename)/ and put the folder in there with the version as the name
<br>You may need to make these folders manually
<br>You must install mingw-gcc for Windows or xpack-gcc for Linux in order to even use the build tool
# Compiling your project
Navigate to the project directory (the same directory as app.xml) and open your terminal
<br>Call zComp.exe by either entering & "C:\full\path\to\zComp.exe" on Windows or by adding the folder zComp.exe is in to PATH and simply typing zcomp or calling the executable in whatever way works for you and your operating system with the working directory being the project folder
<br>If nothing errors, there will be a folder called dst with your compiled exes
# Errors
You may see that if you are using Julia on Windows and you try to recompile the project you may see
```
PermissionError: [WinError 5] Access is denied: 'dst\\internal\\julia\\1.12.6\\share\\julia\\base\\docs\\basedocs.jl'
```
Just delete the dst folder manually
# Licensing
zCompile bundles lots of required runtimes into your project many of which require following specific licences
<br>zCompile has no gaurantees over whether the modules can be distributed freely or which will be used and what licences must be followed
<br>The responsibility is entirely on you to make sure you comply with the licences
<br>If you know all the licenses that must be followed and you can follow them, zCompile dosent add any extra licenses that must be followed as long as you dont distribute zCompile itself
<br>The source code of zCompile is licenced under the GNU General Public Licence v3 and can be seen at /LICENCE or /doc/licence.txt and you can also see the copyright notice at /doc/copyright.txt
