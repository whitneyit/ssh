# SSH setup.

This repo is designed to create a **ssh config** file. [Joël Perras](https://twitter.com/jperras)
wrote up an awesome post over at his [website](http://nerderati.com) titled [Simplify Your Life With an SSH Config File](http://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file).
It really is amazing, and I suggest that you check it out.

To get started, just execute the code below. That will clone this repo in the
current working directory and then copy accross my ssh [config](https://github.com/whitneyit/ssh/blob/master/config)
file into the `~/.ssh` folder, creating it if it does not already exist. Next it
will set the permission of the folder accordinly.

Once that is complete it will add a file to `/usr/local/bin` called
`ssh-setup`. This file allows you to execute the `setup` file from anywhere
within the OS so long as the `/usr/local/bin` folder has been added to your
path. If the folder cannot be found one will be created for you.

Also, if you have [vagrant](https://www.vagrantup.com) installed, it will set
the permissions of the `insecure_private_key` that ships with vagrant.

So to begin, navigate to the folder where you want the git repo cloned to then
execute the bash script below. For example,

```sh
$ mkdir -p $HOME/Code/ssh
$ cd ~/Code/ssh
```

This would mean that the repo will be checked out into your `~/Code/ssh` folder.
If you have some folder where you put all of your git repos, then that would be
a perfect fit for this.

If you don't end up navigating to a specific folder and just end up cloning the
repo out of your `$HOME` folder, the repo will instead be cloned into a new
folder located at `$HOME/ssh`.

So, once you are in the desired folder to store this code, run the bash script
below.

```sh
$ bash -c "$(curl -fsSL https://raw.github.com/whitneyit/ssh/master/setup)"
```

With that complete, you can now create create ssh keys and place them in the
`~/.ssh` folder. I prefer to name my keys after my email addresses so that it is
easy to seperate my work and personal keys. This also allows me to create
multiple keys of the same name and spread them over multiple machines.

The names of the keys that I shall be are adding are located in the [keys](keys)
file.

You can find more information about creating [ssh keys](https://help.github.com/articles/generating-ssh-keys)
here.

To create a new key, you can use the code snippet below.

```sh
$ ssh-keygen -t rsa -C "your_email@example.com"
```

You will then be prompted to enter the location of where you want to save your
nemly created key.

> Enter file in which to save the key.

This is where I enter my email address. After that you will prompteed to enter
a passphrase.

If you don't want to keep entering a [passphrase](https://help.github.com/articles/working-with-ssh-key-passphrases)
you can just leave it blank.

Should you be using [cygwin](https://www.cygwin.com/), ensure that you set the
user group of the key correctly. The code below will achieve that for you.

```sh
$ chgrp Users ~/.ssh/your_email@example.com
```

Next ensure that you set the permissions of the key correctly:

```sh
$ chmod 600 ~/.ssh/your_email@example.com
```

If you are note using my [dotfiles](https://github.com/whitneyit/dotfiles) repo,
you will have to ensure that you have started up the `ssh-agent` and that the
new ssh key(s) habe been **added** to the `ssh-agent`.

To achieve that, execute the following;

```sh
$ eval "$(ssh-agent)"
$ eval ssh-add "~/.ssh/your_email@example.com"
```

Lastly, with all of that setup complete, don't forget to add those keys to your
providers; [GitHub](https://github.com/settings/ssh), [BitBucket](https://bitbucket.org/account/user/whitneyit/ssh-keys), etc.
