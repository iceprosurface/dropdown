## Dropdown Options

|Name|Type|Default|Description|
|:-:|:-:|:-:|:-:|
|text| String | button | Button text |
|disabled| Boolean | false||
|autoBlur| Boolean | true | Auto blur when select item|
|list| Array | [] | Data need to display|

## Dropdown Event

|Name|Arguments|Description|
|:-:|:-:|:-:|
|focus| () ||
|blur| () ||
|select| ({ item: Object, index: Number, next: Function}) |If autoBlur was false, next function can toggle it|