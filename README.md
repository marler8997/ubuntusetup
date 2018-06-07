
#### Make sure you can run "sudo" without a password
```
sudo visudo
```
Then add the line:
```
<user> ALL=(ALL) NOPASSWD: ALL
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

#### Install DMD compiler
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
