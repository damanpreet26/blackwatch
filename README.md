#BLACKWATCH version 1.0
-This is a perfect piece of code for those who want to keep their systems away from unauthorized usage.

-The user gets the error message of wrong passwords being entered into the system.
-Once you enter a wrong password the webcam automatically takes the 4-5 pictures and makes a video on when the wrong password was entered.
-The images are kept at a safe location which is /etc/motion/
-an error file("illegal access") named file is created with the data and time of entry is saved, for the help of the system user.

#REQUIREMENT
1-check the working of the webcam commected to ur system(very important)
2-install software-motion
    	sudo apt-get install motion
3-Create a small script somewhere, e.g. /usr/local/bin/grabpicture (script in files)
4-Make it executable, e.g. chmod +x /usr/local/bin/grabpicture.
5-Test it, by just calling it: /usr/local/bin/grabpicture. Check if you see files appearing in /tmp/motion
###Note: do this carefully - if this fails you'll not be able to gain access to your system again in a regular way.
6-Open with root access /etc/pam.d/common-auth in your favourite editor.
7-Locate the line below. By default there's one line before the one with pam_deny.so. On my 12.04 system it looks like this:

auth    [success=1 default=ignore]      pam_unix.so nullok_secure
In this line change the success=1 to success=2 to have it skip our script on succes. This is an important step.

8-Right below there, add a new line to call the actual script:

auth    [default=ignore]                pam_exec.so seteuid /usr/local/bin/grabpicture

9-Save and close the file. No need to restart anything.
10-Test it.

