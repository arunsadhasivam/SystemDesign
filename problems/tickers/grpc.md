https://www.grpc.io/docs/quickstart/go/

https://grpc.io/blog/installation/

protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/addressbook.proto

PS C:\kafka\Tickers\grpc> protoc -I="." --go_out="." ./service.proto
