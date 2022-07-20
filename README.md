# Under One Roof - JSON Schema

This repository tracks the [JSON Schema](https://json-schema.org/) document used to validate property feeds.

## Branches

The `main` branch includes ALL files including `Pipfile`'s to provide a quick and convenient way to run schema validation using [jsonschema](https://github.com/Julian/jsonschema) (Python) on any changes made before committing. Instructions on how to use are included below.

The `release` branch contains only the files for distribution. These include:

- `properties.json` - Example json file to validate.
- `reference.md` - Schema reference documentation.
- `schema.json` - Schema to validate against.


## How to use  

A Python implementation using [jsonschema](https://github.com/Julian/jsonschema) is included in this repo for convenience. you can choose one of [the implementations](https://json-schema.org/implementations.html#validators) for your language of choice and refer to the relevant documentation.

To use the included Python implementation, simply clone this repository, and install the dependencies (requires [Pipenv](https://pipenv.pypa.io/en/latest/)):

```bash
pipenv install
```

An example data file called `properties.json` has been included to validate against `schema.json`.

To validate via the CLI:

```bash
pipenv run jsonschema -i properties.json schema.json
```

`pipenv run` activates the virtual environment with required dependencies.
`jsonschema` is the name of the [schema validator](https://github.com/Julian/jsonschema).
`-i properties.json` specifies a path to a JSON file to validate.
`schema.json` provides the schema to validate the JSON document against.

Any validation errors will be listed in the output. **If there are no errors nothing will be returned.**

For more descriptive info you can format the output. E.g.

```bash
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

```bash
$ pipenv run jsonschema -i properties.json schema.json -o pretty
===[SUCCESS]===(properties.json)===
```

Programmatic validation can also be performed for more detailed handling. Please refer to the [jsonschema docs](https://python-jsonschema.readthedocs.io/en/stable/).


## How to edit and create a release

Steps in making edits and a corresponding release:

1. Make changes to the schema on the `main` branch.
2. Validate the changes before committing using the above methods.
3. Ensure that the example `properties.json` file is updated to reflect the changes.
4. Update `schemaVersion` in `properties.json` to reflect the new release version.
5. Checkout the `release` branch.
6. Pull in the changes from `main` but only for `properties.json` and `schema.json`.

You can pull in changes to specific _files_ by specifying the paths:

```bash
git checkout main properties.json schema.json
```

7. Make any required updates to `reference.md` if the references require updating.
8. Commit the changes to the `release` branch.
9. Create a new tag on the `release` branch to reflect the new release version. E.g.

```bash
git tag v2.0.1
```

10. Push the changes to the remote repository and include all tags:

```bash
git push origin --tags
```

11. In the [Tags section](https://github.com/inhaus/uor-json-schema/tags) you should see the new tag listed in the repo.
12. In the [Release section](https://github.com/inhaus/uor-json-schema/releases) click "Draft new release".
13. Select "Target: release" as the branch.
14. Select the latest tag that has just been added.
15. Add release title and summary details in a style similar to previous releases.
16. Preview the release to ensure it's correct before clicking "Publish release".
17. The release should now be created. Download the assets file to check it contains the correct files (`properties.json`, `schema.json`, `reference.md`). There should not be any other files included.
18. If all is correct the Assets zip file can now be distributed.