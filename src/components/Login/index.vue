<template>
    <div class="login_body">
        <div>
            <input class="login_text" type="text" placeHolder="账户名/手机号/Email" v-model="username">
        </div>
        <div>
            <input class="login_text" type="password" placeHolder="请输入您的密码" v-model="password">
        </div>
        <div class="login_btn">
            <input type="submit" value="登录" @touchstart="handleToLogin">
        </div>
        <div class="login_link">
            <router-link to="/mine/register">立即注册</router-link>
            <router-link to="/mine/findPassword">找回密码</router-link>
        </div>
    </div>
</template>

<script>
import { messageBox } from '@/components/js'
export default {
    name: "Login",
    data(){
        return{
            username:"",
            password:""
        }
    },
    methods:{
        handleToLogin(){
            this.axios.post('/api2/users/login',{
                username:this.username,
                password:this.password
            }).then(res=>{
                console.log(res)
                var _this = this
                var status = res.data.status;
                if(status === 0){
                    messageBox({
                        title:"登录",
                        content:"登录成功",
                        ok:"确定",
                        handleOk(){
                            _this.$router.push('/mine/center')
                        }
                    })
                }else{
                    messageBox({
                        title:"登录",
                        content:"登录失败",
                        ok:"确定"
                    })
                }
            })
        }
    }
}
</script>

<style scoped>
#content .login_body{  width:100%;}
.login_body .login_text{ width:100%; height: 40px; border:none; border-bottom: 1px #ccc solid; margin-bottom: 5px; outline: none; text-indent: 10px;}
.login_body .login_btn{ height:50px; margin:10px;}
.login_body .login_btn input{ width:100%; height:100%; background:#e54847; border-radius: 3px; border:none; display: block; color:white; font-size: 20px;}
.login_body .login_link{ display: flex; justify-content:space-between;}
.login_body .login_link a{ text-decoration: none; margin:0 5px; font-size: 12px; color:#e54847;}
</style>