# hmg01
Warning!!!Windows Terminal with Git Bash
This repository contains files for setting up the Windows Terminal together with the Git Bash.

Additionally, some Bash and Git dotfiles are supplied (.bash_profile, .bashrc, .bash_prompt, …) based on Okeanos/dotfiles (originally forked from mathiasbynens/dotfiles).

KeePassXC as SSH Agent
The Windows Environment Variable settings and enabled OpenSSH client make using KeePassXC as an SSH agent to manage SSH keys on Windows within the Git Bash possible.

Environment:
Set the following User Environment Variables

HOME : %UserProfile% (this will prevent Git Bash supplied tools from arbitrarily deciding on their own where ~/ is)
GIT_SSH : %SystemRoot%\System32\OpenSSH\ssh.exe
And enable the OpenSSH Agent via the Services management interface by setting the OpenSSH Authentication Agent to automatic and starting it.

Installation
Follow the installation instructions for:

Windows Terminal
Git Bash
KeePassXC
For KeePassXC the SSH support has to be enabled in the KeePassXC settings along with the option to use OpenSSH instead of Pageant. In addition to that individual SSH keys within the KeePass vault have to be enabled and/or loaded manually into the SSH agent.

Git Bash specifics
With Git Bash the bundled OpenSSH binaries will be used by default and not talk to the now enabled Windows OpenSSH agent. So, once the Windows OpenSSH agent is enabled, you can safely delete the Git bundled OpenSSH binaries as described here to make it use the Windows ones instead.

Do not delete %ProgramFiles%\Git\usr\bin\ssh-copy-id, though, as there is no Windows supplied alternative.

%ProgramFiles%\Git\usr\bin\ssh-add.exe
%ProgramFiles%\Git\usr\bin\ssh-agent.exe
%ProgramFiles%\Git\usr\bin\ssh-keygen.exe
%ProgramFiles%\Git\usr\bin\ssh-keyscan.exe
%ProgramFiles%\Git\usr\bin\ssh-pageant.exe
%ProgramFiles%\Git\usr\bin\ssh.exe
%ProgramFiles%\Git\usr\bin\sshd.exe
Place the .git* files into your home directory
Place the .bash* files into your home directory
Place the .ssh/config.d folder into %UserProfile%\.ssh\config.d along with its contents
Create a new file called 90-user and place it into %UserProfile%\.ssh\config.d\90-user with the following contents:

Host *
	User <your account>
	IdentityFile ~/.ssh/id_rsa

Please make sure to have an empty new line at the end.

To aalphabeticallydd new SSH configurations just create files as necessary in the ~/.ssh/config.d that contain the necessary configuration ending with an empty new line line each. To make sure a valid SSH configuration can be created from that the order of files is important, i.e. your custom host configurations should be  between the 00-base and the 90-user files. You have to delete the ~/.ssh/config file after each change to a host and reload the .bashrc file to make the changes available.
