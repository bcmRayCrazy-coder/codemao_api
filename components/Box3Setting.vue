<template>
    <div>
        <h3>1.获取用户cookie</h3>
        <span>请先在<kbd>/box3/login</kbd>步骤中获取用户cookie</span>
        <h3>2.更改用户信息</h3>
        <h4>1)更改昵称</h4>
        <pre>
            <code v-highlight class="http">
PUT /user/update HTTP/2
Host: backend.box3.fun
Cookie: [用户cookie]
Content-Length: 27
Sec-Ch-Ua: "Chromium";v="93", " Not;A Brand";v="99"
Accept: application/json, text/plain, */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36
Sec-Ch-Ua-Mobile: ?0
Authorization: ddb2707a7dacd7992db2781c2c8debdced6d6ff53666c18d13e89f6b45383c82
Sec-Ch-Ua-Platform: "macOS"
Content-Type: application/json
Origin: https://box3.fun
Sec-Fetch-Site: same-site
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://box3.fun/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9

{"displayname":"ray_crazy"}
            </code>
        </pre>
        <h4>2)更改生日、性别</h4>
        <pre>
            <code v-highlight class="http">
POST /api/api/user-server-rpc HTTP/2
Host: box3.fun
Cookie: [用户cookie]
Content-Length: 59
Cache-Control: max-age=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: https://box3.fun
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: same-origin
Sec-Fetch-Dest: empty
Referer: https://box3.fun/sw.js
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9

{
    "type":"updateUserInfo",
    "data":{
        "type":[种类],
        "data":[数据]
        }
}
            </code>
        </pre>
        <span>
            <kbd>[种类]</kbd>有<br>
            <kbd>"gender"</kbd>(性别) <br>
            <kbd>"birthday"</kbd>(生日) <br>
            <kbd>[数据]</kbd>对应<br>
            <kbd>0</kbd>(男) <kbd>1</kbd>(女) <kbd>2</kbd>(保密) <br>
            <kbd>"1969-12-31T23:59:59.999Z"</kbd>(生日日期)格式:YYYY-MM-DDTHH:MM:SS.ms-Z(T不要替换) <br>
        </span>
        <h4>3)更改头像</h4>
        <span>获取剩余更改次数</span>
        <pre>
            <code v-highlight class="http">
POST /api/api/user-server-rpc HTTP/2
Host: box3.fun
Cookie: [用户cookie]
Content-Length: 41
Cache-Control: max-age=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: https://box3.fun
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: same-origin
Sec-Fetch-Dest: empty
Referer: https://box3.fun/sw.js
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9

{"type":"avatarUploadStatus","data":null}
            </code>
        </pre>
        <span>响应</span>
        <pre>
            <code v-highlight class="http">
HTTP/2 200 OK
Date: Fri, 21 Jan 2022 04:51:14 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 92
Access-Control-Allow-Origin: https://box3.fun
Access-Control-Allow-Methods: GET,PUT,POST,DELETE
Access-Control-Allow-Headers: Content-Type
Access-Control-Allow-Credentials: true
Set-Cookie: [用户cookie]
Cache-Control: no-store, no-cache, must-revalidate, proxy-revalidate
Expires: 0
Pragma: no-cache
Surrogate-Control: no-store
Strict-Transport-Security: max-age=15724800; includeSubDomains

{"type":"success","data":{"type":"avatarUploadStatus","data":{"canUpload":1,"lastHash":""}}}
            </code>
        </pre>
        <h4>1)解析响应</h4>
        <span>
            主要位于"data"下的"data"中
            <kbd>"canUpload"</kbd>指剩余可上传次数<br>
            <kbd>"lastHash"</kbd>指上次上传的头像hash
        </span>
        <v-card
            elevation="3"
            color="info"
            width="90%"
        >
            <v-card-title>
                <v-icon>mdi-information-outline</v-icon>
                提示
            </v-card-title>
            <v-card-text style="text-align:left">
                可以通过hash值,得出头像的url:https://static.codemao.cn/<code>hash</code>
            </v-card-text>
        </v-card>
        <h4>2)设置头像</h4>
        <v-card
            elevation="3"
            color="error"
            width="90%"
        >
            <v-card-title>
                <v-icon>mdi-alert-outline</v-icon>
                抱歉
            </v-card-title>
            <v-card-text style="text-align:left">
                目前该api暂未研究,欢迎您来这里做出贡献!联系ray的qq:975875040
            </v-card-text>
        </v-card>
    </div>
</template>