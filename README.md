# ap2-generated

This repository contains the generated Go protobuf and gRPC code for Assignment 2. 
It acts as the single source of truth for contracts shared between the Order and Payment microservices.

## Setup & Usage

To consume this repository in your main Go microservices project:

1. Add the package to your project:
```bash
go get github.com/ZLHRS/ap2-generated@v1.0.0
```

2. Import the packages in your Go code:

### Payment Service Example
```go
import (
    "context"
    pb "github.com/ZLHRS/ap2-generated/payment/v1"
)

type server struct {
    pb.UnimplementedPaymentServiceServer
}

func (s *server) ProcessPayment(ctx context.Context, req *pb.PaymentRequest) (*pb.PaymentResponse, error) {
    // Implementation
}
```

### Order Service Example
```go
import (
    "context"
    pb "github.com/ZLHRS/ap2-generated/order/v1"
)

// Use pb.OrderServiceClient to call order methods
```

## How It Works

Code in this repository is **auto-generated** by a GitHub Actions workflow in the `ap2-protos` repository.
Do not modify files in this repository manually. Any changes will be overwritten on the next generation run.

## Fallback: Local Generation
If you need to generate exactly what GitHub Actions does locally, run this from the `ap2-protos` root directory:
```bash
protoc -I=proto \
  --go_out=../ap2-generated \
  --go_opt=paths=source_relative \
  --go-grpc_out=../ap2-generated \
  --go-grpc_opt=paths=source_relative \
  proto/payment/v1/payment.proto proto/order/v1/order.proto
```
