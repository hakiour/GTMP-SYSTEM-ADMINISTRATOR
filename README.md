# GT-MP SYSTEM ADMINISTRATOR

Administration program for stop/start/restart your gt-mp server, save in-real-time logs, kill screen sessions, etc.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites
* GNU/Linux System (tested on Debian Stretch & Ubuntu Server 16.04.3 LTS)

* Functional [GT-MP Server](https://gt-mp.net/download/)

* [Screen](https://www.gnu.org/software/screen/manual/screen.html) - As window manager

* php > 5.3

#### Optionals:
 * wget
 * unzip
### Installing

First we need to download the script on our server, you can do it throught sftp, git, etc. I do it with the wget command

```
wget https://github.com/hakiour/JokeManager/archive/master.zip
```

Then, if you download the script with wget, we have a .zip file, unzip it with

```
unzip master.zip
```
Now we add the permisions on the script

```
chmod +x gtmp
```
If we use `ls -l`:

<img src="https://i.imgur.com/QEV6KWz.png">

we can see that we have the executable permision on the gtmp script.

## Configuration file
The configuration file is were the global settings for this script are setted. By default the file name is `gtmp_config`, saved on the same folder as the gtmp script.

### Parameters
* *<b>$path</b> = /home/hamza/gt-mp/* : The path of the executable server file, in this case, under the folder `/home/hamza/gt-mp/` I have the `GrandTheftMultiplayer.Server.exe` executable file.

* *<b>$executable</b> = GrandTheftMultiplayer.Server.exe* : The name of the executable server file, by default is `GrandTheftMultiplayer.Server.exe`, but if you change the name of the executable file, need to reflect it on this parameter.

* *<b>$instance_name</b> = gtav* : The name of the [screen](https://www.gnu.org/software/screen/manual/screen.html) session, you can write whatever you want (no spaces), by default is `gtav`.

* *<b>$savelog</b> = y* : If it's true (`y`), when you start the server automatically is generater a `gtmp-server.log` file where it's saved all the commands (and the ouputs) generates on the [screen](https://www.gnu.org/software/screen/manual/screen.html) session. Possible answers: yes (`y`) or no (`n`), default value is `y`.

   * Example of how the log looks like by default: <img src="https://i.imgur.com/ywRTAIh.png">
   
* *<b>$timestampOnLog</b> = n* : Complement of `$savelog` paramenter, when is true (`y`), automatically print the timestamp on the log file. Possible answers: yes (`y`) or no (`n`), default value is `n`.

   * Example of how the log looks like with the `$timestampOnLog` on : <img src="https://i.imgur.com/KzSqfup.png">
   
* *<b>$alwaysSafeStart</b> = y* : If it's true (`y`), before you start the server, kill the old [screen](https://www.gnu.org/software/screen/manual/screen.html) session (if there's more than one session, kill them all, that's why is safe), after killing the [screen](https://www.gnu.org/software/screen/manual/screen.html) sessions (or if there is no one), create a new one. It's the same when you stop the server, after stopping it, kill the [screen](https://www.gnu.org/software/screen/manual/screen.html) sessions. It's ideal if you want a clean start/stop.

### Generating a new gtmp_config file

If we don't have the gtmp_config file, we can run the script `./gtmp start` and the script automatically set up a new gtmp_config file:
<img src="https://i.imgur.com/4xAYN21.png">

But if we have one gtmp_config file and wanna generate a new one, call the script with the newconf parameter (`./gtmp newconf`). The newconf save your old gtmp_config file as gtmp_config.old

## Comands

### Syntax
The syntaxis is: `./gtmp` + [Parameter1] + [OptionalParameter2], Ex: `gtmp start -f`

## Parameters
  * `start`: With this parameter we order the server to start, if we don't have the `$alwaysSafeStart`, we need to have a [screen](https://www.gnu.org/software/screen/manual/screen.html) session running (with the correct `$instance_name`), if we don't have a [screen](https://www.gnu.org/software/screen/manual/screen.html) session running, we can call the parameter `-f` (force).
     * `-f` (force):  with the start command, this create a [screen](https://www.gnu.org/software/screen/manual/screen.html) session if there is no one, then start the server, if there is some screen session running, the program kill them (only de GT-MP screens) and then execute a new one.
      
*Example*:
```
./gtmp start -f
```
*Live example*:

 Here you can see how there is no [screen](https://www.gnu.org/software/screen/manual/screen.html) session running, and because that the command fail the execution of the server, if we call the parameter `-f`orce, we force the creation of a screen session:
 <img src="https://i.imgur.com/zZqAqoR.gif">
 
 <hr>
  * `stop`: With this parameter we order the server to stop, if we don't have the `$alwaysSafeStop`, the program don't kill screen session (what means it still online in the background), we can call the parameter `-f`orce for kill the screen sessions.
     * `-f` (force):  with the stop command, kill the screen GT-MP screen sesions after shutting down the server (it's the same as `$alwaysSafeStop`).
      
*Example*:
```
./gtmp stop -f
```
<hr>
 * `restart`: With this parameter we order the server to stop, and then start again. This command execute a `./gtmp start` and `./gtmp stop`, that means the parameters on `gtmp_config` (`$alwaysSafeStart`, `$alwaysSafeStop`, etc. affects this command). We can call the parameter `-f`orce for emulate `$alwaysSafeStart` and `$alwaysSafeStop`.
      
*Example*:
```
./gtmp restart -f
```
<hr>
 * `-l`: life version, with this parameter we can follow the status of our server in real time (2 sec delay). We can add this to all commands or call it witouth any command.
      
*Example*:
```
./gtmp -l
./gtmp start -l
```
### Built With

* [Php](http://php.net)

## Possible errors and how to solve it

['Cannot open your terminal '/dev/pts/3' - please check.'](https://makandracards.com/makandra/2533-solve-screen-error-cannot-open-your-terminal-dev-pts-0-please-check) - description: This error occurs when you wanna access to the screen session with an user who don't log in the system correctly, what means he don't have his own terminal session (run `script /dev/null` to own the shell).

## Authors

* **Hamza Akiour** - *Developer, Sysadmin & tecLover* - [Hamza Akiour](https://hamza.es)

## License

This project is licensed under the GNU (General Public License) - see the [LICENSE](LICENSE) file for details
