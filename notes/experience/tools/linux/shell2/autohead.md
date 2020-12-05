```
#!/bin/bash
#此程序的功能是新建shell文件并自动生成头说明信息
#第一版本
#2017-10-11 07:37:13
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

#判断要创建的文件是否存在，如果文件名不存在
if [ ! "$1" ]　　#注：这里$1代表程序后的第一个参数
then
echo '请输入要新建的文件名称，例如(sh AutoHead.sh Test.sh)'
exit 1
fi 

#如果文件已经创建，直接用vim打开
#if [ -f "$1" ]
#then
#vim "$1"
#echo '文件已存在。'
#exit 2
#fi 

#创建定义的文件
touch "$1".h 
#添加注释信息 
echo "/*" >> "$1".h
echo "*@Description: ">>"$1".h
echo "*@Author: TangBaoFang">>"$1".h
#echo "*@Data: `date "+%Y-%m-%d %H:%M:%S"`">>"$1".h 
echo "*@Data: `date "+%Y-%m-%d"`">>"$1".h 
echo "*@LastEditors: TangBaoFang">>"$1".h
echo "*@LastEditTime: `date "+%Y-%m-%d"`">>"$1".h 
echo "*@LastEditDescription: ">>"$1".h
echo "*/" >> "$1".h
echo "#pragma once" >> "$1".h
echo "" >> "$1".h
echo "#include <iostream>" >> "$1".h

echo "" >> "$1".h
echo "namespace $2" >> "$1".h
echo "{" >> "$1".h
echo "namespace $3" >> "$1".h
echo "{" >> "$1".h
echo "" >> "$1".h
echo "" >> "$1".h
echo "" >> "$1".h
echo "} // namespace $3" >> "$1".h
echo "} // namespace $2" >> "$1".h


#创建定义的文件
touch "$1".cc 
#添加注释信息 
echo "/*" >> "$1".cc
echo "*@Description: ">>"$1".cc
echo "*@Author: TangBaoFang">>"$1".cc
echo "*@Data: `date "+%Y-%m-%d"`">>"$1".cc 
echo "*@LastEditors: TangBaoFang">>"$1".cc
echo "*@LastEditTime: `date "+%Y-%m-%d"`">>"$1".cc
echo "*@LastEditDescription: ">>"$1".cc
echo "*/" >> "$1".cc
echo "#include \"$1.h\"" >> "$1".cc

echo "#include \"boost/format.hpp\"" >> "$1".cc
echo "#include \"glog/logging.h\"" >> "$1".cc

echo "" >> "$1".cc
echo "namespace $2" >> "$1".cc
echo "{" >> "$1".cc
echo "namespace $3" >> "$1".cc
echo "{" >> "$1".cc
echo "" >> "$1".cc
echo "" >> "$1".cc
echo "" >> "$1".cc
echo "} // namespace $3" >> "$1".cc
echo "} // namespace $2" >> "$1".cc

```