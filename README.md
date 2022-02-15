# Under One Roof JSON Schema

This repository tracks the [JSON Schema](https://json-schema.org/) document used to validate property feeds.

## How to use

To validate against this schema you can choose one of the implementations for your language of choice and refer to `schema.json` to validate against.

Optionally a Python implementation using [jsonschema](https://github.com/Julian/jsonschema) is included in this repo.

To use the Python implementation simply clone this repository, and install the dependencies:

```
pipenv install
```

An example data file called `properties.json` has been included to validate against `schema.json`.

To validate via the CLI:

```
pipenv run jsonschema -i properties.json schema.json
```

Any validation errors will be listed in the output. If there are no errors nothing will be returned.

For more descriptive info you can format the output. E.g.

```
$ pipenv run jsonschema -i properties.json schema.json -o pretty
===[ValidationError]===(properties.json)===

110.0 is not of type 'integer'

Failed validating 'type' in schema['properties']['data']['items']['properties']['price']:
    {'description': 'Price in Pound Sterling. No spaces or commas.',
     'examples': [1100000],
     'id': '#price',
     'title': 'Price',
     'type': 'integer'}

On instance['data'][0]['price']:
    110.0
-----------------------------
```

A successful validation will be confirmed when invalidations have been corrected:

```
$ pipenv run jsonschema -i properties.json schema.json -o pretty
===[SUCCESS]===(properties.json)===
```

Programmatic validation can also be performed for more detailed handling. Please refer to the [jsonschema docs](https://python-jsonschema.readthedocs.io/en/stable/).