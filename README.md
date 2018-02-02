# Goldilocks Input plugin 

This plugin gathers the statistic data from Goldilocks Cluster server. All metrics are configurable, and you can add/modify/remove metrics for Goldilocks statistics data via config file, without recompiling. 

## Quick start

1. Checkout  telegraf 
```
$ go get github.com/influxdata/telegraf
```

2. Checkout this repository and copy goldilocks directory to telegraf 
```
$ git clone https://github.com/ckh0618/telegraf_goldilocks.git
$ cd telegraf_goldilocks
$ cp -R goldilocks $GOPATH/src/github.com/influxdata/telegraf/plugin/inputs
```

3. Add plugin

```
$ echo  "import  _ \"github.com/influxdata/telegraf/plugins/inputs/goldilocks\" " >> $GOPATH/src/github.com/influxdata/telegraf/plugin/inputs/all/all.go

```

4. Build 

```
$ cd $GOPATH/src/github.com/influxdata/telegraf
$ make 
```

5. Getting configurations

You can get telegraf and all plugins configurations into a single config file by issuing a following command. 
```
$ ./telegraf config  > telegraf.conf 
```
you can find input.goldilocks section, and uncomment the section. 


## Configuration of Goldilocks plugin 

The configuration of Goldilocks plugin is consist of two parts. One is for the connection informations to Goldilocks server and the other is for defining metrics. 

### Connection informations 

* goldilocks_odbc_driver_path : path to goldilocks odbc driver location. "?" means GOLDILOCKS_HOME enviroment variables. default("?/lib/libgoldilockscs-ul64.so")
* goldilocks_host  : host address  default ("127.0.0.1")
* goldilocks_port  : port number default ( 22581 )
* goldilocks_user  : user name default( "test" )
* goldilocks_password  : password default("test" )

### Metrics 

Metrics are array of inputs.goldilocks.elements sections. Each section is consist of followings. 

* series_name : series_name for storing data to influxdb 
* sql : sql text 
* tags : tags lists ( should be column name in result set )
* fields : fields lists ( should be column name in result set )
* pivot : if you want to transpose data rows to columns, then true 
* pivot_key : key for pivoting


