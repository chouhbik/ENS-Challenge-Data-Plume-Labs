# Spatiotemporal PM10 concentration prediction
## by Plume Labs

<img src="https://plumelabs.com/plume-labs-logo.png" align="middle" height="200">

## Challenge context
Plume Labs is a technology company providing air quality live data and forecasts to urban consumers and businesses. Our mobile app, the Plume Air Report, provides air quality levels around the world to consumers. Our personal air quality tracker Flow senses pollutants around you to help you avoid them at home and on the go – and crowdsource highly valuable hyperlocal maps in the process. Our global atmospheric pollution API gives businesses and academic teams an access to our unique AI-powered air quality forecasts data platform. Plume Labs is an MIT/Stanford start-up with a team of 25 in New York and Paris and raised $4.5M in seed funding to date.

## Challenge goals
In order to provide air quality forecasts, Plume Labs has built a unique database with readings collected by monitoring stations all over the world. The problem we submit consists in predicting the PM10 readings of some air quality monitoring stations using the readings provided by the monitoring stations nearby as well as urban features. For each PM10 reading in the training dataset, we will provide the following information:

1- Land-use characterization of the monitoring station location (i.e. is it located in a residential area, industrial area, …)

2- Readings at the closest monitoring stations The accuracy obtained by such a prediction model is a very good indicator of how an air quality prediction model performs in locations where there is no monitoring station

<img src="https://plumelabs.files.wordpress.com/2018/12/PRESS_Flow_and_App.jpg" align="middle" height="200">

## Data description
### Input variables
#### Land-Use features at the monitoring station
The land-use classification used is the following:

- **hdres:** high-density residential area
- **ldres:** low-density residential area
- **industry:** industrial area
- **urbgreen:** green area (mostly parks)

The number gives the radius of the area used to compute the feature (in meters). For example, industry_500 gives the share of industrial areas at less than 500 meters to this station. All features are comprised between 0 and 1

#### Roads features at the monitoring station
Two roads features are given:

- **roads_length:** length of all roads around
- **major_roads_length:** length of major roads around

The classification roads / major roads is based on OpenStreetMap classification. The number gives the radius of the area used to compute the feature (in meters). These features are normalized by the size of the area (hence, the unit is arbitrary). For example, roads_length_500 is proportional to the length of roads at less than 500 meters to this station.

#### Readings at the N closest monitoring stations

- **(value_0, …, value_9)** give the readings at the 10 closest monitoring stations, sorted by decreasing distance
- **(distance_0, …, distance_9)** give the distances to the 10 closest monitoring stations, sorted by decreasing distance

Only the stations forming the training dataset are used in this step. Some values may be nan, which means that the corresponding monitoring station did not return any value at this moment.

### Output variable
**The PM10 reading y.**

## Benchmark description
We propose a benchmark where the PM10 reading of a monitoring station is predicted using a weighted average of the readings provided by the stations nearby at the same time, with weights inversely proportional to the distance to the station.
