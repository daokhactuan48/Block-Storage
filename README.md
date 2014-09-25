Block-Storage
=============

Tổng quan các tính năng của Cinder

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

### 2.5.1. Giới Thiệu
   
  - Trong Openstack có khả năng di chuyển volume từ giữa các back-end
  
Có 2 trường hợp của volume:

  - Volume ko được attach vào máy ảo.
  - Volume được attach vào máy ảo.

### 2.5.2. Mô hình bài lab.
   
   a. Mục tiêu bài lab: 

  - Chuyển volume giữa các back-end

   b. Thông tin bài lab:
  
  - Back-end sử dụng là LVM
  - Một máy cài openstack all in one và một máy cài cinder-volume. 

   c. Mô hình 
   
   <img src=http://i.imgur.com/cpHAiYI.jpg width="60%" height="60%" border="1">
  
   d. Các bước cài đặt
   
   



    
    
    
  

  
