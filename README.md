# Pose帮拍应用产品需求文档

| 发布日期 | 2019-12-10（初稿） |
|---|---|
| 产品名称 | Pose帮拍 |
| 文档状态 | 已完成 |
| 文档主人 | 吴扬扬 |
## 价值主张设计
### 1句话版本：  
爱美的人不会摆pose也没关系，pose帮拍摆拍最美照片。
### 1分钟版本：   
Pose帮拍的价值主张是帮爱美的人摆pose，拍出最美照片。对于那些想拍出好看的照片的人群，不会摆pose是一大难题，此产品是一个帮助用户摆拍的智能应用，通过人体关键点识别返回记录用户数值，在图库里匹配择出最相似的网红拍照pose，满足用户需要适应个人习惯的需求。保存历史使用pose数据可节省了用户下次拍照时挑选pose的时间，推荐系统会在下一次用户使用时推荐被使用次数最多的姿势。推荐更符合个人特点的选择，引导用户在拍照过程中调整出最好看的个性化的摆拍姿势。

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
3 | 发现新功能 | 用户未了解过教人拍照摆pose功能，当使用拍照软件拍照时，应用显示识别功能，自动给用户推荐好看的pose，让用户发现并尝试此功能。 | 推荐系统（后期做）
4 | 历史记录 | 用户下一次拍照时，想起之前拍的某张照片很好看，依旧想用那个pose拍照。 | 搜索历史关键点定位数值，筛选出曾经用过的pose。

## 原型
- [原型展示](http://nfunm082.gitee.io/api-pose)
- [原型下载区](https://gitee.com/NFUNM082/api-pose)  
*此产品文档展示的核心功能为识别图像并返回关键点数值，为用户推荐最合适pose。相机应用的滤镜、设置、镜头翻转、图库功能区不做具体展示。*
### 主要功能展示交互与设计
- **Pose帮拍主页面**——拍照功能  
用户进入该应用后可开始拍照，并有【姿势】、【滤镜】、设置、镜头翻转、图库这些功能选择。
![](https://github.com/NFUNM082/API_ML_AI/blob/master/images/%E4%B8%BB%E9%A1%B5%E9%9D%A2.png)
- **拍照页面**——用户按下拍照键后进行下一步操作   
点击主页面的【拍照】键，拍下当前照片，后用户可选择手动收藏、保存照片、分享照片，不喜欢这张照片可不保存返回。  
![](https://github.com/NFUNM082/API_ML_AI/blob/master/images/%E6%8B%8D%E7%85%A7.png)
- **识别、推荐pose页面**——识别图像并返回关键点数值，在pose库里推荐最合适的给用户  
用户按下拍照键后，可单击【识别】，应用开始识别该照片并返回关键点数值，以线框表现。用户可自主开启/关闭线框。在本产品原型中可点击ON查看效果。应用获取用户照片的人体关键点数值，与库中的pose比对，匹配出相近的pose（例如剪刀手）优先推荐给用户选择。用户同样可以自主选择使用某一个pose。  
![开启线框](https://github.com/NFUNM082/API_ML_AI/blob/master/images/%E4%B8%8B%E4%B8%80%E6%AD%A5on.png)
![关闭线框](https://github.com/NFUNM082/API_ML_AI/blob/master/images/%E4%B8%8B%E4%B8%80%E6%AD%A5off.png)  
![推荐pose](https://github.com/NFUNM082/API_ML_AI/blob/master/images/%E5%B7%B2%E6%8E%A8%E8%8D%90.png)
- **pose库**——用户自主选择心仪的pose  
点击主页面的【姿势】，页面下方弹出收录的pose库。“常用”：用户历史使用过的pose，可快速找到之前用过的pose。“爱心”：用户手动收藏的pose。*以上两个分类皆为帮助用户节省挑选的时间* “自拍”、“日常”、“街拍”……：pose库中收录的pose，按使用场景分类，用户可根据当前场景选择分类。
![](https://github.com/NFUNM082/API_ML_AI/blob/master/images/pose%E5%BA%93.png)  
*原型制作所用人物照片素材来源网络，若侵权请联系删除。*
### 产品及功能架构
![产品及功能结构图](https://github.com/NFUNM082/API_ML_AI/blob/master/images/Pose%E5%B8%AE%E6%8B%8D%E4%BA%A7%E5%93%81%E5%8F%8A%E5%8A%9F%E8%83%BD%E7%BB%93%E6%9E%84%E5%9B%BE.png)
### 操作说明
- 用户进入产品主页面即显示相机实景，可进行拍照操作。与普通相机操作习惯类似，在拍照前可以调整相机有关设置、查看图库、前后镜头翻转。页面下方的【姿势】、【滤镜】内存储有pose和滤镜效果，用户点击查看和使用。
- 如果当用户想要以特定的姿势拍照时，按下拍照键后画面出现【识别】按钮，此时应用进行图像识别和返回人体关键点数值，以线框形式展现。用户可看到自身人体关键点数值，也可以关闭线框显示。此时应用会记录下数值，点击下一步应用弹出pose窗口，向用户推荐相似的pose以供选择，第一推荐即有绿色选中提示和画面中出现线框。用户也可点击其他pose示例图片挑选其他的pose，继续拍照。
- 主页面中的【姿势】库是给用户拍照前自行挑选参考pose的。用户可在其中看到历史使用过的pose和自己收藏的pose，以便更快速地找到自己想要的pose，不用在库里翻找上一次用过的那个pose示例。其他的则是按照应用场景分类。

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
**1.百度AI**与此应用有关的有[人体关键点识别](https://ai.baidu.com/tech/body/pose)和[手部关键点识别](https://ai.baidu.com/tech/body/hand)。    
- 人体关键点识别可检测图像中的所有人体，标记出每个人体的坐标位置；不限人体数量。精准定位人体的21个主要关键点
- 手部关键点识别的加值可以帮助对手部动作分析和比对。是百度AI新推出公测新功能，很有可能出BUG.
**2.Face++** 与此应用有关的是人体关键点识别。
包含14个骨骼关键点的对象类型；不限人体数量；可附加异常行为检测。  
Face++在人脸识别类API进行了算法升级，识别准确率较高。
**3.华为 HiAI** 有提供人体关键点识别API，但是局限有：仅能识别14个关键点的坐标信息、最多支持三个人、仅SDK等，故不使用该API做产品设计。
### 使用风险报告
-	所有用到的api可免费调用，使用到应用上要考虑“按量”或“按QPS”灵活升级付费服务。 
-   百度AI手部关键点识别技术目前仍公测中，每日可享500次免费调用。有待正式使用日期。
-	Face++未有手部关键点识别的api，有类似的手势识别功能。免费服务有以下这些限制：并发数有上限且不保证并发：由于资源有限，在调用繁忙的情况下，您的请求有可能会受到并发限制。每个用户使用免费服务只能创建 1000个 FaceSet，总计最多存储 100 万个人脸。
### 所用API
百度：人体关键点识别和手部关键点识别  
Face++：人体关键点。

