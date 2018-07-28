# realtimedashboardplatform
A Real Time Streaming Dashboard Platform using MQTT Protocol. You can create your own Real Time Streaming Dashboard using this platform. All you need is a MQTT broker, and a web server to host your html dashboard page. Infact you don't need a web server, you can open the dashboard page from your file system in a browser. This platform has been extensively tested on Chrome browser.

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

To use a widget add these lines of javascript code to your dashboard page:

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
Below is the description of CreateWidget property:

         bindto: Here you specify where in the html page you want to bind the widget to. You specify the div id here. This widget will be placed in the div id position on the dashboard (html) page.
         datastream: Specify to which topic this widget will bind or subscribe to on the MQTT broker. When you publish data on to this topic, the widget will automatically get updated with the new data.
         (this is topic where the data for the widget will be published on the MQTT broker)
         type: Specify here what type of chart you want this widget to display on the dashboard.
         height: Specify the height of the widget
 
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

Please look at the html page. Use this as a base or a templete to build your dashboard page. This page contains all the Javascript and CSS files needed to build the dashboard.

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

Publish the data to topic demo/piechart to your MQTT Broker. Take a look at the format of the message to be published from the table above for Pie Chart. In this particular case we are published three slices or categories namely -- USA, Europe and Asia -- with values on the pie chart 84, 77 and 89 respectively.


### HTTP API

In the download we also provide a Node app. You can start the Node app.

