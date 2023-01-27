# Onedrive

With your Charite Login, you have a personal OneDrive which holds 1 TB & can be used to share documents with others within Charite.

In addition, there is storage on the sharepoint that can be accessed from within [MS Teams](teams.md).

It can be helpful to connect your local rclone install to Onedrive in order to swiftly backup stuff to Onedrive, e.g. from the [BIH Cluster](../bih-cluster/) or from your local machine.

Run **`brew install rclone`** in the terminal in case you don't have it installed. To set up a new rclone remote, run **`rclone config`** in the terminal and follow the instructions displayed.

## Connect your rclone to Onedrive:

```
** See help for onedrive backend at: https://rclone.org/onedrive/ **

Microsoft App Client Id
Leave blank normally.
Enter a string value. Press Enter for the default (“”).
client_id> 
Microsoft App Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default (“”).
client_secret> 
Edit advanced config? (y/n)
y) Yes
n) No
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes
n) No
y/n> y
If your browser doesn’t open automatically go to the following link: http://127.0.0.1:53682/auth
Log in and authorize rclone for access
Waiting for code...
Got code
Choose a number from below, or type in an existing value
 1 / OneDrive Personal or Business
  \ “onedrive”
 2 / Root Sharepoint site
  \ “sharepoint”
 3 / Type in driveID
  \ “driveid”
 4 / Type in SiteID
  \ “siteid”
 5 / Search a Sharepoint site
  \ “search”
Your choice> 1
Found 1 drives, please select the one you want to use:
0: OneDrive (business) id=b!tpExGJahGEyfOTS0i36lPFwmvGNZzjFMoqUzan_PnUg8ENXQCrk4SrYQYo28pF0O
Chose drive to use:> 0
Found drive ‘root’ of type ‘business’, URL: https://charitede-my.sharepoint.com/personal/andreas_horn_charite_de/Documents
Is that okay?
y) Yes
n) No
y/n> y
```

## Connect your rclone to the Netstim Sharepoint:

```
** See help for onedrive backend at: https://rclone.org/onedrive/ **

Microsoft App Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id> 
Microsoft App Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_secret> 
Edit advanced config? (y/n)
y) Yes
n) No
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes
n) No
y/n> y
If your browser doesn't open automatically go to the following link: http://127.0.0.1:53682/auth
Log in and authorize rclone for access
Waiting for code...
Got code
Choose a number from below, or type in an existing value
 1 / OneDrive Personal or Business
   \ "onedrive"
 2 / Root Sharepoint site
   \ "sharepoint"
 3 / Type in driveID
   \ "driveid"
 4 / Type in SiteID
   \ "siteid"
 5 / Search a Sharepoint site
   \ "search"
Your choice> 5
What to search for> netstim
Found 1 sites, please select the one you want to use:
0: Netstim (https://charitede.sharepoint.com/sites/Netstim) id=charitede.sharepoint.com,7b3d80a0-3fe3-46ad-a1a7-3ae014e29d1b,da2b05c0-12e2-478a-867f-959277b10256
Chose drive to use:> 0
Found 1 drives, please select the one you want to use:
0: Documents (documentLibrary) id=b!oIA9e-M_rUahpzrgFOKdG8AFK9riEopHhn-VknexAlZF3e8zBL8dQLoJt4m3a1pP
Chose drive to use:> 0
Found drive 'root' of type 'documentLibrary', URL: https://charitede.sharepoint.com/sites/Netstim/Shared%20Documents
Is that okay?
y) Yes
n) No
y/n> y
```

