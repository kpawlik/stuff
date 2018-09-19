* [LOG OUTPUT](#log-output)                                                         
* [SERVICES](#services)                                                             
* [TAR](#tar)                                                                       
  * [untar](#untar)                                                                 
  * [tar gzip](#tar-gzip)                                                           
* [SYM LINK](#sym-link)                                                             
* [SSHPASS](#sshpass)                                                               
  * [Fast empty dir](#fast-empty-dir)                                               
* [PS TOP](#ps-top)                                                                 
  * [Run top for process with NAME](#run-top-for-process-with-name)                 
  * [top mem/cpu processes](#top-memcpu-processes)                                  
  * [kill all processes for queries](#kill-all-processes-for-queries)               
* [FILE STORE SERVER (/myworldtiles\_dev)](#file-store-server-myworldtiles_dev)     
* [FIX anywehwere (goto HOME)](#fix-anywehwere-goto-home)                           
  * [mobile app go to homepage](#mobile-app-go-to-homepage)            
* [FIND](#find)
  * [quite find error](#quite-find-error)
* [MAILX](#mailx)                                                                   
* [INSTALL FROM GITHUB](#install-from-github)                                       


```sh
grep -rnw 'directory' -e "pattern"
grep -rnw '/etc/' -e "jdk"
```

# LOG OUTPUT

```sh
> /filename.log 2>&1
```

# SERVICES

## service pgsql
```sh
vim /etc/init.d/postgresql
```

# TAR

## untar
```sh
tar -xzf openssl-1.0.1u.tar.gz
```
## tar gzip
```sh
tar -zcvf archive-name.tar.gz directory-name
```

# SYM LINK
```sh
ln -s source_file target_link
```

# SSHPASS
```sh
sshpass -p'A!!min3' scp -r /path_to_local_file  dukegndv99:/path_to_remote_file
```
## Fast empty dir
```sh
mkdir /tmp/empty
rsync -a --delete /tmp/empty /myworldtiles_stg/geoserver_data/gwc/Cox_myWorld_cox_legacy_grid/
```

# PS TOP

## Run top for process with NAME
```sh
top -c -p $(pgrep -d',' -f NAME)
```
##How long process is running
```sh
ps -p "PID" -o etime=
```
## top mem/cpu processes
```sh
ps aux | sort -k 4 -r | head -20
ps aux | sort -k 3 -r | head -20
```

## kill all processes for queries  
```sh
psql -c "select pid FROM  pg_stat_activity where query like '%user%';" | cat|  awk '{print $1}' | xargs --no-run-if-empty kill $1
```

# FILE STORE SERVER (/myworldtiles_dev)

```
\\catl0fs900
```

# FIX anywehwere (goto HOME)

## mobile app go to homepage
```javascript
window.location.href= "file:///C:/Users/kpawlik/AppData/Local/Ubisense/myWorld/4.4/public/nativeHome.html"
```
# FIND
## quite find error

```sh
RES=`find /myworldtiles_qa/sqlite/incrementals/13-09-2018__01/* 2> null -maxdepth 0 -type d -exec basename {} \; | sort`
if [ "${RES}" == "" ]; then echo "NOT FOUND";else echo "FOUND";  fi

```

# MAILX

```sh
mailx -a file.txt -s "File" Krzysztof.Pawlik@ubisense.net < /dev/null
```

# INSTALL FROM GITHUB

install gofind
```sh
wget https://github.com/kpawlik/gofind/blob/master/cmd/gofind/gofind?raw=true; mv ./gofind?raw=true ./gofind; chmod u=+rwx ./gofind
```
install monitor
```sh
cd /opt/myworld/myworld/WebApps/myworldapp/modules/custom/scripts/interfaces/mosaic/
wget https://github.com/kpawlik/monitor_process_out/blob/master/monitor_process_out?raw=true; mv ./monitor_process_out?raw=true ./monitor_process_out; chmod u=+rwx ./monitor_process_out
```
geocoding
```sh
wget https://github.com/kpawlik/tools/blob/kpawlik-geo-1/geocoding?raw=true; mv ./geocoding?raw=true ./geocoding; chmod u=+rwx ./geocoding
```
drive
```sh
wget https://github.com/kpawlik/tools/blob/kpawlik-geo-1/drive?raw=true; mv ./drive?raw=true ./drive; chmod u=+rwx ./drive
```
gorep
```sh
wget https://github.com/kpawlik/gotools/blob/master/gorep/gorep?raw=true; mv ./gorep?raw=true ./gorep; chmod u=+rwx ./gorep
```
