#install hbase

###download & unzip to home
```
http://archive.apache.org/dist/hbase/hbase-0.94.8/hbase-0.94.8.tar.gz
```

###create directory
```
sudo mkdir /usr/lib/hbase
```

###move  hbase-0.94.8 to hbase
```
mv hbase-0.94.8 /usr/lib/hbase/hbase-0.94.8
```

###Configuring HBase with java
```
cd /usr/lib/hbase/hbase-0.94.8/conf/
gedit hbase_env.sh
>>export JAVA_HOME=/usr/lib/jvm/(folder name)
save & quit
```

###set path
```
gedit ~/.bashrc
append>>export HBASE_HOME=/usr/lib/hbase/hbase-0.94.8
        export PATH=$PATH:$HBASE_HOME/bin
        export JAVA_HOME=/usr/lib/jvm/(folder name)
        export PATH=$PATH:$JAVA_HOME/bin
save & quit
```

###reboot
```
reboot
```

###To start Hbase
```
cd /usr/lib/hbase/hbase-0.94.8/bin
./start-hbase.sh
```

###web interfaces
```
http://localhost:60010    >for master
http://localhost:60030    >for region sever
```

###To stop Hbase
```
cd /usr/lib/hbase/hbase-0.94.8/bin
./stop-hbase.sh
```



#install opentsdb

###DOWNLOAD FROM github
```
git clone git://github.com/OpenTSDB/opentsdb.git
```
(sudo apt-get git)

###run build.sh in opentsdb
```
cd opentsdb
./build.sh
```

###install
```
cd build
sudo make install
```

###create tables for data storage
```
env COMPRESSION=NONE HBASE_HOME=path/to/hbase-0.94.X/ ./src/create_table.sh
```
(first time only)

###start tsd
```
gedit start_tsd.sh &

contents:

#!/bin/bash
tsdtmp=${TMPDIR-'/tmp'}/tsd   
# For best performance, make sure
mkdir -p "$tsdtmp" 
# your temporary directory uses tmpfs
./build/tsdb tsd --port=4242 --staticroot=build/staticroot --cachedir="$tsdtmp" --zkquorum=localhost


save & quit
```

```
檔案=>opentsdb=>start_tsd.sh=>right click => 權限:讀寫all & 允許檔案作為程式執行
```

```
./start_tsd.sh
```
