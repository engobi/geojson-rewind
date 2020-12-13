# geojson-rewind

![Run tests](https://github.com/chris48s/geojson-rewind/workflows/Run%20tests/badge.svg?branch=master)
[![codecov](https://codecov.io/gh/chris48s/geojson-rewind/branch/master/graph/badge.svg?token=0WGM3W8ULH)](https://codecov.io/gh/chris48s/geojson-rewind)
![PyPI Version](https://img.shields.io/pypi/v/geojson-rewind.svg)
![License](https://img.shields.io/pypi/l/geojson-rewind.svg)
![Python Compatibility](https://img.shields.io/badge/dynamic/json?query=info.requires_python&label=python&url=https%3A%2F%2Fpypi.org%2Fpypi%2Fgeojson-rewind%2Fjson)

A Python library for enforcing polygon ring winding order in GeoJSON

The [GeoJSON](https://tools.ietf.org/html/rfc7946) spec mandates the [right hand rule](https://tools.ietf.org/html/rfc7946#section-3.1.6):

> A linear ring MUST follow the right-hand rule with respect to the area it bounds, i.e., exterior rings are counterclockwise, and holes are clockwise.

This helps you generate compliant Polygon and MultiPolygon geometries.

## Installation

```
pip install geojson-rewind
```

## Usage

```py
>>> input = {
...     'geometry': {   'coordinates': [   [   [100, 0],
...                                            [100, 1],
...                                            [101, 1],
...                                            [101, 0],
...                                            [100, 0]]],
...                     'type': 'Polygon'},
...     'properties': {'foo': 'bar'},
...     'type': 'Feature'}
>>> from geojson_rewind import rewind
>>> output = rewind(input)
>>> import pprint
>>> pp = pprint.PrettyPrinter(indent=4)
>>> pp.pprint(output)
{   'geometry': {   'coordinates': [   [   [100, 0],
                                           [101, 0],
                                           [101, 1],
                                           [100, 1],
                                           [100, 0]]],
                    'type': 'Polygon'},
    'properties': {'foo': 'bar'},
    'type': 'Feature'}
```

## Acknowledgements

`geojson-rewind` is a python port of Mapbox's javascript [geojson-rewind](https://github.com/mapbox/geojson-rewind) package. Credit to [Tom MacWright](https://github.com/tmcw) and [contributors](https://github.com/mapbox/geojson-rewind/graphs/contributors).
