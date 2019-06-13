/**
 * @action [前端高级编程][插件]----html常用引导登陆弹窗
 * @author ctocode-dzy
 * @version 2019-01-25
 */

;
(function ($, window, document) {
    "use strict";// 使用严格模式
    var shxxLoginPopUpClass = function (elem, options) {
        this.$element = elem;
        this.settings = $.extend({
            "id": "",
            "ajaxLogin": "",
            "_3rdLanding": false,// 是否启用第三方登陆
            "sendCodeUrl": "",//短信接口
            "registerUrl": "",// 立即注册-url
            "forgotPwdUrl": "",//忘记密码接口
            "verifyApi": "",//验证码接口
            "loginUrl": "",//登陆接口
            "smsloginUrl": "",//登陆接口
            "jumpUrl": ""//返回页面
        }, options);
        if (ctoCheckEmpty(this.settings.id)) {
            this.settings.id = this.__randomString();
        }
        this.wrapObj = "";
        this.maskObj = "";
    }
    shxxLoginPopUpClass.prototype = {
        constructor: shxxLoginPopUpClass,
        //获取js路径
        __getJsPath: function (type, jsName) {
            type = type || "";
            jsName = jsName || "";
            var jsPath = "";
            if (type == 9) {
                var jsArr = document.scripts;
                for (var i = jsArr.length; i > 0; i--) {
                    if (jsArr[i - 1].src.indexOf(jsName) > -1) {
                        jsPath = jsArr[i - 1].src.substring(0, jsArr[i - 1].src.lastIndexOf("/") + 1);
                    }
                }
            } else {
                var scriptArr = document.getElementsByTagName("script");
                var scriptLast = scriptArr[scriptArr.length - 1];
                var scriptSrc = scriptLast.src;
                if (scriptSrc.indexOf(jsName) > -1) {
                    jsPath = scriptSrc.substring(0, scriptSrc.lastIndexOf("/") + 1);
                }
            }
            return jsPath;
        },
        //产生随机数
        __randomString: function (len) {
            var len = len || 6;
            var $chars = 'ABCDEFGHJKMNPQRSTWXYZabcdefhijkmnprstwxyz2345678';
            var maxPos = $chars.length;
            var pwd = "";
            for (var i = 0; i < len; i++) {
                pwd += $chars.charAt(Math.floor(Math.random() * maxPos));
            }
            return pwd;
        },
        //加载css
        __loadCss: function () {
            var stylestr = "";
            stylestr += '<style type="text/css" id="shxxLoginPopUpCss">';
            stylestr += '.shxx-login-main {position:fixed;top:20%;left:50%;width:440px;min-height:365px;border:1px solid #eaeaea;margin-left:-220px;border-radius:5px;background-color:#fff;z-index:1001;border:1px solid #eaeaea;}';
            stylestr += '.shxx-login-main label.error {color:#000;line-height:45px;background:#fff5d9 no-repeat 0 0;text-align:left;white-space:nowrap;height:45px;padding:0 10px;position:absolute;z-index:2;top: 0px;left:300px;}';
            stylestr += '.shxx-login-main .hd {padding:10px 2px;font-size:18px;line-height:24px;border-bottom:1px solid #E70E1D;text-align:center;color:#E70E1D;}';
            stylestr += '.shxx-login-main .hd>a {float:right;width:28px;cursor:pointer;color: #1f1f1f;}';
            stylestr += '.shxx-login-main .bd-container {margin-top:30px;padding: 0 28px;position:relative;}';
            stylestr += '.shxx-login-main dl {background-color:#fff;width:350px;height:45px;margin-left:15px;margin-top:-1px;border:solid 1px #e6e6e6;position:relative;z-index:1;}';
            stylestr += '.shxx-login-main dl dt {font-size:14px;line-height:24px;color:#666;width:75px;padding:10px 0 10px 15px;float:left;}';
            stylestr += '.shxx-login-main dl dd input {font-family:"microsoft yahei";font-size:14px;line-height:25px;width:240px;height:43px;padding:0px;border:none 0;float:left;}';
            stylestr += '.shxx-login-main dl dd.captcha {width:120px;height:45px;float:right;padding:0px;}';
            stylestr += '.shxx-login-main dl dd.captcha span {width:122px;height:45px;float:left;margin:-1px 0 0 -1px;border:solid 1px #e6e6e6;position:relative;z-index:1;text-align:center;}';
            stylestr += '.shxx-login-main dl dd.captcha span a {display:none;font-size:14px;text-decoration:none;line-height:45px;color:#fff;background:rgba(0,0,0,0.5);text-align:center;width:120px;height:45px;position:absolute;z-index:1;top:0;left:0;}';
            stylestr += '.shxx-login-main dl dd.captcha span:hover a {display:block;}';
            stylestr += '.shxx-login-main .bd-handle {line-height:20px;margin-top:15px;overflow:hidden;}';
            stylestr += '.shxx-login-main .bd-handle label {color:#E70E1D;float:left;margin-left:15px;font-size:14px;}';
            stylestr += '.shxx-login-main .db-handle label input[type="checkbox"]{vertical-align:middle;display:inline-block;margin-right:4px;}';
            stylestr += '.shxx-login-main .bd-handle .forget {float:right;margin-right:15px;color:#333333;font-size:14px;}';
            stylestr += '.shxx-login-main .bd-submit {margin:15px;width:350px;height:45px;border:solid 1px #E70E1D;border-radius:5px;cursor:pointer;display:block;text-align:center;line-height:45px;font-family:"microsoft yahei";font-size:16px;font-weight:600;color:#fff;background-color:#E70E1D;} ';
            stylestr += '.shxx-login-main .ft .shejiao {float:left;margin-top:25px;margin-left:35px;font-size:14px;color:#999999}';
            stylestr += '.shxx-login-main .ft .register {margin-top:25px;margin-right:55px;float:right;font-size:14px;color:#E70E1D;}';
            stylestr += '.shxx-login-main .ft .shejiao-icon {padding-left:135px;padding-top:75px;}';
            stylestr += '.shxx-login-main .ft ul {display:block;overflow:hidden;margin:0 auto;}';
            stylestr += '.shxx-login-main .ft li {display:inline;float:left;}';
            stylestr += '.shxx-login-main .ft li i {display:block;width:60px;height:35px;margin:0 auto;}';
            stylestr += '.shxx-login-main .ft li i>img {text-align:center;}';
            stylestr += '.shxx-login-main .ft .remind {float:left;margin-left:45px;margin-top:25px;margin-bottom:25px;font-size:12px;color:#999999;}';
            stylestr += '.shxx-login-mask-show {position: fixed;z-index: 1000;top: 0px;left: 0px;width: 100%;height: 100%;background: rgba(0,0,0,0.5);transition: all 0.3s;}';

            //短信验证码登陆css
            stylestr += '.shxx-sms-login-main {position:fixed;top:20%;left:50%;width:440px;min-height:365px;border:1px solid #eaeaea;margin-left:-220px;border-radius:5px;background-color:#fff;z-index:1001;border:1px solid #eaeaea;}';
            stylestr += '.shxx-sms-login-main label.error {color:#000;line-height:45px;background:#fff5d9 no-repeat 0 0;text-align:left;white-space:nowrap;height:45px;padding:0 10px;position:absolute;z-index:2;top: 0px;left:300px;}';
            stylestr += '.shxx-sms-login-main .hd {padding:10px 2px;font-size:18px;line-height:24px;border-bottom:1px solid #E70E1D;text-align:center;color:#E70E1D;}';
            stylestr += '.shxx-sms-login-main .hd>a {float:right;width:28px;cursor:pointer;color: #1f1f1f;}';
            stylestr += '.shxx-sms-login-main .bd-container {margin-top:30px;padding: 0 28px;position:relative;}';
            stylestr += '.shxx-sms-login-main dl {background-color:#fff;width:350px;height:45px;margin-left:15px;margin-top:-1px;border:solid 1px #e6e6e6;position:relative;z-index:1;}';
            stylestr += '.shxx-sms-login-main dl dt {font-size:14px;line-height:24px;color:#666;width:75px;padding:10px 0 10px 15px;float:left;}';
            stylestr += '.shxx-sms-login-main dl dd input {font-family:"microsoft yahei";font-size:14px;line-height:25px;width:240px;height:43px;padding:0px;border:none 0;float:left;}';
            stylestr += '.shxx-sms-login-main dl dd.captcha {width:120px;height:45px;float:right;padding:0px;}';
            stylestr += '.shxx-sms-login-main dl dd.captcha span {width:122px;height:45px;float:left;margin:-1px 0 0 -1px;border:solid 1px #e6e6e6;position:relative;z-index:1;text-align:center;}';
            stylestr += '.shxx-sms-login-main dl dd.captcha span a {display:block;font-size:14px;text-decoration:none;line-height:45px;color:#fff;background:rgba(0,0,0,0.5);text-align:center;width:120px;height:45px;position:absolute;z-index:1;top:0;left:0;}';
            stylestr += '.shxx-sms-login-main dl dd.captcha span a.yanzhengma {display:none;}';
            stylestr += '.shxx-sms-login-main dl dd.captcha span:hover a {display:block;}';
            stylestr += '.shxx-sms-login-main .bd-handle {line-height:20px;margin-top:15px;overflow:hidden;}';
            stylestr += '.shxx-sms-login-main .bd-handle label {color:#E70E1D;float:left;margin-left:15px;font-size:14px;}';
            stylestr += '.shxx-sms-login-main .db-handle label input[type="checkbox"]{vertical-align:middle;display:inline-block;margin-right:4px;}';
            stylestr += '.shxx-sms-login-main .bd-handle .loginpwd {float:right;margin-right:15px;color:#333333;font-size:14px;}';
            stylestr += '.shxx-sms-login-main .bd-submit {margin:15px;width:350px;height:45px;border:solid 1px #E70E1D;border-radius:5px;cursor:pointer;display:block;text-align:center;line-height:45px;font-family:"microsoft yahei";font-size:16px;font-weight:600;color:#fff;background-color:#E70E1D;} ';
            stylestr += '.shxx-sms-login-main .ft .shejiao {float:left;margin-top:25px;margin-left:35px;font-size:14px;color:#999999}';
            stylestr += '.shxx-sms-login-main .ft .register {margin-top:25px;margin-right:55px;float:right;font-size:14px;color:#E70E1D;}';
            stylestr += '.shxx-sms-login-main .ft .shejiao-icon {padding-left:135px;padding-top:75px;}';
            stylestr += '.shxx-sms-login-main .ft ul {display:block;overflow:hidden;margin:0 auto;}';
            stylestr += '.shxx-sms-login-main .ft li {display:inline;float:left;}';
            stylestr += '.shxx-sms-login-main .ft li i {display:block;width:60px;height:35px;margin:0 auto;}';
            stylestr += '.shxx-sms-login-main .ft li i>img {text-align:center;}';
            stylestr += '.shxx-sms-login-main .ft .remind {float:left;margin-left:45px;margin-top:25px;margin-bottom:25px;font-size:12px;color:#999999;}';

            //注册css
            stylestr += '.shxx-register-main {position:fixed;top:20%;left:50%;width:440px;min-height:460px;border:1px solid #eaeaea;margin-left:-220px;border-radius:5px;background-color:#fff;z-index:1001;border:1px solid #eaeaea;}';
            stylestr += '.shxx-register-main label.error {color:#000;line-height:45px;background:#fff5d9 no-repeat 0 0;text-align:left;white-space:nowrap;height:45px;padding:0 10px;position:absolute;z-index:2;top: 0px;left:300px;}';
            stylestr += '.shxx-register-main .hd {padding:10px 2px;font-size:18px;line-height:24px;border-bottom:1px solid #E70E1D;text-align:center;color:#E70E1D;}';
            stylestr += '.shxx-register-main .hd>a {float:right;width:28px;cursor:pointer;color: #1f1f1f;}';
            stylestr += '.shxx-register-main .bd-container {margin-top:30px;padding: 0 28px;position:relative;}';
            stylestr += '.shxx-register-main dl {background-color:#fff;width:350px;height:45px;margin-left:15px;margin-top:-1px;border:solid 1px #e6e6e6;position:relative;z-index:1;}';
            stylestr += '.shxx-register-main dl dt {font-size:14px;line-height:24px;color:#666;width:75px;padding:10px 0 10px 15px;float:left;}';
            stylestr += '.shxx-register-main dl dd input {font-family:"microsoft yahei";font-size:14px;line-height:25px;width:240px;height:43px;padding:0px;border:none 0;float:left;}';
            stylestr += '.shxx-register-main dl dd.captcha {width:120px;height:45px;float:right;padding:0px;}';
            stylestr += '.shxx-register-main dl dd.captcha span {width:122px;height:45px;float:left;margin:-1px 0 0 -1px;border:solid 1px #e6e6e6;position:relative;z-index:1;text-align:center;}';
            stylestr += '.shxx-register-main dl dd.captcha span a {display:block;font-size:14px;text-decoration:none;line-height:45px;color:#fff;background:rgba(0,0,0,0.5);text-align:center;width:120px;height:45px;position:absolute;z-index:1;top:0;left:0;}';
            stylestr += '.shxx-register-main dl dd.captcha span a.yanzhengma {display:none;}';
            stylestr += '.shxx-register-main dl dd.captcha span:hover a {display:block;}';
            stylestr += '.shxx-register-main .bd-handle {line-height:20px;margin-top:15px;overflow:hidden;}';
            stylestr += '.shxx-register-main .bd-handle label {color:#999;float:left;margin-left:15px;}';
            stylestr += '.shxx-register-main .db-handle label input[type="checkbox"]{vertical-align:middle;display:inline-block;margin-right:4px;}';
            stylestr += '.shxx-register-main .bd-handle .forget {float:right;margin-right:26px;color:#333333;font-size:14px;}';
            stylestr += '.shxx-register-main .bd-submit {margin:25px 15px;width:350px;height:45px;border:solid 1px #E70E1D;border-radius:5px;cursor:pointer;display:block;text-align:center;line-height:45px;font-family:"microsoft yahei";font-size:16px;font-weight:600;color:#fff;background-color:#E70E1D;} ';
            stylestr += '.shxx-register-main .ft .shejiao {float:left;margin-top:25px;margin-left:35px;font-size:14px;color:#999999}';
            stylestr += '.shxx-register-main .ft .register {margin-top:25px;margin-right:55px;float:right;font-size:14px;color:#E70E1D;}';
            stylestr += '.shxx-register-main .ft .shejiao-icon {padding-left:135px;padding-top:75px;}';
            stylestr += '.shxx-register-main .ft ul {display:block;overflow:hidden;margin:0 auto;}';
            stylestr += '.shxx-register-main .ft li {display:inline;float:left;}';
            stylestr += '.shxx-register-main .ft li i {display:block;width:60px;height:35px;margin:0 auto;}';
            stylestr += '.shxx-register-main .ft li i>img {text-align:center;}';
            stylestr += '.shxx-register-main .ft .remind {float:left;margin-left:45px;margin-top:25px;margin-bottom:25px;font-size:12px;color:#999999;}';
            stylestr += '.shxx-register-mask-show {position: absolute;z-index: 1000;top: 0px;left: 0px;width: 100%;height: 100%;background: rgba(0,0,0,0.5);transition: all 0.3s;}';
            //忘记密码css
            stylestr += '.shxx-forget-main {position:fixed;top:20%;left:50%;width:440px;min-height:420px;border:1px solid #eaeaea;margin-left:-220px;border-radius:5px;background-color:#fff;z-index:1001;border:1px solid #eaeaea;}';
            stylestr += '.shxx-forget-main label.error {color:#000;line-height:45px;background:#fff5d9 no-repeat 0 0;text-align:left;white-space:nowrap;height:45px;padding:0 10px;position:absolute;z-index:2;top: 0px;left:300px;}';
            stylestr += '.shxx-forget-main .hd {padding:10px 2px;font-size:18px;line-height:24px;border-bottom:1px solid #E70E1D;text-align:center;color:#E70E1D;}';
            stylestr += '.shxx-forget-main .hd>a {float:right;width:28px;cursor:pointer;color: #1f1f1f;}';
            stylestr += '.shxx-forget-main .bd-container {margin-top:30px;padding: 0 28px;position:relative;}';
            stylestr += '.shxx-forget-main dl {background-color:#fff;width:350px;height:45px;margin-left:15px;margin-top:-1px;border:solid 1px #e6e6e6;position:relative;z-index:1;}';
            stylestr += '.shxx-forget-main dl dt {font-size:14px;line-height:24px;color:#666;width:75px;padding:10px 0 10px 15px;float:left;}';
            stylestr += '.shxx-forget-main dl dd input {font-family:"microsoft yahei";font-size:14px;line-height:25px;width:240px;height:43px;padding:0px;border:none 0;float:left;}';
            stylestr += '.shxx-forget-main dl dd.captcha {width:120px;height:45px;float:right;padding:0px;}';
            stylestr += '.shxx-forget-main dl dd.captcha span {width:122px;height:45px;float:left;margin:-1px 0 0 -1px;border:solid 1px #e6e6e6;position:relative;z-index:1;text-align:center;}';
            stylestr += '.shxx-forget-main dl dd.captcha span a {display:block;font-size:14px;text-decoration:none;line-height:45px;color:#fff;background:rgba(0,0,0,0.5);text-align:center;width:120px;height:45px;position:absolute;z-index:1;top:0;left:0;}';
            stylestr += '.shxx-forget-main dl dd.captcha span a.yanzhengma {display:none;}';
            stylestr += '.shxx-forget-main dl dd.captcha span:hover a {display:block;}';
            stylestr += '.shxx-forget-main .bd-handle {line-height:20px;margin-top:15px;overflow:hidden;}';
            stylestr += '.shxx-forget-main .bd-handle label {color:#999;float:left;margin-left:15px;}';
            stylestr += '.shxx-forget-main .db-handle label input[type="checkbox"]{vertical-align:middle;display:inline-block;margin-right:4px;}';
            stylestr += '.shxx-forget-main .bd-handle .forget {float:right;margin-right:26px;color:#333333;font-size:14px;}';
            stylestr += '.shxx-forget-main .bd-submit {margin:25px 15px;width:350px;height:45px;border:solid 1px #E70E1D;border-radius:5px;cursor:pointer;display:block;text-align:center;line-height:45px;font-family:"microsoft yahei";font-size:16px;font-weight:600;color:#fff;background-color:#E70E1D;} ';
            stylestr += '.shxx-forget-main .ft .shejiao {float:left;margin-top:25px;margin-left:35px;font-size:14px;color:#999999}';
            stylestr += '.shxx-forget-main .ft .register {margin-top:25px;margin-right:55px;float:right;font-size:14px;color:#E70E1D;}';
            stylestr += '.shxx-forget-main .ft .shejiao-icon {padding-left:135px;padding-top:75px;}';
            stylestr += '.shxx-forget-main .ft ul {display:block;overflow:hidden;margin:0 auto;}';
            stylestr += '.shxx-forget-main .ft li {display:inline;float:left;}';
            stylestr += '.shxx-forget-main .ft li i {display:block;width:60px;height:35px;margin:0 auto;}';
            stylestr += '.shxx-forget-main .ft li i>img {text-align:center;}';
            stylestr += '.shxx-forget-main .ft .remind {float:left;margin-left:45px;margin-top:25px;margin-bottom:25px;font-size:12px;color:#999999;}';
            stylestr += '.shxx-forget-mask-show {position: absolute;z-index: 1000;top: 0px;left: 0px;width: 100%;height: 100%;background: rgba(0,0,0,0.5);transition: all 0.3s;}';

            stylestr += '</style>';
            var cssObj = $("#shxxLoginPopUpCss");
            if (cssObj.length < 1) {
                $("head").append(stylestr);
            }
        },
        //加载HTML代码
        __loadHtml: function () {
            var jsPath = this.__getJsPath(9, "sa.dialog.login.js");
            var htmlstr = "";
            htmlstr += '<div class="shxx-login-mask-show" id="ShxxLoginMask' + this.settings.id + '"></div>';
            //短信验证码登陆
            htmlstr += '<div class="shxx-sms-login-main" id="ShxxSMSLoginMain' + this.settings.id + '">';
            htmlstr += '<div class="hd cto-clear">';
            htmlstr += '短信登录';
            htmlstr += '<a class="close" href="javascript:void(0)">x</a>';
            htmlstr += '</div>';
            htmlstr += '<div class="bd cto-clear">';
            htmlstr += '<div class="bd-container" id="tabs_container1" style="height: 240px;">';
            htmlstr += '<form id="formSMSLoginDefault" method="post" data-sign="default">';
            htmlstr += '<dl>';
            htmlstr += '<dt>账&nbsp;&nbsp;&nbsp;号：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="tel" name="ucenter_mobile" placeholder="手机号" autocomplete="off" maxlength="11" onkeyup="value=value.replace(/[^\\d]/g,\'\')">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>短息码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_sms" placeholder="输入短信验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha">';
            htmlstr += '<a class="send-sms" href="javascript:void(0)">获取短信验证码</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>验证码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_captcha" placeholder="输入验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha spanyanzhengma">';
            htmlstr += '<img src="" style="width: 120px;height: 43px;">';
            htmlstr += '<a class="yanzhengma" href="javascript:void(0)">看不清，换一张</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<div class="bd-handle">';
            htmlstr += '<label>';
            htmlstr += '<p class="register"><a class="registerhrhg" href="javascript:void(0);">立即注册</a></p>';
            htmlstr += '</label>';
            htmlstr += '<a class="loginpwd" href="javascript:void(0);">账号密码登录</a>';
            htmlstr += '</div>';
            htmlstr += '<button class="bd-submit bd-submit-dl" type="button">登&nbsp;&nbsp;&nbsp;录</button>';
            htmlstr += '<p class="login-msg" style="padding: 0px 15px;color: #FF3238;margin-top:-10px;"></p>';
            htmlstr += '</form>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            //账号密码登陆
            htmlstr += '<div class="shxx-login-main" id="ShxxLoginMain' + this.settings.id + '" style="display: none;">';
            htmlstr += '<div class="hd cto-clear">';
            htmlstr += '账号登录';
            htmlstr += '<a class="close" href="javascript:void(0)">x</a>';
            htmlstr += '</div>';
            htmlstr += '<div class="bd cto-clear">';
            htmlstr += '<div class="bd-container" id="tabs_container" style="height: 240px;">';
            htmlstr += '<form id="formLoginDefault" method="post" data-sign="default">';
            htmlstr += '<dl>';
            htmlstr += '<dt>账&nbsp;&nbsp;&nbsp;号：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="tel" name="ucenter_mobile" placeholder="手机号" autocomplete="off" maxlength="11" onkeyup="value=value.replace(/[^\\d]/g,\'\')">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl>';
            htmlstr += '<dt>密&nbsp;&nbsp;&nbsp;码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="password" name="ucenter_password" placeholder="6-20个大小写英文字母、符号或数字" autocomplete="off" maxlength="32">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>验证码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_captcha" placeholder="输入验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha">';
            htmlstr += '<img src="" style="width: 120px;height: 43px;">';
            htmlstr += '<a href="javascript:void(0)">看不清，换一张</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<div class="bd-handle">';
            htmlstr += '<label>';
            htmlstr += '<p class="hrhgloginsms"><a class="loginsms" href="javascript:void(0);">短信验证码登陆</a></p>';
            htmlstr += '</label>';
            htmlstr += '<a class="forget" href="javascript:void(0);">忘记密码？</a>';
            htmlstr += '</div>';
            htmlstr += '<button class="bd-submit bd-submit-dl" type="button">登&nbsp;&nbsp;&nbsp;录</button>';
            htmlstr += '<p class="login-msg" style="padding: 0px 15px;color: #FF3238;"></p>';
            htmlstr += '</form>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            //注册
            htmlstr += '<div class="shxx-register-main" id="ShxxRegisterMain' + this.settings.id + '" style="display: none;">';
            htmlstr += '<div class="hd cto-clear">';
            htmlstr += '手机账号注册';
            htmlstr += '<a class="closeRegister" href="javascript:void(0)">x</a>';
            htmlstr += '</div>';
            htmlstr += '<div class="bd cto-clear">';
            htmlstr += '<div class="bd-container" id="tabs_container" style="height: 240px;">';
            htmlstr += '<form id="formRegisterDefault" method="post" data-sign="default">';
            htmlstr += '<dl>';
            htmlstr += '<dt>手机号：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="tel" name="ucenter_mobile" placeholder="手机号" autocomplete="off" maxlength="11" onkeyup="value=value.replace(/[^\\d]/g,\'\')">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>短息码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_sms" placeholder="输入短信验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha">';
            htmlstr += '<a class="send-sms" href="javascript:void(0)">获取短信验证码</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>密&nbsp;&nbsp;&nbsp;码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="password" name="ucenter_password" placeholder="6-20个大小写英文字母、符号或数字" autocomplete="off" maxlength="32">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl>';
            htmlstr += '<dt>确认密码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="password" name="ucenter_password_qr" placeholder="6-20个大小写英文字母、符号或数字" autocomplete="off" maxlength="32">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>验证码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_captcha" placeholder="输入验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha spanyanzhengma">';
            htmlstr += '<img src="" style="width: 120px;height: 43px;">';
            htmlstr += '<a class="yanzhengma" href="javascript:void(0)">看不清，换一张</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<button class="bd-submit bd-submit-zc" type="button">注&nbsp;&nbsp;&nbsp;册</button>';
            htmlstr += '<p class="register-msg" style="padding: 0px 20px;color: #FF3238;margin-top:-15px;"></p>';
            htmlstr += '</form>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            //忘记密码
            htmlstr += '<div class="shxx-forget-main" id="ShxxForgetMain' + this.settings.id + '" style="display: none;">';
            htmlstr += '<div class="hd cto-clear">';
            htmlstr += '修改密码';
            htmlstr += '<a class="closeForget" href="javascript:void(0)">x</a>';
            htmlstr += '</div>';
            htmlstr += '<div class="bd cto-clear">';
            htmlstr += '<div class="bd-container" id="tabs_container" style="height: 240px;">';
            htmlstr += '<form id="formForgetDefault" method="post" data-sign="default">';
            htmlstr += '<dl>';
            htmlstr += '<dt>手机号：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="tel" name="ucenter_mobile" placeholder="手机号" autocomplete="off" maxlength="11" onkeyup="value=value.replace(/[^\\d]/g,\'\')">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>短息码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_sms" placeholder="输入短信验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha">';
            htmlstr += '<a class="send-sms" href="javascript:void(0)">获取短信验证码</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>密&nbsp;&nbsp;&nbsp;码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="password" name="ucenter_password" placeholder="6-20个大小写英文字母、符号或数字" autocomplete="off" maxlength="32">';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<dl style="margin-top: 15px;">';
            htmlstr += '<dt>验证码：</dt>';
            htmlstr += '<dd>';
            htmlstr += '<input class="input-clean" type="text" name="cto_captcha" placeholder="输入验证码" maxlength="4" autocomplete="off" style="width: 100px;">';
            htmlstr += '</dd>';
            htmlstr += '<dd class="captcha">';
            htmlstr += '<span class="ctoCaptcha spanyanzhengma">';
            htmlstr += '<img src="" style="width: 120px;height: 43px;">';
            htmlstr += '<a class="yanzhengma" href="javascript:void(0)">看不清，换一张</a>';
            htmlstr += '</span>';
            htmlstr += '</dd>';
            htmlstr += '</dl>';
            htmlstr += '<button class="bd-submit bd-submit-mm" type="button">确&nbsp;&nbsp;&nbsp;认</button>';
            htmlstr += '<p class="forget-msg" style="padding: 0px 20px;color: #FF3238;margin-top:-15px;"></p>';
            htmlstr += '</form>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            htmlstr += '</div>';
            $("body").append(htmlstr);
        },
        __loadScript: function () {
            var _self = this;
            _self.wrapObj.find("a.close").off("click").on("click", function () {//短信验证码登陆->关闭短信验证码登陆弹窗
                _self.close();
            });
            _self.wrapObj.find("a.registerhrhg").off("click").on("click", function () {//短信验证码登陆->立即注册
                _self.registerHrhg();
            });
            _self.wrapObj.find("a.loginpwd").off("click").on("click", function () {//短信验证码登陆->账号密码登陆
                _self.hrhgLoginPwd();
            });
            _self.wrapObj.find('a.send-sms').off('click').on('click', function () {//短信验证码登陆-发送验证码
                _self._sendSMSCode("formSMSLoginDefault");
            });
            _self.wrapObj.find('span.spanyanzhengma').off('click').on('click', function () {//短信验证码登陆-刷新验证码
                _self.refreshCaptcha();
            });
            _self.wrapObj.find('.bd-submit-dl').off('click').on('click', function () {//短信验证码登陆-登陆提交
                _self.smsLoginUp();
            });
            $(".shxx-login-main").find("a.forget").off("click").on("click", function () {//账号密码登陆->忘记密码
                _self.forgetKeyHrhg();
            });
            $(".shxx-login-main").find("a.loginsms").off("click").on("click", function () {//账号密码登陆-短信验证码登陆
                _self.hrhgPopupPwdToSms();
            });
            $(".shxx-login-main").find('span.ctoCaptcha').off('click').on('click', function () {//账号密码登陆-刷新验证码
                _self.refreshCaptcha();
            });
            $(".shxx-login-main").find('.bd-submit-dl').off('click').on('click', function () {//账号密码登陆-登陆提交
                _self.loginUp();
            });
            $(".shxx-login-main").find('a.close').off('click').on('click', function () {//账号密码登陆-关闭弹窗
                _self.close();
            });
            $(".shxx-register-main").find("a.closeRegister").off("click").on("click", function () {//立即注册-关闭注册
                _self.closeregisterHrhg();
            });
            $(".shxx-register-main").find("a.send-sms").off("click").on("click", function () {//账号注册-发送验证码
                _self._sendSMSCode("formRegisterDefault");
            });
            $(".shxx-register-main").find('span.spanyanzhengma').off('click').on('click', function () {//账号注册-刷新验证码
                _self.refreshCaptcha();
            });
            $(".shxx-register-main").find(".bd-submit-zc").off("click").on("click", function () {//账号注册-确认提交
                _self.userRegister();
            });
            $(".shxx-forget-main").find("a.send-sms").off("click").on("click", function () {//忘记密码-发送验证码
                _self._sendSMSCode("formForgetDefault");
            });
            $(".shxx-forget-main").find(".bd-submit-mm").off("click").on("click", function () {//忘记密码-确认提交
                _self.userForget();
            });
            $(".shxx-forget-main").find("a.closeForget").off("click").on("click", function () {//忘记密码-关闭
                _self.closeForgetKeyHrhg();
            });
            $(".shxx-forget-main").find('span.spanyanzhengma').off('click').on('click', function () {//忘记密码-刷新验证码
                _self.refreshCaptcha();
            });
        },
        index: function () {
            this.__loadCss();
            $("body").css("overflow", "hidden");
            $("html").css("overflow", "hidden");
            this.wrapObj = $("#ShxxSMSLoginMain" + this.settings.id)
            if (this.wrapObj.length < 1) {
                this.__loadHtml();
                this.wrapObj = $("#ShxxSMSLoginMain" + this.settings.id);
            }
            this.maskObj = $("#ShxxLoginMask" + this.settings.id);
            // 验证码初始化
            $('.ctoCaptcha img').attr('src', this.settings.verifyApi);
            this.__loadScript();
        },
        // 关闭登录弹窗事件
        close: function () {
            this.maskObj.remove();
            this.wrapObj.remove();
            $(".shxx-register-main").remove();
            $(".shxx-forget-main").remove();
            $(".shxx-login-main").remove();
            $("body").css("overflow", "auto");
            $("html").css("overflow", "auto");
        },
        // 刷新验证码事件
        refreshCaptcha: function () {
            var imgObj = $('span.ctoCaptcha').children('img');
            imgObj.attr('src', this.settings.verifyApi);
        },
        //切换账号密码登陆
        hrhgLoginPwd: function () {
            $(".shxx-sms-login-main").css("display", "none");
            $(".shxx-login-main").css("display", "block");
            $(".input-clean").val("");
        },
        //切换注册弹窗
        registerHrhg: function () {
            $(".shxx-sms-login-main").css("display", "none");
            $(".shxx-register-main").css("display", "block");
            $(".input-clean").val("");
        },
        //关闭注册弹窗
        closeregisterHrhg: function () {
            $(".shxx-register-main").css("display", "none");
            $(".shxx-sms-login-main").css("display", "block");
            $(".input-clean").val("");
        },
        //切换忘记密码弹窗
        forgetKeyHrhg: function () {
            $(".shxx-login-main").css("display", "none");
            $(".shxx-forget-main").css("display", "block");
            $(".input-clean").val("");
        },
        //账号密码登陆弹窗切换短信验证码登陆弹窗
        hrhgPopupPwdToSms: function () {
            $(".shxx-login-main").css("display", "none");
            $(".shxx-sms-login-main").css("display", "block");
            $(".input-clean").val("");
        },
        //关闭忘记密码弹窗
        closeForgetKeyHrhg: function () {
            $(".shxx-forget-main").css("display", "none");
            $(".shxx-login-main").css("display", "block");
            $(".input-clean").val("");
        },
        // 账号密码登录提交事件
        loginUp: function () {
            var _self = this;
            var formObj = $('#formLoginDefault');
            // 手机判断
            var mobileObj = formObj.find('input[name="ucenter_mobile"]');
            if (!_self._passportFormCheck('mobile', mobileObj, mobileObj.parent('dd'))) {
                return false;
            }
            // 密码判断
            var passwordObj = formObj.find('input[name="ucenter_password"]');
            if (!_self._passportFormCheck('password', passwordObj, passwordObj.parent('dd'))) {
                return false;
            }
            // 验证码处理
            var captchaObj = formObj.find('input[name="cto_captcha"]');
            if (!_self._passportFormCheck('captcha', captchaObj, captchaObj.parent('dd'))) {
                return false;
            }
            var formData = {
                //'username': ctoAesEncrypt(mobileObj.val()),
                'username': mobileObj.val(),
                'validateCode': captchaObj.val(),
                'password': passwordObj.val(),
                'rememberMe': true,
            };
            $.ajax({
                url: _self.settings.loginUrl,
                type: "post",
                async: false,
                dataType: 'json',
                data: formData,
                success: function (result) {
                    if (result.code == 200) {
                        $(".login-msg").html(result.msg);
                        $(".shxxLoginPopUp").html("欢迎：" + result.data.nikeName)
                        delLocalStorageItem("userinfo");
                        delLocalStorageItem("phone");
                        var storage = window.localStorage;
                        storage.setItem("userinfo", JSON.stringify(result.data));
                        storage.setItem("phone", mobileObj.val());
                        _self.close();
                        window.location.href = _self.settings.jumpUrl;
                    }else if(result.code == 400) {
                        if(result.msg == "用户不存在/密码错误"){
                            passwordObj.val("");
                        }
                        captchaObj.val("");
                        _self.refreshCaptcha();
                        $(".login-msg").html(result.msg);
                    }else {
                        passwordObj.val("");
                        captchaObj.val("");
                        _self.refreshCaptcha();
                        $(".login-msg").html(result.msg);
                    }
                }
            });
        },
        smsLoginUp: function () {
            var _self = this;
            var formObj = $('#formSMSLoginDefault');
            // 手机判断
            var mobileObj = formObj.find('input[name="ucenter_mobile"]');
            if (!_self._passportFormCheck('mobile', mobileObj, mobileObj.parent('dd'))) {
                return false;
            }
            // 短信验证码
            var smsNum = formObj.find('input[name="cto_sms"]');
            if (!_self._passportFormCheck('captcha', smsNum, smsNum.parent('dd'))) {
                return false;
            }
            // 验证码处理
            var captchaObj = formObj.find('input[name="cto_captcha"]');
            if (!_self._passportFormCheck('captcha', captchaObj, captchaObj.parent('dd'))) {
                return false;
            }
            var formData = {
                'phone': mobileObj.val(),
                'validateCode': captchaObj.val(),
                'msgValidateCode': smsNum.val(),
            };
            $.ajax({
                url: _self.settings.smsloginUrl,
                type: "post",
                async: false,
                dataType: 'json',
                data: formData,
                success: function (result) {
                    if (result.code == 200) {
                        $(".login-msg").html(result.msg);
                        $(".shxxLoginPopUp").html("欢迎：" + result.data.nikeName)
                        delLocalStorageItem("userinfo");
                        delLocalStorageItem("phone");
                        var storage = window.localStorage;
                        storage.setItem("userinfo", JSON.stringify(result.data));
                        storage.setItem("phone", mobileObj.val());
                        _self.close();
                        window.location.href = _self.settings.jumpUrl;
                    }else if(result.code == 400) {
                        if(result.msg == "短信验证码错误"){
                            smsNum.val("");
                        }
                        captchaObj.val("");
                        _self.refreshCaptcha();
                        $(".login-msg").html(result.msg);
                    }else {
                        smsNum.val("");
                        captchaObj.val("");
                        _self.refreshCaptcha();
                        $(".login-msg").html(result.msg);
                    }
                }
            });
        },
        //注册
        userRegister: function () {
            var _self = this;
            var formObj = $('#formRegisterDefault');
            // 手机判断
            var mobileObj = formObj.find('input[name="ucenter_mobile"]');
            if (!_self._passportFormCheck('mobile', mobileObj, mobileObj.parent('dd'))) {
                return false;
            }
            // 密码判断
            var passwordObj = formObj.find('input[name="ucenter_password"]');
            if (!_self._passportFormCheck('password', passwordObj, passwordObj.parent('dd'))) {
                return false;
            }
            // 确认密码判断
            var passwordreObj = formObj.find('input[name="ucenter_password_qr"]');
            if (!_self._passportFormCheck('password', passwordreObj, passwordreObj.parent('dd'))) {
                return false;
            }
            //确认密码判断是否相同
            if (!_self._passportFormCheck('confirmpwd', passwordObj, passwordreObj)) {
                return false;
            }
            // 验证码处理
            var captchaObj = formObj.find('input[name="cto_captcha"]');
            if (!_self._passportFormCheck('captcha', captchaObj, captchaObj.parent('dd'))) {
                return false;
            }
            // 短信验证码
            var smsNum = formObj.find('input[name="cto_sms"]');
            if (!_self._passportFormCheck('captcha', smsNum, smsNum.parent('dd'))) {
                return false;
            }

            var formData = {
                'username': mobileObj.val(),
                'validateCode': captchaObj.val(),
                'password': passwordObj.val(),
                'passwordConfirm':passwordreObj.val(),
                'msgValidateCode': smsNum.val(),
            };
            $.ajax({
                url: _self.settings.registerUrl,
                type: "post",
                async: false,
                dataType: 'json',
                data: formData,
                success: function (result) {
                    if (result.code == 200) {
                        $(".register-msg").html(result.msg);
                        $(".shxx-login-mask-show").remove();
                        $(".shxx-login-main").remove();
                        $(".shxx-register-main").remove();
                        $(".shxx-forget-main").remove();
                    } else if (result.code == 400) {
                        if(result.msg == "短信验证码错误"){
                            smsNum.val("");
                        }
                        captchaObj.val("");
                        _self.refreshCaptcha();
                        $(".register-msg").html(result.msg);
                    } else {
                        $(".register-msg").html(result.msg);
                    }
                }
            });
        },
        //忘记密码
        userForget: function () {
            var _self = this;
            var formObj = $('#formForgetDefault');
            // 手机判断
            var mobileObj = formObj.find('input[name="ucenter_mobile"]');
            if (!_self._passportFormCheck('mobile', mobileObj, mobileObj.parent('dd'))) {
                return false;
            }
            // 密码判断
            var passwordObj = formObj.find('input[name="ucenter_password"]');
            if (!_self._passportFormCheck('password', passwordObj, passwordObj.parent('dd'))) {
                return false;
            }
            // 验证码处理
            var captchaObj = formObj.find('input[name="cto_captcha"]');
            if (!_self._passportFormCheck('captcha', captchaObj, captchaObj.parent('dd'))) {
                return false;
            }
            // 短信验证码
            var smsNum = formObj.find('input[name="cto_sms"]');
            if (!_self._passportFormCheck('captcha', smsNum, smsNum.parent('dd'))) {
                return false;
            }
            var formData = {
                'username': mobileObj.val(),
                'validateCode': captchaObj.val(),
                'password': passwordObj.val(),
                'msgValidateCode': smsNum.val(),
            };
            $.ajax({
                url: _self.settings.forgotPwdUrl,
                type: "post",
                async: false,
                dataType: 'json',
                data: formData,
                success: function (result) {
                    if (result.code == 200) {
                        $(".forget-msg").html("密码修改成功");
                        $(".shxx-login-mask-show").remove();
                        $(".shxx-login-main").remove();
                        $(".shxx-register-main").remove();
                        $(".shxx-forget-main").remove();
                    } else if (result.code == 400) {
                        if(result.msg == "短信验证码错误"){
                            smsNum.val("");
                        }
                        captchaObj.val("");
                        _self.refreshCaptcha();
                        $(".forget-msg").html(result.msg);
                    } else {
                        $(".forget-msg").html("密码修改失败");
                    }
                }
            });
        },
        //发送短信验证码
        _sendSMSCode: function (obj) {
            var _self = this;
            var formObj = $('#' + obj);
            // 手机判断
            var mobileObj = formObj.find('input[name="ucenter_mobile"]');
            if (!_self._passportFormCheck('mobile', mobileObj, mobileObj.parent('dd'))) {
                return false;
            }
            var data = {
                "phoneNumber": mobileObj.val()
            }
            $.ajax({
                url: _self.settings.sendCodeUrl,
                type: "post",
                async: false,
                dataType: 'json',
                contentType: "application/json",
                data: JSON.stringify(data),
                error: function (e) {
                    console.log(e);
                },
                success: function (result) {
                    if (result.code == 200) {
                        $("a.send-sms").html("短信发送成功");
                        phoneCodeSet();
                    } else {
                        $("a.send-sms").html("短信发送失败");
                        $('a.send-sms').css("pointer-events", "auto");
                    }
                }
            });
        },
        // 验证
        _passportFormCheck: function (type, checkObj, appendObj) {
            type = type || '';
            var success = true;
            var errorStr = '';
            switch (type) {
                case 'mobile':
                    var checkReg = /^1(2[0-9]|3[0-9]|4[479]|5[0-35-9]|6[0-9]|7[0-9]|8[0-9]|9[0-9])\d{8}$/;
                    var checkVal = checkObj.val() || '';
                    if (checkVal == '') {
                        errorStr = '手机号不能为空~';
                        success = false;
                    } else if (!checkReg.test(checkVal)) {
                        errorStr = '请输入正确的手机号~';
                        success = false;
                    }
                    break;
                case 'password':
                    var checkVal = checkObj.val() || '';
                    if (checkVal == '') {
                        errorStr = '密码不能为空~';
                        success = false;
                    }
                    if (checkVal.length > 20 || checkVal.length < 6) {
                        errorStr = '密码长度应在6-20个字符之间';
                        success = false;
                    }
                    break;
                case 'captcha':
                    var checkReg = /^[0-9A-z]{4}$/;
                    var checkVal = checkObj.val() || '';
                    if (checkVal == '') {
                        errorStr = '验证码不能为空~';
                        success = false;
                    } else if (!checkReg.test(checkVal)) {
                        errorStr = '请输入正确的验证码~';
                        success = false;
                    }
                    break;
                case 'confirmpwd':
                    var pwd1 = checkObj.val();
                    var pwd2 = appendObj.val();
                    if(pwd1 != pwd2){
                        errorStr = '输入的两次密码不相同~';
                        checkObj.focus();
                        var errorObj = $('<label class="error">' + errorStr + '</label>');
                        errorObj.appendTo(checkObj.parent('dd'));
                        errorObj.show();
                        setTimeout(function () {
                            errorObj.remove();
                        }, 1500);
                        return false;
                    }
                    break;
            }
            if (success) {
                return true;
            }
            checkObj.focus();
            var errorObj = $('<label class="error">' + errorStr + '</label>');
            errorObj.appendTo(appendObj);
            errorObj.show();
            setTimeout(function () {
                errorObj.remove();
            }, 1500);
            return false;
        }
    };
    $.fn.shxxLoginPopUp = function (options) {
        var shxxLoginPopUpObj = new shxxLoginPopUpClass(this, options);
        shxxLoginPopUpObj.index();
        return shxxLoginPopUpObj;
    }
    $.shxxLoginPopUp = function (options) {
        var shxxLoginPopUpObj = new shxxLoginPopUpClass(this, options);
        shxxLoginPopUpObj.index();
        return shxxLoginPopUpObj;
    }

})($, window, document);

