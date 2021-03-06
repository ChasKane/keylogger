# @ChasKane Fork Notes
I wanted to store my keystroke usage in vim so I could
* track which plugins I'm using the most so I can have a list of features I might need if I switch to another text editor,
* know whether an annoyance I face in editing is actually a constant pattern, or if I'm just falling prey to the availability heuristic.
So I forked this, modified the log file location, and added `activeAppWatch` so I could ignore everything not typed into `iTerm2` (my terminal emulator of choice).

Also, something that tripped me up: since `activeAppWatch` goes in the startup scripts locaiton, at least one of the following must be true (couldn't figure out which when debugging -- again, didn't want to spend too much time on this, and I'm not worried about security on my personal laptop):
* only absolute paths when `printf`ing in the script
* the log file must be writable by `others` (`chmod 666 .log`)


# Mac OS X Keylogger

This repository holds the code for a simple and easy to use keylogger for Mac OS X. It is not meant to be malicious, and is written as a proof of concept. There is not a lot of information on keyloggers or implementing them on Mac OS X, and most of the ones I've seen do not work as indicated. This project aims to be a simple implementation on how it can be accomplished on OS X.

> Note: This keylogger is currently unable to capture secure input such as passwords. See issue #3 for more information.

## Usage

Start by cloning the repository and running the proper make commands, shown below. By default, the application installs to `/usr/local/bin/keylogger`, which can easily be changed in the [`Makefile`](https://github.com/caseyscarborough/keylogger/blob/master/Makefile). `make install` may require root access.

```bash
$ git clone https://github.com/caseyscarborough/keylogger && cd keylogger
$ make && make install
```

The application by default logs to `/var/log/keystroke.log`, which may require root access depending on your system's permissions. You can change this in [`keylogger.h`](https://github.com/caseyscarborough/keylogger/blob/master/keylogger.h#L12) if necessary.

```bash
$ keylogger
Logging to: /var/log/keystroke.log
```

If you'd like the application to run on startup, run the `startup` make target:

```bash
$ sudo make startup
```

## Uninstallation

You can completely remove the application from your system (including the startup daemon) by running the following command (logs will not be deleted):

```bash
$ sudo make uninstall
```

### Optional Parameters

You can pass in two optional parameters to the program. The `clear` option will clear the logs at the default location. Any other argument passed in will be used as the path to the log file for that process. See below:

```bash
# Clear the logfile.
$ keylogger clear
Logfile cleared.

# Specify a logfile location.
$ keylogger ~/logfile.txt
Logging to: /Users/Casey/logfile.txt
```

## Contributing

Feel free to fork the project and submit a pull request with your changes!
