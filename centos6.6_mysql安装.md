>安装mysql

rpm -qa | grep mysql　　// 这个命令就会查看该操作系统上是否已经安装了mysql数据库</br>
rpm -e mysql　　// 普通删除模式</br>
rpm -e --nodeps mysql　　// 强力删除模式，如果使用上面命令删除时，提示有依赖的其它文件，则用该命令可以对其进行强力删除</br>
yum list | grep mysql	 //查看yum上提供的mysql数据库可下载的版本</br>
yum install -y mysql-server mysql mysql-deve	//下载</br>
rpm -qi mysql-server	//查看mysql版本</br>
service mysqld start	//启动mysql</br>
service mysqld restart	//重启mysql</br>
chkconfig --list | grep mysqld	//查看mysql服务是不是开机自动启动</br>
mysqld             0:关闭    1:关闭    2:关闭    3:关闭    4:关闭    5:关闭    6:关闭</br>
chkconfig mysqld on	//设置成开机启动，这样就不用每次都去手动启动了</br>
/usr/bin/mysqladmin -u root password 'root'	//设置账号密码</br>
mysql -u root -p	//进入mysql数据库</br>
Enter password:		//输入密码即可</br>
完毕！</br>

>centos6.6安装mysql5.7.17

因用yum安装的是比较古老的mysql版本，所以需要升级最新版本</br>
首先查看安装的mysql，需要全部移除</br>
rpm -qa | grep mysql</br>
mysql-community-common-5.1.17-1.el6.x86_64</br>
mysql-community-libs-5.2.17-1.el6.x86_64</br>
mysql-community-server-5.1.17-1.el6.x86_64</br>
mysql-community-client-5.1.17-1.el6.x86_64</br>
一共四个需要全部删除</br>
rpm -e --nodeps mysql-community-common-5.1.17-1.el6.x86_64</br>
rpm -e --nodeps mysql-community-libs-5.2.17-1.el6.x86_64</br>
rpm -e --nodeps mysql-community-server-5.1.17-1.el6.x86_64</br>
rpm -e --nodeps mysql-community-client-5.1.17-1.el6.x86_64</br>
rpm -qa | grep mysql</br>
确保没有了mysql</br>

进入：https://dev.mysql.com/downloads/file/?id=467446</br>
下载到的包：mysql-5.7.17-1.el6.x86_64.rpm-bundle.tar</br>
cd /tmp</br>
rz mysql-5.7.17-1.el6.x86_64.rpm-bundle.tar</br>
tar -xvf mysql-5.7.17-1.el6.x86_64.rpm-bundle.tar</br>
rpm -ivh mysql-community-common-5.7.17-1.el6.x86_64.rpm</br>
rpm -ivh mysql-community-libs-5.7.17-1.el6.x86_64.rpm</br>
rpm -ivh mysql-community-client-5.7.17-1.el6.x86_64.rpm</br>
rpm -ivh mysql-community-server-5.7.17-1.el6.x86_64.rpm</br>
chmod 777 -R /var/lib/mysql</br>
service mysqld start</br>
MySQL Daemon failed to start.</br>
正在启动 mysqld： [失败]</br>
getenforce</br>
Enforcing</br>
setenforce 0</br>
service mysqld start</br>
正在启动 mysqld： [确定]</br>
mysql</br>
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)</br>
尼玛，我怎么知道密码？我都没设置密码</br>
/usr/bin/mysqld_safe --skip-grant-tables &</br>
mysql -u root -p</br>
下面的密码直接键入回车即可.</br>
use mysql</br>
update mysql.user set authentication_string=PASSWORD('root') where user='root' and host='localhost';</br>
flush privileges;</br>
exit;</br>
mysql -u root -p</br>
输入密码即可</br>
完毕！</br>
