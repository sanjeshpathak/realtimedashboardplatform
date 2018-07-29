# realtimedashboardplatform

A Real Time Streaming Dashboard Platform using MQTT Protocol. You can create your own Real Time Streaming Dashboard using this platform. All you need is a MQTT broker, and a web server to host your html dashboard page. Infact you don't need a web server, you can open the dashboard page from your file system in a browser. This platform has been extensively tested on Chrome browser.

## MQTT Broker

You need a MQTT Broker for the dashboard platform to work. There are many open source and commercial MQTT Brokers available. One of the most popular open source broker is the Eclipse Mosquitto (<http://mosquitto.org/>). You can download, install it locally and and use it.

In case you do not want to host your own broker, there are brokers available publicly. Here's one hosted by Mosquitto project at <http://test.mosquitto.org/>

The page here lists some hosted MQTT brokers that you can use with limited free usage: <https://diyprojects.io/8-online-mqtt-brokers-iot-connected-objects-cloud/#.W11X4dIzZPY>

Here are some articles that explain what MQTT is all about:

- <https://internetofthingsagenda.techtarget.com/definition/MQTT-MQ-Telemetry-Transport>
- <https://en.wikipedia.org/wiki/MQTT>
- <http://mqtt.org/>

## dashboard.js

Here is how it works. The dashboard.js file has all the code required to run your dashboard. We have created widgets that you can use on your dashboard. There is a sample dashboard named demo.html in the repository. 


Change these values to reflect your MQTT broker's details in dashboard.js:

```sh
var ip = "m10.cloudmqtt.com"; // replace this value with your brokers IP address or domain name
var port = "37629"; // port number for your broker's web socket listener. The dashboard platform will work only with websockets and
not with tcp
usessl = true; // if you connecting to wss protocol set this to true, else false for ws
```

## Building Dashboard Page

To use a widget, add these lines of javascript code to your dashboard page:

```sh
 CreateWidget(
     {
         bindto: "widget-divid",
         datastream: "demo/piechart",
         type: "piechart",
         label: "",
         color: ['#00AA9F', '#018FBD', '#0066A4', '#00635A'],
         height: 200
      });
```

The CreateWidget function takes in an object literal as it's parameter with the following properties. Below is the description of the  CreateWidget function:

- bindto: Here you specify where in the html page you want to bind the widget to. You specify the div id here. This widget will automatically get placed in the div id element on the dashboard (html) page.
- datastream: Specify to which topic this widget will bind or subscribe to on the MQTT broker. When you publish data on to this topic, the widget will automatically get updated with the new data (this is topic where the data for the widget will be published on the MQTT broker).
- type: Specify the type of chart you want this widget to display on the dashboard.
- height: Specify the height of the widget

 This platform currently supports the following widget types:
 
 <table>
 <tr>
  <td>Widget Type
  </td>
  <td>Sample Data Format for publishing to data to the widget
  </td>
  <td>Widget on HTML
  </td>
 </tr>
 <tr>
  <td>piechart
  </td>
  <td>[['USA', 84], ['Europe',77],['Asia', 89]]
  </td>
  <td>
  </td>
 </tr>
 <tr>
  <td>gauge
  </td>
  <td>57
  </td>
  <td>
  </td>
 </tr>
  <tr>
  <td>barchart
  </td>
  <td>[['Product 1', 84], ['Product 2',77],['Product 3', 89]]
  </td>
  <td>
  </td>
 </tr>
   <tr>
  <td>card
  </td>
  <td>32
  </td>
  <td>
  </td>
 </tr>
 <tr>
  <td>currencycard
  </td>
  <td>100000
  </td>
  <td>
  </td>
 </tr>
 <tr>
  <td>simpletable
  </td>
  <td>
  </td>
  <td>
  </td>
 </tr>
 <tr>
  <tr>
  <td>alerttext
  </td>
  <td>Your Alert Text
  </td>
  <td>
  </td>
 </tr>
  <tr>
  <td>labeltext
  </td>
  <td>Your Label Text
  </td>
  <td>
  </td>
 </tr>
 <tr>
 <tr>
  <td>timeseries
  </td>
  <td>[ ['x', '2018-01-01 06:30:05', '2018-01-01 06:35:10', '2018-01-01 06:40:15', '2018-01-01 06:45:20'], ['USA', 55,78, 50, 94], ['International', 65,31, 46, 32] ]
  </td>
  <td>
  </td>
 </tr>
 <tr>
  <td>spline
  </td>
  <td>
  </td>
  <td>
  </td>
 </tr>
 </table>

There is a sample demo page demo.html in the repository here: https://github.com/sanjeshpathak/realtimedashboardplatform/blob/master/demo.html

Please look at the html page. Use this as a base or a templete to build your own dashboard page quickly and easily. This page contains all the Javascript and CSS files needed to build the dashboard.

## Publishing Data to the Dashboard

You can publish and stream data to the widget in two ways:

### MQTT Protocol

To publish data to the widget on the dashboard, publish the data (message format for each of the widget type is in the table above) on to the topic the widget is bound to. For example if you have a pie chart widget on the dashboard as:

```sh
 CreateWidget(
     {
         bindto: "widget-divid",
         datastream: "demo/piechart",
         type: "piechart",
         label: "",
         color: ['#00AA9F', '#018FBD', '#0066A4', '#00635A'],
         height: 200
      });
```

Publish the data to topic **demo/piechart** on to the broker. The data will be automatically routed to the widget and the new values appear in real time on the Pie Chart on the dashboard.


The Eclipse Foundation has a project for the development of MQTT Client libraries for various platforms. Eclipse Paho project provides open-source client implementations of MQTT Prptocol. Here is the home page for Eclipse Paho: <https://www.eclipse.org/paho/>. They have MQTT  client libraries for many languages like Java, Python, C# etc. Download the library of your choice. You can make use of the library to publish data to the MQTT Broker.



### HTTP API

Work in progress. This section will be filled soon.

