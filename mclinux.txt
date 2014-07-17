                                     How To run atmega mcs in linux

[released under creative commons license you can share and change it as per your need and redistribute it but with same license 
author : rohit shetty (rohitfoss00@gmail.com)
date:22/06/2014 
]



#sudo apt-get install avr-libc binutils-avr gcc-avr avrdude

#sudo gedit /etc/udev/rules.d/60-objdev.rules

copy paste this  
 
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="16c0",ATTRS{idProduct}=="05dc", 
MODE="0666",SYMLINK+="USBasp"

#sudo /etc/init.d/udev restart
 connect programmer
#cd /dev |grep USB 

u shld see a USBasp file

now get back to home
# cd ~

###########################
only to know how it works in linux
create a file named a.c 

then to compile
#avr-gcc -mmcu=atmega16 -Os a.c
to convert to hex
#avr-objcopy -j .text -j .data -O ihex a.out a.hex
to initiate microcontroller
#sudo avrdude -c usbasp -p m8
to flash into microcontroller
#sudo avrdude -c usbasp -p m16 -P USBasp -U flash:w:a.hex

###########################
The command for compiling and uploading is tiresome i have included 2 bash scripts 
1.compile
2.uploading

u need to chmod those using

#chmod a+x compile
#chmod a+x upload

to compile 
# ./upload filename
if filename is example.c your command is
# ./compile example

to upload
# ./upload mctype filename

this generates example.hex 

if your microcontroller is 16 bit and filename is example.c 
then

#./ upload 16 example

this uploads example.hex to mc 

this might ask for password as to upload sudoing is neccesary


"
