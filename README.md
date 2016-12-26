# gadgetdaemon  

Compile the code: gcc -o gadgetdaemon daemonize.c  
Start the daemon: ./gadgetdaemon  

Check if everything is working properly: ps xj | grep gadgetdaemon  
The output should be similar to this one:  
+------+------+------+------+-----+-------+------+------+------+-----+  
| PPID | PID  | PGID | SID  | TTY | TPGID | STAT | UID  | TIME | CMD |  
+------+------+------+------+-----+-------+------+------+------+-----+  
|____1 | 3387 | 3386 | 3386 |____?|____-1|____S | 1000 | 0:00 |___./|  
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
