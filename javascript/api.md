<p align="left"><a href="https://findarace.com" target="_blank"><img width="100" height="100" src="https://avatars1.githubusercontent.com/u/44780079?s=200&amp;v=4" alt="Linkit"></a></p>

# findarace.com

This documention is available to help developers integrate with the findarace.com platform.

## Installation

To intialise our library include the following script within you header tags `<head>`:
``` html
<script src="https://js.findarace.com/v1/"></script>
```

You can enable debug mode or change the global namespace (far by default) used by including the following params:
``` html
<script src="https://js.findarace.com/v1/?debug=true&namespace=someNewNamespace"></script>
```

## Setting up conversion tracking (Arthur)

The following needs to be placed on the thank you page after a successful conversion, or called when a conversion happens. It's important that it is only called once per conversion.
``` html
<script type="text/javascript">
  far('conversion', {
    amount: 99.99,
    event: {
      uid: 'SOME-UID',
      name: 'Top Race',
      race: '10km'
    },
    participant: {
      name: 'Participant Name',
      email: 'participant@email.com',
    }
  });
</script>
```

## Conversion Object

A conversion requires the following attributes:

<table class="table" width="100%">
<thead>
  <tr>
    <th width="20%">Attribute</th>
    <th width="20%">Type</th>
    <th width="60%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>amount</code></td>
    <td>String</td>
    <td>The total value of the conversion <code>99.99</code></td>
  </tr>
  <tr>
    <td><code>event</code></td>
    <td>Object</td>
    <td>The event details, see the event object below</td>
  </tr>
  <tr>
    <td><code>participant</code></td>
    <td>Object</td>
    <td>The participant details, see the particpant object below</td>
  </tr>
 </tbody>
</table>

The event object requires the following attributes:

<table class="table" width="100%">
<thead>
  <tr>
    <th width="20%">Attribute</th>
    <th width="20%">Type</th>
    <th width="60%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>uid</code></td>
    <td>String</td>
    <td>A unique id / ref for your event, we recommend matching this to your site <code>SOME-UID</code></td>
  </tr>
  <tr>
    <td><code>name</code></td>
    <td>String</td>
    <td>The event booked <code>Top Race</code></td>
  </tr>
  <tr>
    <td><code>race</code></td>
    <td>String</td>
    <td>The race booked <code>10km</code></td>
  </tr>
 </tbody>
</table>
      
The participant object requires the following attributes:

<table class="table" width="100%">
<thead>
  <tr>
    <th width="20%">Attribute</th>
    <th width="20%">Type</th>
    <th width="60%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>name</code></td>
    <td>String</td>
    <td>The full name of the participant</td>
  </tr>
  <tr>
    <td><code>email</code></td>
    <td>String</td>
    <td>The email address of the particiapant</td>
  </tr>
 </tbody>
</table>


#
For support, if you have any questions or if you just want to chat please do get in touch at [hello@findarace.com](mailto:hello@findarace.com).

Brought to you by [findarace.com](https://findarace.com) | &copy; Find a Race
Because doing sh*t makes you happy :)
