+++
title = "Setting up Jupyter_Lab with OpendTect"
tags = ["python","jupyter","code","opendtect"]
categories = ["howto"]
date = "2022-06-05"
banner = "/blog/jupyterlab-python-setup/image-01.png"
+++
## Fixing the kernel.json file for OpendTect Python
The Jupyter architecture uses "kernel.json" files to identify a Jupyter kernel. If you have installed OpendTect and installed
and selected one of the OpendTect ML Python environments in the Python Settings dialog, you can use the following command sequences on Linux
and Windows to show a list of available Jupyter kernels. Open a console window (press Ctrl-T with the cursor in the OpendTect window) and enter
 the following depending on your system:

For Linux:
```bash
[wayne@amdlinux ~]$ which python
/opt/seismic/OpendTect_6/Python/envs/odmlpython-cuda10/bin/python
[wayne@amdlinux ~]$ jupyter kernelspec list
Available kernels:
  python3    /opt/seismic/OpendTect_6/Python/envs/odmlpython-cuda10/share/jupyter/kernels/python3
```
For Windows:
```posh
(odmlpython-cpu-mkl) C:\Users\wayne>where python
C:\Program Files\OpendTect\Python\envs\odmlpython-cpu-mkl\python.exe
C:\Users\wayne\AppData\Local\Microsoft\WindowsApps\python.exe

(odmlpython-cpu-mkl) C:\Users\wayne>jupyter kernelspec list
Available kernels:
  python3    C:\Program Files\OpendTect\Python\envs\odmlpython-cpu-mkl\share\jupyter\kernels\python3
```
The "where/which" command shows the location of the Python interpreter used by the OpendTect Python environment. The
"jupyter kernelspec list" command shows a folder location that will contain a "kernel.json" file that looks like this:
```json
{
 "argv": [
  "C:/odmlpython/Win64/Python/envs/odmlpython-cpu-mkl\\python.exe",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "Python 3",
 "language": "python"
}
```
The first element in the "argv" JSON array is supposed to be the location of the Python interpreter to be used as the Jupyter kernel.
Unfortunately the Python installed by the OpendTect Installation Manager has a broken "kernel.json" file because it contains
the path to the Python interpreter on the machine where the environment was built and not the location on your system. There are 2 ways
to fix this:
- Edit the installed "kernel.json" file in the OpendTect software installation as per the location reported by the "jupyter kernel list"
command (eg C:\Program Files\OpendTect\Python\envs\odmlpython-cpu-mkl\share\jupyter\kernels\python3\kernel.json), this will probably
require administrator privileges and might not be an option for some users.
- Add an appropriate "kernel.json" file in a user editable location, on Windows under "%APPDATA%\jupyter\kernels" or on Linux/Unix
under "~/.local/share/jupyter/kernels". Keep the name simple (only use ASCII letters, ASCII numbers, simple separators: - hyphen, . period, _ underscore, and
avoid spaces). An easy way is to copy the file from the OpendTect installation and edit the user local copy and replace the Python
location in the "argv" array with what the "where/which" command reports. On Windows this would look like this:
```posh
(odmlpython-cpu-mkl) C:\Users\wayne>xcopy  "C:\Program Files\OpendTect\Python\envs\odmlpython-cpu-mkl\share\jupyter\kernels\python3\kernel.json" %APPDATA%\jupyter\kernels\od_python\kernel.json
Does C:\Users\wayne\AppData\Roaming\jupyter\kernels\od_python\kernel.json specify a file name
or directory name on the target
(F = file, D = directory)? F
C:\Program Files\OpendTect\Python\envs\odmlpython-cpu-mkl\share\jupyter\kernels\python3\kernel.json
1 File(s) copied
```
The edited "kernel.json" file will look like:
```json
{
 "argv": [
  "C:/Program Files/OpendTect/Python/envs/odmlpython-cpu-mkl/python.exe",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "OD Python 3",
 "language": "python"
}
```
Note, as shown here, it might be handy to customise the "display_name" field because this will be displayed in the list of Python environments that
VS Code shows in it's user interface. Also note the use of forward slashes as opposed to backslashes in the file path because
backslashes have special meaning in JSON. Python will handle the path correctly on Windows but if you must use backslashes you will need
to replace each single backslash with a double backslash (eg "C:\\\Program Files\\\OpendTect\\\Python\\\envs\\\odmlpython-cpu-mkl\\\python.exe").
After creating the file you can verify it is recognised by repeating the "jupyter kernelspec list" command:
```posh
(odmlpython-cpu-mkl) C:\Users\wayne>jupyter kernelspec list
Available kernels:
  od_python   C:\Users\wayne\AppData\Roaming\jupyter\kernels\od_python
  python3     C:\Program Files\OpendTect\Python\envs\odmlpython-cpu-mkl\share\jupyter\kernels\python3
```
