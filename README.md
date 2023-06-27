# Instalasi-NFS-di-debian-11

Server :
Install nfs client
---------------------
$ apt install nfs-common

Buat folder yang ingin di share
-----------------------------------------
$ mkdir /exports
$ cd /exports
/exports$ Mkdir backup
/exports$ Mkdir documents
$ cat /etc/exports
/exports$ nano backup/test1.txt
Tuliskan : from server

Pindahkan file asli
------------------------
$ mv /etc/exports /etc/exports.orig

edit file exports
--------------
$ Nano /etc/exports
Tambahkan :
/exports/backup 172.16.3.1/255.255.255.0(rw,no_subtree_check)
Folder_yang _dimount Ip_client/subnet_client(rw,no_subtree_check)

Restart dan cek status
-----------------------------
$ systemctl restart nfs-kernel-server
$ systemctl status nfs-kernel-server

Instal NFS server
----------------------
$ apt install nfs-kernel-server
$ systemctl status nfs-kernel-server


Client :
Install nfs client
---------------------
$ apt install nfs-common

Tampilkan daftar file yang di eksport
--------------------------------------------------
$ showmount --exports ip_server

Buat folder destination 
-------------------------------
$ mkdir /mnt/nfs
$ mkdir /mnt/nfs/backup
$ mkdir /mnt/nfs/documents
$ ls -l /mnt/nfs
$ ls -l /mnt/nfs/backup

Mount dari server ke client
------------------------------------
$ Mount ip_client:/exports/backup /mnt/nfs/backup 

Menampilkan info mounting
-----------------------------------------------
$ df -h

Cek apakah file berhasil di mount
----------------------------------------------
$ ls -l /mnt/nfs/backup
$ cat /mnt/nfs/backup/test1.txt




Untuk membatalkan mount : lakukan di client
------------------------------------
$ Unmount /mnt/nfs/backup
$ Unmount /mnt/nfs/documents
![image](https://github.com/NurFadilah038/Instalasi-NFS-di-debian-11/assets/94078816/d1e55aef-75ee-4e5f-a44a-02fa569255f2)
