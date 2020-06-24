    <script src="https://g.alicdn.com/dingding/dinglogin/0.0.5/ddLogin.js"></script>
<template>
    <div>
        <div id="ding-login"></div>
    </div>
</template>

<script>

export default {
    mounted(){
        let appId = 'dingoa3rtiiyglkdz1vtru' 
        let baseUrl = encodeURIComponent('http://localhost:8080/dtlogin') 
        let url = encodeURIComponent(
            `https://oapi.dingtalk.com/connect/oauth2/sns_authorize?appid=${appId}&response_type=code&scope=snsapi_login&state=STATE&redirect_uri=${baseUrl}`
            ) 

        var obj = DDLogin({
            id: "ding-login",
            goto: url,
            style: "border:none;background-color:#FFFFFF;",
            width: "365",
            height: "400"
        });
        
        var hanndleMessage = function (event) {
            let {origin} = event;
            if (origin == "https://login.dingtalk.com") { 
                let {data:loginTmpCode} = event; 
                window.location.href=`https://oapi.dingtalk.com/connect/oauth2/sns_authorize?appid=${appId}&response_type=code&scope=snsapi_login&state=STATE&redirect_uri=${baseUrl}&loginTmpCode=${loginTmpCode}` // 
            }
        };
        if (typeof window.addEventListener != 'undefined') {
            window.addEventListener('message', hanndleMessage, false);
        } else if (typeof window.attachEvent != 'undefined') {
            window.attachEvent('onmessage', hanndleMessage);
        }
    }
}
</script>
