# application/vnd.dvid-nd-data+json

N-dimensional images are transmitted as an **application/octet-stream**.  The layout of elements within the
data (the schema) is specified by an **application/vnd.dvid-nd-data+json** Media Type, which is in
[JSON](http://www.json.org) as described below.


## Example of JSON 

The following is an example of a valid **application/vnd.dvid-nd-data+json** Media Type.  
Not all elements below are required.

```json
{
	"Axes": [
		{
			"Label": "X",
			"Resolution": 3.1,
			"Units": "nanometers",
			"Size": 100
		},{
			"Label": "Y",
			"Resolution": 3.1,
			"Units": "nanometers",
			"Size": 200
		},{
			"Label": "Z",
			"Resolution": 40,
			"Units": "nanometers",
			"Size": 400
		}
	],
	"Values": [
		{
			"DataType": "uint8",
			"Label": "intensity"
		}
	]
}
```

## Description of object

### "Axes"

#### Description

Specifies the dimensions of the image.  Order of the axes within the list specifies the ordering of the data.
The first object in the list corresponds to the dimension whose index varies most rapidly as we move through
the data bytes.  The second object in the list corresponds to the 2nd most rapidly changing index, and so on.
In the example above, the data would be traversed in the following way:

```c
uint8 *ptr = data;
for (z = 0; z < zsize; z++) {
	for (y = 0; y < ysize; y++) {
		for x = 0; x < xsize; x++) {
			use_uint8(*ptr);
			ptr++;
		}
	}
}
```

#### Objects

The "Axes" value is a list where each element of the list is an object with the following 
name/value pairs:

##### Label (string, required)

What to call this dimension.

##### Resolution (number, required)

The length of a voxel in this dimension.

##### Units (string, required)

The units of length of a voxel in this dimension.  Valid values are:

* nanometers
* micrometers
* millimeters

This list will be updated depending on required support by servers and clients. 
The larger we make this list, the more code is required to interconvert between the 
resolutions of arbitrary units.

##### Size (number, required)

The span of the image (i.e., the number of voxels) in this dimension.


### "Values"

#### Description

Specifies the interleaved values within on voxel of the n-D array.  For example, a RGBA image
would have four values, one for each of the colors and a fourth for the alpha channel.

#### Objects

The "values" value is a list where each element of the list is an object with the following 
name/value pairs:

##### DataType (string, required)

The fixed-size data type for the value.  Valid data types are:

* uint8
* int8
* uint16
* int16
* uint32
* int32
* uint64
* int64
* float32
* float64

##### Label (string, optional)

The name of this value.



