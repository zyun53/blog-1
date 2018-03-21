+++
title = "「アレクサ、おはどん」が上手く行かない"
date = 2018-03-21T00:00:00+09:00
tags = ["alexa", "mastodon"]
+++

こちらに習って、「Alexa、おはどん」をしようとしたのですが、上手く行きません。「おはどん」を
Alexaが上手く理解出ないのでしょうか。

[Google HomeでQiitadonに「おはどん」とトゥートする - Qiita](https://qiita.com/Morichan/items/c3868addbfd41a7a86a0 "Google HomeでQiitadonに「おはどん」とトゥートする - Qiita")

Node-REDの構成は以下の通り。

![Node RED](/media/2018-03-21_node-red.png)

1. alexa home

    Tootの名前でNode-RED Alexa Home Skill Bridgeに登録

1. switch

    switchでTurnOnRequestをmsg.commandで分岐。なくてもいいかも、一つだけなので。

1. function

    mastodonでアクセストークンを発行しておいてください。
    ```
    access_token = "enter your access token."
    
    msg.payload = { visibility: "public", status: "おはどん", access_token: access_token};
    msg.headers = {'content-type':'application/x-www-form-urlencoded'};
    return msg;
    ```

1. http request

    * メソッド: POST
    * URL: https://your_domain/api/v1/statuses
