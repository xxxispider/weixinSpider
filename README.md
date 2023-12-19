# weixinSpider
> weixin spider, wechat spider, 微信爬虫，微信万能cookie，微信阅读数采集，搜狗微信转永久拦截，微信评论采集

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

## 微信文章官方文章API接口
微信官方提供的数据api接口，搜狗微信也可以使用哦。

![image](https://github.com/xxxispider/weixinSpider/assets/154309134/9ad41221-8736-4250-970c-cbb6c71d6e9a)


```json
{
  "base_resp": {
    "ret": 0,
    "errmsg": "ok",
    "wxtoken": 777,
    "cookie_count": 0,
    "base_resp": {
      "ret": 0,
      "errmsg": "ok",
      "cookie_count": 0,
      "sessionid": "svr_5c2c90b3814"
    },
    "sessionid": "svr_5c2c90b3814"
  },
  "user_name": "gh_ea6a4fc39557",
  "nick_name": "邯郸统战",
  "round_head_img": "http://mmbiz.qpic.cn/mmbiz_png/R9ialGhGkcuFtjkVMxqYKwVAnwBOqJZbS6Qafv7dZC7q4gmzSChFzxLBtndFUmOwiaScowic5ET3RpCChd3Lvyb2g/0?wx_fmt=png",
  "title": "宣传惠企政策 助力企业发展（四十）",
  "desc": "",
  "content_noencode": "<section>省略...",
  "create_time": "2023-02-01 17:27",
  "cdn_url": "https://mmbiz.qpic.cn/mmbiz_jpg/R9ialGhGkcuGBHlusmlibAYticnzqQqWTpnMupHbxJA9zNtQlubxaqcEbtXLj0dQIgQczYM8uYEMNPrVDWhDtrJnQ/0?wx_fmt=jpeg",
  "link": "http://mp.weixin.qq.com/s?__biz=Mzg4MTE5NDAwMA==&amp;mid=2247488189&amp;idx=2&amp;sn=4a81352839dfc03bcfa960b6643b48f7&amp;chksm=cf68f7c2f81f7ed49b6ff2e896d0dbd77b9b511a98efb5c2244f0a89711f7252a47b91f37dcf#rd",
  "source_url": "",
  "can_share": 0,
  "alias": "handantongzhan",
  "type": 9,
  "author": "",
  "is_limit_user": 0,
  "show_cover_pic": 0,
  "advertisement_info": [],
  "ori_create_time": 1675243633,
  "user_uin": 0,
  "total_item_num": 2,
  "is_async": 1,
  "comment_id": "0",
  "img_format": "jpeg",
  "svr_time": 1702972195,
  "copyright_info": {
    "copyright_stat": 0,
    "is_cartoon_copyright": 0
  },
  "can_reward": 0,
  "signature": "宣传统战政策，聚焦统战动态，传播统战知识，展示统战成效，交流统战经验",
  "in_mm": 0,
  "app_id": "wx22ea211d97e36b63",
  "show_comment": 0,
  "can_use_page": 0,
  "hd_head_img": "http://wx.qlogo.cn/mmhead/Q3auHgzwzM5zwW2pcxbygcogMSlwCoyYJ8kwlheJ0Zhk2CyFCr2icNA/0",
  "del_reason_id": 0,
  "srcid": "",
  "is_wxg_stuff_uin": 0,
  "need_report_cost": 0,
  "use_tx_video_player": 0,
  "is_only_read": 1,
  "req_id": "1915s8Y7A4qu5br6PX8Hrjwq",
  "use_outer_link": 0,
  "ban_scene": 0,
  "csp_nonce_str": 2105126991,
  "msg_daily_idx": 1,
  "ori_head_img_url": "http://wx.qlogo.cn/mmhead/Q3auHgzwzM5zwW2pcxbygcogMSlwCoyYJ8kwlheJ0Zhk2CyFCr2icNA/132",
  "filter_time": 1675243205,
  "appmsg_fe_filter": "contenteditable",
  "is_login": 0,
  "item_show_type": 0,
  "voice_in_appmsg": [],
  "moon_inline": 1,
  "malicious_title_reason_id": 0,
  "picture_page_info_list": [
    {
      "cdn_url": "https://mmbiz.qpic.cn/mmbiz_gif/Ljib4So7yuWiaibnZHYib0rg4wZibRnXvibHQYoDm0MeFhSib6kPc69ic0gB8Y2jRlaicROoaOKicXD0icekhCxF66pOG1k5w/640?wx_fmt=gif",
      "width": 0,
      "height": 0,
      "poi_info": [],
      "wxa_info": [],
      "bind_ad_info": [],
      "cps_ad_info": []
    },
    {
      "cdn_url": "https://mmbiz.qpic.cn/mmbiz_png/Ljib4So7yuWiaBMvicKntmyVBYVJjfOUa3wO9iaw6sxGibNTmSd9rcVXKJh8rxV1SM02vOgc97qn5usjqbq2OE0OYkA/640?wx_fmt=png",
      "width": 0,
      "height": 0,
      "poi_info": [],
      "wxa_info": [],
      "bind_ad_info": [],
      "cps_ad_info": []
    },
    {
      "cdn_url": "https://mmbiz.qpic.cn/mmbiz_gif/R9ialGhGkcuHs9RT8zhcXpiaM5JonAd7pXW6CaVaCsljX4a0s5UEud5bhLYqvAjEcicBNpwRibbYLiaJvKN3x6UxppA/640?wx_fmt=gif",
      "width": 0,
      "height": 0,
      "poi_info": [],
      "wxa_info": [],
      "bind_ad_info": [],
      "cps_ad_info": []
    },
    {
      "cdn_url": "https://mmbiz.qpic.cn/mmbiz_jpg/R9ialGhGkcuHs9RT8zhcXpiaM5JonAd7pXk0H0N2ibMyiaAe3YibiaJbykgrD81VYOWTj3KCa5ZojJoxLsFfFCibA81LA/640?wx_fmt=jpeg",
      "width": 0,
      "height": 0,
      "poi_info": [],
      "wxa_info": [],
      "bind_ad_info": [],
      "cps_ad_info": []
    },
    {
      "cdn_url": "https://mmbiz.qpic.cn/mmbiz_gif/R9ialGhGkcuHs9RT8zhcXpiaM5JonAd7pXEjYtfGxnScZ8yfT8voLsNSOeNqJ1ibNwBGsmFaYIOW8PCm5OIkHOekA/640?wx_fmt=gif",
      "width": 0,
      "height": 0,
      "poi_info": [],
      "wxa_info": [],
      "bind_ad_info": [],
      "cps_ad_info": []
    }
  ],
  "show_msg_voice": 0,
  "locationlist": [],
  "hotspotinfolist": [],
  "isnew": 0,
  "ad_abtest_padding": 0,
  "malicious_content_type": 0,
  "can_see_complaint": 0,
  "optimizing_flag": 0,
  "fasttmpl_version": 6993346,
  "is_top_stories": 0,
  "video_ids": [],
  "isprofileblock": 0,
  "cdn_url_235_1": "https://mmbiz.qpic.cn/mmbiz_jpg/R9ialGhGkcuGBHlusmlibAYticnzqQqWTpnT5Mb83cZC841BtuUxtx4373DgxBxMvtZgslJfGGicZzvBBc1aTmcO2A/0?wx_fmt=jpeg",
  "cdn_url_1_1": "https://mmbiz.qpic.cn/mmbiz_jpg/R9ialGhGkcuGBHlusmlibAYticnzqQqWTpnMupHbxJA9zNtQlubxaqcEbtXLj0dQIgQczYM8uYEMNPrVDWhDtrJnQ/0?wx_fmt=jpeg",
  "more_read_type": 0,
  "appmsg_like_type": 2,
  "ori_send_time": 1675243633,
  "show_top_bar": 0,
  "related_tag": [],
  "fasttmpl_infos": [],
  "user_info": {
    "is_paid": 0,
    "clientversion": "",
    "ckeys": [],
    "fasttmpl_infos": [
      {
        "type": 0,
        "version": 6993346,
        "lang": "zh_CN",
        "fullversion": "6993346-zh_CN-html",
        "versiongroup": "zh_CN-html"
      }
    ],
    "search_keyword": {
      "item_list": []
    },
    "use_h5webtransfer": 0
  },
  "ainfos": [],
  "related_article_info": {
    "has_related_article_info": 0
  },
  "has_red_packet_cover": 0,
  "is_pay_subscribe": 0,
  "pay_subscribe_info": {
    "preview_percent": 0,
    "desc": "",
    "fee": 0,
    "gifts_count": 0,
    "wecoin_amount": 0
  },
  "video_in_article": [],
  "is_area_shield": 0,
  "shield_areaids": [],
  "appmsg_ext_get": {
    "func_flag": 0
  },
  "anchor_tree": [],
  "voice_in_appmsg_list_json": "{\"voice_in_appmsg\":[]}",
  "live_info": [],
  "lang": "zh_CN",
  "cdn_url_16_9": "https://mmbiz.qpic.cn/mmbiz_jpg/R9ialGhGkcuGBHlusmlibAYticnzqQqWTpnMupHbxJA9zNtQlubxaqcEbtXLj0dQIgQczYM8uYEMNPrVDWhDtrJnQ/0?wx_fmt=jpeg",
  "real_item_show_type": 0,
  "url_item_show_type": 0,
  "video_page_infos": [],
  "can_use_wecoin": 1,
  "wecoin_tips": 0,
  "front_end_additional_fields": {
    "is_auto_type_setting": 0,
    "save_type": 0
  },
  "open_fansmsg": 1,
  "is_cooling_appmsg": 0,
  "ip_wording": {
    "country_name": "中国",
    "country_id": "156",
    "province_name": "河北"
  },
  "show_ip_wording": 1,
  "is_acct_area_shield": 0,
  "shield_acct_areaids": [],
  "style_type": 10000,
  "shield_areas_info": [],
  "create_timestamp": 1675243633,
  "picture_list_in_pictext": [],
  "servicetype": 0,
  "segment_comment_id": "0",
  "show_ad_mark": 0,
  "ad_mark_status": 0,
  "hide_ad_mark_on_cps": 0,
  "claim_source": {},
  "mp_comment_id": "0",
  "extra_comment_id": "0"
}
```


