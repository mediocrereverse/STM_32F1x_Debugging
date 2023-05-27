# STM_32F1x_Debugging
stm32 debugging using the st-link v2 and serial wire debugging (SWD). This is a very easy taught level of some of the basics of debugging for on chip operations without the money to afford something as awesome as a lauterbach or pe micro. 

For starters we have to aquire some POS device to actually try some stuff on. Something not too complicated and easy to learn in a few days/ weeks at max. Oh and remember in this case chat gpt is at your disposal. If you have questions through this process that I cannot answer, please feel free to ask chatgpt. Something preferably under 15$, small, and easy to setup. The best thing for this that I have found that is easy to aquire is the stlink kits with an stm32 on ebay. The stlink will provide a direct connection to the stm32 and will take serial traffic from openocd and telnet commands and send them to the stm32. Think of it as an interperter. Here is a link /example. https://www.ebay.com/itm/404241984023 . This one should also have some base code on it. Something like an led blinking or something. After you recieve this, you can move on to the rest of the article. And it should be noted that gdb can be used with any code. X86, arm, mips, and anything else out there. You can figure that part out more if needed in the future with me in another repo. Here is some pictures of

After getting the devices... if you are not on linux ... get linux... or at least a virtual machine. Go to vmware and download their stuff and an iso of kali or something and boot up. From there download openocd and gdb. Both are in apt: 
sudo apt install openocd
sudo apt install gdb

Now we get to install 

