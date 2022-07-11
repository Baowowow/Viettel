# Week 1: Filesystem
---
## **Mục Lục**

### I. [Tổng quan về Filesystem](#filesystem)

### II. [Các loại file system phổ biến](#2filesystem)

### III. [Tài liệu tham khảo](#reference)

---
<a name='filesystem'></a> 
### I. Tổng quan về filesystem
**File system** xác định cách files được đặt tên, lưu trữ và truy hồi từ 1 thiết bị lưu trữ. Nếu không có *filesystem* thông tin lưu trữ sẽ không được phân loại riêng và gây khó khăn cho việc nhận diện và truy hồi.
**File system** thực hiện lưu trữ và tổ chức dữ liệu và có thể được xem như là mục lục cho tất cả dữ liệu chứa trong thiết bị lưu trữ. Những thiết bị có thể bao gồm hard drives, optical drives và flash drives
**File system** sẽ đặt ra các tiêu chuẩn để đặt tên files, bao gồm số lượng lớn nhất các ký tự, ký tự nào được dùng, hậu tố dài bao nhiêu. Trong nhiều hệ thống, file names không được vào trường hợp nhạy cảm
**File systems** còn chứa các thông tin như kích thước file, cùng với các đặc tính của nó, địa điểm và cấp bậc ở trong danh mục (directory) của metadata. Metadata có thể nhận diện được các free blocks của ổ lưu trữ khả dụng trên drive và bao nhiêu không gian đang khả dụng. File systems sẽ sử dụng metadata để lưu trữ và truy hồi files
1 **file system** cũng bao gồm 1 format để chỉ rõ đường dẫn đến file qua cấu trúc của các directories.
Trước khi files và directories được tạo trên vùng lưu trữ, việc phân vùng sẽ được thực hiện. 1 phân vùng là 1 vùng ổ cứng hoặc vùng lưu trữ khác mà được hệ điều hành quản lý riêng rẽ. 1 file system sẽ được chứa trong 1 phân vùng.

> VD: File system của Linux được tổ chức theo tiêu chuẩn cấp bậc của hệ thống tập tin Filesystem Hierarchy Standard (FHS) 
- Chức năng của các thư mục:
  - /bin: Các chương trình cơ bản
  - /boot: Chứa Linux kernel
  - /dev: chứa các tập tin thiết bị (CDRom, HDD, FDD,…)
  - /etc: chứa các tập tin cấu hình hệ thống.
  - /home: thư mục dành cho người dùng không phải là root
  - /lib: chứa các thư viện dùng chung cho các lệnh nằm trong /bin và /sbin. Thư mục này cũng chứa các module của kernel.
  - /mnt hoặc /media: mount point mặc định cho những hệ thống file kết nối bên ngoài.
  - /opt: thư mục chứa các phần mềm cài thêm
  - /sbin: các chương trình hệ thống
  - /srv: dữ liệu được sử dụng bởi các máy chủ lưu trữ trên hệ thống
  - /tmp: thư mục chứa các file tạm thời
  - /usr: thư mục chứa những file cố định hoặc quan trọng để phục vụ tất cả người dùng
  - /var: dữ liệu biến được xử lý bởi daemon, điều này bao gồm các tệp nhật ký, hàng đợi, cache,…
  - /root: các tệp cá nhân của người quản trị (root account)
  - /proc: sử dụng cho Linux kernel, chúng được sử dụng bởi kernel để xuất dữ liệu sang không gian người dùng.
 
 > So sánh giữa FileSystem giữa Window và Linux
<a name='2filesystem'></a>  
### II. Các loại file system phổ biến
<a name='reference'></a> 
Có rất nhiều loại file systems, với cấu trúc logic và đặc tính khác nhau.Các loại file system có thể được phân biệt bởi hệ điều hành và yêu cầu của HĐH đó
Các loại file system phổ biến bao gồm:
#### 1.File allocation table (FAT): 
File allocation table tạm dịch là Bảng cấp phát tập tin. Được hỗ trợ bởi hệ điều hành Microsoft Windows. FAT được ra thiết kế vào năm 1977 cho floppy disk nhưng sau đó được thay đổi để phù hợp cho hard disk. FAT còn được sử dụng để lưu trữ thông tin như trong các thiết bị như máy ảnh kỹ thuật số, flash memory và một số thiết bị cầm tay khác.
FAT không hỗ trợ bảo mật nội bộ. Nếu user đăng nhập được vào 1 máy tính thì sẽ có toàn quyền truy cập vào files và folders trong phân vùng FAT trên máy tính
FAT cung cấp truy câp nhanh đến files. Tốc độ truy cập files sẽ phụ thuộc vào kiểu file, loại file, kích thước phân vùng, sự phân mảnh và số file trong folder
Mỗi file trong FAT sẽ được đại diện bởi 1 danh sách liên kết các block. Phần cuối của block trước sẽ chứa ID của  block tiếp theo và nó được lưu vào bảng cấp phát, sẽ có 1 giá trị đặc biệt (giá trị âm) để thể hiện rằng 1 block đang nằm ở cuối chuỗi. Bảng cấp phát còn chứa 1 bit để xác định xem 1 block có đang sẵn hay không. Starting block sẽ được lưu trong Directory Table Format cùng với filename và metadata tương ứng



Hiện nay FAT không thể đáp ứng được hiệu năng và sự mở rộng của hệ thống nên không còn được sử dụng bởi Windows và được thay thế bằng NTFS
- Version tiên tiến nhất của FAT là FAT32 với các đặc tính như sau:
     - Hỗ trợ max file size 4GB và ổ đĩa lớn (lên đến 2TB) cùng với hiệu năng lưu trữ tốt hơn
     - Cung cấp truy cập nhanh với kích thước phân vùng trong khoảng từ 500Mb đến 2GB
#### 2. NTFS (New technology file system):
NTFS hay New Technology File System được sử dụng để lưu trữ và truy hồi files trên các hệ điều hành Windows mới.
- Hỗ trợ file lên tới 16 EB, tuy nhiên giới hạn thực tế là 2 TB
- Security: Cung cấp bảo mật cho file và folder. Security được đảm bảo bằng việc cấp quyền truy cập NTFS cho các files và folders. Mỗi file và folder trong NTFS đều có 1 danh sách điều khiển truy cập (Access Control List). Nó chứa users và groups SID (Security Identifier - Mã định danh bảo mật) và đặc quyền được cấp cho họ
- Nén File: Cung cấp việc nén file đến 50%
- Độ tin cậy cao: Là file system có thể khôi phục. Sử dụng các logs trao đổi để cập nhật file và folders logs tự động. Hệ thống cũng có khả năng chịu lỗi tốt. Nếu quá trình trao đổi logs thất bại do lỗi nguồn hay hệ thống thì các log đã được trao đổi sẽ được sử dụng để khôi phục dữ liệu
- Hỗ trợ Bad-cluster mapping. Nó nghĩa là file system có thể phát hiện được các vùng đĩa bị lỗi và những dữ liệu đó sẽ được truy hồi và lưu trữ ở khu vực khác. Khu vực bị lỗi này sẽ được đánh dấu lại để bảo vệ dữ liệu lưu trữ về sau.
#### 3. HFS (Hierarchical file system)
HFS là file system được sử dụng trên máy tính Macintosh để tạo ra 1 directory vào thời điểm ổ đĩa cứng được format
So với các file system khác, HFS giảm đi số lượng block cấp phát cũng như kích thước block, từ đó các files lớn sẽ sử dụng ít không gian ổ đĩa hơn và nâng giới hạn file lên 8 Eb. Cụ thể hơn có 4 blocks cấp phát trong HFS, mỗi block 512 bytes. HFS cung cấp 1 cơ chế chủ động khi sẽ tự động tìm đủ không gian trống để cấp cho 1 file mới trước khi thực hiện viết và hạn chế việc phân mảnh. Và cũng vì thế việc tăng file sizes sẽ đẫn dến việc phải viết lại files.
#### 4. GFS (Global file system)
GFS là file system được sử dụng cho HĐH Linux. GFS là 1 cluster các files được chia sẻ giữa 1 số các máy tính và các hệ thống cuối nơi dữ liệu hay dịch vụ được truy cập, lưu trữ và dẫn đến. Khi khoảng cách vật lý của 2 hệ thống rất xa nó không thể gửi files trực tiếp cho nhau thì GFS file system sẽ giúp chúng có thể chia sẻ dữ liệu trực tiếp. GFS cung cấp việc truy cập trực tiếp đến block storage được chia sẻ và có thể được sử dụng như 1 local file system
#### 5. Ext (Extended File System)
Extended File System hay hệ thống mở rộng tập tin là filesystem đầu tiên được thiết kế dành riêng cho Linux. 
Cấu trúc dữ liệu của ext filesystem được chia thành nhiều block. Các block này được nhóm lại thành các block group. Trên một hệ thống filesystem lớn có khoảng hàng ngàn các block như vậy. Dữ liệu của một file bất kỳ sẽ được chứa trong một block group duy nhất nào đó khả dụng. Điều này giúp giảm thiểu số lần truy xuất trên đĩa khi đọc một lượng lớn dữ liệu nối tiếp nhau.
Mỗi block group sẽ luôn bao gồm superblock và descriptor table (bảng mô tả) của block group đó giống hệt nhau. Và các block group còn bao gồm các block sau: block bitmap, inode bitmap, inode table, và cuối cùng là data block (block thực sự chứa dữ liệu)
#### 6. XFS 
File system có khả năng mở rộng và hiệu năng cao. Nó được tạo ra để hỗ trợ các file lớn (lên đến 16 EB) và cấu trúc directory phức tạp (lên đến 10 triệu entries)
Đặc điểm chính của XFS là metadata journaling (ghi lại nhật ký metadata) giúp việc khôi phục sau crash nhanh và đơn giản hơn. XFS file system còn có thể chống phân mảnh và thay đổi kích thước file dữ liệu,… nhưng không thể shrink – chia nhỏ phân vùng XFS.
Một đặc tính quan trọng của XFS đó là khả năng bảo đảm tốc độ truy xuất dữ liệu cho các ứng dụng (Guaranteed Rate I/O),  cho phép các ứng dụng duy trì được tốc độ truy xuất dữ liệu trên disk

### IV. Tài liệu tham khảo
- [FileSystem là gì? | #3 (kipalog.com)](https://kipalog.com/posts/FileSystem-la-gi-----3)
- [What is a File System? (techtarget.com)](https://www.techtarget.com/searchstorage/definition/file-system)
- [(9) File Allocation Table - YouTube](https://www.youtube.com/watch?v=V2Gxqv3bJCk)
- [Types of File Systems | FAT | FAT32 | NTFS | exFAT | HFS+| APFS | – Byte-Notes
](https://byte-notes.com/types-of-file-systems/)
- [Chapter 8. The XFS File System Red Hat Enterprise Linux 6 | Red Hat Customer Portal
](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/storage_administration_guide/ch-xfs)
- [Giới thiệu một số File System phổ biến - VinaHost
](https://blog.vinahost.vn/gioi-thieu-mot-so-file-system)
- [What is a Global File System? - Definition from Techopedia
](https://www.techopedia.com/definition/1019/global-file-system-gfs)
- [File System | What is a File System - javatpoint](https://www.javatpoint.com/file-system)



