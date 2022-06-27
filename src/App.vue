<script>
export default {
  data() {
    return {
      message: '',
      messageColor:"green",
      visibility:false,
      subscribedEmails:[],
      agreement: false,
      email:''
    };
  },
  methods: {
    subscribe(){
      let inSubscribed = this.subscribedEmails.indexOf(this.email)>=0;
      if (inSubscribed ){
        this.message = "You have already subscribed to the newsletter";
        this.messageColor = "red";
      }
      else if (!this.agreement){
        this.message = "Check agreement field";
        this.messageColor = "red";
      }
      else if(!inSubscribed && this.agreement){
        this.message =  "You have successfully subscribed to the newsletter";
        this.messageColor = "green";
        this.subscribedEmails.push(this.email);
        this.email = "";
      }
    },
    showModal() {
      this.visibility = true;
    },
    close(){
      this.visibility = false;
    }
  }
};
</script>

<template>
  <div id="app">
    <button @click="showModal">Subscribe</button>
    <dialog class="modal" :open="visibility">
      <div class="content">
        <div class="close" @click="close">X</div>
        <h1><span class="bigger">10%</span> off </h1>
        <div class="first_order">your first order</div>
        <hr width="200px"/>
        <p class="subscribe_text">Subscribe to receive 10% off promocode plus exclusive offers and deals</p>
        <div><label>Email-address</label></div>
        <div><input type="text" v-model="email"/></div>
        <div><button class="button" @click="subscribe">Subscribe</button></div>
        <div>
          <label><input type="checkbox" v-model="agreement"/>I agree with privacy policy</label></div>
        <div v-if="message" v-bind:style="{color:messageColor}">{{ message }}</div>
      </div>
  </dialog>
  </div>
</template>

<style>
 body{font-family:Roboto;}
  .subscribe_text{
    margin-bottom:40px;font-size:14px;
  }
  .modal{
    background-image:url('assets/Frame 2547.png');
    background-position:right;
    background-repeat:no-repeat;
    width:864px;height:502px;
    /*width:500px;height:400px;*/
    border:1px solid black;
    padding:0px;
  }
  .modal .content{
    padding:10px;
  }
  .first_order{
    font-size:24px;font-weight:bold;color:#828688;
  }
  .close{ position:absolute;right:10px;top:10px;cursor:pointer;
  }
  .bigger{
    font-size:104px;
  }
  .button{margin:10px 0px;height:40px;border-radius:35px;padding:5px;background-color: #C24DFE;color:white;width:106px;}
  input[type='text']{font-size:1.5em;border-radius:5px;border-color:#DDDDDD;}
</style>
