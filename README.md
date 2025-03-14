# global-river-runner
Let's make a global river runner

# Use

The basic operation is to issue a GET request of the form:

```
https://your-river-runner-domain.com/processes/river-runner/execution?lat=<y>&lng=<x>
```

Performance is best if your request header includes `Accept-Encoding: gzip`  and `Accept: application/json`.

Some domain to keep in mind:

|Domain   | Version  | Behind Cloudfront?  |
|---|---|---|
|https://merit.internetofwater.app   | stable  | Yes  |
|https://merit-nldi.internetofwater.app   | stable  | No  |
|http://d1za2aav0xp6il.cloudfront.net  | latest  | Yes  |
|https://merit-dev-z3iqgg3uaa-uc.a.run.app  | latest  | No  |

# Back-end Deployment
Deployment requires an instance of [pygeoapi](https://pygeoapi.io) and postgres with PostGIS installed. 

The pygeoapi instance must include the [river-runner](https://github.com/webb-ben/pygeoapi/blob/river-runner/pygeoapi/process/river_runner.py) process as well as [several other modifications](https://github.com/geopython/pygeoapi/compare/master...webb-ben:river-runner).

We have prepared [docker images](https://hub.docker.com/r/webbben/pygeoapi-river-runner/tags) for both the latest and current stable versions of pygeoapi with the necessary modifications.

A copy of the hydrography database used is documented and available for download [here](https://www.sciencebase.gov/catalog/item/614a8864d34e0df5fb97572d).

## Cloud 
See the [deploy/cloud](deploy/cloud) directory for Dockerfiles and pygeoapi configurations necessary to deploy an appropriately configured pygeoapi container to the cloud service of your choice. Note the need to use environmental variables `URL` (your desired service URL for the pygeoapi base path), and `DBHOST`, `DBUSER`,`DBNAME`, `DBPASSWORD` (to connect to your database). The pygeoapi river-runner is designed to be a stateless application, so your database must be deployed separately. 

## Local
See the [deploy/local](deploy/local) directory for a docker-compose and pygeoapi configuration for a pygeoapi and postgis stack.
