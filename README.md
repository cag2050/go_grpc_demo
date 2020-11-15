### 项目包含：
1. grpc 使用
2. grpcurl 使用

### grpc 步骤
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

### grpcurl 的使用
1. 安装包：`$ go get -u github.com/fullstorydev/grpcurl`、`$ go install github.com/fullstorydev/grpcurl/cmd/grpcurl`
2. 启动reflection反射服务：examples/helloworld/greeter_server/main.go 文件中添加代码`reflection.Register(s)`，并重启server端
3. 终端运行list命令`grpcurl -plaintext localhost:50051 list`，查看服务列表
4. 终端运行list命令`grpcurl -plaintext localhost:50051 list helloworld.Greeter`，查看服务 helloworld.Greeter 的方法列表
5. 终端运行describe命令`grpcurl -plaintext localhost:50051 describe helloworld.Greeter`，查看 Greeter 详细描述
6. 终端运行describe命令`grpcurl -plaintext localhost:50051 describe helloworld.HelloRequest`，查看 HelloRequest 详细描述
7. 终端运行describe命令`grpcurl -plaintext localhost:50051 describe helloworld.HelloReply`，查看 HelloReply 详细描述

### 报错
1. 报错：undefined: grpc.SupportPackageIsVersion7，原因：grpc版本不是最新的；解决：安装最新grpc包：`go get -u google.golang.org/grpc`

### 参考资料
资料 | 网址
--- | ---
grpc-go | https://github.com/grpc/grpc-go
Quick start | https://grpc.io/docs/languages/go/quickstart/
grpc-go/examples/helloworld/ | https://github.com/grpc/grpc-go/tree/master/examples/helloworld
grpcurl仓库 | https://github.com/fullstorydev/grpcurl
书籍《Go语言高级编程》4.8 grpcurl工具 | https://weread.qq.com/web/reader/dd63214071cc7fa3dd61bb8kd8232f00235d82c8d161fb2