# Systemd Service Files for Telos

Running the Telos services using systemd rather than a simple start/stop script gives you some neat advantages. Systemd can auto start those services at boot time, restart them automatically when they fail and uses a binary logging system that is very powerful when it comes to filtering, storing and rotating the logs. 

## How to install

Copy the service files to `/etc/systemd/system`. You probably need to adapt some paths for your Telos data/config directories. If you did not execute `make install` after building Telos you also need to adapt the executable path (make sure you always use the full path, even if the nodeos executable is in your PATH environment variable). 

The Telos services are run as telos user (do not use root to run your nodes), this means there either has to be a telos user on your system or you need to adapt the user/group setting as well.

## Running the Services

To start a service such as the Telos node, simply run `systemctl start telos-nodeos.service` or `systemctl stop telos-nodeos.service` to stop it. You can find the current state by executing `systemctl status telos-nodeos.service`.

## Enable the Services

To automatically start a service after the system has booted up, use `systemctl enable telos-nodeos.service`.

## View the Logs

You can use journalctl to view the log files, by calling `journalctl -u telos-nodeos.service`. Useful options are `-f` (continously prints the newest log entries to the console), `-e` (jumps to the end of the logs), `--since` (shows entries that are newer than the given date) and `-b` (shows the log entries since the last boot). All options can be found in the [official documentation](https://www.freedesktop.org/software/systemd/man/journalctl.html).
