# Шифрование Диска Luks


## find device name with lsblk or fdisk -l

``` 
fdisk /dev/sda → n → w
```

## crypt newly created partitions 

``` 
 cryptsetup luksFormat --cipher aes-cbc-essiv:sha256 -s 256 -y /dev/sda4
 cryptsetup luksFormat --cipher aes-cbc-essiv:sha256 -s 256 -y /dev/sdb4
 cryptsetup luksFormat --cipher aes-cbc-essiv:sha256 -s 256 -y /dev/sdc4 
 cryptsetup luksFormat --cipher aes-cbc-essiv:sha256 -s 256 -y /dev/sdd4
```

## mount crypted partitions with cryptsetup

```
 cryptsetup luksOpen /dev/sda4 crypt-0
 cryptsetup luksOpen /dev/sdb4 crypt-1
 cryptsetup luksOpen /dev/sdc4 crypt-2
 cryptsetup luksOpen /dev/sdd4 crypt-3
```
## find device id with

``` 
 ls -al /dev/disk/by-id/
```

## create zpool data with:

```

 zpool create -f -o cachefile=none -o ashift=12  data mirror /dev/disk/by-id/dm-uuid-CRYPT-LUKS2-0f5f5f55904e46d9881f30b5a5931a15-crypt-0 /dev/disk/by-id/dm-uuid-CRYPT-LUKS2-237b9e2eaae54dfc8c2b189f24fab6e0-crypt-3 mirror /dev/disk/by-id/dm-uuid-CRYPT-LUKS2-418459e9bbc646e7af20625bd85956b5-crypt-2 /dev/disk/by-id/dm-uuid-CRYPT-LUKS2-a938fe3f94554dbf8b1c412d538e1bcd-crypt-1
 
```
# fil /etc/crypttab with 

```
ls -al /dev/disk/by-uuid/

```

<target name>  <source device>    <key file>  <options>
 crypt-0 /dev/disk/by-uuid/3df047b1-cfda-4048-a0cd-c8c999807a52  none luks,noauto
 crypt-1 /dev/disk/by-uuid/42bbae6a-bb13-4d48-99a3-cee54c011ac5  none luks,noauto
 crypt-2 /dev/disk/by-uuid/0bc21b33-a8dd-48a3-b2b4-501d2f18e8cc  none luks,noauto
 crypt-3 /dev/disk/by-uuid/b0c2c60f-5130-46d0-835b-9e43d0fd1ec6  none luks,noauto
`
 
## Create zfs mountpoint
 
```
zfs set mountpoint=/var/lib/vz data
 
