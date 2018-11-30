# Real Time Streaming Dashboard Platform

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

Here is how it works. The dashboard.js file has all the code required to run your dashboard. We have created widgets that you can use on your dashboard. There is a sample dashboard named **demo.html** in the repository. Take a look at this file. It lists all the javascript and css files needed to run the dashboard. All these files are included in the repository and come with the download.


Change these values to reflect your MQTT broker's details in **dashboard.js**:

```
var ip = "m10.cloudmqtt.com"; // replace this value with your brokers IP address or domain name
var port = "37629"; // port number for your broker's web socket listener. The dashboard platform will work only with websockets and
not with tcp
usessl = true; // if you are connecting to wss protocol set this to true, else false for ws
```


## Building Dashboard Page

To use a widget, add these lines of javascript code to your dashboard page:

```
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
- datastream: Specify to which topic this widget will bind or subscribe to on the MQTT broker. When you publish data on to this topic, the widget will automatically get updated with the new data (this is the topic where the data for the widget will be published on the MQTT broker).
- type: Specify the type of chart you want this widget to display on the dashboard.
- height: Specify the height of the widget

 This platform currently supports the following widget types:
 
 

 <table>
 <tr>
  <td>Widget Type
  </td>
  <td>Sample Data Format for publishing to data to the widget
  </td>
 </tr>
 <tr>
  <td>piechart
  </td>
  <td>[['USA', 84], ['Europe',77],['Asia', 89]]
  </td>
 </tr>
 <tr>
  <td>gauge
  </td>
  <td>57
  </td>
 </tr>
  <tr>
  <td>barchart
  </td>
  <td>[['Product 1', 84], ['Product 2',77],['Product 3', 89]]
  </td>
 </tr>
   <tr>
  <td>card
  </td>
  <td>32
  </td>
 </tr>
 <tr>
  <td>currencycard
  </td>
  <td>100000
  </td>
 </tr>
 <tr>
  <td>simpletable
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
 </tr>
  <tr>
  <td>labeltext
  </td>
  <td>Your Label Text
  </td>
 </tr>
 <tr>
 <tr>
  <td>timeseries
  </td>
  <td>[ ['x', '2018-01-01 06:30:05', '2018-01-01 06:35:10', '2018-01-01 06:40:15', '2018-01-01 06:45:20'], ['USA', 55,78, 50, 94], ['International', 65,31, 46, 32] ]
  </td>
 </tr>
 </table>

There is a sample demo page demo.html in the repository here: https://github.com/sanjeshpathak/realtimedashboardplatform/blob/master/demo.html

Please look at the html page. Use this as a base or a templete to build your own dashboard page quickly and easily. This page contains all the Javascript and CSS files needed to build the dashboard.

View a real time dashboard live in action here: <http://rtsdp.eu5.org/dashboard/TestMosquittoOrgDashboard.html>. 

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

The repository has Java client source (MQTTDemo.java) files under Java directory. You can use this program to stream data to demo.html dashboard. It also contain jar file from Eclipse Paho MQTT Client library for Java (org.eclipse.paho.client.mqttv3-1.2.0.jar) under Java/lib folder. 

There is also a demo.jar file. You can directly run this program to stream data to demo.html dashboard. This program accepts three command line arguments: MQTTBrokerURL MQTTbrokerUsername and MQTTbrokerPassword.

```
> java -jar demo.jar tcp://brokerdomainname:port username password
```


You can also use MQTT Lens (https://chrome.google.com/webstore/detail/mqttlens/hemojaaeigabkbcookmlgmdigohjobjm?hl=en) a Google Chrome application that you can use to send data to MQTT Broker. You can use MQTT Lens to test your dashboard.

### HTTP API

Planning to build a HTTP API interface for publishing data to the dashboard. This REST API will convert from a HTTP POST to a MQTT publish. You can use this API to publish data to your dahboard. This is still a work in progress. This section will be filled soon.


## CreateWidget

Below is the description of the  CreateWidget function:

### Pie Chart

```
 CreateWidget(
     {
         bindto: "widget-divid", // div id in the dashboard page where you want the widget to be displayed
         datastream: "piecharttopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
         type: "piechart", // Pie Chart widget will be displayed on the dashboard
         label: "", // A label that appears below the Pie Chart
         color: ['#00AA9F', '#018FBD', '#0066A4', '#00635A'], // Specify Colors to be used for display on Pie Chart
         height: 200 // height of the Pie Chart to be dsiplayed on dashbaord (in Pixels)
      });
```

### Bar Chart

```
 CreateWidget(
     {
         bindto: "widget-divid", // div id in the dashboard page where you want the widget to be displayed
         datastream: "barcharttopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
         type: "barchart", // Bar Chart widget will be displayed on the dashboard
         color: ['#00AA9F', '#018FBD', '#0066A4', '#00635A'], // Specify Colors to be used for display for bars on Bar Chart
         height: 200 // height of the Pie Chart to be dsiplayed on dashbaord (in Pixels)
      });
```

### Gauge Chart

```
 CreateWidget(
     {
         bindto: "widget-divid", // div id in the dashboard page where you want the widget to be displayed
         datastream: "gaugetopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
         type: "gauge", // Gauge Chart widget will be displayed on the dashboard
         label: "Label for Guage Chart", // A label that appears below the Gauge Chart
         color_threshold_values: [40, 80, 100], // threshold values for displaying different colors
         color_pattern: ['#FF0000', '#F97600', '#60B044'] // Custom Colors for the above corresponding threshold
         height: 200 // height of the Pie Chart to be dsiplayed on dashbaord (in Pixels)
      });
```

### Card

```
 CreateWidget(
     {
         bindto: "widget-divid", // div id in the dashboard page where you want the widget to be displayed
         datastream: "cardtopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
         type: "card", // A Card widget will be displayed on the dashboard
         label: "label text", // This label appears inside the card
         color: ['#00AA9F'] // Specify Color to be used for background of the Card
      });
```

### Currency Card

```
 CreateWidget(
     {
         bindto: "widget-divid", // div id in the dashboard page where you want the widget to be displayed
         datastream: "cardtopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
         type: "currencycard", // A Currecny Card widget will be displayed on the dashboard
         label: "label text", // This label appears inside the card
         locale: "en-US", // Locale
         style: "currency",
         currency: "USD", // Currency Symbol to be displayed
         minimumFractionDigits: 0 //number of decimals
         threshold: 7500, // Threshold Value, if the displayed value execeeds this value, the background of the card changes to threshold_background_color color
         threshold_background_color: "#FF0000"
      });
```

### Alert Text

```
  CreateWidget(
      {
          bindto: "widget-divid",
          datastream: "alerttexttopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
          type: "alerttext" // When a new data is published to this widget, alert pop up window appears on the dashboard at widget-divid location on the dashboard
      });
```     
     
### Text Label

A text label is just a plain text. You can dynamically update the label on the dashboard.

```
  CreateWidget(
      {
          bindto: "widget-divid",
          datastream: "labeltexttopic", // topic of MQTT Broker where this widget will be listening to or getting the data from
          type: "labeltext" // The text published to this topic will be dynamically displayed at widget-divid location on the dashboard
      });
```

### Table

Using the simple table widget you can update each individual rows in the table separately. You can have as many rows (and as many columns) in the table as you want. Each row is bound to a topic.

```
  CreateWidget(
      {
          bindto: "widget-divid",
          type: "simpletable" // 
          datastream: ['firstrowtopic', // topic of MQTT Broker where this row will be listening to or getting the data
                       'secondrowtopic', // topic of MQTT Broker where this row will be listening to or getting the data from
                       'thirdrowtopic', // topic of MQTT Broker where this row will be listening to or getting the data from
                       'fourthrowtopic' // topic of MQTT Broker where this row will be listening to or getting the data from
                      ]								              ]
      });
```

