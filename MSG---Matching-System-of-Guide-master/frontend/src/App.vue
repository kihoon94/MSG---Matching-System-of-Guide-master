<template>
    <v-ons-page>
        <div id="app">
            <div id="nav">
                <v-ons-button @click="$ons.notification.alert('홈!')">Home Button</v-ons-button>
                    <div align="right">
                        <v-ons-button @click="$ons.notification.alert('로그인!')">Login</v-ons-button>
                        <v-ons-button @click="$ons.notification.alert('회원가입!')">Assign</v-ons-button>
                    </div>
            </div>
        </div>
    </v-ons-page>
</template>

<script>
    export default {
        name: 'test',
        data () {
            {

            }
            return {
            }
        },
        methods: {
            // forceRerender() {
            //     if (!this.$session.exists()) {
            //         return true;
            //     }
            //     else{
            //         return false;
            //     }
            // },
            // logout: function () {
            //     alert('success logout')
            //     this.$session.destroy()
            //     this.$router.push('/temp')
            // }
        }
    }
</script>

<style>
</style>