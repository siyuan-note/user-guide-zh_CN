在服务器上伺服思源笔记最简单的方案是通过 Docker 部署，镜像名称是 `b3log/siyuan`，目前没有版本标签，只有最新版。
{: id="20201227173504-opkavin"}

## 文件结构
{: id="20201227174700-39dg7ur"}

整体程序位于 `/opt/siyuan/` 下，基本上就是 Electron 安装包 resources 文件夹下的结构：
{: id="20201227174134-hptryqy"}

* {: id="20201227174714-t7ew8rk"}appearance：图标、主题、多语言
  {: id="20210208145140-jwvzb91"}
* {: id="20201227174726-zztkpj2"}guide：帮助文档
  {: id="20210208145140-em39k3o"}
* {: id="20201227174744-z7qo4j2"}stage：界面和静态资源
  {: id="20210208145140-1tyrmez"}
* {: id="20201227174842-tr8u7q0"}kernel：内核程序
  {: id="20210208145140-99h8xv0"}
{: id="20201227174705-0hl54vz"}

## 启动入口
{: id="20201227174908-s19h988"}

构建 Docker 镜像时设置了入口：`ENTRYPOINT [ "/opt/siyuan/kernel" ]`，使用 `docker run b3log/siyuan` 并带参即可启动：
{: id="20201227180709-rglrztt" updated="20210301202239"}

* {: id="20201227201514-c7brkss"}`--conf` 指定配置文件夹路径，配置文件夹在宿主机上通过 `-v` 挂载到容器中
  {: id="20210208145140-7f45i9c" updated="20210301202448"}
* {: id="20210301202244-4sel9pe"}`--data` 指定数据文件夹路径，数据文件夹在宿主机上通过 `-v` 挂载到容器中
  {: id="20210301202244-umqom3o" updated="20210301202457"}
* {: id="20201227201521-fs7hlwf"}`--resident` 指定为 true 常驻内存
  {: id="20210208145140-tgabyhf"}
{: id="20201227201453-yh75kqd"}

更多的参数可参考((20201225172241-ifgc4hm "这里"))。下面是一条启动命令示例：
{: id="20210301201353-sffb1m7" updated="20210301202520"}

`docker run -v conf_dir_host:conf_dir_container -v data_dir_host:data_dir_container -p 6806:6806 b3log/siyuan --resident=true --conf=conf_dir_container --data=data_dir_container`
{: id="20201227181459-iml8ebp" updated="20210301202408"}

* {: id="20201227193950-dp2hioi"}`conf_dir_host`：宿主机上的配置文件夹路径
  {: id="20210208145140-w9i02jr"}
* {: id="20201227194032-68h45ue"}`conf_dir_container`：容器内配置文件夹路径，和后面 `--conf` 指定成一样的
  {: id="20210208145140-2ave4tv"}
* {: id="20201227194227-k2r2xan"}`data_dir_host`：宿主机数据文件夹路径
  {: id="20210208145140-eyz02oy"}
* {: id="20201227194257-5idyo8v"}`data_dir_container`：容器内数据文件夹路径
  {: id="20210208145140-p17fze7" updated="20210301202534"}
{: id="20201227174657-0k1ruhd"}

为了简化，建议将 conf、data 文件夹路径在宿主机和容器上分别配置为一致的，比如：
{: id="20201227194509-hdnzkry"}

* {: id="20201227194543-y71qqsd"}`conf_dir_host` 和 `conf_dir_container` 配置为 /siyuan/conf
  {: id="20210208145140-jdja3yp"}
* {: id="20201227194623-2um0t40"}`data_dir_host` 和 `data_dir_container` 配置为 /siyuan/data
  {: id="20210208145140-jxt6ydf"}
{: id="20201227194542-ejfp46x"}

对应的启动命令示例：
{: id="20201227194830-86gbz55"}

`docker run -v /siyuan/conf:/siyuan/conf -v /siyuan/data:/siyuan/data -p 6806:6806 b3log/siyuan --resident=true --conf=/siyuan/conf/ --data=/siyuan/data/`
{: id="20201227194658-m3auzob" updated="20210301202637"}

## 内核 API
{: id="20201227194925-7ipoiv6"}

### 打开文件夹
{: id="20201227195443-zxgp2sw"}

POST `/notebook/mount`，参数：
{: id="20201227195224-cnwhfri"}

* {: id="20201227195626-jsv1r80"}`url`：固定传入 `http://127.0.0.1:6806/siyuan/`，即 box.url
  {: id="20210208145140-lxewxwx"}
* {: id="20201227195644-i7xcm1g"}`path`：内核数据文件夹下的某个文件夹路径，即 box.path
  {: id="20210208145140-vcsnpch"}
{: id="20201227195500-v08m84n"}

### 关闭文件夹
{: id="20201227195737-xbkf95m"}

POST `/notebook/unmount`，参数：
{: id="20201227195742-df6gznf"}

* {: id="20201227195805-rq7h6m9"}`url`：固定传入 `http://127.0.0.1:6806/siyuan/`，即 box.url
  {: id="20210208145140-qaqj3jl"}
{: id="20201227195758-qsyk4py"}


{: id="20201227173504-847cs1q" type="doc"}
