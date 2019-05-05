<template>
  <v-ons-page modifier="white">
    <custom-toolbar v-bind="toolbarInfo"></custom-toolbar>
    <div id="SignUp">
      <h1 style="font-size: 40px; color: #A9BCF5" align="center">MSG</h1>
      <h1 style="font-size: 25px" align="center">이름</h1>
      <input class="register_name" v-model="user.name" placeholder="Name">
      <h1 style="font-size: 25px" align="center">이메일</h1>
      <input class="register_id" v-model="user.email" placeholder="Email">
      <h1 style="font-size: 25px" align="center">패스워드</h1>
      <input class="register_pw" v-model="user.password" type="password"  placeholder="password" align="center">
      <h1 style="font-size: 25px" align="center">타입</h1>
      <select class="register_type" v-model="user.type">
        <option disabled value="">Please select one</option>
        <option>여행객</option>
        <option>가이드</option>
      </select>
      <p align="center">
        <button class="register_button" @click="signUp()">SignUp</button>
      </p>
    </div>
  </v-ons-page>
</template>

<script>

  import firebase from 'firebase';

export default {
  methods: {
    signUp(){
      firebase.auth().createUserWithEmailAndPassword(this.user.email, this.user.password)
              .then((user) => {
                console.log(user)
                alert('제출되었습니다.');
                this.$store.commit('navigator/pop');
              })
              .catch((error) => {
                console.log(error)
                alert(error)
              })
    }
  },
  data() {
    return {
      user: {
        email: '',
        password: '',
        name: '',
        type: ''
      }
    };
  }
};
</script>

<style>
  .register_button{
    width: 150px;
    height: 61px;
    padding-top: 1px;
    border: none;
    border-radius: 0;
    background-color: #A9BCF5;
    cursor: pointer;
    text-align: center;
    color: #fff;
    font-size: 20px;
    font-weight: 700;
    line-height: 61px;
    -webkit-appearance: none;
  }
  .register_name{
    background: #fff;
    display: block;
    margin: auto;
    padding: 5px 35px 10px 15px;
  }
  .register_id{
    background: #fff;
    display: block;
    margin: auto;
    padding: 5px 35px 10px 15px;
  }
  .register_pw{
    background: #fff;
    display: block;
    margin: auto;
    padding: 5px 35px 10px 15px;
  }
  .register_type{
    background: #fff;
    display: block;
    margin: auto;
    padding: 5px 35px 10px 15px;
  }
</style>
