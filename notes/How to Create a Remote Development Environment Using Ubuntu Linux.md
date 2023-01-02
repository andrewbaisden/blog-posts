_If you enjoy this topic, you will probably like my articles, tweets, and stuff. If you're wondering, check out my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow since I'm offering programming and motivating tools and information to help you achieve your dreams._

There are many advantages to having your own local Linux development environment which you can connect to from your host operating system. So imagine a scenario where you have let's say a MacBook and macOS installed as your primary operating system. Now let's assume that you have Linux installed via a virtualisation tool like [UTM](https://mac.getutm.app/) or [Parallels](https://www.parallels.com/uk/) which I wrote a tutorial for by the way [How to Install Ubuntu Linux on Apple Silicon MacBooks](https://dev.to/andrewbaisden/how-to-install-ubuntu-linux-on-apple-silicon-macbooks-1nia).

You can use Secure Shell (SSH) to connect to your Ubuntu operating system from your Mac operating system which is pretty cool. This will give you the power to do almost anything from your console like creating folders, setting up projects, installing tools etc... It is equivalent to using your console in macOS so you have all of the commands at your disposal but now in your Ubuntu setup.

It is a very similar setup and comparable to connecting to an Amazon AWS Linux instance using an SSH client. But the advantage of this method is that the Linux instance is on your local computer so you don’t require an internet connection to use it.

It is good practice and it gives you an alternative to using a cloud service which might be paid. Another bonus is that there is even a way to connect to your home Ubuntu machine over the Internet! So you could potentially have your own custom server you would just need to leave it powered on before you leave the house and use it remotely of course!

## Connecting your main operating system to Ubuntu Linux

### Ubuntu Linux SSH setup

The first thing we will need to do is sign into our Ubuntu Linux operating system. Now we have to enable SSH to work within our environment. When Ubuntu Linux is first installed, remote access through SSH is disabled by default. Enabling SSH in Ubuntu Linux is a simple process. To install and enable SSH on your Ubuntu Linux system, complete the instructions below as root or a user with sudo privileges:

Go to applications and open the Terminal now update and install the package you see below.

```shell
sudo apt update
sudo apt install openssh-server
```

Ubuntu has a firewall setup tool known as UFW. If your system has a firewall, ensure the SSH port is open.

```shell
sudo ufw allow ssh
```

When the installation is finished, the SSH service will be launched automatically. You may check if SSH is running by using this code.

```shell
sudo systemctl status ssh
```

The result should be an output that indicates that the service is active and set to start on system boot like here.

```shell
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: e>
     Active: active (running) since Fri 2022-12-30 18:06:34 UTC; 1min 58s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 810 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 843 (sshd)
      Tasks: 1 (limit: 2236)
     Memory: 4.7M
        CPU: 34ms
     CGroup: /system.slice/ssh.service
             └─843 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
```

It's done, you can now use SSH to connect to your Ubuntu system from any workstation. Any SSH client tool should be sufficient I have listed a few below.

[Visual Studio Code Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
[iTerm2](https://iterm2.com/)
[hyper](https://hyper.is/)
Apple Terminal (pre installed on OS)
Linux Terminal (pre installed on OS)
[Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=en-gb&gl=gb)
[PuTTY](https://www.putty.org/)

### Using SSH to connect to Ubuntu Linux

Now it's time for the fun part! Let's connect to Ubuntu Linux from our main operating system. Any of the tools above should work however we are going to use the Visual Studio Code Remote - SSH extension because we will be able to open project folders inside of Visual Studio Code! And we can save the connection settings too meaning we don't have to type it out every single time.

Install the Visual Studio Code Remote - SSH extension if you have not already. Now there is just one extremely important step that we have to do first. We need to know the IP address of our Ubuntu computer so that we can connect to it over LAN (Local Area Network). The command will look much like this `ssh username@ip_address` so with your Ubuntu Linux username and the IP address. See this fake example below.

```shell
linuxuser@12.3.4.56
```

To get your IP address use the command below in Ubuntu Linux.

```shell
ip a
```

In the output look for something like this.

```shell
# Output
inet 192.123.34.5/67

# Remove the slash and number at the end and use this one
inet 192.123.34.5

# The example SSH connection string replace with your details
ssh linuxuser@192.123.34.5
```

Back in your main operating system you can do a quick test to see if the IP address is reachable. Ping the IP address using the code here but change it to the IP address for your case. You will know it's working if you see bytes returning and it does not say timeout or something along those lines.

```shell
ping 192.123.34.5
```

Ok enough testing lets connect to it now! The fastest way would be to just put the SSH connection code in your command line for example `ssh linuxuser@192.123.34.5`. Type yes and enter the password for your Ubuntu Linux install and its done you should be connected! Now you can use all of the usual BASH commands.

Lets try using the Visual Studio Code Remote - SSH extension now so you can access any folder in your code editor. Just get it up and running and enter the same connection string. Enter your password as before and you should be connected in Visual Studio Code. Now use the Visual Studio Code Terminal to access your Ubuntu Linux operating system.

_If you like this article, chances are that you would like my posts, tweets and content as well. If you are curious, have a look at my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow because I am sharing programming and motivation resources and knowledge to support you in achieving your goals 💫_
