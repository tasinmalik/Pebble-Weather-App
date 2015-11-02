// Pebble-Weather-App

var UI = require('ui');
// Create a Card with title and subtitle
var card = new UI.Card({
  title:'Weather',
  subtitle:'Fetching...'
});

// Display the Card
card.show();
var ajax = require('ajax');
// Construct URL
var cityName = 'Ann Arbor';
var URL = 'http://api.openweathermap.org/data/2.5/weather?q=' + cityName
          + '&appid=' + myAPIKey;
// Make the request
ajax(
  {
    url: URL,
    type: 'json'
  },
  function(data) {
    // Success!
    console.log('Successfully fetched weather data!');
  },
  function(error) {
    // Failure!
    console.log('Failed fetching weather data: ' + error);
  }
);
function(data) {
  // Success!
  console.log('Successfully fetched weather data!');

  // Extract data
  var location = data.name;
  var temperature = Math.round(data.main.temp - 273.15) + 'C';

  // Always upper-case first letter of description
  var description = data.weather[0].description;
  description = description.charAt(0).toUpperCase() + description.substring(1);
}
// Show to user
card.subtitle(location + ', ' + temperature);
card.body(description);
