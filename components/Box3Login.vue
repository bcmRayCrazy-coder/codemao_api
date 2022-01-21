<template>
    <div>
        <h3>1.获取cookie</h3>
        <pre>
            <code v-highlight class="http">
POST /auth/login HTTP/2
Host: backend.box3.fun
Cookie: [目前的cookie]
Content-Length: 43
Sec-Ch-Ua: "Chromium";v="93", " Not;A Brand";v="99"
Accept: application/json, text/plain, */*
Content-Type: application/json
Authorization: 
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36
Sec-Ch-Ua-Platform: "macOS"
Origin: https://box3.fun
Sec-Fetch-Site: same-site
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://box3.fun/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9

{
    "account":"[用户名]",
    "password":"[密码]"
}
            </code>
        </pre>
        <h4>返回(如果登录成功)</h4>
        <pre>
            <code v-highlight class="http">
HTTP/2 200 OK
Date: Thu, 20 Jan 2022 04:37:13 GMT
Content-Type: application/json;charset=utf-8
Vary: Accept-Encoding
Access-Control-Allow-Origin: https://box3.fun
Access-Control-Allow-Methods: GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS, PATCH
Access-Control-Max-Age: 3600
Access-Control-Allow-Headers: Origin, No-Cache, x-requested-with, authorization, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers,Authorization, credential, X-XSRF-TOKEN, token, encrypt, accept, notCheck, check, Access-Control-Allow-Origin, Cache-Control, Device-ID
Access-Control-Allow-Credentials: true
Set-Cookie: box-auth2=[怎么能告诉你呢]; Path=/; Domain=.box3.fun; Max-Age=31536000; Expires=Fri, 20 Jan 2023 04:37:13 GMT; Secure; HttpOnly; SameSite=none
Strict-Transport-Security: max-age=15724800; includeSubDomains

{"code":200,"msg":"success","data":{"id":1165227,"cmid":1104861,"displayname":"ray_crazy","wearingSkins":{"head":"pilot","hips":"pinkGirl","leftFoot":"pilot","leftHand":"pilot","leftLowerArm":"purpleGirl","leftLowerLeg":"codeWriter","leftShoulder":"zombieGirl","leftUpperArm":"purpleGirl","leftUpperLeg":"codeWriter","neck":"zombieGirl","rightFoot":"pilot","rightHand":"pilot","rightLowerArm":"purpleGirl","rightLowerLeg":"codeWriter","rightShoulder":"zombieGirl","rightUpperArm":"purpleGirl","rightUpperLeg":"codeWriter","torso":"purpleGirl"},"permission":128,"createdAt":"2020-04-09T00:50:34.873","updatedAt":"2022-01-19T16:05:00.752","birthday":"[保密哦]","avatar":"https://static.codemao.cn/FvicqdFT0-k9-nBD7c8q_AMijHo_","avatarHash":"QmfSoNiJozzkjj8eJFwQPAwCFvsWWWGhR36pPe9RhADJ8K","status":1,"blocklist":[],"gender":0,"username":"bcmray","phone":"+86*******5408","email":"","language":"zh_CN","description":"来 119.29.64.129 看我","avatarStatus":2,"firstLogin":false,"reputation":100,"authInfo":10,"flags":3,"mutedTill":"1969-12-31T16:00:00","bannedTill":"1969-12-31T16:00:00","banEditor":false,"gold":0,"tag":0,"token":"[保密哦]","isSetPassword":true},"traceId":null}
            </code>
        </pre>
        <h4>返回(如果登录失败)</h4>
        <pre>
            <code v-highlight class="http">
HTTP/2 200 OK
Date: Fri, 21 Jan 2022 02:03:21 GMT
Content-Type: application/json;charset=utf-8
Vary: Accept-Encoding
Access-Control-Allow-Origin: https://box3.fun
Access-Control-Allow-Methods: GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS, PATCH
Access-Control-Max-Age: 3600
Access-Control-Allow-Headers: Origin, No-Cache, x-requested-with, authorization, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers,Authorization, credential, X-XSRF-TOKEN, token, encrypt, accept, notCheck, check, Access-Control-Allow-Origin, Cache-Control, Device-ID
Access-Control-Allow-Credentials: true
Set-Cookie: HttpOnly;Secure;SameSite=None
Strict-Transport-Security: max-age=15724800; includeSubDomains

{"code":10001000,"msg":"noSuchUser","data":null,"traceId":null}
            </code>
        </pre>
        <span>
            我们要记住cookie的值,以便于以后操作。<br>
            判断是否成功:"msg"=="success"?<br>
        </span>

        <br>

        <h3>2.解析响应</h3>
        <span>
            用户一切信息都在于"data"中<br><br>
            1.用户名<br>
            位于"displayname"中<br>
            2.用户头像<br>
            位于"avatar"中<br>
            3.用户id<br>
            位于"username"中<br>
            4.用户生日<br>
            位于"birthday"中<br>
            5.用户性别<br>
            位于"gender"中,0是男,1是女<br>
            6.用户邮箱<br>
            位于"email"中<br>
            7.用户黑名单<br>
            位于"blocklist"中<br>
            8.封禁<br>
            "bannedTill"中,若是1969-12-31表示没有被封禁过,若是之前的日期表示被封禁过，若是以后的日期表示正在封禁<br>
            "banEditor"表示是否有编辑器权限<br>
        </span>
        <br>
        <h3>3.再次获取用户信息</h3>
        <pre>
            <code v-highlight class="http">
POST /auth/online/1 HTTP/2
Host: backend.box3.fun
Cookie: [上一步得到的cookie]
Content-Length: 0
Sec-Ch-Ua: "Chromium";v="93", " Not;A Brand";v="99"
Accept: application/json, text/plain, */*
Authorization: 
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36
Sec-Ch-Ua-Platform: "macOS"
Origin: https://box3.fun
Sec-Fetch-Site: same-site
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://box3.fun/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
            </code>
        </pre>
        <span>响应(成功)同上(步骤1)</span>
        <h4>响应(未登录或登录失败)</h4>
        <pre>
            <code v-highlight class="http">
HTTP/2 200 OK
Date: Fri, 21 Jan 2022 02:06:35 GMT
Content-Type: application/json;charset=utf-8
Content-Length: 33
Access-Control-Allow-Origin: https://box3.fun
Access-Control-Allow-Methods: GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS, PATCH
Access-Control-Max-Age: 3600
Access-Control-Allow-Headers: Origin, No-Cache, x-requested-with, authorization, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers,Authorization, credential, X-XSRF-TOKEN, token, encrypt, accept, notCheck, check, Access-Control-Allow-Origin, Cache-Control, Device-ID
Access-Control-Allow-Credentials: true
Set-Cookie: HttpOnly;Secure;SameSite=None
Strict-Transport-Security: max-age=15724800; includeSubDomains

{"code":401,"msg":"UNAUTHORIZED"}
            </code>
        </pre>
        <br>
        <br>
        <h3>实战 Javascript + axios</h3>
        <pre>
            <code v-highlight class="javascript">
/**用axios进行登录
 * @author bcmray_crazy
 */
 // 用户id
 var userid = "";
 // 用户密码
 var pwd = "";
 // 发送请求
 axios
    .post("https://box3.fun/auth/login",{
        "account":userid,
        "password":pwd
    });
    .then(({data})=>{
        var info = JSON.parse(data);
        if(info.msg != 'success') return console.warn("用户名或密码错误");
        var userData = info.data;
        console.log(userData);
    });
    .catch(err=>{
        // 若请求发送失败或相应404会报错,需要抓住
        console.error(err);
    });
            </code>
        </pre>
    </div>
</template>
<style>
    pre{
        text-align: left;
    }
</style>