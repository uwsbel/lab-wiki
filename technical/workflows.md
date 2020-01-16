# Workflows

## Remote Access

These workflows are great for working on a computer which is not physically available to the user. In some cases, they also enable one to work on a computer which is already in use by someone else.

#### Visual Studio Code

Microsoft's Visual Studio Code (and its Open Source variants) is an extensible code editor built on the Electron framework. It provides sophisticated code editing along with features familiar to Visual Studio IDE users such as integrated support for interactive debugging and the powerful IntelliSense completion/linting engine.

###### Pros
- Can be used from virtually any desktop OS: Windows, Mac, and Linux are equally supported
- Extremely customizeable
- Git Integration
- Easily adaptable to local development

###### Cons
- The UI can be a bit clunky at times
- Susceptible to lag
- Documentation for useful extensions can be rather limited

##### Setting up remote access

###### 1. Install the **Remote - SSH** extension
 - Access the extensions menu (Ctrl+Shift+X)
 - Search for `Remote - SSH` and click the "Install" button

![The Extensions menu](/lab-wiki/images/technical/vscode_extensions.png)

###### 2. Add a new host (_optional_)
 - Open the **Remote Explorer** pane, this can be done by clicking on the sidebar icon or using the command palette
 - Mouse over the **SSH TARGETS** heading and click on the + that appears to add a new SSH endpoint
 - Type the `ssh` command you would use to access that server in the popup dialog

![Add an SSH endpoint](/lab-wiki/images/technical/vscode_add_endpoint.png)
 
###### 3. Connect to a remote machine
 - Open the **Remote Explorer** pane, this can be done by clicking on the sidebar icon or using the command palette
 - Mouse over target machine from the list of **SSH TARGETS** and click on the icon that appears to the right of the pane to "Connect to Host in New Window"