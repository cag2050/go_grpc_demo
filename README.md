### 步骤
1. 初始化项目
2. 安装包：`go get -u google.golang.org/grpc`、`go get -u google.golang.org/protobuf/cmd/protoc-gen-go`、`go get -u google.golang.org/grpc/cmd/protoc-gen-go-grpc`；更新PATH：`$ export PATH="$PATH:$(go env GOPATH)/bin"`
3. 编写 examples/helloworld/helloworld/helloworld.proto
4. 生成gRPC代码，在 examples/helloworld 目录下，运行命令：`
$ protoc --go_out=. --go_opt=paths=source_relative \
--go-grpc_out=. --go-grpc_opt=paths=source_relative \
      helloworld/helloworld.proto`
5. 编写：examples/helloworld/greeter_server、examples/helloworld/greeter_client
6. 在 examples/helloworld 目录下，运行server：`$ go run greeter_server/main.go`；在另一个终端，运行client：`$ go run greeter_client/main
.go Alice`，可看到输出：`Greeting: Hello Alice`


### 参考资料
资料 | 网址
--- | ---
grpc-go | https://github.com/grpc/grpc-go
Quick start | https://grpc.io/docs/languages/go/quickstart/
grpc-go/examples/helloworld/ | https://github.com/grpc/grpc-go/tree/master/examples/helloworld