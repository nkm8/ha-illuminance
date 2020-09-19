# Illuminance Sensor

Estimates outdoor illuminance based on current weather conditions and time of day. At night the value is 10. From a little before sunrise to a little after the value is ramped up to whatever the current conditions indicate. The same happens around sunset, except the value is ramped down. Below is an example of what that might look like over a three day period.

![Image of sensor history](images/illuminance_history.png)

The following sources of weather data are supported:

* Weather Underground
* [AccuWeather (symbol)](https://www.home-assistant.io/integrations/accuweather/)

Follow the installation instructions below.
Then add the desired configuration. Here is an example of a typical configuration:

```yaml
sensor:
  - platform: illuminance
    entity_id: weather.accuweather_home
```

## Installation

Place a copy of:

[`__init__.py`](custom_components/illuminance/__init__.py) at `<config>/custom_components/illuminance/__init__.py`  
[`sensor.py`](custom_components/illuminance/sensor.py) at `<config>/custom_components/illuminance/sensor.py`  
[`manifest.json`](custom_components/illuminance/manifest.json) at `<config>/custom_components/illuminance/manifest.json`

where `<config>` is your Home Assistant configuration directory.

>__NOTE__: Do not download the file by using the link above directly. Rather, click on it, then on the page that comes up use the `Raw` button.

## Configuration variables

* **api_key**: Weather Underground API key. Required when using WU.
* **entity_id**: Entity ID of AccuWeather entity. See examples below. Required when using AccuWeather.
* **name** (*Optional*): Name of the sensor. Default is `Illuminance`.
* **scan_interval** (*Optional*): Polling interval.  For non-WU configs only applies during ramp up period around sunrise and ramp down period around sunset. Minimum is 5 minutes. Default is 5 minutes.
* **query**: Weather Underground query. See [here](https://www.wunderground.com/weather/api/d/docs?d=data/index). Required when using WU.

## Examples

### AccuWeather Entity

AccuWeather can only be configured via the Integrations menu under Configuration in the Home Assistant UI

### Weather Underground

```yaml
sensor:
  - platform: illuminance
    name: WU Illuminance
    api_key: !secret wu_api_key
    query: !secret wu_query
    scan_interval:
      minutes: 30
```

## Caveats

Weather Underground no long provides free API keys. In fact, as of this writing they have notified that the REST API will be discontinued.

## Releases Before 2.1.0

See [here](https://github.com/pnbruckner/homeassistant-config/blob/master/docs/illuminance.md)
