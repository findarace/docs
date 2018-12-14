<p align="left"><a href="https://findarace.com" target="_blank"><img width="100" height="100" src="https://avatars1.githubusercontent.com/u/44780079?s=200&amp;v=4" alt="Linkit"></a></p>

# Search Tools

Using our Search Tools we have made it easy to direct your users to a custom set of results on findarace.com.

## Some Examples

Our base events url:
```
https://findarace.com/events
```

Display 5km & 10km runs:
```
https://findarace.com/events?sports=running&categories=5km,10km
```

Display 5km & 10km runs in May 2019:
```
https://findarace.com/events?sports=running&categories=5km,10km&from=2019-05-01&to=2019-05-31
```

Display 5km & 10km runs in May 2019 within 20 miles of the findarace.com HQ:
```
https://findarace.com/events?sports=running&categories=5km,10km&from=2019-05-01&to=2019-05-31&location=SO239AH&radius=20
```

## Usage

Our events page accepts the following parameters to refine the search results.

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
    <td><code>sports</code></td>
    <td>Array / String</td>
    <td><code>any</code></td>
    <td>
      Filter results by sport
      <br><code>https://findarace.com/events?sports=running,triathlon</code>
      <br><a href="#sports-categories">Sport Categories</a>
    </td>
  </tr>
  <tr>
    <td><code>categories</code></td>
    <td>Array / String</td>
    <td><code>any</code></td>
    <td>
      Filter results by event categories
      <br><code>https://findarace.com/events?categories=10km,half-marathon</code>
      <br><a href="#event-categories">Event Categories</a>
    </td>
  </tr>
  <tr>
    <td><code>organisers</code></td>
    <td>Array / String</td>
    <td><code>any</code></td>
    <td>
      Filter results by organisers.
      <br><code>https://findarace.com/events?organisers=findarace</code>
    </td>
  </tr>
  <tr>
    <td><code>from</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>today</td>
    <td>
      Date to start returning results from
      <br><code>https://findarace.com/events?from=2018-01-01</code>
    </td>
  </tr>
  <tr>
    <td><code>to</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>any</td>
    <td>
      Date to show events until
      <br><code>https://findarace.com/events?to=2019-01-01</code>
    </td>
  </tr>
  <tr>
    <td><code>location</code></td>
    <td>String</td>
    <td>any</td>
    <td>
      Filter results by address
      <br><code>https://findarace.com/events?location=SO239AH</code>
    </td>
  </tr>
  <tr>
    <td><code>lat</code> <code>lng</code></td>
    <td>String<br><code>X.XXXXXXXXXX</code></td>
    <td>any</td>
    <td>
      Filter results by lat/lng
      <br><code>https://findarace.com/events?lat=57.32285750&lng=-4.42438170</code>
    </td>
  </tr>
  <tr>
    <td><code>radius</code></td>
    <td>Int</td>
    <td><code>25</code></td>
    <td>
      Radius used when filtering by location
      <br><code>https://findarace.com/events?location=London&radius=150</code>
    </td>
  </tr>
 </tbody>
</table>

> Multiple sports, event categories and organisers can be supplied as an array or comma seprated list of strings (for readability). 
> Location can be passed as lat/lng values or an address string with an optional radius value.


## Categories

Current list only subject to change.

### Sports Categories

`running` `obstacle-mud-running` `endurance-running` `road-cycling` `mountain-biking` `triathon` `duathlon` `aquathlon` `multisport` `swimming` `swimrun` `adventure-race` `childrens`

### Event Categories

`5km` `10km` `half-marathon` `marathon` `ultra` `enduro` `super-sprint` `sprint` `olympic` `half-ironman-70.3` `ironman` `pool` `sea` `lake` `river` `mountain-bike` `sportive` `audax-reliability-ride` `time-trial` `cyclocross` `road` `trail` `fell-running` `mountain-marathon` `obstacle` `extreme` `mountain`

Brought to you by [findarace.com](https://findarace.com) | &copy; Find a Race
Because doing sh*t makes you happy :)
