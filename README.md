MMM-PublicTransportVVO


- **[MMM-PublicTransportVVO](https://github.com/ChristianGeie/MMM-PublicTransportVVO)** <br> Display live departures from public passenger transport service of the 'Verkehrsverbund Oberelbe' (VVO).


MMM-PublicTransportVVO is a module for the [MagicMirror](https://github.com/MichMich/MagicMirror) project by
[Michael Teeuw](https://github.com/MichMich).

It shows live public transport information for Verkehrsverbund Oberelbe (Germany) based on http://widgets.vvo-online.de api data.

You can enter a delay time for "How long does it take to get to my station?".
Then the module calculates the next reachable departures and draws all unreachable departures in a different style or color.

## Screenshot

The module looks like this:

![Example for Dresden, Hauptbahnhof with  delay of 5 minutes](img/MMM-PublicTransportVVO_screenshot1.png)
![Example for Dresden, Hauptbahnhof with  delay of 3 minutes](img/MMM-PublicTransportVVO_screenshot2.png)

## Installation

Just clone the module into your MagicMirror modules folder:

```
git clone https://github.com/ostfilinchen/MMM-PublicTransportVVO.git
```

## The `stationId`
You don't need the stationId absolutely. If you want to use the Id, you must do the following steps. But you can first try it with the stationname. Stationnames are for example Dresden Hauptbahnhof or Dresden Bahnhof Neustadt.

You can verify it with the url like:
```
http://widgets.vvo-online.de/abfahrtsmonitor/Haltestelle.do?hst=Dresden Hauptbahnhof
```
or
```
http://widgets.vvo-online.de/abfahrtsmonitor/Haltestelle.do?hst=Dresden Bahnhof Neustadt
```
If you get an answer from the webservice with your stationname, it's all fine and you can take this instead of the id.
So the parameter `stationId` is an object.

### How to get it

If you will use the `stationId` as an integer value for your module you have to do these steps. To get it open the browser and type: 
```
http://widgets.vvo-online.de/abfahrtsmonitor/Haltestelle.do?hst=
```
After the "=" you had to write the station like "Dresden Hauptbahnhof". You get an array and the last position shows you the stationId.

### How to verify it

```
curl http://widgets.vvo-online.de/abfahrtsmonitor/Haltestelle.do?hst=33000037
```
returns a array including station name, location and given `stationId`

## Configuration

The module quite configurable. These are the possible options:

|Option|Description|
|---|---|
|`name`|The name of the module instance (if you want multiple modules).<br><br>**Type:** `string`<br>**Default value:** `MMM-PublicTransportVVO`|
|`stationId`|The Name / ID of the station. How to get the ID for your station is described below.<br><br>**Type:** `string` or `integer`<BR>**Default value:** `33000037`<br> This value is **Required**.|
|`marqueeLongDirections`|Makes a marquee/ticker text out of all direction descriptions with more than 25 characters. If this value is false, the descriptions are trimmed to the station names. If the movement is not fluent enough for you, you should turn it off.<br><br>**Type:** `boolean`<br>**Default value:** `true`|
|`updateInterval`|How often the module should be updated. The value is given in milliseconds.<br><br>**Type:** `integer`<br>**Default value:** `30000` // 30 seconds|
|`hidden`|Visibility of the module.<br><br>**Type:** `boolean`<br>**Default value:** `false`|
|`delay`|How long does it take you to get from the mirror to the station? The value is given in minutes.<br><br>**Type:** `integer`<br>**Default value:** `10` // 10 minutes|
|`showTableHeaders`|Show the table headers with information about location and station name.<br><br>**Type:** `boolean`<br>**Default value:** `true`|
|`showTableHeadersAsSymbols`|Show the table headers as text or symbols.<br><br>**Type:** `boolean`<br>**Default value:** `false`|
|`colored`|should the departuretime shown red if the delay is reached<br><br>**Type:** `boolean`<br>**Default value:** `false`|
|`PercentOverDelay`|it's a Percent Value who is gave the `coloredtrafficlights`-Parameter the Value of yellow color.<br><br>**Type:** `integer`<br>**Default value:** `42` <br><br> Why 42? Because it's the answer of everything.|
|`coloredtrafficlights`|should the departuretime shown red, yellow or green. it shown red if the delay is reached, yellow if the delay + `PercentOverDelay` is reached. If its over delay + `PercentOverDelay` it shows green.<br><br>**Type:** `boolean`<br>**Default value:** `false`|
|`TimeOrMinutes`|Shows Departuretime in Minutes or Timeformat.<br><br>**Type:** `string`<br>**Default value:** `Minutes` <br>**Possible values:** `Minutes` or `Time`|
|`BreakPointTimeToMinutes`|Point when Departuretime is change from Time to Minutes<br><br>**Type:** `integer`<br>**Default value:** `30`|


Here is an example of an entry in `config/config.js`:

```javaScript
{
    module: 'MMM-PublicTransportVVO',
    position: 'top_right',
    config: {
        stationId: 33000313,
        hidden: false,
        delay: 0,
        updateInterval: 120000,
        marqueeLongDirections: false,
        showTableHeaders: true,  
        showTableHeadersAsSymbols: true,
    }
},
```

## Multiple Modules

Multiple instances of this module are possible. Just add another entry of the MMM-PublicTransportVVO module to the `config/config.js` of your mirror.

## Special Thanks

* [Michael Teeuw](https://github.com/MichMich) for the great tool and many others to build a MagicMirror.
* [Bangee44](https://github.com/Bangee44) for creating the [MMM-swisstransport](https://github.com/Bangee44/MMM-swisstransport) module, on which this one is heavily based.
* [ChristianGeie](https://github.com/ChristianGeie) for creating the [MMM-PublicTransportVVO](https://github.com/ChristianGeie/MMM-PublicTransportVVO) module, on which this one is heavily based.
* The community of [magicmirror.builders](https://magicmirror.builders) for help in the development process.

## Issues

If you find any problems, bugs or have questions, please [open a GitHub issue](https://github.com/ostfilinchen/MMM-PublicTransportVVO/issues) in this repository.
