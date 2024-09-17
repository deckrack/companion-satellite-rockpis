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

    `sudo hostnamectl hostname sat-$RANDOM`

10. Get more swap space

    `fallocate -l 4G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile`

    `mount -o remount,size=2G /tmp/`

11. Run the Satellite install script
    
    `curl https://raw.githubusercontent.com/bitfocus/companion-satellite/main/pi-image/install.sh | bash`

12. Install a specific Satellite version

    `sudo satellite-update`

13. Choose `latest-beta`

14. Teminal should report “config ok” and then “Update is complete”

