# Table of Contents
- [Introduction](#blender-extension-template)
- [Tips](#tips)
    - [Development extras](#development-extras)
    - [Using python packages](#using-python-packages)

# Blender Extension Template
This template is intended to help speed up blender extension development with python. The template is itself a working operator, that demonstrates how to:
- implement an extension
- interact with Blender UI
- divide code into separate modules and utilize them

__init__.py contains further information on the topics above.

# Tips
## Development extras
If you start out with add-on development make sure to enable 'Python Tooltips' and 'Development Extras' under:

*Edit -> Preferences -> Interface*.

With that functionality enabled you can right click on a menu item and review its code. This is helpful, if you want to integrate your operators with the existing blender UI. As it is done in *OBJECT_MT_ExampleMenu.py*. The name of the menu 'VIEW3D_MT_object_asset' was found by inspecting the source code of the corresponding menu script.

## Using python packages
It is possible (although, not very convenient) to use pip packages with the python installation that comes with blender. Pip is by default part of the bundled python installation. 

### Installing a package
In order to install a package locate your Blender installation. Under Windows this is 
```
C:\Program Files\Blender Foundation\Blender {blender_version}\
```
by default. 
Inside your Blender folder should be a folder called 'python' and inside that folder a another one called 'bin'. This is where the bundled python interpreter is located. Open a terminal, cd into that folder and than run a regular pip install command from that folder:
```
python -m pip install atudomain-git --user
```
Replace 'atudomain-git' with the name of the package you want to install. Pip should download the package and its dependencies and return with a message indicating success. Under Winwdows it should look like this:
![successfully installation](https://github.com/thorbenbaerentson/blender_extension_template/tree/main/images/install_package.png "Successfull installation")

### Locate the package on disk
In order to use the newly installed package we must tell python where to look for that package. To find out where the package was installed we can use the command pip show <package>.
```
python -m pip show atudomain-git
```
Again replace atudomain-git with the name of the package you want to install. This command returns some information about the package. Among these information is value called 'Location'. This is the path where pip installed the package to. 
![show package](https://github.com/thorbenbaerentson/blender_extension_template/tree/main/images/show_package.png "Show package")

### Importing the package
Using the loacation obtained using the 'show'-Command we can tell python where to look for the newly installed package. 
```python
# Add the path to sys.path, so the interpreter finds the package.
import sys
packages_path = "c:\\users\\{user}}\\appdata\\roaming\\python\\python311\\site-packages"
sys.path.insert(0, packages_path)
# Then import the modules
from atudomain.git import Git
```
Now we can use the package inside our code.