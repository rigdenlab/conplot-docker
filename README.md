# ConPlot: Online Analysis of Contact Plots

[![CI Status](https://travis-ci.com/rigdenlab/conplot.svg?branch=master)](https://travis-ci.com/rigdenlab/conplot)
![Docker Automated build](https://img.shields.io/docker/automated/filosanrod/conplot)

## About this repository

This repository contains the files required to compile a ConPlot's Docker image. You can visit ConPlot's main repository [here](https://github.com/rigdenlab/conplot).


## How to use this image


ConPlot is a web-based application that can be used [here](http://www.conplot.org). Alternatively, it is also possible to use ConPlot locally on your personal machine using the Docker image provided at this [DockerHub repository](https://hub.docker.com/r/filosanrod/conplot). First, pull the latest image as follows:


```bash
$   docker pull filosanrod/conplot:latest
```

You will also need a REDIS instance running on your machine. You can use the latest Docker image and start a container as follows:

```
$   docker run --name redis_db -d redis:latest
$   docker run --name conplot_app --link redis_db:redis -e KEYDB_URL="redis://redis_db:6379" -p 80:80 -d filosanrod/conplot:latest gunicorn app:server --preload --workers=6 --timeout 120 --graceful-timeout 120 --max-requests 5 --log-level=info -b :80
```
Note that the last command will also link the REDIS DB instance to ConPlot app container. After you set up running the multiple docker containers, you will be able to access the app on `http://0.0.0.0:80/home`.

