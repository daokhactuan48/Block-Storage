Block-Storage
=============



# 1.Giới Thiệu Về Block Storage trong Openstack
  
  Block storage là một project trong Openstack cung cấp khả năng lưu trữ dưới dạng block cho các máy ảo. Block Storage có tên mã phần mềm là Cinder.
  
# 2. Giới Thiệu các tính năng của Block storage

## Các tính năng:
-  Attach/Detach volume vào Máy ảo
-  Tạo Snapshot cho Volume
-  Tạo/Xóa Volume 
-  Tăng kích cỡ volume
-  Boot volume từ máy ảo
-  Migrate volume 

#### 2.1.Tạo và Xóa Volume 

  2.1.1.Lệnh tạo volume
  
    cinder --display_name [ten_volume] <size>
    
  Ví du: cinder --display_name vd 1
  
  2.1.2.Lệnh Xóa Volume
  
    cinder delete <ID>
  ID: Là ID của volume muốn xóa
  
#### 2.2. Attach/Detach volume từ máy ảo

   2.2.1.Lệnh Attach volume vào máy ảo
   
    nova volume-attach <ID_VM> <ID_Volume>
    
  ID_VM: ID của máy ảo muốn attach volume vào
  ID_Volume: ID của volume 
  
   2.2.2. Lệnh Detach volume vào máy ảo
   
    nova volume-detach <ID_VM> <ID_volume>

#### 2.3. Tạo snapshot cho volume

   2.3.1. Lệnh tạo snapshot
  
    snapshot-create --display-name <ten_snapshot> <ID_Volume>
   
   2.3.2. Lệnh liệt kê snapshot 
   
    cinder snapshot-list
    
   2.3.3. Xóa snapshot
   
    cinder snapshot-delete <snapshot ID>

#### 2.4. Tăng kích cỡ cho volume

   2.4.1 Lệnh thay đổi size volume
   
    cinder extend <ID_Volume> <size>
    
  Chú ý: <size> phải lớn hơn kích cỡ hiện tại của volume
  
#### 2.5. Tính năng Migrate volume.

##### 2.5.1. Giới Thiệu
   
  - Trong Openstack có khả năng di chuyển volume từ giữa các back-end
  
Có 2 trường hợp của volume:

  - Volume ko được attach vào máy ảo.
  - Volume được attach vào máy ảo.

##### 2.5.2. Mô hình bài lab.
   
a. Mục tiêu bài lab: 

  - Chuyển volume giữa các back-end

b. Thông tin bài lab:
  
  - Back-end sử dụng là LVM
  - Một máy cài openstack all in one và một máy cài cinder-volume. 
  - Ubuntu 14.04
  - Máy cài cinder-volume phải add thêm hard disk vào.

c. Mô hình 
   
  <img src=http://i.imgur.com/cpHAiYI.jpg width="60%" height="60%" border="1">
  
d. Các bước cài đặt

###### Cài đặt trên Openstack trên 1 node
B1: Cài đặt Openstack AIO theo link sau: https://github.com/vietstacker/icehouse-aio-ubuntu14.04.

###### Cài đặt Cinder-volume trên máy volume 
B2: Cài đặt LVM và tạo volume group
  
    # apt-get install lvm2
    # pvcreate /dev/sdb
    # vgcreate cinder-volumes /dev/sdb

B3: Cài đặt các gói Cinder-volume

    # apt-get install cinder-volume

B4: Cấu hình file sau: /etc/cinder/cinder.conf

    osapi_volume_listen = 0.0.0.0
    osapi_volume_listen_port = 8776
    glance_host = 10.10.10.24
    glance_port = 9292
    iscsi_ip_address = 10.10.10.18
    iscsi_port = 3260
    rpc_backend = cinder.openstack.common.rpc.impl_kombu
    rabbit_host = 10.10.10.24
    rabbit_port = 5672
    rabbit_userid = guest
    rabbit_password = RABBIT_PASS
    [database]
    connection = mysql://cinder:CINDER_DBPASS@10.10.10.24/cinder
    [keystone_authtoken]
    auth_host = 10.10.10.24
    auth_port = 35357
    auth_protocol = http
    admin_tenant_name = service
    admin_user = cinder
    admin_password = CINDER_PASS

Chú ý: 
CINDER_DBPASS: là pass của cinder trên database

CINDER_PASS: pass của user cinder trong keystone

RABBIT_PASS: pass của RABIIT




    
    
    
  

  
