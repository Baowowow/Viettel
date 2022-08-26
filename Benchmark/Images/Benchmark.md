# Benchmark Ceph và Gluster
----        
## Mục Lục 
[I. Các thông số đánh giá](#pm)
- [1. IOPS](#iops)
- [2. Throughput](#tp)
- [3. Latency](#lat)           

[II. Kết quả đánh giá](#rating)   
- [1. Test case 1](#tc1)  
- [2. Test case 2](#tc2)  
- [3. Test case 3](#tc3)  



---- 
<a name='pm'></a> 
## I. Các thông số đánh giá

<a name='iops'></a> 
### 1. IOPS 
**IOPS** - Input/Output operation per second: Đơn vị đo tiêu chuẩn được sử dụng cho các thiết bị lưu trữ để đo số lượng tác vụ đọc ghi được hoàn thành trong 1 giây. Thông số **IOPS** càng cao thì tốc độ xử lý càng nhanh, tác vụ xử lý càng nhiều giúp tăng hiệu năng thiết bị.

<a name='tp'></a> 
### 2. Throughput
**Throughput** (Thông lượng): Tốc độ truyền dữ liệu (mb/s). Nếu IOPS đo số lượng tác vụ đọc ghi được hoàn thành trong 1 giây thì **Throughput** đo số bits được đọc hoặc viết mỗi giây

<a name='lat'></a> 
### 3. Latency
**Latency** là tổng thời gian hoàn thành từ khi 1 yêu cầu được nhận cho đến khi người yêu cầu nhận được phản hồi từ hệ thống
<a name='diff'></a> 

## II. Kết quả đánh giá
<a name='tc1'></a> 
### 1. Test case 1: Kiểm tra đồng thời random read & random write
Dùng Fio tạo 1 file 500MB, thực hiện việc đọc/ghi đồng thời với blocksize 4KB theo tỉ lệ 75% – 25% (tức 3 đọc/1 ghi) và thực hiện đồng thời 64 tác vụ một lúc

| System | Bandwidth | IOPS | Latency | Throughput|                                                                                                          
|--------------|-----|--------------|-------------|--------------|
| HDD | Read: 835kb/s / Write: 278kb/s  | Read: 203 / Write: 67 | Read:  / Write: | Read:  / Write:  |
| Ceph AIO | Read: 167kb/s / Write: 56kb/s  | Read: 40 / Write: 13 | Read:  / Write: | Read:  / Write:  |
| Distributed Gluster | Read: 482kb/s / Write: 161kb/s  | Read: 117 / Write: 39 | Read:  / Write: | Read:  / Write:  |                      |
| Replicated Gluster | Read: 364kb/s / Write: 121kb/s  | Read: 88 / Write: 29 | Read:  / Write: | Read:  / Write:  |
| Distributed Replicated Gluster | Read: 263kb/s / Write: 88kb/s  | Read: 64 / Write: 21 | Read:  / Write: | Read:  / Write:  |
| Disperse Gluster | Read: 70kb/s / Write: 23kb/s  | Read: 17 / Write: 5 | Read:  / Write: | Read:  / Write:  |

>Kết quả IOPS trên ổ HDD

 <img src="./Images/rrwHDD.png">


>Kết quả IOPS trên Ceph

 <img src="./Images/rrwceph.png">


>Kết quả IOPS trên volume distributed của Gluster

 <img src="./Images/rrw1.png">


>Kết quả IOPS trên volume replicated của Gluster

 <img src="./Images/rrw2.png">


>Kết quả IOPS trên volume distributed replicated của Gluster

 <img src="./Images/rrw3.png">

>Kết quả IOPS trên volume dispersed của Gluster

 <img src="./Images/rrw4.png">


<a name='tc2'></a> 
### 2. Test case 2: Kiểm tra random read
Dùng Fio tạo 1 file 200MB, thực hiện việc đọc với blocksize 4KB và thực hiện đồng thời 64 tác vụ một lúc

| System | Bandwidth | IOPS | Latency | Throughput|                                                                                                          
|--------------|-----|--------------|-------------|--------------|
| HDD | 1311kb/s  | 320 |  |   |
| Ceph AIO | 539kb/s  | 131 |  |   |
| Distributed Gluster | 1360kb/s  | 331 |  |   |                      |
| Replicated Gluster | 1296kb/s  | 316 |  |   |
| Distributed Replicated Gluster | 1076kb/s  | 262 |  |   |
| Disperse Gluster | 459kb/s  | 112 |  |   |

>Kết quả IOPS trên ổ HDD

 <img src="./Images/rrHDD.png">


>Kết quả IOPS trên Ceph

 <img src="./Images/rrceph.png">


>Kết quả IOPS trên volume distributed của Gluster

 <img src="./Images/rr1.png">


>Kết quả IOPS trên volume replicated của Gluster

 <img src="./Images/rr2.png">


>Kết quả IOPS trên volume distributed replicated của Gluster

 <img src="./Images/rr3.png">

>Kết quả IOPS trên volume dispersed của Gluster

 <img src="./Images/rr4.png">

<a name='tc3'></a> 
### 3. Test case 3: Kiểm tra random write
Dùng Fio tạo 1 file 200MB, thực hiện việc ghi với blocksize 4KB và thực hiện đồng thời 64 tác vụ một lúc

| System | Bandwidth | IOPS | Latency | Throughput|                                                                                                          
|--------------|-----|--------------|-------------|--------------|
| HDD | 3969kb/s  | 969 |  |   |
| Ceph AIO | 818kb/s  | 199 |  |   |
| Distributed Gluster | 3569kb/s  | 871 |  |   |                      |
| Replicated Gluster | 2628kb/s  | 641 |  |   |
| Distributed Replicated Gluster | 2106kb/s  | 514 |  |   |
| Disperse Gluster | 62kb/s  | 15 |  |   |

>Kết quả IOPS trên ổ HDD

 <img src="./Images/rwHDD.png">


>Kết quả IOPS trên Ceph

 <img src="./Images/rwceph.png">


>Kết quả IOPS trên volume distributed của Gluster

 <img src="./Images/rw1.png">


>Kết quả IOPS trên volume replicated của Gluster

 <img src="./Images/rw2.png">


>Kết quả IOPS trên volume distributed replicated của Gluster

 <img src="./Images/rw3.png">

>Kết quả IOPS trên volume dispersed của Gluster

 <img src="./Images/rw4.png">



 ## 3. Đo Latency với IOPing
Ta có thể kiểm tra độ trễ Latency của từng request độc lập bằng công cụ IOPing. Kết quả như sau:

 | System | Latency |                                                                                                   
|--------------|--------------|
| HDD | 724.6us  | 
| Ceph AIO | 28.9ms  | 
| Distributed Gluster | 771.5us  | 
| Replicated Gluster | 696.6us  | 
| Distributed Replicated Gluster | 750.7us | 
| Disperse Gluster | 1.05ms  | 

>Kết quả Latency trên ổ HDD

 <img src="./Images/latencyHDD.png">


>Kết quả IOPS trên Ceph

 <img src="./Images/latencyCeph.png">


>Kết quả IOPS trên volume distributed của Gluster

 <img src="./Images/latencyvol1.png">


>Kết quả IOPS trên volume replicated của Gluster

 <img src="./Images/latencyvol2.png">


>Kết quả IOPS trên volume distributed replicated của Gluster

 <img src="./Images/latencyvol3.png">

>Kết quả IOPS trên volume dispersed của Gluster

 <img src="./Images/latencyvol4.png">
