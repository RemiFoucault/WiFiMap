# WiFiMap
This project aim to create an interractive map of a room using RSSI from surrounding WiFi signals.
The map is a grid of various size.
The project is composed of two parts :
  - An Android App that makes the measurements for one cell of the map and send them to a web server
  - A Java software that reads all the measurements and create a heat map of the room

The map is interractive since moving according to time. You can select a router and then see the heat map of the room for this router and for a precise time.
