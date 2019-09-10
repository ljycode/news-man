<template>
    <div>
        <form action="" v-if="!isReg">
            <p>
                用户名：<input type="text" v-model="name">
            </p>
            <p>
                密码：<input type="password" v-model="password">
            </p>
            <button type="button" @click="login()">登录</button>
            <button type="button" @click="reg()">注册</button>
        </form>
        <form action="" v-else>
            <p>
                用户名：<input type="text" v-model="name">
            </p>
            <p>
                密码：<input type="password" v-model="password">
            </p>
            <p>
                再次输入密码：<input type="password" v-model="repeat">
            </p>
            <button type="button" @click="addUser()">确定</button>
            <button type="button" @click="cancel()">取消</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: "Login",
        data () {
            return {
                isReg: false,
                name: '',
                password: '',
                repeat: ''
            }
        },
        methods: {
            login () {
                if (localStorage.getItem('name') === this.name && localStorage.getItem('password') === this.password) {
                    this.$router.push('/home/list');  // 点击登录，路由进入home/list
                    this.name = '';
                    this.password = '';
                } else {
                    alert("输入的用户名或密码错误");
                }
            },
            reg () {
                this.isReg = true;
            },
            cancel () {
                this.isReg = false;
            },
            addUser () {
                if (this.password === this.repeat) {
                    localStorage.setItem('name', this.name);
                    localStorage.setItem('password', this.password);
                    this.name = '';
                    this.password = '';
                    this.isReg = false;
                } else {
                    alert("两次密码输入不一致");
                }
            }
        }
    }
</script>

<style scoped>

</style>