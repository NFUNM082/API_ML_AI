# 智能拍照pose推荐应用

| 发布日期 | 2019-12-10（初稿） |
|---|---|
| 文档状态 | 未完成 |
| 文档主人 | 吴扬扬 |
## 价值主张设计
### 背景
1.移动社交催生出以照片作为交流的社交方式，拍照类应用成为固定需求，独特的拍照功能受到青睐。
2.自拍软件成为如今很多人必备的手机应用，尤其女性的使用频率很高。自拍软件除了其美颜功能吸引到用户的使用，用户也会想要在拍照时摆出好看的pose，因此很多美颜相机推出了教人拍照新功能，用户可在软件中选择自己喜欢的网红拍照姿势，屏幕中就会出现该姿势的线框。
3.其实每个人都有自己习惯的拍照姿势，如果用户原先就有自己喜欢的拍照姿势，只是希望能调整成更佳的，但不知道如何做。目前还没有找到有一款自拍软件所带的教人拍照功能是可以识别用户自身姿势并做出推荐的。
### 目标
帮助想以好看的pose拍照的人群节省在数据库里挑选的时间，推荐更符合个人特点的pose，引导用户调整自身姿势至最佳。
### 加值宣言
-	该智能拍照pose推荐应用是与自拍软件结合的产品，结合图像识别分析和推荐系统，在自拍软件中教人拍好看照功能的基础上，推荐用户想要拍适合自己的好看照片的个性化需求。
-	调用了百度AI的人体关键点识别和手部关键点识别的API，当用户试拍了一张照片后，应用可对用户的肢体动作即姿势进行检测并返回人体部位关键点定位数值。
-	（后期）用户可直接按照自己习惯和喜好摆出pose试拍，应用自动匹配相似的网红拍照姿势，引导用户调整自身姿势使得照片更美观。
-	（后期）应用自动储存用户使用过的pose数据，推荐系统会在下一次用户使用时推荐被使用次数最多的姿势。
### 核心价值
识别用户的试拍照片返回人体部位关键点定位数值，以用户试拍照片为基础，并在应用内已存数据中自动匹配，推荐给用户最佳相似的拍照姿势引导修正。更快让用户的个性化需求得以实现，同时获得更好的拍照体验。。
### 核心价值与用户痛点
1.	刚使用该软件的人未接触过教人拍照功能，要先根据教程学习如何查看好看的拍照姿势。
2.	用户挑了很多个数据库里的网红拍照姿势一个个去试，花费很多时间且不一定能找到自己喜欢的。
3.	用户想要以一种特定的姿势拍照，但是细节不知道如何摆正，很难在既有的数据库里找到自己想要的那种姿势。
4.	用户被别人夸赞上次拍照片的pose很好看，想找到上次拍照时用的是哪种pose。
### 人工智能概率性与用户痛点
百度AI人体分析的手部关键点识别和人体关键点识别分别可识别图像中所有手部、人体位置，精确定位手部、人体关键点并返回关节节点的坐标信息。  
Face++的人体关键点技术可定位并返回人体各部位关键点坐标位置，可进行动作分类和行为识别。  
错误概率：应用支持多人拍照，可识别和储存多人人体部位关键点的坐标位置，因此一台应用中历史储存的信息就不止机主用户一个人，在推荐历史pose时可能会出现非该用户的他人信息。但是此概率较小也可避免。每个人都有自己的特性因此人体关键点存在不同，使用时应用会根据使用者的关键点数据来推荐pose，用户也可在“使用过的pose”里查找自己想要的pose。此错误概率对用户正常使用的影响较小。
### 需求列表与人工智能API加值

标题 | 案例 | API及功能
-|-|-
1 | 识别检测 | 用户试拍一张照片后，应用检测照片中的人体部位关键点检测，返回关键点数值以进行匹配。 | 百度AI-人体关键点检测、手部关键点识别；Face++-人体关键点。
2 | 推荐最佳pose | 用户想要用自己喜欢的姿势拍照，但是细节动作不知道如何摆才好看，需要找到和既定姿势相近的进行比对和学习调整。 | 推荐系统（后期做）
3 | 发现新功能 | 用户未了解过教人拍照摆pose功能，当使用拍照软件拍照时，应用自动给用户推荐好看的pose，让用户发现并尝试此功能。 | 推荐系统（后期做）
4 | 历史记录 | 用户下一次拍照时，想起之前拍的某张照片很好看，依旧想用那个pose拍照。 | 搜索历史关键点定位数值，筛选出曾经用过的pose。

## API
### API调用
#### 百度
- 人体关键点识别：  
检测图像中的人体并返回人体矩形框位置，精准定位21个核心关键点，包含头顶、五官、颈部、四肢主要关节部位，支持多人检测、大动作等复杂场景。  
接口地址：https://aip.baidubce.com/rest/2.0/image-classify/v1/body_analysis  
服务实例：  
输入  
```
import requests
import base64

'''
人体关键点识别
'''

request_url = "https://aip.baidubce.com/rest/2.0/image-classify/v1/body_analysis"
f = open('C:/Users/admin/Desktop/timg.jpg', 'rb')
img = base64.b64encode(f.read())

params = {"image":img}
access_token = '24.2d1aae592f1ccec3e9b41791d9c2dae2.2592000.1578589192.282335-17992819'
request_url = request_url + "?access_token=" + access_token
headers = {'content-type': 'application/x-www-form-urlencoded'}
response = requests.post(request_url, data=params, headers=headers)
if response:
    print (response.json())
```  
输出  
![百度人体关键点识别.png](https://upload-images.jianshu.io/upload_images/9437529-44aa1f7d56d1781a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 手部关键点识别：  
检测图片中的手部并返回手部矩形框位置，定位手部的21个主要骨节点。  
接口地址：https://aip.baidubce.com/rest/2.0/image-classify/v1/hand_analysis  
服务实例：  
输入  
```
import requests
import base64

'''
手部关键点识别
'''

request_url = "https://aip.baidubce.com/rest/2.0/image-classify/v1/hand_analysis"
f = open('C:/Users/admin/Desktop/hands.jpg', 'rb')
img = base64.b64encode(f.read())

params = {"image":img}
access_token = '24.2d1aae592f1ccec3e9b41791d9c2dae2.2592000.1578589192.282335-17992819'
request_url = request_url + "?access_token=" + access_token
headers = {'content-type': 'application/x-www-form-urlencoded'}
response = requests.post(request_url, data=params, headers=headers)
if response:
    print (response.json())
```  
输出  
![百度手部关键点识别.png](https://upload-images.jianshu.io/upload_images/9437529-b79e6eb22758d0e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### Face++
- HumanBody Segment API（人体关键点）：  
定位并返回人体各部位关键点坐标位置。关键点定位了头、颈、肩、肘、手、臀、膝、脚等部位。  
接口地址：https://api-cn.faceplusplus.com/humanbodypp/v1/skeleton  
服务实例： 
输入  
```
import urllib.request
import urllib.error
import time

http_url = 'https://api-cn.faceplusplus.com/humanbodypp/v1/skeleton'
key = "uFv2kNuA331u_pZRlZKEoy_ZyTbkEKjT"
secret = "2vED9Ye9anJjngSyKVATLHcD8Ks88cTM"
filepath = r"C:\Users\admin\Desktop\timg.jpg"

boundary = '----------%s' % hex(int(time.time() * 1000))
data = []
data.append('--%s' % boundary)
data.append('Content-Disposition: form-data; name="%s"\r\n' % 'api_key')
data.append(key)
data.append('--%s' % boundary)
data.append('Content-Disposition: form-data; name="%s"\r\n' % 'api_secret')
data.append(secret)
data.append('--%s' % boundary)
fr = open(filepath, 'rb')
data.append('Content-Disposition: form-data; name="%s"; filename=" "' % 'image_file')
data.append('Content-Type: %s\r\n' % 'application/octet-stream')
data.append(fr.read())
fr.close()
data.append('--%s' % boundary)
data.append('Content-Disposition: form-data; name="%s"\r\n' % 'return_landmark')
data.append('1')
data.append('--%s' % boundary)
data.append('Content-Disposition: form-data; name="%s"\r\n' % 'return_attributes')
data.append(
    "gender,age,smiling,headpose,facequality,blur,eyestatus,emotion,ethnicity,beauty,mouthstatus,eyegaze,skinstatus")
data.append('--%s--\r\n' % boundary)

for i, d in enumerate(data):
    if isinstance(d, str):
        data[i] = d.encode('utf-8')

http_body = b'\r\n'.join(data)

# build http request
req = urllib.request.Request(url=http_url, data=http_body)

# header
req.add_header('Content-Type', 'multipart/form-data; boundary=%s' % boundary)

try:
    # post data to server
    resp = urllib.request.urlopen(req, timeout=5)
    # get response
    qrcont = resp.read()
    # if you want to load as json, you should decode first,
    # for example: json.loads(qrount.decode('utf-8'))
    print(qrcont.decode('utf-8'))
except urllib.error.HTTPError as e:
    print(e.read().decode('utf-8'))
```  
输出  
![face++人体关键点.png](https://upload-images.jianshu.io/upload_images/9437529-063439b6a2992be1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### API比较
1.百度AI与此应用有关的有人体关键点识别和手部关键点识别。  
免费版适用于个人开发者和企业测试期使用。50000次/天的调用量；2 QPS的并发支持；5工作日内的客服响应。  
2.Face++与此应用有关的是人体关键点。  
能够定位并返回人体各部位关键点坐标位置。关键点定位了头、颈、肩、肘、手、臀、膝、脚等部位。可进行动作分类和人体关键点构图。  
免费服务有以下这些限制：并发数有上限且不保证并发：由于资源有限，在调用繁忙的情况下，您的请求有可能会受到并发限制。每个用户使用免费服务只能创建 1000个 FaceSet，总计最多存储 100 万个人脸。一个用户只能有一个 API Key 使用免费服务，而且该 API Key 不能转为正式 API Key。  
### 使用风险报告
-	 所有用到的api可免费调用，使用到应用上要考虑“按量”或“按QPS”灵活升级付费服务。  
-	Face++人脸识别领域占有技术优势，在人体关键点中可附加异常行为检测。  
-	Face++未有手部关键点识别的api，仅使用百度的手部关键点识别api
### 所用API
百度：人体关键点识别和手部关键点识别  
Face++：人体关键点。

