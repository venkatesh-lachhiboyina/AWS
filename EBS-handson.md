first I have created an EC2 instnace. so we got an volume default how we mentioned in the launching details
then I need an extra volume. so I have created a volume of some GB and attach my new volume to my instance

fdisk -l command shows all the fixed disk list

now, we need to do patition for the data so use 
fdisk /dev/xvdf1(file system) command, you can do partition now use n to start partition and give w to exit after the partition.

now you have to format the data using mkfs command 
use mkfs /dev/xvdf1 command to format the data

then, you can mount this where ever you want like use command 
umount /dev/xvdf1 /var/www/html(this is path where you mounted), still this is an temporary mount

so, unmount it using
umoumt /var/www/html

then now we can do permanant mount 

vi /etc/fstab

file system        path        mkfs   defaults   0(fsk) 0(dump)

ex: /dev/xvdf1   /var/www/html  ext4  dfaults    0      0
save the file and


use mount -a, now its mounted 
check df -h
