

# Smart Speaker with Pi 3


### BOSE Radio Wave/CD

This is a legend product of **BOSE** it sold from 1998-2018. We will use this as the speaker we are going to add to the **HiFi Berry 2**

[Operation Manual](https://assets.bose.com/content/dam/Bose_DAM/Web/consumer_electronics/global/products/speakers/wrcd/pdf/owg_en_wrcd.pdf)

[Service Manual](https://drive.google.com/file/d/1gkQiOSfg_a449GaNvmqlSzYBA_F7n1ts/view?usp=sharing)


### RPI Zero w Configuration

I use the original **Imager** to set up `ssh` and **Wifi** config

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/BluGxLnb/82e2b924-d60b-48aa-9aa0-c26d2b20c0f7.png?v=3f8453ce6388728ce6d26efc68ea468a)

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/d5uORlm1/ab238a2f-1f81-4941-8486-f7eabff66632.png?v=46525ce93b8192310ec785bd1460be68)

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/v1uO0KJA/e54e4fcb-8e12-411a-ad29-7ec40989835b.png?v=6a72ca7abdacd8229eecf0c93a93027a)



This is my Pi Zero condition once installed the **Pi-OS-Lite**

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/KoujJGnJ/e77f3cee-b3e9-46cb-a91f-426b9ab8bbeb.jpg?v=84466c57e14ff59160955100dba138c9)


- Software Configuration
	Edit config.txt

		$ sudo nano /boot/config.txt
and comment out the line
		
		# dtparam=audio=on
		
and at the end of the file add the lines

		# HiBerry AMP 2 
			dtoverlay=hifiberry-dacplus

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/Z4uADvpx/1858a141-e9e6-4a0c-a998-6318156f68b5.jpg?v=559a69eb30b26a1a406553fbb944f1f7)

and then reboot:
		
		$ sudo reboot

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/9ZuogG2Q/80188b0d-a4d2-41fd-9571-d50e87194acd.jpg?v=103feb71c001b8c82d03f9b6cb629244)
 
 
 - Configure **ALSA**

With this command, it will create a file called _asound.conf_
		
		$ sudo nano /etc/asound.conf 
 
 And then reboot
 
 - Operating System Check 

Check if the audio card has been installed

		$ aplay -l 
 
![](https://p10.tr2.n0.cdn.getcloudapp.com/items/rRuOgDd9/9e16428a-d269-48d5-8b64-9cc8c29a3136.jpg?v=3128bc419dc20d87c7bcd09591721cff) 

### Music Playing

There are many **Linux** players you can chose, such as **vlc**, **mplauer2** and so on. We will use the **mpd** + **mpc**

`mpd`: the music player\
\

`mpc`: the command line controller\


1. Install the software
	2. ALSA has been pre-installed on RSPI
	3. AlsaMixer is a GUI to control the volume
	4. **amixer** is a command line tool change the volume 



				$ sudo apt-get install mpd mpc -y

![5 minutes to download](https://p10.tr2.n0.cdn.getcloudapp.com/items/geuRykmJ/72ba1824-72b8-402a-ae45-39acc2f7e1eb.jpg?v=83608dbfc7183e6aee39da3a01e51b3e)
2. Change the permissions for them

		$ sudo service mpd stop
		$ sudo chmod -R g+w /var/lib/mpd
		$ sudo chmod -R g+w /var/run/mpd
		$ sudo service mpd start

![](https://p10.tr2.n0.cdn.getcloudapp.com/items/2Num7kmJ/fe4c4158-7c25-48e1-be70-ca9779bceefe.jpg?v=0eb09e719ac5088c02eb9df207a94d4b)

 
### HiFiBerry

![](https://www.hifiberry.com/wp-content/uploads/2017/09/amp2-4000x4000-1024x1024.jpg)

[Official Introduction](https://www.hifiberry.com/shop/boards/hifiberry-amp2/) 

#### Feature Highlights 

- up to **60 W** 
- power range form **12-24 v**
- no need to separate power on **Pi**
- support all series of **Pi** family 


#### Connection Parameters 


| Speaker Resistance | Operating Voltage | Operating Frequency | Sampling Size |
|:--|:--|:--|:--|
| 4 $\Omega$ | 12-18 V | 44.1-192 kHz | 16-32 bit |
| 8 $\Omega$ | 24 V | 44.1-192 kHz | 16-32 bit |


#### Hardware Configuration Map

HiBerry Amp 2 Pins used:
- I2C (GPIO 2, 3) SDA and SCL pins 3 and 5 are used to control the HiBerry Amp 2
- GPIO 4 is used to control the MUTE function of the power stage. Pulling it low mutes the output.
- GPIOs 18-21 (pins 12, 35, 38 and 40) are used for audio interface
- Pin 27 and 28 are always reserved for an ID EEPROM Since over-the-air FM Radio uses I2C, I will need to figure out how to use HiBerry Amp 2 and Si4702 as I2C slave devices.



---
Reference 

[HiFiBerry Amp2](https://www.amazon.com/HiFiBerry-Hifiberry-AMP2-Amp2/dp/B076DLCRHF/ref=pd_rhf_eetyp_s_bmx_gp_7l9r2bon_sccl_1_8/130-6880759-6626323?pd_rd_w=TcPQm&content-id=amzn1.sym.77fee36f-fb5d-4f34-86d8-acb593d1b351&pf_rd_p=77fee36f-fb5d-4f34-86d8-acb593d1b351&pf_rd_r=6BD0H26VP89SY2BANGR9&pd_rd_wg=SkwUp&pd_rd_r=408bb28a-625e-4469-bb48-af8299166728&pd_rd_i=B076DLCRHF&psc=1)

[Officail Instructions](https://www.hifiberry.com/firststeps/)

[Online Tutorial](https://sites.google.com/site/cartwrightraspberrypiprojects/home/home-automation-categories/entertainment/alarm-clock-radio/hiberry-amp-2)

[Play Musics on Headless Pi](https://sites.google.com/site/cartwrightraspberrypiprojects/home/home-automation-categories/entertainment/alarm-clock-radio/internet-radio-basics?authuser=0)

[Setup Hifiberry Amp2](http://www.waailap.nl/instruction/215/setup-hifiberry-amp2.html)

[Google Drive for supporting files](https://drive.google.com/drive/folders/1ZKWPPmsLRKeqfVNe4JSCYAWsTDMtde4u?usp=sharing)
