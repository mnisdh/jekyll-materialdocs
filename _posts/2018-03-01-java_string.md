---
layout: post
title:  "Java String"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java String
comments: 1
---

{% highlight javascript linenos %}
var items = require("./items");
var conns = [];
var ids = [];

var Reset = "\x1b[0m"
var Bright = "\x1b[1m"
var Dim = "\x1b[2m"
var Underscore = "\x1b[4m"
var Blink = "\x1b[5m"
var Reverse = "\x1b[7m"
var Hidden = "\x1b[8m"

var FgBlack = "\x1b[30m"
var FgRed = "\x1b[31m"
var FgGreen = "\x1b[32m"
var FgYellow = "\x1b[33m"
var FgBlue = "\x1b[34m"
var FgMagenta = "\x1b[35m"
var FgCyan = "\x1b[36m"
var FgWhite = "\x1b[37m"

var BgBlack = "\x1b[40m"
var BgRed = "\x1b[41m"
var BgGreen = "\x1b[42m"
var BgYellow = "\x1b[43m"
var BgBlue = "\x1b[44m"
var BgMagenta = "\x1b[45m"
var BgCyan = "\x1b[46m"
var BgWhite = "\x1b[47m"

function addConn(ws){
    conns.push(ws);
    ids.push("");

    console.log(FgWhite, "-------connection------- // count : " + conns.length);
};
function updateId(ws, id){
    var idx = conns.indexOf(ws);
    ids[idx] = id;

    console.log(FgWhite, "-------login------- // " + ids[idx]);
};
function deleteConn(ws){
    var idx = conns.indexOf(ws);
    console.log(FgWhite, "-------close------- // " + ids[idx]);

    conns.splice(idx, 1);
    ids.splice(idx, 1);
};
function getId(ws){
    var idx = conns.indexOf(ws);
    return ids[idx];
}
function getAnotherIds(ws){
    var currentId = getId(ws);
    var result = [];
    for(i = 0; i < ids.length; i++){
        if(ids[i] != currentId) result.push(ids[i]);
    }

    return result;
}

function sendMessageFromId(id, data){
    var ws = conns[ids.indexOf(id)];
    if(ws){
        var json = JSON.parse(data);
        ws.send(JSON.stringify(json));

        console.log(FgCyan, "--------------response-------------");
        console.log(FgGreen, data);
        console.log(FgCyan, "-----------------------------------");

        return data;
    }

    return "not found websocket";
};
function sendMessageFromWebSocket(ws, data){
    console.log(FgCyan, "***************request*************");
    console.log(FgBlue, data);
    console.log(FgCyan, "***********************************");
    var json = JSON.parse(data);
    var result;

    var currentId = getId(ws);

    if(json.hasOwnProperty('LOGIN')){
        if(json.LOGIN.USERID === json.LOGIN.USERPW) {
            result = items.LoginResult;
            updateId(ws, json.LOGIN.USERID);
        }
        else result = items.LoginFailResult;
    }
    else if(json.hasOwnProperty('USERINFO')) result = items.UserInfo(ids);
    else if(json.hasOwnProperty('LOGOUT')) result = items.Logout;
    else if(json.hasOwnProperty('ALARMACK')) {
        result = items.AlarmAck;
        
        var anotherIds = getAnotherIds(ws);
        for(i = 0; i < anotherIds.length; i++){
            sendMessageFromId(anotherIds[i], items.AlarmAckRpt(json.ALARMACK.ALARMSYSID, json.ALARMACK.ALARMDEFINITIONID, currentId));
        }
    }
    else if(json.hasOwnProperty('ALARMACKRPT')) result = items.AlarmAckRpt;
    // else if(json.hasOwnProperty('ALARMRET')) result = items.AlarmRet;
    else if(json.hasOwnProperty('ALARMRETCHK')) result = items.AlarmRetChkRsp;
    else if(json.hasOwnProperty('ALARMRETRPT')) result = items.AlarmRetRpt;
    else if(json.hasOwnProperty('ALARMDEL')) result = items.AlarmDel;
    else if(json.hasOwnProperty('FAULTRPT')) result = items.FaultRpt;
    else if(json.hasOwnProperty('NOTI')) result = items.Noti;
    else if(json.hasOwnProperty('NOTIRPT')) result = items.NotiRpt;
    else if(json.hasOwnProperty('BREAKCHK')) result = items.BreakChk;
    // else if(json.hasOwnProperty('BREAK')) result = items.Break;
    else if(json.hasOwnProperty('BREAKBACKREQUEST')) result = items.BreakBackRequest;
    else if(json.hasOwnProperty('BREAKBACKRESPONSE')) result = items.BreakBackResponse;
    else if(json.hasOwnProperty('ALARMRESET')) result = items.AlarmReset;
    else if(json.hasOwnProperty('EMERGENCY')) result = items.Emergency;
    else if(json.hasOwnProperty('KEEPALIVEB')) result = json;
    else if(json.hasOwnProperty('CHECK')) result = items.Check;

    console.log(FgCyan, "--------------response-------------");
    console.log(FgGreen, result);
    console.log(FgCyan, "-----------------------------------");

    if(result) ws.send(JSON.stringify(result));

    return result;
};

const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 3000 });
wss.on("connection", function(ws) {
    addConn(ws);
    
    ws.on('message', function onMessage(data){ sendMessageFromWebSocket(ws, data);});
    ws.on("close", function onClose(code, reason) { deleteConn(ws); });
});

process.on('uncaughtException', function (err) {
    console.error(err.stack);
    console.log(FgWhite, "Node NOT Exiting...");
});


const port = 8081;
const http = require("http");
const url = require("url");
const qs = require("querystring");

var server = http.createServer(function(request, response){
    if(request.url != "/favicon.ico"){
        if (request.method == 'POST') {
            var body = '';
            var id = request.url.substring(1);

            if(id.indexOf("/test") < 0){
                request.on('data', function (data) {
                    body += data;
        
                    if (body.length > 1e6) request.connection.destroy();
                });
        
                request.on('end', function () {
                    //var post = qs.parse(body);
                    response.end(sendMessageFromId(id, body));
                });
            }
            else{
                var result = new Object();
                var alarmRpt = new Object();
                alarmRpt.JOBID = 11;
                var alarms = [];
                
                for(i = 0; i < 100; i++){
                    alarms.push(items.Alarm(i + ""));
                }

                result.ALARMRPT = alarmRpt;
                result.ALARM = alarms;

                response.end(sendMessageFromId(id.replace("/test", ""), JSON.stringify(result)));
            }
        }
    }
});

server.listen(port, function(){
    console.log(FgWhite, port + " server is running...");
});
{% endhighlight %}



**String 함수**  

length(문자열의 길이) :
{% highlight java linenos %}
String a = "String/Test";

// 길이
System.out.println(a.length());
{% endhighlight %}


indexOf(문자열의 위치) :
{% highlight java linenos %}
// 위치검색
System.out.println(a.indexOf("T"));
System.out.println(a.indexOf("Test"));
{% endhighlight %}


split(문자열을 구분자 단위로 분해) :
{% highlight java linenos %}
// 특정 구분자로 분해
String[] temp = a.split("/");
for(String item : temp) System.out.println(item);

// 빈문자열로 자르면 문자열을 글자 하나 단위로 분해
String[] temp2 = a.split("");
{% endhighlight %}


substring(지정한 인덱스대로 문자열을 분해) :
{% highlight java linenos %}
// 문자열 자르기
// substring에서 인덱스는 문자열 앞으로 생각하고 사용
System.out.println(a.substring(0, 6));
{% endhighlight %}


replace(특정문자열을 지정한 문자열로 바꿈) :
{% highlight java linenos %}
// 문자열 바꾸기
System.out.println(a.replace("Te", "Px"));
{% endhighlight %}


startsWith(특정 문자열로 시작되는지 확인) :
{% highlight java linenos %}
// 특정 문자열로 시작되는지를 검사
System.out.println(a.startsWith("Str"));
{% endhighlight %}