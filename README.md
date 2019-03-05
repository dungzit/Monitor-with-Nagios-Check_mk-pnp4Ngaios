# Monitor-with-Nagios-Check_mk-pnp4Ngaios
ted on 6 Tháng Mười, 2017 by maytinhlion	

Nagios là một hệ thống giám sát mạnh mẽ cho phép các tổ chức xác định và giải quyết các vấn đề cơ sở hạ tầng CNTT trước khi chúng ảnh hưởng nghiêm trọng đến quá trình kinh doanh.

Đầu tiên ra mắt vào năm 1999, Nagios đã phát triển với hàng ngàn dự án được phát triển bởi cộng đồng Nagios trên toàn thế giới . Nagios chính thức bảo trợ bởi doanh nghiệp Nagios, hỗ trợ các cộng đồng trong một số cách khác nhau thông qua doanh số bán hàng thương mại của sản phẩm và dịch vụ .

Nagios theo dõi toàn bộ cơ sở hạ tầng CNTT của bạn để đảm bảo hệ thống, ứng dụng, dịch vụ và quy trình kinh doanh đang hoạt động tốt. Trong trường hợp thất bại, Nagios có thể cảnh báo vấn đề với nhân viên kỹ thuật, cho phép họ bắt đầu quá trình phục hồi trước khi bị sự cố, ảnh hưởng đến quá trình kinh doanh, người sử dụng, hoặc khách hàng. Với Nagios bạn không bao giờ phải giải thích tại sao một sự cố vô hình lại xảy ra đối với cơ sở hạ tầng mấu chốt của tổ chức.
A. Chức năng

    Giám sát trạng thái hoạt động của các dịch vụ mạng (SMTP, POP3, IMAP, HTTP, ICMP, FTP, SSH, DHCP, LDAP, DNS, name server, web proxy, TCP port, UDP port, cở sở dữ liệu: mysql, portgreSQL, oracle)
    Giám sát các tài nguyên các máy phục vụ và các thiết bị đầu cuối (chạy hệ điều hành Unix/Linux, Windows, Novell netware): tình trạng sử dụng CPU, người dùng đang log on, tình trạng sử dụng ổ đĩa cứng, tình trạng sử dụng bộ nhớ trong và swap, số tiến trình đang chạy, các tệp log hệ thống.
    Giám sát các thông số an toàn thiết bị phần cứng trên host như: nhiệt độ CPU, tốc độ quạt, pin, giờ hệ thống…
    Giám sát các thiết bị mạng có IP như router, switch và máy in. Với Router, Switch, Nagios có thể theo dõi được tình trạng hoạt động, trạng thái bật tắt của từng cổng, lưu lượng băng thông qua mỗi cổng, thời gian hoạt động liên tục (Uptime) của thiết bị. Với máy in, Nagios có thể nhận biết được nhiều trạng thái, tình huống sảy ra như kẹt giấy, hết mực…
    Cảnh báo cho người quản trị bằng nhiều hình thức như email, tin nhắn tức thời (IM), âm thanh …nếu như có thiết bị, dịch vụ gặp trục trặc
    Tổng hợp, lưu giữ và báo cáo định kỳ về tình trạng hoạt động của mạng.

B. Đặc điểm

Các hoạt động kiểm tra được thực hiện bởi các plugin cho máy phục vụ Nagios và các module client trên các thiết bị của người dùng cuối, Nagios chỉ định kỳ nhận các thông tin từ các plugin và xử lý những thông tin đó (thông báo cho người quản lý, ghi vào tệp log, hiển thi lên giao diện web…).

Thiết kế plugin đơn giản cho phép người dùng có thể tự định nghĩa và phát triển các plugin kiểm tra các dịch vụ theo nhu cầu riêng bằng các công cụ lập trình như shell scripts, C/C++, Perl, Ruby, Python, PHP, C#.

Có khả năng kiểm tra song song trạng thái hoạt động của các dịch vụ( đồng thời kiểm tra nhiều dịch vụ).

Hỗ trợ khai báo kiến trúc mạng. Nagios không có khả năng nhật dạng được topo của mạng. toàn bộ các thiết bị, dịch vụ muốn được giám sát đều phải khai báo và định nghĩa trong cấu hình.

Gửi thông báo đến người/nhóm người được chỉ định sẵn khi dịch vụ/host được giám sát gặp vấn đề và khi chúng khôi phục hoạt động bình thường.(qua e-mail, pager, SMS, IM…)

Khả năng định nghĩa bộ xử lý sự kiện thực thi ngay khi có sự kiện sảy ra với host/ dịch vụ.

Giao diện web cho phép xem trạng thái của mạng, thông báo, history, tệp log.
C. Triển khai hệ thống moniroting với Nagios + Check_mk + pnp4Nagios

Mặc định hệ thống Nagios chỉ là phần Core cung cấp một hệ thống thống kê dịch vụ, ghi nhận alert, cảnh báo, phân tích dữ liệu…. bên cạnh đó nó còn phải đi kèm các plugin hỗ trợ monitor hay còn gọi là cac agent thường dùng là mrpe tuy nhiên với mỗi service đặt ra cho một host thì tương ứng với một request đề giải quyết vướng mắc đó một developer đã phát triển một sản phẩm free gọi là check_mk chỉ với một resquest (session) là có thể có đầy đủ các thông tin monitor từ host thông qua các script được thiết kế sẵn.

Một điều không kém phần quan trộng đó chính là chart bản thân Nagios ko hỗ trợ chart mà vận cần các plugin khác hỗ trợ chart ở đây sử dụng pnp4Nagios vì nó và check_mk là một cặp được thiết kế đi cùng nhau hỗ trợ đơn giản hóa các cấu hình cho người dùng loại bỏ các nhân tố phức tạp trong việc khai báo một service cũng như chart.
I. Chuẩn bị

– 1 Server Centos 5.6 (full update)

– Down bản cài đặt

o Nagios tại http://nagios.org/download/core

(bản sử dụng trong bài Nagios-3.3.1)

o Nagios Plugins tạii http://nagios.org/download/plugins

(bản sử dụng trong bài nagios-plugins-1.4.15

o Check_mk bản stable tại http://mathias-kettner.de/check_mk_download.html

(bạn sử dụng trong bài check_mk-1.1.12p6)

o PNP4Nagios tại http://docs.pnp4nagios.org/pnp-0.4/dwnld

(bạn sử dụng trong bài pnp4nagios-0.6.16)

clip_image001[4]
II. Cài đặt Nagios Core

Bước 1: đăng nhập quyền root và cài đặt các gói yêu cầu cần thiết trước khi cài đặt Nagios

# yum install httpd php gcc glibc glibc-common gd gd-devel xinetd -y

clip_image003[4]

 

Bước 2:Tạo tài khoản cho hệ thống nagios

Tạo tài khoản nagios cho hệ thống nagios có thể thay đổi tài khoản khác nhưng yêu cầu cần nhớ thông tin để cấu hình cho các module khác trên nagios

# useradd -m nagios

# passwd nagios

Tạo nhóm mặc định dành cho nagios (nhóm này tên đặt không bắt buộc nhưng yêu cầu thêm option khai báo cho các cài đặt module khác)

# groupadd nagcmd

# usermod -a -G nagcmd nagios

# usermod -a -G nagcmd apache

Bước 3:cài đặt Nagios Core

Giải nén gói cài đặt

# tar -xzvf nagios-3.3.1.tar.gz

Chuyển vào thư mục vùa xả nén

# cd nagios

Chạy script config nagios với group vừa tạo (thay đổi tên group cho phuù hợp)

# ./configure –with-command-group=nagcmd

Biên dịch Nagios source code

# make all

Cuối cùng là cài đặt thư viện, init script, config mẫu cho Nagios

# make install

# make install-init

# make install-config

# make install-commandmode

Cài đặt giao diện web Nagios

# make install-webconf

Tạo một tài khoản Administrator dùng để quản trị trên giao diện web của Nagios

# htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin

Restart dịch vụ httpd

# service httpd restart

Bước 4:Cài đặt Nagios Plugins

Giải nén gói cài đặt Nagios-Plugins

# tar -xzvf nagios-plugins-1.4.15.tar.gz

Chuyển vào thư mục vùa giải nén

# cd nagios-plugins-1.4.15

Biên dịch gói cài đặt khai báo tùy chọn user và group nagios cho phuù hợp

# ./configure –with-nagios-user=nagios –with-nagios-group=nagios

Cài đặt

# make

# make install

Bước 5:start nagios

Thêm Nagios và httpd vào chệ độ tự động start khi hệ thống boot

#chkconfig –add nagios

#chkconfig nagios on

# chkconfig httpd on

Bước 6: kiểm tra cấu hình Nagios

# /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

Nếu không có lỗi thì hệ thống đã sẵn sàng start

# service nagios restart

Đăng nhập và kiểm tra giao diện webbase của Nagios

http://sns-vmw-nagios/nagios/
Phần 2: Triển khai hệ thống monitor với Nagios + Check_mk + pnp4Ngaios

Tiếp tục Phần 1 trong phần này chúng ta sẽ thao tác các bước cài đặt component check_mk
III. Cài đặt Check_mk

Bước 1: Giải nén gói cài đặt

# tar -xzvf check_mk-1.1.12p6.tar.gz

Bước 2: Chuyển vào thư mục check_mk vừa giải nén

# cd check_mk-1.1.12p6

Bước 3: cài đặt check_mk

# ./setup.sh

Tùy việc cấu hình các thiết lập Nagios từ bài trước mà khai báo các thông tin cho phù hợp với các thông tin cài đặt để default thì mọi thứ sẽ các bạn để mặc định không cần khai báo

clip_image001[8]

Sau khi hoàn tất cài đặt thì restart httpd và nagios

# service httpd restart

# service nagios restart

# service xinetd start

Đăng nhập vào giao diện riêng của check_mk thay thế cho giao diện mặc định của Nagios  (các alert được tổ chức hợp lý và dễ quan sát hơn so với giao diện core nagios)

http://10.72.0.78/check_mk

Lúc này sẽ hiện thông báo

clip_image003[8]

Đó là do hệ thống chưa cài đặt mod-python cho apache

# yum install mod_python -y

Sau đó là restart httpd và nagios để cập nhất mod-python

clip_image005[8]
II. Cài đặt Check_mk_agent

Check_mk agent là một agent nhỏ được cài đặt trực tiếp trên các host được Nagios monitor có nhiệm vụ run các script có sẵn hoặc do chúng ta thiết lập để trả ra các thông số monitor cần thiết cho nagios.

Trong bài này chúng ta sẽ cai đặt chủ yếu hướng dẫn trên centos và Solaris (nexenta,opensolaris)
1. Check_mk_agent trên Centos

Check_mk_agent được download toàn bộ tại

http://mathias-kettner.de/check_mk_download.html

Đối với hệ thống centos, fedora, redhat trên site sẽ cung cấp sẵn gói rpm

check_mk-agent-1.1.12p6-1.noarch.rpm

Upload gói cài đặt lên server centos cần monitor

# wget http://mathias-kettner.de/download/check_mk-agent-1.1.12p6-1.noarch.rpm

Và tiến hành cài đặt xinetd trước do service agent này sẽ hoạt động chung với xinetd

# yum install xinetd –y

# service xinetd start

# rpm -ivh check_mk-agent-1.1.12p6-1.noarch.rpm

Thay đổi cấu hình check_mk_agent

# vim /usr/bin/check_mk_agent

Thay dòng

    MK_CONFDIR=”/to/be/changed”

thành MK_CONFDIR=”/etc/check_mk”

Thư mục check_mk này sẽ được dùng như thu mục mặc định trên client load các file config service của client

Tạo thư mục /etc/check_mk và một file trắng mrpe.cfg (file config servive của host)

# mkdir /etc/check_mk

# touch /etc/check_mk/mrpe.cfg

Restart agent trên xinetd

# service xinetd restart

Kiểm tra kết quả bằng cách kiểm tra port 6556

# netstat -a | grep 6556

clip_image007[8]

Cuối cùng là telnet port 6556 và kiểm tra hoạt động của agent

clip_image008[8]
2. Check_mk_agent trên Solaris (nexenta, open solaris)

Gói cài đặt check_mk_agent trên solaris (nexenta, opensolaris) ở thời điểm hiện tại viết bài viết này thì vẫn trong giai đoạn phát triển và hoàn thiện thêm nhưng vẫn hàon toàn đáp ứng được các nhu cầu monitor căn bản

Vì lý do đó nên gòi cài đặt này hiện tại sẽ nằm trong gói cài đặt Innovation_release (trong mục download của check_mk). Download và giải nén lấy gói cài đặt

clip_image010[8]

clip_image012[8]

clip_image014[8]

Lấy gói cài đặt này upload lên server solaris đường dẫn /usr/bin và đổi tên thành check_mk_agent

# chmod a+x /usr/bin/check_mk_agent

Thay đổi cấu hình check_mk_agent

# vim /usr/bin/check_mk_agent

Thay dòng

    MK_CONFDIR=”/to/be/changed”

thành MK_CONFDIR=”/etc/check_mk”

Thư mục check_mk này sẽ được dùng như thu mục mặc định trên client load các file config service của client

Tạo thư mục /etc/check_mk và một file trắng mrpe.cfg (file config servive của host)

# mkdir /etc/check_mk

# touch /etc/check_mk/mrpe.cfg

Thêm service check_mk_agent vào /etc/services

check_mk 6556/tcp # CheckMk

Tim file tcpd và copy vào thư mục như sau

# mkdir /usr/sfw/sbin

# cp /us r/sbin/tcpd /usr/sfw/sbin/tcpd

Thêm vào cuối file /etc/inet/inetd.conf

check_mk stream tcp nowait root //usr/sfw/sbin/tcpd /usr/bin/check_mk_agent

Chạy các lệnh cập nhật service mới

# inetconv

check_mk -> /var/svc/manifest/network/ check_mk-tcp.xml l

Importing check_mk-tcp.xml …Done

Lưu ý: inetconv –f dùng để reload lại config khi cần thiết trong trường hợp cầu hình lại

Kế tiếp là enable dịch vụ

# inetconv -e

svc:/network/check_mk/tcp:default enabled

Kiểm tra trạng thái dich vu check_mk

# svcs svc:/network/check_mk/tcp:default

STATE STIME FMRI

online Mar_19 svc:/network/check_mk/tcp:default

Kiểm tra port

# netstat -a | grep check_mk

*.check_mk *.* 0 0 49152 0 LISTEN

Kiểm tra các tham số cài đặt mặc định

# inetadm -l svc:/network/check_mk/tcp:default

Lúc này tcp_wrappers=FALSE cần chuyển thành TRUE

# inetadm -m svc:/network/check_mk/tcp:default tcp_wrappers=TRUE

Kiểm tra lại các thuộc tính cần set

#inetadm -l svc:/network/check_mk/tcp:default

Kiểm tra hoạt động của agent bằng cách:

# telnet 127.0.0.1 6556
Cài đặt Nagios trên Centos

Trong bài này chúng ta sẽ òoàn chỉnh việc cài đặt Ngios 3.3.1 trên Centos.

Tài liệu tham khảo vận hành theo dõi tại http://support.nagios.com/knowledge-base/official-documentation

image
Bước 1: Cài đặt các gói thư viện – service cần thiết

    yum install httpd gcc glibc glibc-common gd gd-devel php

Bước 2: Tạo account và group dành cho việc run các command thông qua giao diện web

    useradd -m nagios

Tạo nhóm nagcmd và đưa user nagios và apache vào nhóm

    groupadd nagcmd

    usermod -a -G nagcmd nagios

    usermod -a -G nagcmd apache

Bước 3: Tạo thư mục và down các file cài đặt Nagios

    mkdir /opt/Nagios

Download gói core của Nagios và Plugins

http://www.nagios.org/download/download.php

Gói tải về trong bài này là Nagios-3.3.1.tar.gz và nagios-plugins-1.4.15-35-g355a.tar.gz
Bươc 4: cài đặt Nagios

Xả nén 2 file trong thư mục Nagios vùa tạo

    cd /opt/Nagios

    tar –xzvf nagios-3.3.1.tar.gz

    cd nagios-3.3.1

Biên dịch và cấu hình Nagios

    ./configure –with-command-group=nagcmd

    make all

    make install

    make install-init

    make install-config

    make install-commandmode

Xong bước này thì Nagios đã sẵn sàng trong /usr/local/nagios
Bước 5: Cài đặt giao diện web cho Nagios

    make install-webconf

Tạo user quản trị giao diện web

    htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin

    Start dịch vụ httpd

    service httpd start

    chkconfig httpd on

Bước 6 : Cài đặt Nagios plugin

    cd /opt/Nagios

    tar xzf  nagios-plugins-1.4.15-35-g355a.tar.gz

    cd  nagios-plugins-1.4.15-35-g355a

Biên dịch và cài đặt Nagios

    ./configure –with-nagios-user=nagios –with-nagios-group=nagios

    make

    make install

Cấu hình địa chỉ admin nhận các alerts trong file  /usr/local/nagios/etc/objects/contacts.cfg

Sữa dòng

    email nagios@localhost ; <<***** CHANGE THIS TO YOUR EMAIL ADDRESS ******

Check lại file cấu hình mặc định của Nagios

    /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

    Total Warnings: 0

    Total Errors: 0

Start dịch vụ Nagios

    chkconfig –add nagios

    chkconfig nagios on

    service nagios start

Bước 7: log on và kiểm tra kết quả qua trang admin

    http://ip-address/nagios/

Lưu ý:

Khi cài đặt xong hệ thống Nagios mặc định sẽ add localhost làm đối tượng monitor đầu tiên lúc này dịch vụ http của localhost sẽ được monitor nhưng luôn gặp thông báo warning vì không tìm thấy index.html hay index.php.. vì lúc này folder /var/www/hmtl đang rỗng vì thế để giải quyết warning chỉ cần tão một file index.html trong /var/www/html

    touch /var/www/html/index.html
