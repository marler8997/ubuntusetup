
#### Make sure you can run "sudo" without a password

You can either edit `/etc/sudoers` like this:
```
sudo visudo
```
Then add this line to the END OF THE FILE (if you don't add it to the end it doesn't work, not sure why):
```
<user> ALL=(ALL) NOPASSWD: ALL
```

The second option is you can just add a file in `/etc/sudoers.d` with this config.  You can do this with an echo command:
```
# you need to change the shell to root user, because the redirect needs root permissions
# which means you can just add "sudo" to the echo command
sudo su
echo "<user> ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/<some-name>
```

#### Install Visual Studio Code
Download ".deb" file "https://go.microsoft.com/fwlink/?LinkID=760868"
```
sudo dpkg -i <file>.deb
```

> Note: this means you can open/edit files using `code <filename>`

#### Install git
```
sudo apt-get install git gitk git-gui
```
Create the "~/git" folder where I keep most of my git repositories.
```
mkdir ~/git
```

It gets annoying to enter username/password all the time. Run this to have git save your credientials:
```
git config --global credential.helper store
```

#### Create a ~/bin directory

The "~/bin" directoy is where I keep all my command line tools.
```
mkdir ~/bin
```
The permanently add this directory to the PATH.  Open "~/.profile" and add the following line:
```
PATH="~/bin:$PATH"
```

#### Create the set-title function in `.bashrc`

```bash
function set-title() {
  if [[ -z "$ORIG" ]]; then
    ORIG=$PS1
  fi
  TITLE="\[\e]2;$*\a\]"
  PS1=${ORIG}${TITLE}
}
```

This allows you to run `set-title my new title" in your terminal to set the window title.

#### Install DMD compiler


##### Use `install.sh` script
```
mkdir ~/dlang
curl -fsS https://dlang.org/install.sh > ~/dlang/install.sh
chmod a+x ~/dlang/install.sh

# Install latest
~/dlang/install.sh
# Install specific version
~/dlang/install.sh install dmd-2.079.0
```

Now create links to binaries:
```
ln -s ~/dlang/dmd<version>/linux/bin64/dmd ~/bin/dmd
ln -s ~/dlang/dmd<version>/linux/bin64/rdmd ~/bin/rdmd
```


#### Manual installation

Goto http://dlang.org/download and download the tar.xz file.

> I like to install manually so I can maintain multiple versions of the compiler.

```
mkdir ~/dmd<version>
mv ~/Downloads/dmd<version>.tar.xz ~/dmd<version>
cd ~/dmd<version>
tar xf dmd<version>.tar.xz
rm dmd<version>.tar.xz
```

Then create links to the `dmd` and `rdmd` binaries in the user's bin directory:
```
ln -s ~/dmd<version>/dmd2/linux/bin64/dmd ~/bin/dmd
ln -s ~/dmd<version>/dmd2/linux/bin64/rdmd ~/bin/rdmd
```

#### Clone the bidmake repo

```
git clone https://github.com/marler8997/bidmake
```

Follow README.md to install the developer build, should end up being able to run bidmake by typing `bb` on the command line.

#### Clone utils/build repo

```
cd ~/git
git clone https://github.com/marler8997/utils
cd utils
bb
```
