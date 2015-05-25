# Welcome #
This project is a .NET web app that allows you to provision a new virtual machine from an existing VM or a template, within a VMware clustered environment. This app has limited testing against stand-alone ESXi servers, so it may or may not work completely. I hope to update it in the near future to handle this.

# Installation #
Installation is straightforward, each download is a packaged zip file that can be directly imported into IIS. You can also extract the contents into a folder and create the virtual directory from there. This app is a .NET 4.5 application and as such you will need to install that on your server if it's not already installed.

Styling is handled by BluePrint CSS so you will need to visit their website and download the archive. Then just unzip and copy the blueprint folder into the root of your virtual directory.

# How does it work? #
Once installed simply point any web browser to your virtual directory and provide your credentials. By default you will need to provide a server that is running the SDK service and a valid username and password. Once you click the connect button a connection will be established to your server and the next page will be populated with data.

The provisioning page contains information related to the new vm. All available vm's will be displayed in the Source VM dropdown list. You provide a name for your new vm in the Target VM field. Any customizations will be loaded into the OS Customizations dropdown.

All available clusters will be loaded into the Cluster dropdown list. Changing the cluster will update the Datastore, Port Group and Resource pool fields. These fields are also populated initially based on the first returned cluster object from VMware.

Finally the CPU and RAM allottments are completely arbitrary. I picked for CPU values, 1, 2 or 4 and RAM as 2, 4 or 8. I don't power up the VM so these can be easily changed after the clone is complete. Last but not least is the networking information, I store the ip for DNS in the web.config file so feel free to change that. You provide IP, Subnet and gateway the extent of my checking is to validate they are legitimate values.

At any time if there is an error or something is omitted that is required a message is displayed to the user. I struggled with this early on, but opted to use a panel on the page that is hidden and get's displayed as needed.

# Customizations #
If you checkout the repo you have access to the entire source code. From there you can modify the app quite heavily. In our production environment I have modified it to act more like a wizard. The source code is heavily documented for this, so feel free to check it out.

There is a form the admin fills out for documenting the project and purpose of the vm and who is responsible for it. I have also included a confirmation page at the end so the admin can validate manually if all the values are correct. As we manage a lot of Windows servers, I also provide the admin a method of pre-staging the computer object in Active Directory. All this information is then emailed to the admin after the cloning process has started.

# What's next? #
There are several items on my list for upcoming features
  * Standalone ESXi support
  * Handle missing OS Customizations
  * Consolidate specialized functions into generic ones