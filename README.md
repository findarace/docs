<p align="left"><a href="https://findarace.com" target="_blank"><img width="100" height="100" src="https://avatars1.githubusercontent.com/u/44780079?s=200&amp;v=4" alt="Linkit"></a></p>

# API (BETA)

Our beta event API allows you to access a json feed of our event data.

Currently the following endpoint is setup for swimming events:

# Events Endpoint

Request all event types.
```
https://findarace.com/api/events
```

Or restrict by one or more types (supply multiple types as a comma seperated list).
```
https://findarace.com/api/events/running
https://findarace.com/api/events/swimming,swimrun
https://findarace.com/api/events/road-cycling,mountain-biking
```
Current Event Types
`running` `obstacle-mud-running` `endurance-running` `road-cycling` `mountain-biking` `triathon` `duathlon` `aquathlon` `multisport` `swimming` `swimrun` `adventure-race` `childrens` 


This endpoint also accepts the following (GET or POST) parameters

`qty`<br>
Description: Quantity to return on each page (results are paginated by default)<br>
Format: Integer<br>
Default: `50`<br>
Max: `100`<br>
Example: `https://findarace.com/api/events/running?qty=20`<br>

`fromDate`<br>
Description: Date to start returning results from.<br>
Format: String `YYYY-MM-DD`<br>
Default: today<br>
Example: `https://findarace.com/api/events/running?formDate=2018-01-01`<br>

``` json
{
  "meta": [
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

The json response will return a `data` property which is an array of the mathcing events and a `meta` property which is an object with info on the reqest:

`total` The total number of events found.
`count` Number of events on this page.
`per_page` Number of events returned per page.
`total_pages` Total number of results pages
`links.previous` Link to the previous page (if it exists).
`links.next` Link to the next page (if it exists).

# Event Endpoint

JSON Response

```
"title": "The Monthly Mile South Shields - November",
      "shortTitle": "",
      "date": "2018-11-07T00:00:00+00:00",
      "url": "https://findarace.com/events/the-monthly-mile-south-shields-november",
      "jsonUrl": "https://findarace.com/api/event/44814",
      "links": {
        "website": "http://runeatsleep.co.uk/themonthlymile/",
        "regestration": ""
      },
      "location": {
        "text": "South Shields, South Tyneside",
        "latitude": "54.99406430",
        "longitude": "-1.41167840",
        "address": "The New Crown, South Shields. NE33 3NG",
        "tags": Array[10][
          "8",
          "Coast Road",
          "Coast Rd",
          "South Shields",
          "Tyne and Wear",
          "England",
          "United Kingdom",
          "GB",
          "NE33",
          ""
        ]
      },
      "distances": Array[1][
        "1 mile"
      ],
      "images": Array[0][
        
      ],
      "sports": Array[1][
        "running"
      ],
      "categories": Array[3][
        "1km-to-5km",
        "1-mile-or-less",
        "road"
      ],
      "overview": "A Wednesday evening one mile run in South Shields, Tyne and Wear. The 1 mile distance is not raced too often anymore (especially on roads), and we hope this challenging race distance is enjoyable for all levels of runner. Registration in The New Crown, South Shields. North East Running Project of the Year Award",
      "organiser": false,
      "tags": Array[0][
        
      ]
```
