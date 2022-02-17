<template>
  <div class="container">
    <div class="left">
      <img src="@/assets/envelope-to-paper-plane-animation.gif" alt="animation"/>
      <div class="preview-container" v-show="show">
          <span>Id : </span>
          <input type="text" :value="preview.id" class="preview" />
          <a :href="preview.url" target="_blank"> <button>Show Email</button></a>
      </div>
    </div>
    <div class="right">
      <form @submit.prevent="sendEmail">
        <input type="text" placeholder="Name" v-model="name"/>
        <input type="email" placeholder="Email" v-model="email" />
        <input type="text" placeholder="Subject" v-model="subject" />
        <textarea placeholder="Message"  v-model="message"/>
        <button>SEND</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      name:"",
      email:"",
      subject:"",
      message:"",
      preview: {
        id:"",
        url:""
      },
      show:false
    }
  },
  methods: {
    sendEmail() {
      if (this.name==="" || this.email==="" || this.subject==="" || this.message==="") {
        this.$toast.error("All fields are required", {
            position:'top-right',
            pauseOnHover:true,
            duration:5000
        });
      }else {
        this.axios.post('https://nodemailer-server-1994.herokuapp.com/api/mail/send', 
          {name:this.name, email:this.email,subject:this.subject, message:this.message }
        )
        .then((res) => {
          this.$toast.success("Check your inbox", {
            position:'top-right',
            pauseOnHover:true,
            duration:5000
          });
          this.preview.id = res.data.id;
          this.preview.url = res.data.url;
          this.show = true
        })
        .catch((err) => {
          this.$toast.error()(err.message, {
              position:'top-right',
              pauseOnHover:true,
              duration:5000
          });
        })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import './../assets/style.css';
</style>
