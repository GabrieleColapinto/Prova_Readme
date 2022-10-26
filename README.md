# Polibot
Polibot is a application for Windows (x64) developed to build an info point with voice interaction inside the Polytechnic University of Bari. The info point will be realized with an horizontal screen with an hologram pyramid on top of it. The users will interact with the hologram of a robot head projected inside the pyramid.

At the moment it is a prototype and it can provide a limited amount of informations.
The informations it can provide in its initial release are about the location of the classrooms and the way to connect to the Wi-Fi of the Polytechnic.

:it: The prototype is developed for a Windows version with the italian language installed and some of the files are in italian. :it:

## Repository content
The repository contains the following folders:
* Polibot_project
* Set up
* Installer

The "Installer" folder contains the file you need to use to be able to use the application as an end user. If that is the case go to the [installation section](#Installation).

The "Polibot_project" folder contains the Unity project of the application and the "Set up" folder contains the files you need to use before starting to work in Unity. If you want to develop the project go to the [development section](#Development).
# Installation
> Installer > Polibot_installer_x64.exe

If you want to install the application all you have to do is to go in the "Installer" folder and use "Polibot_installer_x64.exe".
The other folders and files are not important for your purpose. They were used to develop the installer program.
# Development
This application is a thesis project of a student of the Polytechinc University of Bari. You may find his thesis helpful in the development process because he described the steps he made to realize the prototype of this application. The dissertation is in italian but probabily it will not be a problem because the developers who will continue this project are italian. You can find the thesis [here](https://github.com/GabrieleColapinto/Tesi-di-laurea-triennale).

In order to develop the project you have to install Unity (currently version [2021.3.2f1](https://unity3d.com/unity/whats-new/2021.3.2)) and use the files in the "Set up" folder.

Go to the "Set up" folder and follow these steps:
1. Install Python and **_make sure to add the Python location to the path_**
2. Install VC_redist.x64.exe (reboot is not required)
3. Use both the files that change the system registry
4. Set up the virtual environment of Python

## Files that change the system registry
The two files that change the system registry are "Attivazione_riconoscimento_vocale.reg" and "voce_Cosimo.reg". The first file activates the voice recognition on your system. You could do the same going in the following path in the Windows settings:
> Start > Settings > Privacy > Speech

The second file allows third party applications to use the voice "Microsoft Cosimo" available in the italian version of Windows. If you don't have the italian language installed on your system you don't have this voice and you have to download it. First install the italian language in:
> Start > Settings > Time & language > Language

Then you have to download the voice used by the application by downloading the italian voice package from:
> Start > Settings > Time & language > Speech

## Setting up the Python virtual environment
The virtual environment folder has to be in the main forlder of the project i.e. the one which contains the "Assets" folder.

Go to the main forlder of the project, open a Powershell window as an administrator and type the following commands:

```
py -3.8 -m venv .\Polibot_venv
call .\Polibot_venv\Scripts\activate.bat
```
You may need to authorize the execution of the batch file.

After you created and activated the virtual environment using Python 3.8 you have to install the required packages of the project using the following commands:
```
python -m pip install --upgrade pip
python -m pip install -U pip setuptools wheel
pip install --no-cache-dir -r .\requirements.txt
```
Now you are ready to use the project in Unity and work on it.
# Releasing new versions of the application
After you build another version of the application you will have to update the installer "Polibot_installer_x64.exe" in order to distribute it. To do so you need to install [InstallForge](https://installforge.net/) and update the files inside the "Install" folder.

The "Install" folder contains the "App" and "Dependencies" folders, the installer program and the InstallForge configuration file "Installer_file_x64.ifp".

If you want to edit the configuration file you need to know the various tabs of InstallForge. You can get this knowledge from the [thesis](https://github.com/GabrieleColapinto/Tesi-di-laurea-triennale) or from other sources of your choice.

The "App" folder contains the files and folders derived from the Unity building process and the "Assets" frolder containing files external to Unity. At the moment those files are the vocalization server and [Rasa](https://rasa.com/). After you build a new version of the application you have to copy its files in the App folder. **_Make sure to delete the folder labeled as "Do Not Ship"._**

In the "Dependencies" folder you will find the files used by InstallForge to make the application work. Beside the installers of Python and Visual C++ and the requirements for the virtual environment of Python you will find a file to edit the system registry and two batch files.

The file "Configurazione.bat" creates and sets up the virtual environment of Python.

The .reg file activates the voice recognition. You can edit the system registry in InstallForge but, unfortunetly, you can only set string values for the variables so if you have to set a value of another type you will have to use a .reg file. Due to another flaw of InstallForge you can't use a .reg file directly from the "Commands" tab but you have to write a .bat file that uses a .reg file. This is the case of the "Modifica_registro.bat" file.