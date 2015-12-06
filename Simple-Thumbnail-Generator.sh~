#!/bin/bash
clear
echo "This is a simple bash script to resize jpg images to a box of specified values while preserving aspect ratio. You should run it from the folder with the images you want resized (you may need to run as root). It ignores files marked with the current pre tag (and overwrites them). Also tells you how many files were proccessed."
echo "This script was made by George Marusteru @ Hatch Hackerspace Bucharest" 
echo "This script is offered as is, you can consider it GPLv3 liscence, meaning this is free software and you can do whatever you want with it except release it in a different liscence." 
read -e -p "Please specify your user name (the script may need to be run as root, this just changes the files ownership back to you when done):" owner;
echo "Thank you, your username is: $owner"
read -e -p "Please specifiy a pre tag (the underscore is included, ex: 'thumb'): " -i "thumb" tag;
echo "Thank you, your pre tag is: $tag"
read -e -p "Please specify the X limit (width) of your bounding box:" xvalue;
if [ $xvalue -ne 0 -o $xvalue -eq 0 2>/dev/null ]
then
echo "Everything looks fine. Your X limit (width) is: $xvalue"
else 
echo "Yeah, $xvalue doesn't look like a number. This might fail."
fi 
read -e -p "Please specify the Y limit (height) of your bounding box:" yvalue; 
if [ $yvalue -ne 0 -o $yvalue -eq 0 2>/dev/null ]
then
echo "Everything looks fine. Your Y (height) is: $yvalue"
else 
echo "Yeah, $yvalue doesn't look like a number. This might fail."
fi
read -e -p "Please specify the quality value (compression) for your files [1-100] (ex:'70', default '75'): " -i "75" quality; 
if [ $quality -gt 0 -a $quality -le 100 -o $quality -eq 0 2>/dev/null ]
then
echo "Everything looks fine. Your quality value is: $quality"
else 
echo "Yeah, $quality doesn't look like a valid number [1-100]. Defaulting to 75."
quality=75
fi
count=0
for i in [!^$tag]*.jpg [!^$tag]*.JPG 
do
echo "Processing image $i ..."
djpeg $i | pnmscale -xysize $xvalue $yvalue | cjpeg -optimize -progressive -quality $quality > $tag"_"$i 
chown $owner $tag"_"$i
echo $i processed
count=$[$count+1]
done
echo "$count files proccessed."
