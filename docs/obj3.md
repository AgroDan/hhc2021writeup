# Thaw Frost Tower's Entrance

After speaking with Grimy McTrollkins, he tells me that the entrace to the Frost Tower is frozen and nobody can get inside. There's a thermostat visible from the window that is accessible via wifi. By sitting right outside the window where the thermostat is...

![Right outside](img/obj3/img2.png)

I can open up the interface to the USB wifi dongle and scan for any available access points:

```sh
elf@10f3638f3d62:~$ iwlist wlan0 scanning
wlan0     Scan completed :
          Cell 01 - Address: 02:4A:46:68:69:21
                    Frequency:5.2 GHz (Channel 40)
                    Quality=48/70  Signal level=-62 dBm  
                    Encryption key:off
                    Bit Rates:400 Mb/s
                    ESSID:"FROST-Nidus-Setup"
```

Found one! Now that I detected it, I can also associate with it and obtain an IP address:

```sh
elf@10f3638f3d62:~$ iwconfig wlan0 essid FROST-Nidus-Setup   
** New network connection to Nidus Thermostat detected! Visit http://nidus-setup:8080/ to complete setup
(The setup is compatible with the 'curl' utility)
```

The network is nice enough to tell me how to configure it. Since I'm joined to the network, I can connect to `nidus-setup:8080` with curl as per instructions:

![Running curl](img/obj3/img1.png)


Uh oh. Well before I register I have to figure out exactly what the API wants from me. Thankfully it lists a meaningful API documentation page:

```sh
elf@10f3638f3d62:~$ curl http://nidus-setup:8080/apidoc  
◈──────────────────────────────────────────────────────────────────────────────◈

Nidus Thermostat API

◈──────────────────────────────────────────────────────────────────────────────◈

The API endpoints are accessed via:

http://nidus-setup:8080/api/<endpoint>

Utilize a GET request to query information; for example, you can check the
temperatures set on your cooler with:

curl -XGET http://nidus-setup:8080/api/cooler

Utilize a POST request with a JSON payload to configuration information; for
example, you can change the temperature on your cooler using:

curl -XPOST -H 'Content-Type: application/json' \
  --data-binary '{"temperature": -40}' \
  http://nidus-setup:8080/api/cooler


● WARNING: DO NOT SET THE TEMPERATURE ABOVE 0! That might melt important furniture

Available endpoints

┌─────────────────────────────┬────────────────────────────────┐
│ Path                        │ Available without registering? │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/cooler                 │ Yes                            │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/hot-ice-tank           │ No                             │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/snow-shower            │ No                             │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/melted-ice-maker       │ No                             │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/frozen-cocoa-dispenser │ No                             │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/toilet-seat-cooler     │ No                             │ 
├─────────────────────────────┼────────────────────────────────┤
│ /api/server-room-warmer     │ No                             │ 
└─────────────────────────────┴────────────────────────────────┘
```

I tried playing with all of the API paths, but as expected, the only one I could access was `/api/cooler` because otherwise I would need to register to access it them. Since all I wanted to do was to melt the frost off of the door, I simply checked the temperature...

```sh
elf@10f3638f3d62:~$ curl http://nidus-setup:8080/api/cooler
{
  "temperature": -39.87,
  "humidity": 93.38,
  "wind": 2.09,
  "windchill": -42.24
}
```

Then adjusted to be above freezing!

```sh
elf@10f3638f3d62:~$ curl -XPOST -H 'Content-Type: application/json' -d '{"temperature": 40}' http://nidus-setup:8080/api/cooler
{
  "temperature": 39.89,
  "humidity": 95.51,
  "wind": 1.45,
  "windchill": 42.63,
  "WARNING": "ICE MELT DETECTED!"
}
```

The door was officially open. But just for yuks I tried to see if I could register anyway:

```sh
elf@32e3893c1110:~$ curl http://nidus-setup:8080/register    
◈──────────────────────────────────────────────────────────────────────────────◈

Nidus Thermostat Registration

◈──────────────────────────────────────────────────────────────────────────────◈

Welcome to the Nidus Thermostat registration! Simply enter your serial number
below to get started. You can find the serial number on the back of your
Nidus Thermostat as shown below:

+------------------------------------------------------------------------------+
|                                                                              |
|                                                                              |
|                              ....'''''''''''''...                            |
|                         .'''...  ...............',,,'.                       |
|                     .''.        ........''',,,;;;;,'.',,'.                   |
|                  .,'.                   ......'',;;;;;;,.',;.                |
|                ',.l.                          ....'',;:::;:xl:,              |
|              ,,.                                  ....',;:cl:,,::            |
|            .,,                      ,::::,           ....';:cc:;cx,          |
|          .'  .                     :dkkkkd;             ...';:ccdc.;.        |
|         ..                                                ...';::c;.,'       |
|        '.                                                  ...';:c:;'.;      |
|       .                                                      ...,;::;,.;     |
|      ..                          ....'.'.'.''                 ...';::;'.,    |
|      .                          .. ';'.'..,..                  ...,;::;.;.   |
|     '                                ..  .. .                   ...,::;,.c   |
|     .                                                           ...';::;';.  |
|    '                                                             ...,;:;,.;  |
|    ,                              ...........                    ...,;:;;.c  |
|    ,      ...                     .  .....  .                   .;:l:;::;.l  |
|    ;      .x.                     ....   ....                   .:ccc;:;;.l  |
|    ,      ...                     ......... .                   ...',;;;,.c  |
|    '.                             ...... . ..                    ...,;;;'.,  |
|     ;                             .  .   ....                   ...',;;,.:   |
|     ;                             ...........                  ....',;,'.;   |
|      :                                                        ....',,,'.c    |
|      .,              ----->       xx.x..x.x.x                .....',,'.:.    |
|       ''                                                    .....',,'.:.     |
|        ',                ......'';oxxxxxxdc.              ......''''.:.      |
|         .:               ....'ldlx00KKKKXXXd.l;         ......',''..:.       |
|           ;,'              ...,;coO0000KKKO:...       .......',;lc:;         |
|            .l;                ....,;;;;;,'....... .........'''.'ol.          |
|              'o;..                .......................'',''lo.            |
|                .:o.                     ..................'kdc.              |
|                  .,c;.                     .............,cc'                 |
|                      ':c:'.              ..........';cc:.                    |
|                          .;ccc:;,'.........',;:cllc,.                        |
|                               ...,;;::::::;,'..                              |
|                                                                              |
|                                                                              |
|                                                                              |
|                                                                              |
+------------------------------------------------------------------------------+



  Serial Number: ______________________


             +------------+
             |   Submit   |
             +------------+

```

Since I needed to access the thermostat to obtain the serial (and I couldn't find it once I got inside anyway), and since it didn't look like there was an easy way to submit my registration via cURL, I had to walk away from this one. Oh well!

At least I got the door open!