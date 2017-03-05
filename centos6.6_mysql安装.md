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
