# Hello-DW
python脚本中怎么递归遍历文件夹
#在python脚本中,怎么递归遍历文件夹及其子文件夹下的文件,最后按.xls目录查找并复制文件到新文件夹.
#目前只写出了复制当前文件夹的内容.

#!/usr/bin/env python 
# -*- coding: utf-8 -*-          #识别中文

import sys,os,re
reload(sys)
import pandas as pd
import numpy as np
import shutil
import xlrd

#指定文件路径
path_file='D:/aaa/bbb/'  #文件路径
path_file=unicode(path_file,'utf-8')
filename_path='D:/3aaa.xls'  #文件列表
filename_path=unicode(filename_path,'utf-8')

filelist=os.listdir(path_file)        #或者获取文件夹中的文件名称
#filelist = os.listdir(path_file)    #遍历文件夹中所有文件，此处以ls或file
#print(len(filelist))

file_name=pd.read_excel(filename_path)   #读取所需文件列表

file_name['count']=0    #定义新的一列count，用于计数
for file in filelist:
    m=file_name.shape[0]   #表格的行数
    olddir=os.path.join(path_file,file) #每一个文件路径
    for i in range(m):
        if str(file_name['name'][i]) in file:   #寻找对应的文件名
            F="D:/3HA" #新文件夹名称（先建好）
            newdir=os.path.join(F,file)
            shutil.copy(olddir,newdir)      #复制到新文件夹中
            file_name['count'][i]=file_name['count'][i]+1   #计数
            print(file)  #打印出文件名，其实我是为了看它是不是在运行
        else:
            continue

file_name.to_excel('file_name_count.xlsx')        #保存新的文件列表
