# Content

## Tips
- DUMP or STORE is required to generate output
- Case Sensitivity
  - sensitive: relations, fields, function
  - insensitive: keywords

## Data Types
### relations, bags, tuples, fields
- a relation is a bag(outer bag)
- a bag is a collection of tuples
- a tuple is an oredered set of fields
- a field is a piece of data

获取field:
- positional notation(start with 0): e.g: $0 $1 $2
- name

获取complex data type:
- use dot to access the fields in the tuples

### Data Type
- Simple Types:
  - int
  - long
  - float
  - double
  - chararray
  - bytearray
  - boolean
  - datetime
  - biginteger
  - bigdecimal
- Complex Types:
  - tuple: (field [, field ...])
  - bag:
    - inner bag: {tuple [, tuple ...]}
    - outer bag
  - map: [key#value <, key#value ...>]

###