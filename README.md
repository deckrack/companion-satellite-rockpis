# companion-satellite-rockpis
Prebuilt companion-satellite image for RAXDA Rock Pi S

## Manual Construction
1. Flash the latest [Armbian Bookworm Minimal](https://www.armbian.com/rockpi-s/) onto an 8GB or larger microSD card
2. Put the card in the Rock Pi S. Power it and give it an Ethernet internet connection. If a blue LED is flashing, the Rock Pi has booted.
3. SSH into the Rock Pi
   
     `SSH -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null root@rockpi-s`
   
4. Provide the Armbian default password `1234`
5. When prompted, create root password `satellite`
6. When prompted, make a new user with Name `Satellite`, username `satellite`, password `satellite`
7. When prompted, accept the recommended user language.
8. If prompted, Skip generating other locales
9. Set the hostname

    `sudo hostnamectl hostname sat-0`

10. Reboot with `sudo reboot` to make the hostname stick
11. Get more swap space

    `fallocate -l 4G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile`

    `mount -o remount,size=2G /tmp/`

12. Run the Satellite install script
    
    `curl https://raw.githubusercontent.com/bitfocus/companion-satellite/main/pi-image/install.sh | bash`

13. Install a specific Satellite version

    `sudo satellite-update`

14. Choose `latest-beta`

15. Teminal should report “config ok” and then “Update is complete”

## Unique hostnames
On a DHCP network, each Rock Pi should have a unique hostname. This command will randomize the hostname.

`sudo hostnamectl hostname sat-$RANDOM`

## Turn a microSD card into a .img on macOS

1. Identify the microSD disk attached to your mac

   `diskutil list`

2. Copy the disk into a compressed .img file. Substitute the disk name in for `diskX`.
   
   `sudo dd if=/dev/diskX bs=64K | gzip -c > companion-satellite-rockpis.img.gz`

