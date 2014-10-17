Ceph cluster
# Benchmarks


<!-- .slide: data-background="images/ceph_benchmarks_bottom_to_top.svg" data-background-size="auto 95%" -->


## Block device benchmarks
(simple)
```sh
dd if=/dev/zero of=/dev/sdh1 bs=1G count=1 oflag=direct

dd if=/dev/zero of=/dev/sdh1 bs=512 count=1000 oflag=direct
```


## Block device benchmarks
(advanced)
```sh
fio --size=100m \
	--ioengine=libaio \
	--invalidate=1 \
	--direct=1 \
	--numjobs=10 \
	--rw=write \
	--name=fiojob \
	--blocksize_range=4K-512k \
	--iodepth=1
```


<iframe src="https://asciinema.org/api/asciicasts/13037?size=medium&amp;theme=solarized-light" id="asciicast-iframe-13037" name="asciicast-iframe-13037" scrolling="no"></iframe>



## Network benchmarks
```sh
netperf  -t TCP_STREAM -H 127.0.0.1
```


## OSD benchmark
```sh
ceph tell osd.X bench
```


## rados benchmark
```sh
rados bench -p bench 30 write
```
Do this on a throwaway pool!
