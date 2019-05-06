

This  will give you a quick and easy way to add a NODEMCU to Apple's HomeKit on an iOS device. It opens up all sorts of possibilities including Scripts running on the server, combined with Apples HomeKit "Scenes", it makes for a powerful combo!

This is by no means a complete solution or ready for long term use but it demonstrates what's possible with a bit more work :)

Whats needed:

NODEMCU ( ESP8266 Module ) ,
Raspberry Pi or some other server ,
Solid State Relay or Normal relay with control circuit , 
Bread board - optional ,
Project Box ,
Some Time , 
iOS device ,
Extension Lead to carve up ,

Step 1: Setup the Server

This project requires the use of a server to run the HomeBridge software. I used a Raspberry Pi as I had it readily available but in theory anything that can run Node.Js should work!

You can follow this guide here to get this up and running on a Raspberry Pi. 

https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi

Once installed you need install a plugin and customise the config.json file

Step 2: Config and Plugins

Open your config.json file which should be in ~/.homebridge/config.json using your favourite text editor and add the following

{
  
 "bridge": {

"name": "Homebridge",

"username": "CC:22:3D:E3:CE:30",

"port": 51826,

"pin": "031-45-154"

},

"platforms": [

],

"accessories": [

{

"accessory": "Http",

"name": "Living Room Lamp",

"on_url": "http://NODEMCU_IP:80/LED=ON",

"off_url": "http://NODEMCU_IP:80/LED=OFF",

"http_method": "GET"

}

]

}

You will also need to install the homebride-http plugin. The HomeBridge software will make HTTP GET requests to the NODEMCU which will then turn the Solid State Relay on or off. The call looks like this:

http://NODEMCU_IP:80/LED=ON

http://NODEMCU_IP:80/LED=OFF

To install the plugin type:

sudo npm install homebridge-http or sudo npm install -g homebridge-http

Step 3: Setup the Solid State Relay and the NODEMCU

 1. Upload the code to the NODEMCU 
 
 2. Connect circuit as ：  
            NODEMCU GND --> Module pin - ,
            NODEMCU 3v3 --> Module pin +  ,
            NODEMCU D4 --> Module pin S 
            
 All usual warnings apply when dealing with 120/ 220 vdc - TAKE CARE.
 
Customise your IP address as needed.

This should now be ready for testing.

Launch homebridge on the server! ( Just open up a terminal and type "homebridge" if it give an error try typing "sudo Homebridge"

Step 5: Test!

Now that everything is in place its time to test!

Download Elgatu Eve from the App Store on you iOS device.

You should see Homebridge as an accessory available to be connected. Use the pin number 031-45-154, this can be customised in the config.json file.

Once connected you can move this around within the App into the desired Room etc. Give Siri a test! It should be able to control the relay using voice!

