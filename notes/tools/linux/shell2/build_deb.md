```
#!/bin/bash

path=`pwd`
if [ ! -d "debian" ]
then
	mkdir "debian"
else
	rm -rf "debian"
	mkdir "debian"
fi 

for filename in `ls src`
do
	echo $filename
	if [ ${filename##*.} != "txt" ]
	then
		path1=$path/src/$filename
		cd $path1

		bloom-generate rosdebian --os-name ubuntu --ros-distro melodic
		if [ $? -ne 0 ]; then
		  exit 0
		fi

		fakeroot debian/rules binary
		if [ $? -ne 0 ]; then
		  exit 0
		fi

		#path2=$path/debian/$filename
		#if [ ! -d "$path2" ]; then
	    #mkdir "$path2"
		#fi

		#rm -rf $path2/*
		mv ../ros-melodic-*deb $path/debian
		rm -rf debian obj-x86_64-linux-gnu ../ros-melodic-*deb

		#echo

#		sudo dpkg -i $path2/*



	fi
done

echo -e "\033[32m--------------------------------\033[0m"
echo -e "\033[32m--------------------------------\033[0m"

ls $path/debian

echo -e "\033[32m--------------------------------\033[0m"
echo -e "\033[32m--------------------------------\033[0m"

```

simple:
```
#!/bin/bash

path=`pwd`
if [ ! -d "debian" ]
then
	mkdir "debian"
fi

path1=$path/src/$1
cd $path1

bloom-generate rosdebian --os-name ubuntu --ros-distro melodic
if [ $? -ne 0 ]
then
	exit 0
fi
fakeroot debian/rules binary
if [ $? -ne 0 ]
then
	exit 0
fi

mv ../ros-melodic-*deb $path/debian
rm -rf debian obj-x86_64-linux-gnu ../ros-melodic-*deb

echo -e "\033[32m------------------------------\033[0m"
echo -e "\033[32m------------------------------\033[0m"

ls $path/debian

```