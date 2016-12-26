Compile the code: gcc -o firstdaemon daemonize.c
Start the daemon: ./firstdaemon
Check if everything is working properly: ps -xj | grep firstdaemon
The output should be similar to this one:
+------+------+------+------+-----+-------+------+------+------+-----+
| PPID | PID  | PGID | SID  | TTY | TPGID | STAT | UID  | TIME | CMD |
+------+------+------+------+-----+-------+------+------+------+-----+
|    1 | 3387 | 3386 | 3386 | ?   |    -1 | S    | 1000 | 0:00 | ./  |
+------+------+------+------+-----+-------+------+------+------+-----+
What you should see here is:

The daemon has no controlling terminal (TTY = ?)
The parent process ID (PPID) is 1 (The init process)
The PID != SID which means that our process is NOT the session leader
(because of the second fork())
Because PID != SID our process can't take control of a TTY again
Reading the syslog:

Locate your syslog file. Mine is here: /var/log/syslog
Do a: grep firstdaemon /var/log/syslog
The output should be similar to this one:
  firstdaemon[3387]: First daemon started.
  firstdaemon[3387]: First daemon terminated.

A note: In reality you would also want to implement a signal handler and set up the logging properly (Files, log levels...).

Further reading:

Linux-UNIX-Programmierung - German
Unix Daemon Server Programming