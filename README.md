# Data process scripts for detection

## 视频截帧保存
   脚本 extract_frames.py

##  将图片上传到bucket
    1. 配置脚本 bkt-upload-config.json
    2. qshell 命令  qshell qupload 300 bkt-upload-config.json

## 转化为labelx 格式发包打标
   转化脚本transform2labelx_json.py， 根据具体任务选择参数，如发分类包
   采用img2json_cls， 检测包采用 img2json_det

## 检测发包回收后，解析为voc 格式，可以选择将新的图片添加到原来的voc 格式数据集中或创建新的voc 数据集
   脚本labelx_new_voc.py， 根据具体情况微调脚本

   出现文件名重复的图片时，会在新文件名后添加_re，直到与原数据集中的图片文件名不再重复为止

   脚本运行时，如下所示，会先显示共要处理多少张图片，然后显示处理至多少张图片，如果出现相同文件名的图片，会显示rename
   ```
   add to original voc data set
   the totoal image number is 15000.
   Dealing the 1th image.
   Dealing the 2th image.
   rename
   Dealing the 3th image.
   ```
   
   脚本中类 jsontoVoc(srcJson,expectPath,isBucket,imageSplitrate,addtoorigin)

   参数解析
   ```
   srcJson:标识labelx源文件路径

   expectPath:表示输出的原VOC格式数据集路径（或新的voc格式数据集如果你想创建新的voc 数据集）

   isBucket:表示图片是否来源于远程地址

   imageSplitrate:表示0-1的浮点数，表示图片随机初始化为训练集的概率,默认为None

   addtoorigin:表示是否将新的图片添加到原有的voc 格式数据集中
   ```