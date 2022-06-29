# JSON Specifications

This repository contains the message specifications, which are used in the kosmos project. The file contains
als a possible way to generate the cryptographical signatures. The definition of the layout, on which the
signatures are made, will also be defined.

## Table of Contents
- [Signatures](#signatures)
    - [Layout](#layout)
    - [Example](#example)
- [Checks](#checks)
- [Structure](#structure)

## Signatures
In this chapter the handling of the signatures is described. 

### Layout

In this subchapter we describe the layout on which the signature will be generated. The same layout
has to be used to verify the data. 

In the root level of every message the `body` field exists. This field is used to generate the signature. It is important to note that the JSON has to be recursively sorted according to the keys. This way we ensure that (using the same private key) the same signature is generated every time. This is necesssary since we sign the string of a JSON not the JSON itself.

The signature field then consists of the field `signature`containing the signature itself and the field `meta`. The `meta`field contains information about the time of the signature, the algorithm used as well as the `serialNumber`field which can be used to query the corresponding certificate from Vault to verify the signature.

### Example

```json
"signature": {
    "signature": "fQqO/l1Qzw7Cdg6lgOb/6BISVSoH/2VVup3GBy9uafaKu3zTyOJeGZno6uUWigjvxpXs+mForOv2n7GA80cw/IssS236dJrHLG9ZcfbZPRU7ylcFNzMTS3tMpkSmH0i398HFMrP/t4VxDrEzQZgTfxz6YtrgvMFwTOXoP9dxAW4l7VPNqxIYXrIGSBWwoBqjW0VzAIsimVefGny58xDpRYA4AeqyjSx843faMCZ/r4aOK+dNysFLEscrwTtYUXsyaWeQLhb7DXgLeArXOTW9gK09+Bw8sqJgNWnZQzui2C/49NTn+z644/rpZp+oGt0U27a8mFgA/TKowdkJAqHKJQ==",
    "meta": {
      "date": "2021-04-15T14:41:10.608266+02:00",
      "algorithm": "RSA with PSS padding and SHA-256 hash",
      "serialNumber": "06:ff:9f:05:a7:19:97:f6:a0:f9:df:e6:e8:91:67:09:03:e6:1e:1d"
    }
}
```
## Checks

On this repository an automatic validation of the example and formal jsons is enabled. You can exeute
those test on a local system using the python tool `jsonschema`. To install this tool, please visit the 
webpage of [jsonschema](https://github.com/Julian/jsonschema).

## Structure

On the root level of this repository exists the directory `mqtt_payloads`
behind this every message type has his own folder. The following table shows
which directory on which mqtt topic is been used. The character `<` shows the
start of a variable and `>` the end of a variable.

| directory | mqtt topic |
| --------- | ---------- |
| analysis | `kosmos/analyses/<ContractId>` |
| blockchain | `kosmos/bc/<ContractId>` |
| contract-creation | `kosmos/contract/create` |
| contract-removal | `kosmos/contracts/delete` |
| data | ` kosmos/machine-data/<machineID>/sensor/<sensorID>/update` |
| ml-trigger | `kosmos/analytics/<model url>/<model tag>` |
