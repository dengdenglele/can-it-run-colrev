# issue
The setup of CoLRev requires a system with linux kernel.
Students attending the project are usually running Windows or MacOS as their main operating system.
Compatibility is not given without further adjustments or installation of the existing operating system.
The creation of a completely new and foreign environment can also be frightening and lead to abondonment of the project.

# challenge
How can students participate regardless of the underlying operating system.
Varying knowledge and skill of CLI between students.
What is important from an usability standpoint for a seamless and painless usage.
Solutions needed to reduce the processing stress on hardware.
Promote to work and develop in an open source environment.

# solution
During three runs of the project, three different approaches were conducted.

In the first run, the students were given a full-blown copy of an Ubuntu 22.04 installation as a virtual machine image.
CoLRev and all neccessary tools were pre-installed.

In the second run, students using Windows were advised to install Windows Subsystem for Linux 2.
CoLRev and associated tools needed to be setup manually.


In the third run, students could begin to start their programming work entirely online with GitHub Codespaces.
During the first run, all dependencies are setup automatically without user interaction.

## VirtualBox with Ubuntu 22.04 LTS
The students were required to install VirtualBox, download and import the Ubuntu image with CoLRev, setup the SSH connection between the Ubuntu virtual machine and the GitHub server.
This approach is resource heavy.
Depending on the hardware used, graphical glitches in general usage can happen.
A lot of components are running in the background which are not essential for the programming task at hand.
For example the default GUI of Ubuntu (called the desktop environment "GNOME") is taxing on the underlying hardware.
It also takes up a lot of storage space due to a lot of exccess programs.
The usage of a complete desktop environment within a virtual machine is taxing on the hardware.
Students running mobile PCs complained about loud fans and hot temperatures of the CPU.
Advantages is the complete separation of host system and guest system.

## Running WSL2 with Ubuntu 22.04 LTS
The usage of WSL2 is running next to the underlying Windows operating system.
The installation is fairly simple as only one command needs to be executed within PowerShell as administrator.
Inside WSL2 students need to be run several commands, which can be copy and pasted from the CoLRev developer setup documentation.
A common pitfall was Docker Desktop for Windows not running in the background.
The performance is significantly better, because only essential components of Ubuntu 22.04 LTS are loaded.
WSL2 is deeply integrated into Windows and not strictly separated from the operating system. 
Any commands run inside can potentially harm Windows system files when run with privileged rights (sudo).
Initially WSL2 only provides a command line interface.
If needed, programs with a GUI such as gitk or Nautilus file explorer can be called directly from CLI.

## Going online with GitHub Codespaces and Ubuntu 22.04 LTS
Students from the University of Bamberg have access to GitHub Pro.
They can run virtual machines from within the browser.
This is a "specialized" server solution provided by GitHub.
The students have access to a VSC environment completely running in the browser.
Since VSC is a electron app (browser program by nature), glitches do not happen.
The browser only approach with VSC does not allow the usage of plugins (though they can be installed).
SSH is not needed, as anything happens within the browser.
If anything fails, students can terminate and delete an exising Codespaces instance.
Performance is only limited by the computers ability to render a webpage and the connection speed provided by the ISP.
All computational tasks are run directly on the servers provided by GitHub.
Different types of servers can be created depending on the processing powers needed.
The smallest CPU is already sufficient for a seamless workflow with CoLRev in the cloud.
Problems can occur, when machines are not turned off.
This needs to be done manually, otherwise the free contingent will be reached and warning via mail will be sent.
Students aiming to use a local IDE can use Visual Studio Code.
As GitHub and Visual Studio Code are both owned by Microsoft, a respecive plugin for VSC is available.
Using the GitHub Codespaces within a local installation requires the user to log in with their GitHub credentials. 
Any SSH setup is not needed and handled by the plugin.
The terminal shown in VSC while Codespaces plugin is running is the bash session running on GitHub servers.
Regular plugins (e.g. Git Graph) can be combined with Codespaces, when VSC is running on bare metal.



# future outlook
None of the presented solutions is perfect.
Compatibility is directly linked to performance.
Another approach would be dual booting Linux and Windows.
Running the linux kernel on bare metal provides the best performance.
Plans to provide students with a virtual machine hosted from the Rechenzentrum were abondaned as our request was not answered.
External cloud providers such as Linode or AWS can provide virtual private servers (VPS) for development.
Respective images with CoLRev can be created beforehand, but setting up the SSH connection is not trivial.
Registration and usage is free within a specific range, e.g. AWS offers a free tier for 1 year, but requires a complete registration with banking credentials.
Students unwilling to dual-boot their system can be provided with an external SSD with Ubuntu 24.04 LTS and CoLRev pre-installed.

