#What does it do and How do I use it?

this keeps track of users, stored in 'participants.p'.  It gives them an ID,
tracks their names, phone number, a bit.ly URL for each, and visits to that
URL overall and for that day.  It also tracks what day of the program they're
on.

'TEXTUSERS' will run through all users and text them a message (defined at the
top of the file) with their bit.ly URL.  it also updates the day of the program
for each user, as well as the statistics for visits for their bit.ly address.

'REMINDUSERS' is designed to run later in the day of TEXTUSERS. It looks to see
if the bit.ly address has been visited that day since the previous text, and if
not it sends another text message defined at the top of the file.

'ADDUSER' is for adding users, removing users, and viewing the user data.  To
add a new user, simply type ```./adduser``` and follow the prompts.  To see the
user data, type ```./adduser -w```.  If you screw up and want to delete a user,
you can do so by typing ```./adduser -r <user_id>'''


#Installation

##step 1

Clone this.
Open a terminal, CD to a directory of choice, and type:
```
git clone https://github.com/dramsay9/chetan-text.git
```


##step 2

Copy/edit/overwrite config files in folder (update bit.ly and twilio API tokens)


##step 3

Make sure these files are executable. Go to the folder with the code and type:
```
chmod +x addusers remindusers textusers
```


##step 4

Install dependencies.  Go to the folder with the code and type:
```
pip install -r requirements.txt
```
if that fails you should set up an environment, or (hackily) redo that command
prepended with 'sudo -H'


##step 5

Set up your computer to text automatically in the morning, and send a reminder
in the afternoon using cron or launchd.

To set up cron jobs:

1. type "crontab -e" in terminal
2. add the following lines... note there are *tabs* in between each
number/asterisk (note the first text is sent at 9a, the second at 2p- you can
change the two numbers to change the job timing)

```
0   9   *   *   *   /path/to/textusers >>
/path/to/chetan-text/output.log
0   14   *   *   *   /path/to/remindusers >>
/path/to/chetan-text/output.log
```

the results of the texting can be found in output.log.

Cron jobs will not work on Mac OSX if the computer is asleep.  You can set your
computer to wake up so it will execute these jobs at the appropriate times by
going to Energy Saver and clicking Schedule in the bottom corner.  This is
slightly hacky, and cron has been consumed by launchd in OSX (which also has
the ablilty to run the scripts once when the computer is on if a call has been
missed).  Check this out here for an example of how to program launchd and/or
use GUI tools to handle launchd programming:
http://superuser.com/questions/126907/how-can-i-get-a-script-to-run-every-day-on-mac-os-x

