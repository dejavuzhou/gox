# gox
通过github.com/golang,一键安装golang.org/x的包

### 对于大陆的gopher来说,go get 安装 golang.org/x的包经常失败
### 所以在这里写了一个bash脚本一键安装golang.org/x的包
- windows用户 git-bash 来执行gox.sh这个脚本
- *unix用户 先`chmod +x gox.sh` 添加可以执行权限.在使用`./gox.sh`执行一键安装

```shell
#!/usr/bin/env bash
#为了兼容windows下的bash
cd $GOPATH;
#创建 $GOPATH/src/golang.org/x 目录
mkdir -p src/golang.org/x;
cd src/golang.org/x;
echo "已经安装的golang.org/x package";
ls;
echo "下面一行 for in 中包的名字您可以自己来定义"
for name in "glog" "image" "perf" "snappy" "term" "sync" "winstrap" "cwg" "leveldb" "text" "net" "build" "protobuf" "dep" "sys" "crypto" "gddo" "tools" "scratch" "proposal" "mock" "oauth2" "freetype" "debug" "mobile" "gofrontend" "lint" "appengine" "geo" "review" "arch" "vgo" "exp" "time";do
   if [ -d "$name" ]
   then
     cd $name;
     echo $name "包已经存在,使用git pull来更新源码";
     git pull;
   else
     git_url="https://github.com/golang/${name}.git";
     echo "开始clone golang.org/x 在github.com上的镜像代码:${git_url}";
     git clone --depth 1 "$git_url";
     cd $name;
   fi
   #go install;
done
```
