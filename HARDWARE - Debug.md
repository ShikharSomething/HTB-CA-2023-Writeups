**Challenge Name:** Debug

**Category:** Hardware

**Description:** Your team has recovered a satellite dish that was used for transmitting the location of the relic, but it seems to be malfunctioning. There seems to be some interference affecting its connection to the satellite system, but there are no indications of what it could be. Perhaps the debugging interface could provide some insight, but they are unable to decode the serial signal captured during the device's booting sequence. Can you help to decode the signal and find the source of the interference?

**My first thoughts:** So this was an easy rated challenge so it had to be and it was easy. We are provided again with a .sal file.

**Solution:** So now we are provided with a single .sal file and I immediately opened it up in Saleae and I saw two channels and they were named TX and RX. Most of the communication was happening with the RX channel so I think that was the tranmission wire and TX was the ground wire. So what I did after seeing the RX communication was at first I thought of adding SPI analyzer thinking that the TX channel was the clock but then I thought that for the TX channel to be a clock there should be some fluctuations but there weren't any so I went on and put async serial analyzer on the RX channel. I put the async serial analyzer with the default settings but it didn't seem to work so now I was just trying various standard baud rates (because I felt too lazy to calculate the baud rate myself). And then boom 115200 baud rate worked. The output looked something like this. [Picture](https://github.com/ShikharSomething/HTB-CA-2023-Writeups/blob/main/Screenshot%202023-03-25%20112728.png). And now to
actually "capture the flag" you have to be a bit smart over here. The flag is split into several parts and is put in the output.


    WARNING: The deep space observatory is offline HTB{
    INFO: Communication systems are offline reference code: 547311173_
    WARNING: Unauthorized subroutines detected! reference code: n37w02k_
    WARNING: The satellite dish can not sync with the swarm. reference code: c0mp20m153d}
  
  
If you analyze this output clearly you will get the flag HTB{547311173_n37w02k_c0mp20m153d}
