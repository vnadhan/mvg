# MVG: MultiViz Analytics Engine Client Library
<a href="https://pypi.org/project/va-mvg/">
<img src="https://badge.fury.io/py/va-mvg.svg" alt="Package version">
</a>
<img alt="PyPI - Python Version" src="https://img.shields.io/pypi/pyversions/va-mvg.svg?style=flat-square">

A Python library to interface the the **M**ulti**V**iz Analytics En**G**ine ('MVG')

* setup a session towards the vibium-cloud service

* interface the services by means of API calls. [API documentation](https://api.beta.multiviz.com/docs).

## Documentation

Usage of the library and several examples can be found [here](https://vikinganalytics.github.io/mvg/).
## Obtaining the library

```
pip install va-mvg
```

## Basic Usage

1. Create a session by instantiating a MVG object. A session is a combination
of an endpoint (server address) and a token. The token is used both for
authentication and authorization.
The token is provided by Viking Analytics.

2. Call the API functions

3. Errors are propagated via exceptions. It is up to the calling application
to handle error cases.

## Important Concepts

* endpoint: The server providing the analytics and data handling functions.
Represented by an URL. The endpoint is set when creating the session.

* source ID (sid): an identifier representing a measurement source,
typically a sensor. The sid is set on the client side and will be used
as a reference for the source and all information related to it
(e.g. measurements and analysis results).

* token: authentication and authorization token (to be provided by Viking
Analytics)

* meta information: additional information attached to sources or measurements.
For some analyses the meta information needs to contain specific key-value pairs,
but in general meta information is managed by the client side.
Meta information will be stored along the sources/measurements and can be
retrieved from the server side, even if it is not processed on the
server side. Example of meta information for a source
```python
{"sensor_type": "arduino",
 "location": "gearbox"}
``` 

* measurements: measurements is numerical data (typically a list of float values
representing sensor data) identified by the source ID (the sensor recording the
measurement) and the timestamp when the measurement was recorded. It is the
responsibility of the client side to convey source ID and timestamp to the server
side.

* features: features are the analytics functions supported by the server side.
An analytics function is invoked on a set of measurements by requesting
an analysis.

* analysis: an analysis applies a feature on a set of previously stored data.
To specify an analysis the feature, the data, and the parameters need to be
specified by the client side. Data needs to be available on the server.
All calls to analysis are asynchronous. So the flow is to (1) request an
analysis (2) poll for status (3) retrieve results when the analysis is completed.
Each analysis is assigned a unique ID (request_id). Completed analyses are stored
on the server side and can be retrieved by means of the jobid.
It is primarily the clients side's responsibility to keep track of analyses.

## Version handling of mvg and API version

The version string of the MVG API on the server side has the form
v{MAJOR}.{MINOR}.{PATCH}.
An increase of MAJOR means an incompatible change which requires an
upgrade of mvg, an increase in MINOR does not require an upgrade of
mvg, but may then not allow to access new features of the API. See mvg
documentation and examples/0-check_version.ipynb for details.

## Additional Documentation

* API documentation on mvg, autogenerated from mvg.py

### Examples

Under the examples section there are a number of jupyter notebooks
with Python code to show how to use the library for interfacing the
Viking Analytics Engine. The notebooks can be downloaded by 
clicking "View Page Source" link located on the top left of the
examples. You will need to change the extension to .ipynb before
running them.

### Analysis Classes (beta)

Analysis classes provide a simple and powerful way to parse and
inspect the results for analysis calls for our features.
Apart from converting the results to dataframes, 
they can be used in an interactive
shell to inspect the results from analysis calls.

In the directory anlysis_class_examples there are scripts for 
showing how to use the analysis classes. 

### Maintainer

Maintainer of the mvg library is Viking Analytics AB. <https://www.vikinganalytics.se>

### Bug Reporting, Pull request, and support ...

... please use the issue tracking and pull requests on 
https://github.com/vikinganalytics/mvg

### License

The mvg library is licensed under Apache License 2.0, see LICENSE file.
