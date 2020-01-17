package main

import "fmt"

func main() {
	fmt.Printf("hello, world\n")
}


name it as sample.go

C:\Ticer > go build .\test.go 

it creates text.ext
 C:\Ticer >.\test.exe
hello, world

Install protobuf
================


syntax:
========

protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/addressbook.proto

command:
========
PS C:\kafka\Tickers> protoc -I="." --go_out="." ./service.proto
PS C:\kafka\Tickers>

