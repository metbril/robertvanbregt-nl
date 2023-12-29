---
title: "Simplify car wash sensor in Home Assistant"
slug: simplify-car-wash-sensor-in-home-assistant
date: 2023-12-29T12:55:47+01:00
author: Robert van Bregt
tags: ["home automation"]
categories:
  - Technology
  - Home Automation
---
For some years I have been using the [Car Wash custom component for Home Assistant][repo] to have an indication if it is a good idea or not to wash the family car. It's fairly simple. You define a weather sensor to use and you're done.

What the car wash sensor actually does, is check for unfavorable current or forecasted weather conditions, precipitation and temperatures.

Recently, Home Assisant changed [how weather forecasts are retrieved][hablog] and deprecated some functionality.

As a thought experiment and to simplify my setup, I replace the car wash entity with a simple template binary sensor helper.

The template is this:

```yaml
{% set entity_id = 'weather.buienradar' %}
{% set days_to_check = 4 %}
{% set freeze_temp = 0 %}
{% set unfavorable_conditions = ['fog', 'hail', 'lightning', 'lightning-rainy', 'pouring', 'rainy', 'snowy', 'snowy-rainy', 'exceptional'] %}
{% set forecast = state_attr(entity_id, 'forecast')[:days_to_check] %}
{% set conditions = [states(entity_id)] + forecast | map(attribute='condition') | list %}
{% set bad_condition = conditions | select("in", unfavorable_conditions) | list | length != 0 %}
{% set precipitation = forecast | map(attribute="precipitation") | select("greaterthan", 0) | list | length != 0 %}
{% set temps = [ state_attr(entity_id, 'temperature') ] + forecast | map(attribute="temperature") | list + forecast | map(attribute="templow") | list %}
{% set freezing = temps | select("lessthan", freeze_temp) | list | length != 0 %}
{{ bad_condition or precipitation or freezing }}
```

Additionaly, I have set the device type of the sensor to "Problem", so it will show an appropriate icon.

![](./car-wash.png)

[repo]: https://github.com/Limych/ha-car_wash/
[hablog]: https://www.home-assistant.io/blog/2023/09/06/release-20239/#weather-forecast-service