<!--- Copyright (c) 2016 Gordon Williams, Pur3 Ltd. See the file LICENSE for copying permission. -->
Infrared Record and Playback with Puck.js
============================================

* KEYWORDS: Tutorials,Puck.js,BLE,Bluetooth,LED,Light,Lightbulb,IR,Infrared
* USES: Puck.js,Web Bluetooth

This video shows you how to control Infrared devices using Puck.js.

[[http://youtu.be/et58ozE-Cu8]]

You'll need a [Puck.js](/Puck.js) and an (Infrared Receiver)[/IRReceiver]

Recording
---------

The code used in the video is:

```
digitalWrite(D2,0);
pinMode(D1,"input_pullup");
var d = [];
setWatch(function(e) {
  d.push(1000*(e.time-e.lastTime));
}, D1, {edge:"both",repeat:true});
```

You can also use the following to output the contents of the `d` array
rounded to 1 decimal place (which is much more readable):

```
console.log(d.map(a=>a.toFixed(1)).toString())
```

For the particular light bulb used in the video, the codes are as follows:

```
var commands = {
  off:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,1.7,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,0.6,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0],
  on:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0.5],
  white:[9.0,4.4,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0.5],
  red:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,1.7,0.5,0.6,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.6,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5],  
  green:[8,8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5],
  blue:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0.5],
  dim:[8.9,4.6,0.4,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,39.9,8.9,2.3,0.4,96.2,8.9,2.3,0.5],
  bright:[8.9,4.6,0.4,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5],
  flash:[8.9,4.6,0.4,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.4],
  fade:[8.9,4.8,0.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,0.6,0.5,0.6,0.5,1.8,0.5,0.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5,106.8,0.4]
};
```

Playback
--------

All you need to do to play back is to pass an array into `Puck.IR`. For example if you have
a lightbulb like the one I used, simply typing `Puck.IR(commands.on)` will turn it on.

You can also use Web Bluetooth to send data from a webpage to *any Puck* - it doesn't have
to be pre-programmed as the Web Page can send the code and data at once.

```HTML_demo_link
<html>
 <head>
  <style>
body {
  margin: 5%;
  background-color: #000;
}

table {
  width:100%;
  height:100%;
 table-layout: fixed;
}

td {
  background-color: #444;
  color: #fff;
  border: 2px solid white;
  border-radius: 5px;  
  font-size: 5vw;
  margin: 5px;
  text-align:center;
  cursor: pointer;
  user-select: none;
}
  </style>    
 </head>
 <body>
  <script>
var commands = {
  off:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,1.7,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,0.6,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0],
  on:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0.5],
  white:[9.0,4.4,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0.5],
  red:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,1.7,0.5,0.6,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.6,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5],  
  green:[8,8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5],
  blue:[8.9,4.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5,96.2,8.9,2.3,0.5],
  dim:[8.9,4.6,0.4,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,39.9,8.9,2.3,0.4,96.2,8.9,2.3,0.5],
  bright:[8.9,4.6,0.4,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,0.6,0.5,1.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.5],
  flash:[8.9,4.6,0.4,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,1.8,0.4,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,1.8,0.5,1.7,0.5,39.9,8.9,2.3,0.4],
  fade:[8.9,4.8,0.8,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.7,0.5,1.7,0.5,1.8,0.5,1.8,0.5,0.6,0.5,0.6,0.5,1.8,0.5,0.5,0.5,0.6,0.5,0.6,0.5,0.6,0.5,0.6,0.5,1.7,0.5,1.8,0.5,0.6,0.5,1.7,0.5,1.7,0.5,1.7,0.5,39.9,8.9,2.3,0.5,106.8,0.4]
};

function sendIR(array) {
  Puck.write('Puck.IR(['+array+']);\n')
}
  </script>
  <script src="https://www.puck-js.com/puck.js"></script>
  <table>
    <tr>
     <td onclick="sendIR(commands.on)">ON</td>
     <td onclick="sendIR(commands.off)">OFF</td>
     <td onclick="sendIR(commands.flash)">FLASH</td>
     <td onclick="sendIR(commands.fade)">FADE</td>
    </tr>
    <tr>
     <td></td>
     <td onclick="sendIR(commands.dim)">DIM</td>
     <td onclick="sendIR(commands.bright)">BRIGHT</td>
     <td></td>
    </tr>
    <tr>
     <td onclick="sendIR(commands.red)" style="background-color:red">RED</td>
     <td onclick="sendIR(commands.green)" style="background-color:green">GREEN</td>
     <td onclick="sendIR(commands.blue)" style="background-color:blue">BLUE</td>
     <td onclick="sendIR(commands.white)">WHITE</td>
    </tr>
  </table>
 </body>
</html>
```

Buying
------

You can buy the IR remote control lights like the ones I used from
[eBay](http://www.ebay.com/sch/i.html?_nkw=rgb+led+light+ir+remote+control&_sacat=0).
They are also available in strip form.

**Note:** while some of these lights look identical, they often use a different
set of control codes. About the only way to be sure is to record your own codes.