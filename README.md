# WiFiMap
This project aim to create an interractive map of a room using RSSI from surrounding WiFi signals.
The map is a grid of various size.
The project is composed of two parts :
  - An Android App that makes the measurements for one cell of the map and send them to a web server through HTTP
  - A Java software that reads all the measurements and create a heat map of the room

The map is interractive since moving according to time. You can select a router and then see the heat map of the room for this router and for a precise time.

I used a free online web server (http://ptsv2.com/) to record the HTTP request made from the app and then downloaded them as txt files so they could be used by the java softawe to create the map.
I would recommand to create a basic local web server on your network that receive the requests and transcribe them automatically into txt files.

You will find more informations about the app and the software in the two next folders.
