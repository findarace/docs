<p align="left"><a href="https://findarace.com" target="_blank"><img width="100" height="100" src="https://avatars1.githubusercontent.com/u/44780079?s=200&amp;v=4" alt="Linkit"></a></p>

# Event API (Beta)

Using our Search Tools we have made it easy to direct your users to a custom set of results on findarace.com.

## API Access

Our events page now accepts a load of query params to refine the search results, I’ve also run this by our SEO chap to determine if he requires any additional tracking parameters be included.

View all live events:
```
https://findarace.com/events
```


# Usage

## Events

Base events url:
```
https://findarace.com/events
```

Our events page accepts the following params (POST or GET) to refine the search results.

```
https://findarace.com/api/events/running
https://findarace.com/api/events/swimming,swimrun
```

Supply multiple types as a comma seperated list:
```
https://findarace.com/api/events/road-cycling,mountain-biking,swimming
```

Current event types include 

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
    <td colspan="4"><strong>Categories</strong><br>Can be supplied as an array or comma seprated list of strings (for readability). 
</td>
  </tr>
  <tr>
    <td><code>sports</code></td>
    <td>array, string</td>
    <td><code>any</code></td>
    <td>
      Filter results by sport<br>
      `running` `obstacle-mud-running` `endurance-running` `road-cycling` `mountain-biking` `triathon` `duathlon` `aquathlon` `multisport` `swimming` `swimrun` `adventure-race` `childrens`
    </td>
  </tr>
  <tr>
    <td colspan="4"><strong>Date</strong><br>Rahfgluidafgs dfgh  dfghsdfgjshdfgjk sdg sdfgjshdgljksdgf skjdfhgdks</td>
  </tr>
  <tr>
    <td><code>from</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>today</td>
    <td>
      Date to start returning results from<br>
      <code>https://findarace.com/events?from=2018-01-01</code>
    </td>
  </tr>
  <tr>
    <td><code>to</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>today</td>
    <td>
      Date to show events until<br>
      <code>https://findarace.com/events?to=2019-01-01</code>
    </td>
  </tr>
  <tr>
    <td colspan="4"><strong>Location</strong><br>Location can be passed as lat/lng values or an address string with an optional radius value.</td>
  </tr>
  <tr>
    <td><code>location</code></td>
    <td>String<br><code>YYYY-MM-DD</code></td>
    <td>today</td>
    <td>
      Date to show events until<br>
      <code>https://findarace.com/events?to=2019-01-01</code>
    </td>
  </tr>
 </tbody>
</table>


## Sports Categories



## Event Categories

`5km`, `10km`, `half-marathon`, `marathon`, `ultra`, enduro, super-sprint, sprint, olympic, half-ironman-70.3, ironman, pool, sea, lake, river,
mountain-bike, sportive, audax-reliability-ride, time-trial, cyclocross, road, trail, fell-running, mountain-marathon, obstacle, extreme, mountain

Brought to you by [findarace.com](https://findarace.com) | &copy; Find a Race
