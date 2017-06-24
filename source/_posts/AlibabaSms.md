---
title: AlibabaSms
date: 2017-05-25
tags: Node.js
---

#### 开通阿里短信服务 
#### 新建短信签名 

签名 （产品名称） 

上传 企业营业执照、组织机构带代码证、税务登记证

备注：主要用途：验证手机号是否为本人操作; 

<!-- more -->

#### 新建短信模板

模板内容 您的验证码是${no}。如非本人操作，请忽略本短信。

#### 使用node.js发送请求
    var http = require('http');
    var querystring = require('querystring');
    
    var data={
        ParamString: '{"no":"123456"}',
        RecNum: '电话号码',
        SignName: '签名名称',
        TemplateCode: '模板代码'
    };

    var querys = querystring.stringify(data);

    var options = {
        hostname: 'sms.market.alicloudapi.com',
        port:80,
        path: '/singleSendSms?' + querys,
        method: 'GET',
        headers:{'Authorization':'APPCODE '+'自己的AppCode'}
    };

    //发送请求
    var req = http.request(options,function(res){
        console.log('STATUS:' + res.statusCode);//打印状态
        res.setEncoding('utf8');
        res.on('data',function(chunk){
            var returnData = JSON.parse(chunk);//返回结果
            console.log(returnData);
        });
        res.on('end',function(){//请求结束
            console.log('END'); 
        });  
    });

    req.on('error', function(e){//请求出现错误
         console.log('ERROR：' + e.message);
    });

    req.end();
