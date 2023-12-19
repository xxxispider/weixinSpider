# weixinSpider
> weixin spider, wechat spider, crawl, 微信爬虫，微信万能key，微信阅读数采集，搜狗微信转永久拦截，微信评论采集，微信公众号采集

提供技术解决方案，解决微信相关的采集需求。帮助采集小伙伴解决技术壁垒。

# 实现的功能
- 文章评论内容采集
- 文章内容采集
- 搜狗微信转永久URL采集
- 公众号信息采集
- 公众号推送文章采集
- 公众号历史数据采集
- 视频号相关采集（开发中）
- ...
## 联系方式
- 电报群 https://t.me/+iqXGb01UXNxhMWNl
- potato账号

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/0b9b51ad-5bb4-4dfd-8acb-d57eefcbf365)


# 技术方案
## 万能key
在获取阅读数或者评论数据时需要uin和key。每次请求key是变换的，微信有一个万能key，可以一直持续获取，只要保持更新就行了。

代码参考
```python
def get_rsp(self, uin, key, __biz, mid, sn, idx, comment_id):
  headers = {
      "Host": "mp.weixin.qq.com",
      "origin": "https://mp.weixin.qq.com",
      "x-requested-with": "XMLHttpRequest",
      "user-agent": "自行替换，Mozilla/5.0...............",
      "content-type": "application/x-www-form-urlencoded; charset=UTF-8",
      "accept": "*/*",
      "sec-fetch-site": "same-origin",
      "sec-fetch-mode": "cors",
      "sec-fetch-dest": "empty",
      "accept-language": "zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7"
  }
  
  url = "https://mp.weixin.qq.com/mp/getappmsgext"
  params = {
      "f": "json",
      "mock": "",
      "uin": uin,
      "key": key,
      "wxtoken": "777",
      "devicetype": "Windows&nbsp;11&nbsp;x64",
      "clientversion": "63060012",
      "__biz": __biz,
      "x5": "0"
  }
  data = {
      # "r": "0.6980405644408527",
      "__biz": __biz,
      "appmsg_type": "9",
      "mid": mid,
      "sn": sn,
      "idx": idx,
      # "scene": "126",
      "abtest_cookie": "",
      "devicetype": "Windows 11 x64",
      "version": "63060012",
      "is_need_ticket": "0",
      "is_need_ad": "0",
      "comment_id": comment_id,
      "is_need_reward": "0",
      "both_ad": "0",
      "reward_uin_count": "0",
      "send_time": "",
      "msg_daily_idx": "8",
      "is_original": "0",
      "is_only_read": "1",
      "is_temp_url": "0",
      "item_show_type": "0",
      "tmp_version": "1",
      "more_read_type": "0",
      "appmsg_like_type": "2",
      "related_video_sn": "",
      "related_video_num": "5",
      "vid": "",
      "is_pay_subscribe": "0",
      "pay_subscribe_uin_count": "0",
      "has_red_packet_cover": "0",
  
      "album_video_num": "5",
      "cur_album_id": "undefined",
      "is_public_related_video": "NaN",
      "encode_info_by_base64": "undefined",
      "exptype": ""
  }
  # response = requests.post(url, headers=headers, cookies=None, params=params, data=data, verify=False)
  response = requests.post(url, headers=headers, cookies=None, params=params, data=data, )
  # print(response.text)
  return response

```

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/5231f4b2-cad2-4b9f-a0c2-250ec8365287)

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/f1feccbd-04a7-4050-aa95-c9127b8b8a57)
## 微信公众号推送采集
实时获取微信推送数据采集

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/6342d785-19e2-40c8-b6e0-263225a3b2c0)

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/b9c1b9b2-ef4d-4cd5-9f42-c2f2e927ef48)

## 微信历史数据采集
![image](https://github.com/xxxispider/weixinSpider/assets/154309134/9566a399-3545-4eab-b76e-274e0f01da39)

## 微信文章官方文章API接口
微信官方提供的数据api接口，搜狗微信也可以使用哦。

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/9ad41221-8736-4250-970c-cbb6c71d6e9a)

## 其他功能
需要其他功能，可以联系我

联系方式






