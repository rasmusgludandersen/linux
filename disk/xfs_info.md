# xfs_info


Check current features

`xfs_info /boot`

```shell
meta-data=/dev/sda1              isize=512    agcount=4, agsize=65472 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=0 inobtcount=0 nrext64=0
data     =                       bsize=4096   blocks=261888, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=1566, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```

Unmount partition

`umount /boot`

Activate bigtime

`xfs_admim -O bigtime=1 /dev/sda1`

Remount partition

`mount /boot`

