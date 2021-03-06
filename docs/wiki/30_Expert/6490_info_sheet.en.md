# 6490 info sheet

### 6490 Partitions

```
	mtd0     0x00000000    0x04000000    Filesystem ARM               eMMC
	mtd1     0x04000000    0x04800000    Kernel ARM                   eMMC
	mtd2       0x0a0000      0x0c0000    Urlader                      SPI
	mtd3       0x0c0000      0x100000    Environment                  SPI
	mtd4       0x100000      0x140000    Environment                  SPI
	mtd5       0x140000      0x1e0000    DOCSIS                       SPI
	mtd6     0x04800000    0x08800000    Filesystem ATOM              eMMC
	mtd7     0x08800000    0x09000000    Kernel ATOM                  eMMC
	mtd8       0x000000      0x080000    cefdk                        SPI
	mtd9       0x080000      0x090000    cefdk_config                 SPI
	mtd10      0x090000      0x0a0000    GPT_Backup                   SPI
	mtd11    0x09000000    0x0d000000    Filesystem ARM (reserved)    eMMC
	mtd12    0x0d000000    0x0d800000    Kernel ARM (reserverd)       eMMC
	mtd13    0x0d800000    0x11800000    Filesystem ATOM (reserved)   eMMC
	mtd14    0x11800000    0x12000000    Kernel ATOM (reserved)       eMMC
```

### 6490 Backup from Bootloader

```
	retr ENV
	retr CONFIG
	quote GETENV linux_fs_start
```

### 6490 Flash via Bootloader

> !! WARNING: very incomplete !!\
> !! not appropriate for all box variants !!\
> !! Risk to destroy the device permanently !!\
> !! Only for people with indepth knowledge of the device !!\
> !! No liability !!\

```
	ftp 192.168.178.1
	Name (192.168.178.1:xyz): adam2
	Password: adam2
	ftp> quote MEDIA FLSH
	ftp> binary
	ftp> passive
	ftp> put filesystem.image mtd0             (alt: mtd11)
	ftp> put kernel.image mtd1                 (alt: mtd12)
	ftp> lcd x86
	ftp> put filesystem.image mtd6             (alt: mtd13)
	ftp> put kernel.image mtd7                 (alt: mtd14)
	ftp> quote SETENV linux_fs_start 0 or 1    (toggle if flashed to alternative set)
	ftp> quote REBOOT
	ftp> exit
```


