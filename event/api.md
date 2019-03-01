<p align="left"><a href="https://findarace.com" target="_blank"><img width="100" height="100" src="https://avatars1.githubusercontent.com/u/44780079?s=200&amp;v=4" alt="Linkit"></a></p>

# Event API (Beta)

Our Event API allows you to access a JSON feed of our event data.

## API Access

Our API is currently in private beta, to request access please do get in touch at [support@findarace.com](mailto:support@findarace.com).

# Usage

## Events

Request all events:
```
https://findarace.com/api/events
```

Or restrict by one or more event types:
```
https://findarace.com/api/events/running
https://findarace.com/api/events/swimming,swimrun
```

Supply multiple types as a comma seperated list:
```
https://findarace.com/api/events/road-cycling,mountain-biking,swimming
```

Current event types include `running` `obstacle-mud-running` `endurance-running` `road-cycling` `mountain-biking` `triathon` `duathlon` `aquathlon` `multisport` `swimming` `swimrun` `adventure-race` `childrens` 

Request a specific event by ID:
```
https://findarace.com/api/events/9999
```

This endpoint accepts the following parameters (GET or POST):

<table class="table" width="100%">
<thead>
  <tr>
    <th width="20%">Param</th>
    <th width="15%">Type</th>
    <th width="15%">Default</th>
    <th width="50%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>qty</code></td>
    <td>Integer<br>Max: <code>100</code></td>
    <td><code>50</code></td>
    <td>
      Quantity to return on each page, results are paginated by default<br>
      <code>https://findarace.com/api/events?qty=20</code>
    </td>
  </tr>
  <tr>
    <td><code>fromDate</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>today</td>
    <td>
      Date to start returning results from<br>
      <code>https://findarace.com/api/events?formDate=2018-01-01</code>
    </td>
  </tr>
 </tbody>
</table>

Example response:

``` javascript
{
  "data": [
    {
      "title": "Event Title",
      ...
    },
    {
      "title": "Another Event Title",
      ...
    },
  ],
  "meta": {
    "pagination": {
      "total": 9999,
      "count": 50,
      "per_page": 50,
      "current_page": 2,
      "total_pages": 200,
      "links": {
        "previous": "https://findarace.com/api/events/running?page=1"
        "next": "https://findarace.com/api/events/running?page=3"
      }
    }
  }
}
```

The JSON response will always return a `data` property which is an array of the matching event objects and a `meta` property which is an object with information on the request `pagination`.

The following properties are available for every API request and the `pagination` object contains the following properties:

<table class="table" width="100%">
<thead>
  <tr>
    <th width="20%">Property</th>
    <th width="15%">Type</th>
    <th width="65%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>total</code></td>
    <td>Integer</td>
    <td>The total number of events found</td>
  </tr>  
  <tr>
    <td><code>count</code></td>
    <td>Integer</td>
    <td>Number of events on this page</td>
  </tr>
  <tr>
    <td><code>per_page</code></td>
    <td>Integer</td>
    <td>Number of events returned per page</td>
  </tr>
  <tr>
    <td><code>total_pages</code></td>
    <td>Integer</td>
    <td>Total number of results pages</td>
  </tr>
  <tr>
    <td><code>links</code></td>
    <td>Object</td>
    <td>Link to the previous / next pages if either exists</td>
  </tr>
 </tbody>
</table>

## Event Object

An individual event is will have the following properties:

<table class="table" width="100%">
<thead>
  <tr>
    <th width="20%">Property</th>
    <th width="20%">Type</th>
    <th width="60%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>title</code></td>
    <td>String</td>
    <td>The event title</td>
  </tr>
  <tr>
    <td><code>shortTitle</code></td>
    <td>String</td>
    <td>The event short title</td>
  </tr>
  <tr>
    <td><code>date</code></td>
    <td>String</td>
    <td>
       Event date <code>ISO 8601</code>
    </td>
  </tr>
  <tr>
    <td><code>url</code></td>
    <td>String</td>
    <td>The findarace.com event url</td>
  </tr>
  <tr>
    <td><code>jsonUrl</code></td>
    <td>String</td>
    <td>The findarace.com API url</td>
  </tr>
  <tr>
    <td><code>links</code></td>
    <td>Object</td>
    <td>Website and registration urls</td>
  </tr>
  <tr>
    <td><code>location</code></td>
    <td>Object</td>
    <td>Location information</td>  
  </tr>
  <tr>
    <td><code>distances</code></td>
    <td>Array</td>
    <td>Array of distance strings</td>
  </tr>
  <tr>
    <td><code>images</code></td>
    <td>Array</td>
    <td>Array of image urls</td>
  </tr>
  <tr>
    <td><code>sports</code></td>
    <td>Array</td>
    <td>Array of sport type strings</td>
  </tr>
  <tr>
    <td><code>categories</code></td>
    <td>Array</td>
    <td>Array of event category strings</td>
  </tr>
  <tr>
    <td><code>overview</code></td>
    <td>String</td>
    <td>Full description of the event</td>
  </tr>
  <tr>
    <td><code>organiser</code></td>
    <td>Object / Boolean</td>
    <td>Event orgainser info or false if not an organiser</td>
  </tr>
  <tr>
    <td><code>tags</code></td>
    <td>Array</td>
    <td>Array of event tag strings</td>
  </tr>
 </tbody>
</table>

Example JSON response:

``` javascript
{
  "data": [
    {
      "title": "A Beach Race",
      "shortTitle": "",
      "date": "2019-06-22T00:00:00+01:00",
      "url": "https://findarace.com/events/a-beach-race",
      "jsonUrl": "https://findarace.com/api/event/23423",
      "links": {
        "website": "https://eventwebsite.com/events/name",
        "regestration": "https://abookingsite.com/event/5454545"
      },
      "location": {
        "text": "Winchester UK",
        "latitude": "54.55666",
        "longitude": "-1.6556556",
        "address": "100 High Street, Winchester, Hampshire SO23 9AH",
        "tags": [
          "100",
          "High Street",
          "Winchester",
          "Hampshire",
          "SO23 9AH",
          "England",
          "United Kingdom",
          "GB",
          "SO23"
        ]
      },
      "distances": [
        "10 km"
      ],
      "images": [
        "https://imageurl.com/image1.png",
        "https://imageurl.com/image2.png"
      ],
      "sports": [
        "obstacle-mud-running"
      ],
      "categories": [
        "10km",
        "6km-to-10km",
        "6-to-10-miles",
        "obstacle"
      ],
      "overview": "The full event description is here",
      "organiser": {
        "name": "Find a Races",
        "url": "https://findarace.com/far"
      },
      "tags": []
    }
  ],
  "meta": {
    "pagination": {
      "total": 1,
      "count": 1,
      "per_page": 100,
      "current_page": 1,
      "total_pages": 1,
      "links": []
    }
  }
}
```

Brought to you by [findarace.com](https://findarace.com) | &copy; Find a Race
Because doing sh*t makes you happy :)
