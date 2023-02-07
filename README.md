# 自己构建的flannel服务

## 解决的问题

官方默认的VNI是1，如果我们想运行多个就会有问题，如下图，我有一台机器需要部署多个flannel
服务，目前发现直接运行会有一些冲突的问题

![images](./images/QQ20230207-094524%402x.png)

## 解决方法

解决方法就是修改vxlan.go 的配置定义

## 问题

官方默认的VNI是1，如果我们想运行多个就会有问题，解决方法就是修改vxlan.go 的配置定义

backend/vxlan/vxlan.go

```code
package vxlan

import (
	"encoding/json"
	"fmt"
	"net"

	"golang.org/x/net/context"

	"github.com/coreos/flannel/backend"
	"github.com/coreos/flannel/pkg/ip"
	"github.com/coreos/flannel/subnet"
)

func init() {
	backend.Register("vxlan", New)
}

const (
	defaultVNI = 2
)

```

## 编译

推荐的还是基于go mod，对于支持go mod 的可以直接使用，不支持的flannel 版本，可以先转换，然后使用go mod构建，官方包含了说明文档

## 说明

目前主要是为了解决自己的问题，VNI 修改为了2，具体运行就是直接修改以前使用的rpm，然会替换
版本就行了,同时注意以上是修改的v0.7.1 版本的，其他版本的类似修改
