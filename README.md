# STM_32F1x_Debugging
stm32 debugging using the st-link v2 and serial wire debugging (SWD). This is a very easy taught level of some of the basics of debugging for on chip operations without the money to afford something as awesome as a lauterbach or pe micro. 

For starters we have to aquire some POS device to actually try some stuff on. Something not too complicated and easy to learn in a few days/ weeks at max. Oh and remember in this case chat gpt is at your disposal. If you have questions through this process that I cannot answer, please feel free to ask chatgpt. Something preferably under 15$, small, and easy to setup. The best thing for this that I have found that is easy to aquire is the stlink kits with an stm32 on ebay. The stlink will provide a direct connection to the stm32 and will take serial traffic from openocd and telnet commands and send them to the stm32. Think of it as an interperter. Here is a link /example. https://www.ebay.com/itm/404241984023 . This one should also have some base code on it. Something like an led blinking or something. After you recieve this, you can move on to the rest of the article. And it should be noted that gdb can be used with any code. X86, arm, mips, and anything else out there. You can figure that part out more if needed in the future with me in another repo.

After getting the devices... if you are not on linux ... get linux... or at least a virtual machine. Go to vmware and download their stuff and an iso of kali or something and boot up. From there download openocd and gdb. Both are in apt: 
sudo apt install openocd
sudo apt install gdb

With these tools everything should be good to go. Nettools may need to be installed if you have arch like me for telnet. Telnet will be used to do some basic command things and to copy over the baseline code. Then tansition into gdb for debugging the code. then jump into ghidra and look at the actual binary. That will also be in a seperate repo. 

#Connecting the STM32 to the ST-LINK V2
swdio>dio
swclk>dclk
gnd>gnd
3.3>3.3 - depends on voltage of your chip. mine was 3.3v

Thats it.
Now we can start using our tools. 

Plug the stlink in. The stm32 should start blinking or doing something. On mine the power lights up and the PC13 blinks. If this does not work, check your connections. If this does not work you could follow along by removing all interface commands and connecting through the microusb port. Now to connect to openocd, a file is needed. Specifically a .cfg file. All the premade ones exist in */usr/share/openocd/scripts* if installed on linux, specifically with apt. Some other distros might differ... go hunting. It should be noted that we have to connect to both the interface (stlink) and the target (stm32). I just made a new script in the target folder and called it stm32fXX.cfg. Here are some commands: 
cd /usr/share/openocd/scripts/target/
touch stm32fXX.cfg - I think mine is a f1x but I just made this so it would connect to the interface and target at the same time
sudo nano stm32fXX.cfg
paste this: 
source [find interface/stlink-v2.cfg]
source [find target/stm32f1x.cfg]
save and exit using ctrl+s, ctrl+x
openocd -f stm32fXX.cfg - the -f signifies that it is a file

you now should have a terminal that states that you are connected and to connect to a few ports for stuff. This is good. Pop another terminal open using ctrl+shift+t. Type:

telnet localhost 4444 - localhost is our local network and port 4444 is the connection to the stlink that openocd opened for you to use. It is the default listener for metasploit which means a similar connection can be used with metasploit ...?

Now you should see a pending carat screen like this. 


After this you can type help and a menu will pop up with the commands you can use with telnet to do stuff to the processor. And there is a lot of things. One thing we can do is halt. Type halt and enter. If there was an led blinking, it no longer is! Type resume to resume code execution as normal. 
commands:
halt
resume
step

to dump flash use command:
dump_image stm32dump.bin 0xbaseaddress 0xsize - mine for example was dump_image stm32dump.bin 0x8000000 0x00010000 

