# realtimedashboardplatform
A Real Time Streaming Dashboard Platform using MQTT Protocol. You can create your own Real Time Streaming Dashboard using this platform. All you need is a MQTT broker, and a web server to host your html dashboard page.

Here is how it works. The dashboard.js file has all the code required to run your dashboard. We have created widgets that you can use on your dashboard.


Change these values to reflect your MQTT brokers in dashboard.js:
var ip = "m10.cloudmqtt.com"; // replace this value with your brokers IP address or domain name
var port = "37629"; // port number for your broker's web socket listening to. The dashboard platform will work only with websockets and
not with tcp.

And in this method, change the useSSL property:
function connectMQTT() {
    client = new Paho.MQTT.Client(ip, Number(port), id);
    client.onConnectionLost = onConnectionLost;
    client.onMessageArrived = onMessageArrived;
    client.connect({
        userName: username,
        password: password,
        useSSL: true, // if you are not using wss, change this property to false
        onSuccess: onConnect,
        onFailure: onFailure,
        reconnect: true
    });
}

To use a widget add these lines of code to your dashboard page:

 CreateWidget(
     {
         bindto: "widget-divid",
         datastream: "demo/piechart",
         type: "piechart",
         label: "",
         color: ['#00AA9F', '#018FBD', '#0066A4', '#00635A'],
         height: 200
      });

Below is the description of CreateWidget property:

         bindto: Here you specify where in the html page you want to bind the widget to. You specify the div id here.
         datastream: Specify to which topic this widget will bind or subscribe to on the MQTT broker
         (this is topic where the data for the widget will be published on the MQTT broker)
         type: Specify here what type of chart you want this widget to display on the dashboard.
         height: Specify the height of the widget
 
 <table>
 <tr>
  <td>Widget Type
  </td>
  <td>Message Format
  </td>
  <td>Widget on HTML
  </td>
 </tr>
 <tr>
  <td>piechart
  </td>
  <td>[['Fulfilled', 84], ['No Show',77],['Yet to Arrive', 89]]
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
  <td>[['Fulfilled', 84], ['No Show',77],['Yet to Arrive', 89]]
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

There is a sample demo page demo.html in the repository here:
