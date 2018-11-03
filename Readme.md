# Getting Started in CloudSlang RHEL 7.5 Linux on VirtualBox
# Setting up Prerequisite Tools

1. Head over to the Red Hat Linux [download section](https://developers.redhat.com/products/rhel/download/) and click the View Older Downloads link. In the download links, select the DVD iso files. This normally should start your download. 
2. Download Virtual Box from the [download section](https://www.virtualbox.org/wiki/Downloads) and install it on your machine.

# Virtualization Host Requirements

1. Virtualization hosts must have at least one CPU.
2. It is recommended that virtualization hosts have at least 2 GB of RAM. 
3. It is recommended that each virtualization host has at least 10 GB of internal storage.


# Mount RHEL on VirtualBox

1. Start VirtualBox and click `New`
2. Name your machine, preferably with a descriptive but memorable name (e.g., `redhat-box`), select type `Linux`, and version `Red Hat (64 bit)` (unless you downloaded the 32 bit version. A note on this, some machines you may need to go inside your UEFI/BIOS firmware, and [enable Intel VT-x](http://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/) to be able to run the 64 bit version, highly recommended!)
3. Next set your RAM. I decide to set mine to 2048MB, but RHEL 7.5 Linux requires *much* less than that.
4. Create a virtual hard disk now and select `VDI` and `Dynamically allocated` on the next screens.
5. Select a reasonable disk size (e.g., 40GB). Note that all of those settings are not that important at the moment as they can be changed in the future
6. Once this wizard completes, finally go to `Storage > Storage Tree > Controller: IDE > Optical Drive + icon > Choose Disk` and navigate to where the ISO file you downloaded previously is stored (I personally moved the ISO under `C:\Users\USERNAME\VirtualBox VMs\rhel-server-7.5-x86_64-dvd.iso`. 
7. Click ok and you are now ready to Start the VM
8. Once started, select `Boot Red Hat Linux (x86_64)`

# Install Red Hat on VirtualBox

We now want to install Red hat Linux as guest to our Virtual Box, following the steps listed below: 

1. Once you boot the VM, this brings us to the boot screen and you can select the first option to start the installation:
![Start Install RHEL 7](images/installation_1.png)

2. Select your language of choice at the opening menu:
![Select Language](images/installation_2.png) 

3. This brings you to the options page. You will see that the Begin Installation button is not lit because we need to set up a few things first. Start by choosing the install type you want. For simplicity, I’ve selected Minimal Install.

4. Open up the System section to choose the hard disk:
![Install Disk](images/installation_3.png)

5. Now you will see the Begin Installation button is lit up and ready to go! Go for it ?
![Install Begin](images/installation_4.png)

6. With the install underway, we can configure the root password and also set up a non-root user for you to use.
![Install Begin](images/installation_5.png)

7. Root password needs to be reasonably complex:
![Install Begin](images/installation_6.png)

8. Next up you can configure the non-root user for daily administration. Obviously, you will fill in your information rather than mine in here…unless you want me to have access that is:
![Install Begin](images/installation_7.png)

9. As quickly as it started, it’s all done! (results may vary depending on internet and hard drive speeds):
![Install Begin](images/installation_8.png)

10. Once you reboot the server after the installation completes, you’ll find yourself at the initial login prompt enter the password and you are done!
![Install Begin](images/installation_9.png)

# Getting Started in CloudSlang
### Installing JAVA
CloudSlang requires JDK 8+ to run. Install the latest Java 8 i.e. Java 1.8.0_XXX-XXX where ‘1.8.0’ states it is Java 8. To begin, make sure that all the packages currently installed on your RHEL system are updated to their latest versions:

```sh
$ sudo yum update -y
$ sudo yum install java-1.8.0-openjdk
```
You can verify that you have the appropriate version by running the following command:

```sh
$ java -version
```
You should see "1.8.somethingorother" Because reasons.

### Installing CloudSlang-Cli
The CloudSlang CLI is a command line interface tool that can be used to run flows. In this section, we will download the CloudSlang CLI tool and the available content (predefined operations and flows). 

- First, [Download](https://github.com/CloudSlang/cloud-slang/releases/latest) the CLI with content zip file.
    ```sh
    $ wget https://github.com/CloudSlang/cloud-slang/releases/download/cloudslang-1.0.23/cslang-cli-with-content.zip
    ```
    
- Unzip the archive.
     ```sh
    $ unzip cslang-cli-with-content.zip
    ```
- This will create a cslang directory. If you list the contents of that directory,
     ```sh
    ls ~/cslang
    ```
    
You will notice three directories in it:

- `python-lib`, which is used for external Python libraries.
- `cslang`, which contains the CloudSlang CLI files. The `cslang/bin` folder contains a file named cslang which is used to start up the CLI. The `cslang/lib` contains the necessary dependencies for the application.
- `content`, which contains the ready-made CloudSlang content.

### Creating, Compiling and Running

In order to run the example flow attached, on the CloudSlang server, first change to the `/cslang/bin` directory.
```sh
cd ~/cslang/cslang/bin/
```
Run the executable called `cslang` in order to start up the CLI.
```sh
./cslang
```
After a moment, you'll see the CloudSlang welcome screen.
```sh
1.0.23
Welcome to CloudSlang. For assistance type help.
cslang>
```
Extract the `examples.zip` to the content directory and enter the following command in the CLI. 

```sh
run --f ../content/examples/flows/hello_world.sl
```

The run command triggers the flow. --f specifies the path to the flow. While the flow is running, the CLI displays the task names that are executed. Once the flow finishes, the CLI outputs some useful information like the flow outputs and the flow result.

In our case, the flow result will either be SUCCESS (which means it prints the text Hello, World) or FAILURE (which means a problem occurred).
