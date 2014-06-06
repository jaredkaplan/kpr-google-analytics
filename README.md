Google Analytics Library for KPR
================================

This library provides a client API for use with Google Analytics Measurement Protocol. The Measurement Protocol is documented here:

https://developers.google.com/analytics/devguides/collection/protocol/v1

Getting Started
===============

This library can be imported into Kinoma Studio and added to an application's build path settings. To use the Google Analytics platform, you must create a Google Analytics account and then create a mobile app property to obtain a tracking ID that can be used with your application. Once you have a tracking code for your application, you use the API to send your tracking data to the Measurement Protocol service.

Example
-------

```javascript
// get a reference to the GoogleAnalytics module
var GA = require( "GoogleAnalytics" );

// create a new Tracker instance
var tracker = new GA.Tracker( "UA-12345678-9" );

// create info data to be collected for the tracking event
var appInfo = new GA.ApplicationInfoParams( "My Application", "com.mycompany.myapp", "1.0" );
var eventInfo = new GA.EventInfoParams( "startup", "init", "Initializing application" );
  
// send the tracking data to the Google Analytics service
tracker.send( GA.EVENT, appInfo, eventInfo );
```

API Reference
-------------

The following reference describes the Tracker API and the data info param classes that are defined in the *GoogleAnalytics* module.

###Tracker

The Tracker object is used to send tracking data to the Google Analytics service using the Measurement Protocol.

Creating a new instance of a *Tracker* object:

```javascript
var tracker = new GA.Tracker( trackingId, clientId, userId, userAgent, anonymize, useSalt );
```

Some data should only be configured once because it is sent with every request to the Google Analytics service. This data can be added to the tracker using the `addDefaults()` method.

```javascript
var params = new GA.ApplicationInfoParams( "My Application", "com.axlogic.myapp", "1.0" );

tracker.addDefaults( params );
```

Data is sent to the Google Analytics service using the tracker's `send()` method, by specifying a tracking hit type and a list of info param objects. The hit type must be one of the following constants from the *GoogleAnalytics* module:

* GoogleAnalytics.EVENT
* GoogleAnalytics.EXCEPTION
* GoogleAnalytics.TIMING
* GoogleAnalytics.SCREENVIEW
* GoogleAnalytics.PAGEVIEW
* GoogleAnalytics.TRANSACTION
* GoogleAnalytics.ITEM
* GoogleAnalytics.SOCIAL

```javascript
tracker.send( type, params, ... );
```

Convenience methods are also available for sending common tracking info for specific hit types. These methods create the appropriate info params object and call the tracker's send method. Additional params can also be specified as an array of info param objects for each call.

To send event tracking data:

```javascript
tracker.sendEvent( category, action, label, value, params );
```

To send exception tracking data:

```javascript
tracker.sendException( description, fatal, params );
```

To send timing tracking data:

```javascript
tracker.sendTiming( category, variable, time, label, params );
```

To send screenview tracking data:

```javascript
tracker.sendScreenview( screenName, linkId, params );
```

###SystemInfoParams

The SystemInfoParams object is used to configure the system information sent to the Google Analytics service.

Creating a new instance of a *SystemInfoParams* object:

```javascript
var params = new GA.SystemInfoParams( screenResolution, viewportSize, screenColors, userLanguage );
```

###ApplicationInfoParams

The ApplicationInfoParams object is used to configure the application information sent to the Google Analytics service.

Creating a new instance of a *ApplicationInfoParams* object:

```javascript
var params = new GA.ApplicationInfoParams( name, id, version, installerId );
```

###EventInfoParams

The EventInfoParams object is used to configure the event information sent to the Google Analytics service.

Creating a new instance of a *EventInfoParams* object:

```javascript
var params = new GA.EventInfoParams( category, action, label, value );
```

###ContentInfoParams

The ContentInfoParams object is used to configure the content information sent to the Google Analytics service.

Creating a new instance of a *ContentInfoParams* object:

```javascript
var params = new GA.ContentInfoParams( screenName, linkId );
```

###TimingInfoParams

The TimingInfoParams object is used to configure the timing information sent to the Google Analytics service.

Creating a new instance of a *TimingInfoParams* object:

```javascript
var params = new GA.TimingInfoParams( screenName, linkId );
```

###ExceptionInfoParams

The ExceptionInfoParams object is used to configure the exception information sent to the Google Analytics service.

Creating a new instance of a *ExceptionInfoParams* object:

```javascript
var params = new GA.ExceptionInfoParams( description, fatal );
```

###CustomDimensionInfoParams

The CustomDimensionInfoParams object is used to configure the custom dimenstion information sent to the Google Analytics service.

Creating a new instance of a *CustomDimensionInfoParams* object:

```javascript
var params = new GA.CustomDimensionInfoParams( index, value );
```

###CustomMetricInfoParams

The CustomMetricInfoParams object is used to configure the custom metric information sent to the Google Analytics service.

Creating a new instance of a *CustomMetricInfoParams* object:

```javascript
var params = new GA.CustomMetricInfoParams( index, value );
```

###SessionInfoParams

The SessionInfoParams object is used to configure the session information sent to the Google Analytics service.

Creating a new instance of a *SessionInfoParams* object:

```javascript
var params = new GA.SessionInfoParams( status );
```