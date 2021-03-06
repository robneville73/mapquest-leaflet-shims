# Mapquest-leaflet-shims

If you want to use MapQuest's Leaflet plugins with an Ember application (more specifically with ember-leaflet [http://www.ember-leaflet.com/]),
then you need to include MapQuest's leaflet plugin libraries (see https://developer.mapquest.com/documentation/leaflet-plugins/). Downloading these resources requires your specific
MapQuest API key to be passed and each library (maps [for tiles], geocoding, routing and traffic) need to be individually downloaded at run-time. To control this behavior, edit your config/environment.js file as follows:

```javascript
ENV.MapQuestAPI = {
    key: 'your_super_secret_api_key',
    map: 'true',        //default is 'true'
    geocoding: 'true',  //default is 'false'
    routing: 'true',    //default is 'false'
    traffic: 'true'     //default is 'false'
    version: '2.2'      //default is '2.2', this is the MapQuest API version number to use.
  };
```

To install into your project, simply run:

* `ember install mapquest-leaflet-shims`
* edit your environment.js file accordingly

To access in your code, use the global MQ object:


```javascript
let geocode = MQ.geocode(); //MQ is global
return new RSVP.Promise(function(resolve, reject) {
  geocode.search(locationObj)
    .on('success', function(e) {
      let bestMatch = e.result.best;
      resolve(bestMatch);
    });
});
```


 * see https://developer.mapquest.com/documentation/leaflet-plugins/geocoding/ for details on MQ's libraries
 * if you're not returning call in a promise-aware hook (i.e. model hooks), I highly recommend wrapping this stuff in ember-concurrency tasks (https://github.com/machty/ember-concurrency)

## Installation

* `git clone <repository-url>` this repository
* `cd mapquest-leaflet-shims`
* `npm install`
* `bower install`

## Running

* `ember serve`
* Visit your app at [http://localhost:4200](http://localhost:4200).

## Running Tests

* `npm test` (Runs `ember try:each` to test your addon against multiple Ember versions)
* `ember test`
* `ember test --server`

## Building

* `ember build`

For more information on using ember-cli, visit [http://ember-cli.com/](http://ember-cli.com/).
