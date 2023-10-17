# Raspberry Pi Windows GCC cross-compiler setup

## Setup instructions
1. Download GCC version 10.2.1 Raspberry Pi image (img) and windows toolchain installer (exe).
   Link: https://gnutoolchains.com/raspberry/
2. Using 7zip extract the image from the compressed xz container.
   Link: https://www.7-zip.org/download.html
3. Flash img file to sd card using windows PC, adapter and software called Balena Etcher
   Link: https://etcher.balena.io/
4. Insert SD card into raspberry pi and proceed with regular setup instructions skipping updates at the end.
5. Resize the root partition of the drive to match the whole available size of the sd card using method 2 of this tutorial (ignore swap as it is not present)
   Link: https://www.golinuxcloud.com/extend-resize-primary-partition-non-lvm-linux/#Method_2_Change_size_of_partition_using_fdisk_utility
6. Update raspberry pi system using `sudo apt update` followed by `sudo apt full-upgrade`
7. Reboot raspberry pi.
8. Enable ssh on raspberry pi using `sudo systemctl enable --now ssh`
9. Install SmarTTY on Windows PC
   Link: https://sysprogs.com/SmarTTY/
10. Install gcc toolchain exe downloaded in step 1 on Windows PC.
11. Reboot Windows PC.
12. Clone or Download git repo to Windows PC and open `hello_world.cpp` in VSCode.
13. Run the command `arm-linux-gnueabihf-g++.exe -ggdb hello_world.cpp -o hello_world` in the VSCode terminal.
14. Open SmarTTY and setup a new ssh connection using the IP of the Raspberry Pi found using `ip addr` and the login credentials created in step 4.
15. SmarTTY should be in home directory of Raspberry Pi. Drag the compiled binary into the window of SmarTTY to transfer the binary to the raspberry Pi.
16. In SmarTTY run the command `chmod a+x hello_world` to make the binary executable.
17. In SmarTTY run `./hello_world` to make sure the binary runs.
18. In SmarTTY run `gdbserver :1234 hello_world` to create a gdb server.
19. In VSCode terminal run `arm-linux-gnueabihf-gdb.exe hello_world`
20. In the following prompt run `target remote <Raspberry IP address>:1234`
21. Add breakpoints such as writing `b main` hitting enter, and then writing `c` and entering again.
22. Keep entering `n` until the program exits.
23. Enter `q` to exit gdb prompt in VSCode.
24. Look at SmarTTY screen to see `Hello World!` outputed to stdout.
