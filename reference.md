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
- `trp` [int] [required] Tax on Real Property units. `0` accepted if not known.
- `summary` [string] Summary description of the property. HTML accepted.
- `description` [string] [required] Long description of the property. HTML accepted.
- `link` [string] [required] Fully-qualified URL of the property.
- `address` [object] Address of the property.
  - `line1` [string] First line of the address. Can be `null` if not known.
  - `line2` [string] Second line of the address. Can be `null` if not known.
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
  - `postcode` [string] [required] Postal code including a space. Can be `null` if postcode is confidential or unknown.
- `location` [object] Latitude and longitude coordinates.
  - `lat` [number] [required] Latitude coordinates. Floating point number or `null`.
  - `lon` [number] [required] Longitude coordinates. Floating point number or `null`.
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
  - `garage` [boolean] Does the property have a garage? Accepted values:
    - `true`
    - `false`
    - `null`
- `info` [array] [required] An array of strings for key property information. Array can be empty if none.
- `images` [array] [required] An array of objects for property images. Array can be empty if none. Accepted image formats: jpg|jpeg|webp|avif|png
  - `url` [string] [required] Fully-qualified URL of the image.
  - `description` [string] Description of the image.  `null` accepted.
  - `order` [int] Optional display order.
- `plans` [array] [required] An array of objects for property plans. Array can be empty if none.
  - `url` [string] Fully-qualified URL of the image. `null` accepted.
  - `description` [string] Description of the image.  `null` accepted.
- `brochure` [string] Fully-qualified URL of an associated property brochure.  `null` accepted.
