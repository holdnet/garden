# Share an external USB drive via Samba on your Raspberry Pi

Over this past weekend, I finally setup a network share via Samba on  my Raspberry Pi with an old external USB hard drive I had laying around. My RetroPie installation already serves up a Samba share - so my goal  was to throw an additional folder in there that mounts to an external  drive. After a bit of trial and error, here’s how I pulled it off.

Step one was to format my drive to the ext4 filesystem. I read  varying opinions on which filesystem is recommended for this procedure,  and ext4 seemed to be a good choice in the end. While there are ways to  format your drive directly via the [CLI](https://www.raspberrypi.org/forums/viewtopic.php?t=38429) - I decided to use a trial of [ExtFS for Mac](https://www.paragon-software.com/home/extfs-mac/) and it was very easy.

Next, I plugged my external drive into the RPi and connected over SSH. Once you’re connected, run the following command:

```bash
sudo fdisk -l
```

Now, look towards the bottom and assuming this is the only additional drive you have plugged in, you should see something like this:

```bash
Device     Boot Start       End   Sectors   Size Id Type
/dev/sda1  *        2 975400959 975400958 465.1G 83 Linu
```

/dev/sda1 is the name of the partition on our external drive.

Next we’re going to create a directory within our `/media/` folder to mount our drive into, and also a sub-directory within it. The reason for the sub-directory is that I want to avoid seeing the  lost+found folder on the ext4 partition we created.

```bash
sudo mkdir /media/USBHDD
sudo mkdir /media/USBHDD/share
```

After that, we want to ensure that we have the full access to the directory.

```bash
sudo chmod -R 777 /media/USBHDD/share
```

Next, we want to mount our external drive into that new directory.

```bash
sudo mount -t auto /dev/sda1 /media/USBHDD
```

Now we’ll need to update our Samba config. If you’re already running  RetroPie, you’ve already got Samba installed. If not, you may need to  run the following command.

```bash
sudo apt-get install samba samba-common-bin
```

Before you edit your Samba config, make a quick backup copy of the current file.

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.old
```

Now, jump into the config file.

```bash
sudo nano /etc/samba/smb.conf
```

We’re going to want to jump straight to the bottom of this file - so if you’re on a Mac just hit **fn** and the **down** **arrow** a few times.

Once you get to the bottom, you should see a list of familiar folders that RetroPie already shares (roms, bios, configs, and splashscreens).  Create another sections just below the last that looks like this:

```bash
[share]
comment = Share
path = "/media/USBHDD/share"
writeable = yes
guest ok = yes
create mask = 0777
directory mask = 0777
force user = pi
```

The name and the comment can be customized, but definitely make sure your **path** matches the one you created earlier.

And finally, you’ll want to restart your Samba daemons.

```bash
sudo systemctl restart smbd
```

At this point you should be able to read and write to your Samba share via Finder by clicking on **retropie** under the **Shared** heading and then accessing your new folder called **share**.

The final step we’ll want to do is edit our fstab configuration so  that our drive will properly mount whenever our Raspberry Pi reboots.

```bash
sudo nano /etc/fstab
```

Add the following line to the bottom of the config file (making sure to match the values you’ve used previously). `/dev/sda1 /media/USBHDD auto noatime 0 0` And now we’re done. Enjoy your new network share drive. Personally I’ve  hooked mine into every device on my network that can run Kodi for a  personal media library accessible throughout the home.