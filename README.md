Summary
====

After buying VPS wondering to use VPS dry point Han, happened to cool the weather, wondering a script every day to remind myself the day's weather conditions. Download status reminder function is post-function, based on itchat built after the platform can be very convenient to add new features.



#itchat principle introduction

itchat is an open source WeChat personal interface, it can simulate the web-side WeChat landing. Thus using the Python script or command line mode to use personal micro-signal, to push the various notifications to the purpose of WeChat. Including pushing weather information, pushing all the dynamics on your server to your WeChat.


Overall design ideas
-------

The directory structure of the project is:

Robee:<br/>
│ bytime.py<br/>
│ chat_robot.py<br/>
│ check_aria2.py<br/>
│ LICENSE<br/>
└─│ weather.py<br/>


Where chat_robot is the main file, initializes itchat in the file, creates a process for each query script, and unifies itchat's send function to push the message.

Weather info (weather.py)
-------

China weather has three interfaces to obtain weather information data, but the information obtained in addition to the mobile interface to obtain the current temperature information is accurate, the other interface data are clearly inaccurate, so give up.

The final use of a well-known weather API, you can query the next few days the weather, air quality, life index, etc., to meet our basic needs.

Get the data for the json data, the api description of the reply to the json format also made a corresponding description. After finishing the data, the integration is returned to the sentence to be pushed.

Download dynamic push (check_aria2.py)
-------

I used the downloader for aria2, the downloader provides a set of json / rpc interface for the web interface to manage the default port for the 6800. But did not find the interface API, with the port for the packet capture itself to find api

http://ipaddress:6800/jsonrpc?tm=1504257059456

And with json format jsonrpc, id, method, params information.

Which tm item I observed is the corresponding operation, tm = 1504257059456 representative is to get the download has been stopped entry. Other tm values ​​can be viewed by the corresponding packet

In python simulation of the web side to send the format of the information, the information obtained to sort, you can get the current download complete the information.

Push film trends（film.py）
-------

design by beautifulsoup4，
There are many tutorials on the talk, to achieve the principle it's similar with download push .

Use Turing machine (tuling.py)
-------


Bring your own WeChat robot with Turing's API.People can chat with their own robots, but also quite interesting.

First in the itchat TEXT-type message in the registration function
Second, in this function, the incoming msg through the Turing api to get the results after the return can be

Custom message reply type (query_database.py)
-------

But because the Turing robot is still not smart enough, and sometimes can be said to answer is very intellectual barrier.

So in mysql to create a table, its internal only three variables, since the increase id, title and content.

After accepting the message, first through the query function database whether there is a similar statement, if any, then reply to the sentence, if not then to the Turing robot to reply.