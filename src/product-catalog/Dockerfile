FROM golang:1.22-alpine AS builder
 # base image

#go to docker hub for go lang image

WORKDIR /usr/src/app

COPY . . 
 # copy source code , else fails

RUN go mod download

RUN go build -o product-catalog ./   
 # creates file

#here we an stop docker file by CMD or ENTRYPOINT like CMD [./product-catalog]

FROM alpine AS release 

WORKDIR /usr/src/app

COPY ./products ./products  
 # because the content is in product.json
COPY --from=builder /usr/src/app/product-catalog ./

#EXPOSE ${PRODUCT_CATALOG_PORT}
ENV PRODUCT_CATALOG_PORT 8088
ENTRYPOINT ["./product-catalog"]

