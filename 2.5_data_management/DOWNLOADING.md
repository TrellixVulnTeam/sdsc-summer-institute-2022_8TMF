# Data Management: Or how (not) to handle your data in an HPC environment

- [Before we begin: A few disclaimers](DISCLAIMERS.md)
- [Easy access: Setting up SSH keys](SSH.md)
- [CIFAR through the tubes: Downloading data from the internet](DOWNLOADING.md)
- [More files, more problems: Advantages and limitations of different filesystems](FILESYSTEMS.md)
- [Going parallel: Lustre basics](LUSTRE.md)
- [Back that data up: Data transfer tools](TRANSFER.md)

## CIFAR through the tubes: Downloading data from the internet [:notes:](https://www.youtube.com/watch?v=_cZC67wXUTs) [:microphone:](https://en.wikipedia.org/wiki/Series_of_tubes)


[CIFAR](https://www.cs.toronto.edu/~kriz/cifar.html)

```
$ ssh expanse
```

```
wget https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz
```

```
--2022-07-26 08:50:09--  https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz
Resolving www.cs.toronto.edu (www.cs.toronto.edu)... 128.100.3.30
Connecting to www.cs.toronto.edu (www.cs.toronto.edu)|128.100.3.30|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 170498071 (163M) [application/x-gzip]
Saving to: ‘cifar-10-python.tar.gz’

cifar-10-python.tar 100%[===================>] 162.60M  34.0MB/s    in 5.3s    

2022-07-26 08:50:15 (30.4 MB/s) - ‘cifar-10-python.tar.gz’ saved [170498071/170498071]
```

```
[xdtr@login02 ~]$ ls -lh
total 163M
-rw-r--r-- 1 xdtr abc123 163M Jun  4  2009 cifar-10-python.tar.gz
```

```
tar -xf cifar-10-python.tar.gz
```

```
[xdtr@login02 ~]$ ls -lh
total 163M
drwxr-xr-x 2 xdtr abc123   10 Jun  4  2009 cifar-10-batches-py
-rw-r--r-- 1 xdtr abc123 163M Jun  4  2009 cifar-10-python.tar.gz
```

```
[xdtr@login02 ~]$ ls -lh cifar-10-batches-py/
total 177M
-rw-r--r-- 1 xdtr abc123 158 Mar 30  2009 batches.meta
-rw-r--r-- 1 xdtr abc123 30M Mar 30  2009 data_batch_1
-rw-r--r-- 1 xdtr abc123 30M Mar 30  2009 data_batch_2
-rw-r--r-- 1 xdtr abc123 30M Mar 30  2009 data_batch_3
-rw-r--r-- 1 xdtr abc123 30M Mar 30  2009 data_batch_4
-rw-r--r-- 1 xdtr abc123 30M Mar 30  2009 data_batch_5
-rw-r--r-- 1 xdtr abc123  88 Jun  4  2009 readme.html
-rw-r--r-- 1 xdtr abc123 30M Mar 30  2009 test_batch
```

```
md5sum cifar-10-python.tar.gz
```

```
c58f30108f718f92721af3b95e74349a  cifar-10-python.tar.gz
```

```
md5sum cifar-10-python.tar.gz > cifar-10-python.md5
```

```
[xdtr@login02 ~]$ ls -lh
total 163M
drwxr-xr-x 2 xdtr abc123   10 Jun  4  2009 cifar-10-batches-py
-rw-r--r-- 1 xdtr abc123   57 Jul 26 08:53 cifar-10-python.md5
-rw-r--r-- 1 xdtr abc123 163M Jun  4  2009 cifar-10-python.tar.gz
```

```
[xdtr@login02 ~]$ md5sum -c cifar-10-python.md5 
cifar-10-python.tar.gz: OK
```

```
curl https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz -o cifar-10-python.tgz
```

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  162M  100  162M    0     0  28.1M      0  0:00:05  0:00:05 --:--:-- 33.3M
```

```
[xdtr@login02 ~]$ ls -lh
total 326M
drwxr-xr-x 2 xdtr abc123   10 Jun  4  2009 cifar-10-batches-py
-rw-r--r-- 1 xdtr abc123   57 Jul 26 08:53 cifar-10-python.md5
-rw-r--r-- 1 xdtr abc123 163M Jun  4  2009 cifar-10-python.tar.gz
-rw-r--r-- 1 xdtr abc123 163M Jul 26 08:54 cifar-10-python.tgz
```

```
wget https://raw.githubusercontent.com/sdsc/sdsc-summer-institute-2022/main/2.5_data_management/cifar-10-python.sha256
```

```
[xdtr@login02 ~]$ sha256sum -c cifar-10-python.sha256 
cifar-10-python.tgz: OK
```

#

Next - [More files, more problems: Advantages and limitations of different filesystems](FILESYSTEMS.md)
