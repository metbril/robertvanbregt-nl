--- 
date:  2021-12-21T21:50:00+01:00
title: Coronadashboard in Home Assistant
description: ""
slug:  coronadashboard-in-home-assistant
authors: []
tags: [huisautomatisering, corona]
categories: [English, Technologie]
series: []
externalLink: ""
featured_image: Coronadashboard COVID-19 Rijksoverheid nl.png
---
The Dutch government provides a [Coronadashboard][coronadashboard] to the general public with statistics about the pandemic. It contains, among others, data on the vaccination rate and the number of contaminations. I wanted to know if it was possible to integrate a dashboard in my own Home Assistant instance.

After some searching I found that [the data is also available as a JSON feed][domoticz].

There is a feed for the whole country, one for each safety region and one for each municipality.

I'm interested in the nationwide statistics, but also in those for my local community.

## Find country feed

The feed for the whole country is simply available at https://coronadashboard.rijksoverheid.nl/json/NL.json.

## Find safety region feed

Each safety region ("*veiligheidsregio*") has it's own feed.

You can find the id by opening the regular [Coronadashboard][coronadashboard], scroll down and search for its name. The link for the page end with the id. For example, the link for Amsterdam-Amstelland is https://coronadashboard.rijksoverheid.nl/actueel/veiligheidsregio/VR13, so the id is `VR13`.

The feed for the safety region is available at `https://coronadashboard.rijksoverheid.nl/json/<id>.json`, where you need to replace `<id>` with the one you found.

The feed for Amsterdam-Amstelland is https://coronadashboard.rijksoverheid.nl/json/VR13.json.

## Find the feed for your municipality

Each municipality ("gemeente") has it's own feed.

You can find the id by opening the regular [Coronadashboard][coronadashboard], scroll down and search for its name. The link for the page end with the id. For example, the link for Amsterdam is https://coronadashboard.rijksoverheid.nl/actueel/gemeente/GM0363 so the id for Amsterdam is `GM0363`.

The feed for the municipality is available at `https://coronadashboard.rijksoverheid.nl/json/<id>.json`, where you need to replace `<id>` with the one you found.

The feed for Amsterdam is https://coronadashboard.rijksoverheid.nl/json/GM0363.json

# Get the data

First, you need to get the data. The resulting json file is big, so it's wise to only get it once and then pull all information from it within Home Assistant. The limit for a sensor states is 255 characters, so the data needs to be put into attributes.

I only get some specific attributes, to prevent filling up my database too quickly. Some attributes have data for almost 2 years now.

The feed is only updated daily, so there's no need to get it frequently. I decided to get it every hour nevertheless, since it's not always updated at the same time of day and I want to have the data as soon as possible.

```yaml
sensor:
  - platform: rest
    name: Coronadashboard Landelijk
    resource: https://coronadashboard.rijksoverheid.nl/json/NL.json
    method: GET
    scan_interval: 3600  # seconds; once per hour
    value_template: "OK"  # the default json would exceed 255 character limit
    json_attributes:
      - last_generated
      - difference
      - vaccine_coverage_per_age_group_estimated

  # GM0363 = Amsterdam
  # Search for yours at https://coronadashboard.rijksoverheid.nl/
  #
  - platform: rest
    name: Coronadashboard Lokaal
    resource: https://coronadashboard.rijksoverheid.nl/json/GM0363.json
    method: GET
    scan_interval: 3600  # seconds; once per hour
    value_template: "OK"  # the default json would exceed 255 character limit
    json_attributes:
      - last_generated
      - difference
      - vaccine_coverage_per_age_group
```

## Update sensors with data

After you have fetched the data, you can create template sensors with specific values from the results.

```yaml
template:
  - sensor:

      - name: "Vaccinatiegraad 18+ Landelijk"
        unit_of_measurement: "%"
        icon: mdi:needle
        attributes:
          last_generated: >
            {{ as_local(
                 state_attr('sensor.coronadashboard_landelijk',
                 'last_generated')
                 | as_datetime) }}
          updated: >
            {{ as_local(
                state_attr('sensor.coronadashboard_landelijk',
                'vaccine_coverage_per_age_group_estimated')
                ['last_value']
                ['date_unix']
                | as_datetime) }}
        state: >
          {{ state_attr('sensor.coronadashboard_landelijk',
            'vaccine_coverage_per_age_group_estimated')
            ['last_value']
            ['age_18_plus_fully_vaccinated']
          }}

      - name: "Positieve testen Lokaal"
        unit_of_measurement: "geteld"
        icon: mdi:test-tube
        attributes:
          last_generated: >
            {{ as_local(
                 state_attr('sensor.coronadashboard_lokaal',
                 'last_generated')
                 | as_datetime) }}
          updated: >
            {{ as_local(
                state_attr('sensor.coronadashboard_lokaal',
                'difference')
                ['tested_overall__infected_moving_average']
                ['old_date_unix']
                | as_datetime) }}
        state: >
          {{ state_attr('sensor.coronadashboard_lokaal',
           'difference')
            ['tested_overall__infected_moving_average']['old_value']
          }}

      - name: "Positieve testen per 100k Lokaal"
        unit_of_measurement: "geteld"
        icon: mdi:test-tube
        attributes:
          last_generated: >
            {{ as_local(
                 state_attr('sensor.coronadashboard_lokaal',
                 'last_generated')
                 | as_datetime) }}
          updated: >
            {{ as_local(
                state_attr('sensor.coronadashboard_lokaal',
                'difference')
                ['tested_overall__infected_per_100k_moving_average']
                ['old_date_unix']
                | as_datetime) }}
        state: >
          {{ state_attr('sensor.coronadashboard_lokaal',
           'difference')
            ['tested_overall__infected_per_100k_moving_average']['old_value']
          }}
```

[domoticz]: https://github.com/akamming/domoticz-coronadashboard
[coronadashboard]: https://coronadashboard.rijksoverheid.nl/
