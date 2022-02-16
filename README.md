# Under One Roof JSON Schema

This repository tracks the [JSON Schema](https://json-schema.org/) document used to validate property feeds.

## How to use

### Schema

To validate against this schema you can choose one of [the implementations](https://json-schema.org/implementations.html#validators) for your language of choice and refer to the relevant documentation. Use `schema.json` to validate your JSON document against. `properties.json` has been provided as an example.

### This repo

Optionally a Python implementation using [jsonschema](https://github.com/Julian/jsonschema) is included in this repo.

To use the Python implementation simply clone this repository, and install the dependencies (requires [Pipenv](https://pipenv.pypa.io/en/latest/)):

```
pipenv install
```

An example data file called `properties.json` has been included to validate against `schema.json`.

To validate via the CLI:

```
pipenv run jsonschema -i properties.json schema.json
```
`pipenv run` activates the virtual environment with required dependencies.    
`jsonschema` is the name of the [schema validator](https://github.com/Julian/jsonschema).    
`-i properties.json` specifies a path to a JSON file to validate.    
`schema.json` provides the schema to validate the JSON document against.    

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


---
## Schema Refrence

The following provides a quick reference to schema validation.

### Root

- `schema` [string] [required] Corresponds to schema version. No need to edit.
- `data` [array] [required] Array key for property data.


### Data

- `ref` [string] [required] Agent property reference or UUID. Must be unique. 
- `title` [string] [required] Title of the property. Plaintext only.
- `type` [string] [required] Transaction type. Accepted values: 
  - `sale`
  - `rent`
- `price` [int] [required] Price in Pound Sterling. No spaces or commas. If 'POA', set price to `0` and ensure that `priceOnApplication` is set to `true`.
- `priceOnApplication` [boolean] True if the property price is POA. False otherwise. Accepted values:
  - `true`
  - `false`
- `status` [string] [required] Availability status of the property. Accepted values:
  - `available`
  - `under offer` If type: sale
  - `sold` If type: sale
  - `let agreed` If type: rent
  - `let` If type: rent
- `instructionDate` [string] [required] The date the property was placed on the market. ISO 8601 format with optional timezone. E.g. `"2021-11-08T08:33:19+00:00"`.
- `market` [string] [required] Local or Open market. Accepted values: 
  - `local`
  - `open`
- `trp` [int] [required] Tax on Real Property units.
- `summary` [string] Summary description of the property. HTML accepted.
- `description` [string] [required] Long description of the property. HTML accepted.
- `link` [string] [required] Fully-qualified URL of the property.
- `address` [object] Address of the property.
  - `line1` [string] [required] First line of the address.
  - `line2` [string] Second line of the address.
  - `parish` [string] [required] Parish if Guernsey. 'Alderney' or 'Sark' otherwise. Accepted values: 
    - `Castel`
    - `Forest`
    - `St. Andrew`
    - `St. Martin`
    - `St. Peter Port`
    - `St. Pierre du Bois`
    - `St. Sampson`
    - `St. Saviour`
    - `Torteval `
    - `Vale`
    - `Alderney`
    - `Sark`
  - `island` [string] [required] Island of the Guernsey Bailiwick. Accepted values:
    - `Guernsey`
    - `Alderney`
    - `Sark`
  - `postcode` [string] [required] Postal code including a space. If postcode is confidential or unknown, set as `GY0 0ZZ`.
- `location` [object] Latitude and longitude coordinates.
  - `lat` [number] [required] Latitude coordinates. Floating point number.
  - `lon` [number] [required] Longitude coordinates. Floating point number.
- `features` [object] Property features.
  - `bedrooms` [int] [required] Number of bedrooms.
  - `bathrooms` [int] [required] Number of bathrooms.
  - `parking` [boolean] Does the property have parking? Accepted values:
    - `true`
    - `false`
    - `null`
  - `garden` [boolean] Does the property have a garden? Accepted values:
    - `true`
    - `false`
    - `null`
  - `garage`  [boolean] Does the property have a garage? Accepted values:
    - `true`
    - `false`
    - `null`
- `info` [array] [required] An array of strings for key property information.
- `images` [array] [required] An array of objects for property images.
  - `url` [string] [required] Fully-qualified URL of the image.
  - `description` [string] Description of the image.
- `plans` [array] [required] An array of objects for property plans.
  - `url` [string] [required] Fully-qualified URL of the image.
  - `description` [string] Description of the image.
- `brochure` [string] Fully-qualified URL of an associated property brochure.
