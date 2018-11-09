一个注册页面的vue模版，对于前端所使用的input标签，vue基本可以完全兼容
好难- -
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>DEMO</title>
    <script src="./vue.js"></script>
</head>
<body>
<div id="app">
    <p>
        email：<input v-model="mail"/>
    </p>
    <p>
        code setting：<input type="password" v-model="pw"/>
    </p>
    <p>
        name：<input v-model="name" placeholder="请参考组织/企业/品牌名称"/>
    </p>
    <p>
        localtion：
        <select v-model="province">
            <option value="zhejiang">浙江</option>
            <option value="shanghai">上海</option>
        </select>
        <select v-model="city">
            <option v-for="(val,key) in citys" v-bind:value="key">{{val}}</option>
        </select>
    </p>
    <p>
        verificationcode：
        <input v-model="verificationCode">
        please input：1234
    </p>
    <p>
        <input type="button" v-on:click="check" value="提交"/>
        <input type="button" v-on:click="inputDefault" value="默认值"/>
    </p>
    <p style="color:green" v-if="error=='success'">提交成功</p>
    <p style="color:red" v-if="error=='less'">缺少内容</p>
    <p style="color:red" v-if="error=='VerificationCode'">验证码错误</p>
</div>
<script>
    new Vue({   //创建一个Vue的实例
        el: "#app", //挂载点是id="app"的地方
        created: function () {
            this.changeProvince();
        },
        data: {     //数据
            province: "zhejiang",
            mail: "",
            pw: "",
            name: "",
            city: "",
            citys: {},
            <!-- 城市
            provinceWithCity: {
                zhejiang: {
                    hangzhou: "杭州",
                    shaoxing: "绍兴"
                },
                shanghai: {
                    pudong: "浦东区",
                    jingan: "静安区"
                }
            ---->
               
            },
            verificationCode: "",
            error: ""
        },
        methods: {
            changeProvince: function () {
                this.citys = this.provinceWithCity['zhejiang'];
                this.$watch('province', function (newVal, oldVal) {
                    this.citys = this.provinceWithCity[newVal];
                })
            },
            check: function () {    //提交内容检查
                if (this.mail && this.pw && this.name && this.province && this.city) {
                    if (this.verificationCode === '1234') {
                        this.error = 'success';
                        console.log([this.mail, this.pw, this.name, this.province, this.city]);
                    } else {
                        this.error = 'VerificationCode'
                    }
                } else {
                    this.error = 'less';
                }
            },
            inputDefault: function () {
                this.mail = '123@qq.com';
                this.pw = '123';
                this.name = 'abc';
                this.province = 'zhejiang';
                this.city = 'hangzhou';
                this.verificationCode = '1234';
            }
        }
    })
</script>
</body>
</html>
