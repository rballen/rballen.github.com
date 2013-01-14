---
layout: post
title: "Move Raspberry Pi Filesystem to USB"
description: "raspberry pi, rpi, filesystem, usb"
category: linux
tags: [raspberry-pi, linux]
---

I've gone thru so many of those damn sd cards and it's time to move off to a usb thumb drive. My ScanDisk class 4 is working better for debian and arch but it still locks up and I have to hard reboot every 4 days or so. I use my pi as a server and need it to be always up. So after doing a lot of research I settled on the [Kingston 64G datatravelor gen 2](http://www.amazon.com/gp/product/B008AGAFQU/ref=pd_sim_e_9)

The rpi has to boot from the sd card so /boot will remain on the sd and everything else will run from the usb. I like to multiboot so I will use gparted to create 4 partitions.
>1. debian 10G
>1. archpi 10G
>1. data partition 43G
>1. swap 1G 

I can verify with blkid:

{% highlight bash %}
 sudo blkid
/dev/sda1: LABEL="debian" UUID="4f73b2ee-1b84-4601-afb4-fb995a01cf05" TYPE="ext4" 
/dev/sda2: LABEL="arch" UUID="6a886875-401c-426f-9dc5-eecd3251ee00" TYPE="ext4" 
/dev/sda3: LABEL="data" UUID="613f8492-f15d-462d-a1f5-2ba4b252b47e" TYPE="ext4" 
/dev/sda4: LABEL="swap" UUID="7874f628-bee1-4c24-91e8-ecb50c318c59" TYPE="swap" 
{% endhighlight %}


Before shutting down my pi I'll make a backup of /boot/cmdline.txt and then instruct pi to look to 2nd partion of usb for arch after boot.

{% highlight bash %}
sudo cp /boot/cmdline.txt /boot/cmdline.txt.original
# now edit /boot/cmdline.txt and instruct root with the new boot: root=/dev/mmcblk0p2 to root=/dev/sda2
{% endhighlight %}

I used cp instead of rsync and did the transfer between the usb and sd on my linux laptop. The 2nd partion is mounted to /media/archusb and the sd card is mounted to /media/archarm
   
{% highlight bash %}
sudo cp -av /media/archarm/* /media/archusb/
sync
{% endhighlight %}

It's faster now and it's been up for 4 days so far.