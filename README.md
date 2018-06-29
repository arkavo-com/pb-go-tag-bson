# pb-go-tag-bson
Adds bson:"-" tag to XXX_ fields in .pb.go

This utility is useful if you insert structs generated from protocol buffers into MongoDB. 

Note: XXX_ fields were introduced in github.com/golang/protobuf v1.1.0

#### Before
```go
type Entity struct {
	Type                 string   `protobuf:"bytes,1,opt,name=type" json:"type,omitempty"`
	Id                   string   `protobuf:"bytes,2,opt,name=id" json:"id,omitempty"`
	XXX_NoUnkeyedLiteral struct{} `json:"-"`
	XXX_unrecognized     []byte   `json:"-"`
	XXX_sizecache        int32    `json:"-"`
}
```

#### After
```go
type Entity struct {
	Type                 string   `protobuf:"bytes,1,opt,name=type" json:"type,omitempty"`
	Id                   string   `protobuf:"bytes,2,opt,name=id" json:"id,omitempty"`
	XXX_NoUnkeyedLiteral struct{} `json:"-" bson:"-"`
	XXX_unrecognized     []byte   `json:"-" bson:"-"`
	XXX_sizecache        int32    `json:"-" bson:"-"`
}
```

## Install
`go get -u github.com/arkavo-com/pb-go-tag-bson` 

## Usage

`pb-go-tag-bson -dir /path/to/pbfiles`

/path/to/pbfiles is a directory that contains *.pb.go .  Recursively checks child directories.

`pb-go-tag-bson -dir /path/to/pbfiles -verbose`

Provides output of files analyzed and processed.