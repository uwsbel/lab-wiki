# Workflows

_This page used to be a general Workflows page but it only had info about VS code so I (Jay) am re-purposing it_

#### Visual Studio Code (vscode/code-oss) - Overview

Microsoft's Visual Studio Code (and its Open Source variants) is an extensible code editor built on the Electron framework. It provides sophisticated code editing along with features familiar to Visual Studio IDE users such as integrated support for interactive debugging and the powerful IntelliSense completion/linting engine.

###### Pros
- Can be used from virtually any desktop OS: Windows, Mac, and Linux are equally supported
- Extremely customizeable
- Git Integration
- Easily adaptable to local development
- Integrated debugger works with most toolchains
- Supports SSH tunneling and STDIO forwarding

###### Cons
- The UI can be a bit clunky at times
- Susceptible to lag when searching or saving files
- Documentation for useful extensions can be rather limited

##### Setting up remote access

###### 1. Install the **Remote - SSH** extension
 - Access the **Extensions Pane** (Ctrl+Shift+X)
 - Search for `Remote - SSH` and click the "Install" button

![The Extensions menu](/lab-wiki/images/technical/vscode_extensions.png)

###### 2. Add a new host (_optional_)
VS Code will attempt to load a list of hosts from the local user's SSH config, but if that is not successful the following steps may be used to add a new endpoint to the list:

 - Open the **Remote Explorer** pane, this can be done by clicking on the sidebar icon or using the command palette
 - Mouse over the **SSH TARGETS** heading and click on the + that appears to add a new SSH endpoint
 - Type the `ssh` command needed to connect to that server in the popup dialog

![Add an SSH endpoint](/lab-wiki/images/technical/vscode_add_endpoint.png)
 
###### 3. Connect to a remote machine

There are a couple of ways to connect to a remote machine using VS Code, only one of the options is detailed here.

 - Open the **Remote Explorer** pane, this can be done by clicking on the sidebar icon or using the command palette
 - Mouse over target machine from the list of **SSH TARGETS** and click on the icon that appears to the right of the pane to "Connect to Host in New Window"
 - A new window will appear which opens files and runs tasks on the remote server instead of the local machine
 - Wait for the remote session to finish configuring before proceeding

![Connect to the target system](/lab-wiki/images/technical/vscode_connect.png)

It is okay to close the local window at this time, the remote window does not need it to continue.

###### 4. Install any necessary extensions on the remote machine (_as needed_)
 - Access the **Extensions Menu** in the connected window
 - Search for the extension. 
 - Clicking the "Install" button on a given extension will download and install the extension on the remote system... so long as it is compatible with that system. Certain packages may not be supported, or they may be supported only in local instances of VS Code

> **NOTE**: For full C/C++ highlighting, autocompletion, and debugging support, the `C/C++` extension from Microsoft is required.

###### 5. Moving forward
Visual Studio Code operates on remote systems much like it does locally. The following features may be additionally useful to remote users:

 - Press `Ctrl + Tilde` to open a terminal on the remote system using that system's default shell. If a specific remote folder is opened in the **Explorer** pane, the terminal will automatically `cd` to that directory.
 - The `Remote - SSH` plugin has experimental support for remote windows machines as well. Visit the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) for more information.
 
#### Useful Extensions

These are the extensions that Jay uses in his Synchrono development. There is a snippet at the bottom which will install them all for you if you have blind trust in me.

These all seem to work together to provide C++ Intellisense, etc... CMake Tools took some fiddling to get set-up properly, I will hopefully add a section detailing how I did that.
- C/C++
- C++ Intellisense
- CMake Tools

Misc
- Settings Sync - Brings across all my settings no matter which workstation (Windows/Linux/etc...) I'm on
- Surround - Shortcuts to surround code with () "" {} or whatever else you want
- vscode-cudacpp - Syntax highlighting for CUDA code
- Remote - SSH - See Colin's wonderful explanations above
- Remote - SSH: Editing Config Files - Not quite sure what this adds beyond the normal Remote - SSH extension

Install Jay's extensions (to be pasted into a Linux prompt):

    code --install-extension kriegalex.vscode-cudacpp
    code --install-extension ms-vscode-remote.remote-ssh
    code --install-extension ms-vscode-remote.remote-ssh-edit
    code --install-extension ms-vscode.cmake-tools
    code --install-extension ms-vscode.cpptools
    code --install-extension Shan.code-settings-sync
    code --install-extension yatki.vscode-surround
