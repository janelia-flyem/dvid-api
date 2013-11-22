## Media Types for DVID API

This repository holds descriptions of each non-standard Media Type (formerly known as MIME types)
supported by the DVID API.  

### Current Media Types

#### application/vnd.dvid-nd-data+json

N-dimensional images are transmitted as an application/octet-stream.  The layout of elements within the
data is specified by an **application/vnd.dvid-nd-data+json** Media Type, which is JSON as documented by 
the [nd-data specification](https://github.com/janelia-flyem/dvid-api/blob/master/nd-data.md).

