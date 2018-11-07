# EFK Stack example

This small repo contains a starting point to have up and running EFK stack. F stands for [FluentD](https://www.fluentd.org/). The rest of course is Elastic search and Kibana from [ELK](https://www.elastic.co/elk-stack) stack.
Why FluentD instaed of old good Logstash? FluentD is much more container friendly. 

###General

My intent was to create reliable and easy to setup stack, that can be run on any environment. Elastic search and Kibana are wrapped into docker container. Configuration actually highly flexible and can be changed. Both ES and Kibana version specified in the .env file to easily update it. 
FluentD has to be installed on the host environment to have access to logs. It also can be configured to forward logs andwhere.

###How to run

To run this project you need to have docker installed and td-agent (fluentd) installed. 

- Information about how to install fluentD agent can be found [here](https://docs.fluentd.org/v1.0/categories/installation)
- Information about how to setup docker can be found in the official [docs](https://docs.docker.com/)

FluentD has one not-included-by-default plugin for elastic search, more details [here](https://docs.fluentd.org/v1.0/articles/out_elasticsearch). 
As soon as you will have everything installed, you will have to build docker images and change fluentD config.
To run both Elastic search and Kibana, simply run `docker-compose up` and wait for a while so everything will be pulled and loaded. 
When you will run td-agetn for the first time, you will see path to the configuration in the logs. I hope you are reading logs)) Just replace default configuration with the one in the `fluentD/td-agent.conf`. Update it with proper sources and add normal paths to the logs. That's it.

###Contribute

As usual, create a PR for any improvements or bug fixes.
At this point, regex provided in the fluentD config is not working well with my apps logs. Feel free to update it. There is a really neat [app](http://fluentular.herokuapp.com/) for testing fluentD regexes. 
Also, agent configuration can be improved to support more sources.