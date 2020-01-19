https://www.grpc.io/docs/quickstart/go/

https://grpc.io/blog/installation/

protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/addressbook.proto

PS C:\kafka\Tickers\grpc> protoc -I="." --go_out="." ./service.proto
https://raw.githubusercontent.com/grpc/grpc-go/master/examples/helloworld/greeter_client/main.go


go packagemanger - use go mod
==============================

    c:\Arun>go mod vendor 


good examples:
===============

https://github.com/grpc/grpc-go/tree/master/examples


        INSTALL
        $ go get -u google.golang.org/grpc/examples/helloworld/greeter_client
        $ go get -u google.golang.org/grpc/examples/helloworld/greeter_server
        TRY IT!
        Run the server

        $ greeter_server &
        Run the client

        $ greeter_client
