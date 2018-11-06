<p align="left"><a href="https://findarace.com" target="_blank"><img width="100" height="100" src="https://avatars1.githubusercontent.com/u/44780079?s=200&amp;v=4" alt="Linkit"></a></p>

# API (Beta)

Our beta event API allows you to access a json feed of our event data.

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
      
      ```
      https://findarace.com/api/events?qty=20
      ```
    </td>
  </tr>
  <tr>
    <td><code>fromDate</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>today</td>
    <td>
      Date to start returning results from<br>
      
      ```
      https://findarace.com/api/events?formDate=2018-01-01
      ```
    </td>
  </tr>
 </tbody>
</table>

Example response

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

The json response will always return a `data` property which is an array of the matching event objects and a `meta` property which is an object with information on the reqest `pagination`.

The following properties are available for every api request via the `meta.pagination` attribute:

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
    <td>Event date <code>ISO 8601</code></td>
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
    <td>
      Website and registration urls
      <code>
      {
        "website": "https://findarace.com",
        "regestration": "https://findarace.com/register"
      }
      </code>
    </td>
  </tr>
  <tr>
    <td><code>location</code></td>
    <td>Object</td>
    <td>
      Location information
      <code>
      {
        "text": "Winchester UK",
        "latitude": "54.55666",
        "longitude": "-1.6556556",
        "address": "100 High Street, Winchester, Hampshire SO23 9AH",
        "tags": Array[10][
          "100",
          "High Street",
          "Winchester",
          "Hampshire",
          "SO23 9AH",
          "England",
          "United Kingdom",
          "GB",
          "SO23",
        ]
      }
      </code>
    </td>  
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
    <td>
      Event orgainser info or false
      <code>
      ```
      {
        "name": "Organiser Name",
        "url": "https://findarace.com/organiser"
      }
      ```
      </code>
    </td>
  </tr>
  <tr>
    <td><code>tags</code></td>
    <td>Array</td>
    <td>Array of event tag strings</td>
  </tr>
 </tbody>
</table>

## Full example response

``` javascript
{
  "data": Array[1][
    {
      "title": "Worthing Beach Race",
      "shortTitle": "",
      "date": "2019-06-22T00:00:00+01:00",
      "url": "https://findarace.com/events/worthing-beach-race",
      "jsonUrl": "https://findarace.com/api/event/170260",
      "links": {
        "website": "https://gladiator-races.com/events/2019-worthing-beach/",
        "regestration": "https://endurancecui.active.com/event-reg/select-race?e=55328253"
      },
      "location": {
        "text": "Worthing Beach, West Sussex",
        "latitude": "50.80901850",
        "longitude": "-0.37108500",
        "address": "Worthing Beach, Marine Parade, Worthing, West Sussex, UK",
        "tags": Array[9][
          "41",
          "Marine Parade",
          "Worthing",
          "West Sussex",
          "England",
          "United Kingdom",
          "GB",
          "BN11 3PP",
          ""
        ]
      },
      "distances": Array[1][
        "10 km"
      ],
      "images": Array[1][
        "https://s3-eu-west-1.amazonaws.com/assets.findarace.com/Users/170256/Events/Worthing-Beach-Register-Now_180907_210920.png"
      ],
      "sports": Array[1][
        "obstacle-mud-running"
      ],
      "categories": Array[4][
        "10km",
        "6km-to-10km",
        "6-to-10-miles",
        "obstacle"
      ],
      "overview": "Join us in Worthing, West Sussex, for a 10k obstacle course packed out with 25+ world-class obstacles including sea entry (weather dependant. Join thousands of participants and help each other to finish the course. Finisher's medal, tech T shirt. Find out more online!",
      "organiser": {
        "name": "Gladiator Races",
        "url": "https://findarace.com/https-gladiator-races-com-"
      },
      "tags": Array[0][
        
      ]
    }
  ],
  "meta": {
    "pagination": {
      "total": 1,
      "count": 1,
      "per_page": 100,
      "current_page": 1,
      "total_pages": 1,
      "links": Array[0][
        
      ]
    }
  }
}
```
