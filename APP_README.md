The app was concieved using Android Studio 3.4.1
You can find in the attached folder "Classroom Wifi" the entirety of the project.

The app targets Android API level 28 but is compatible with Android since API level 14.
It uses the PermissionManager library created by karanchuri : https://github.com/karanchuri/PermissionManager/blob/master/LICENSE.md

To summarize how the app works in a few words, for a specific position (a row and a column number) it makes measurements of the 
surrounding Wifi routers. When measuring, the results are temporarilly written in a csv file on the mobile phone. Then at the end of 
the measurements, all the results are transferred to a web server.


Here is a more complete explanation of the process :

On the launch of the app, the onCreate method sets the GUI, request the required permissions and finally calls the measurementInit 
method that sets the BroadcastReceiver required to collect the results from the measurements.

When the user presses Start, the clickButtonStart method begins by checking that the location is enabled, updates the GUI and write 
in the csv file the position the user did put. It then launches a unique scan to determine the duration this takes. Indeed this 
duration depends on the type of hardware uses to manage Wifi and is different for almost every type of mobile phone.
It then launches a thread that start by a synchronisation. The aim of the app being to create a map of different measurements of 
Wifi at differents places for a same time, the differents users of the app must but synchronised in their measurements. I used for 
that the currentTimeMillis method that returns an absolute time in numbers of second since the epoch. The app will wait that this 
number of seconds is a multiple of 32 before continuing. A second thread will then launch a cyclic measurement with a 32 seconds 
period (limitation due to Android 9.0). This way, a user can start the measurement at any time and thanks to the synchronisation 
it will always join the 32 seconds period. After each scan, the data are written in the csv file with as header the time of scan 
and the number of routers scanned.

Finally when the user press the Stop button, the clickButtonStop method will launch the upload of the data. The csv file will be 
read and send to a web server via HHTP POST request.



To finish, I noticed that even with the process of synchronisation there can still be a small difference between the different 
times of measurements and I don't understand where this small delay (maximum one or two seconds) comes from.
