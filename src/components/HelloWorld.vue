<template>
  <div class="hello">
    <input type="text" placeholder="http://example.com" v-model="url" required/>
    <button v-on:click="add">生成</button>
    <h2 v-if="is_showing">短縮URL</h2>
    <a v-bind:href="short_url">{{ short_url }}</a>
    <h2 v-if="is_showing">有効期限</h2>
    <p>{{expire}}</p>
  </div>
</template>

<script>
 import axios from 'axios'
 export const HTTP = axios.create({
     baseURL: `http://localhost:4567/`
 })
 export default {
     name: 'HelloWorld',
     data () {
         return {
             'url': '',
             'short_url': '',
             'expire': '',
             'is_showing': false
         }
     },
     methods: {
         add: function() {
             HTTP.post(`/add`, {
                 'url': this.url
             }).then(response => {
                 if(response.data["code"] == 0) {
                     console.log(response.data);
                     this.$data.is_showing = true
                     this.$data.short_url = response.data["url"]
                     this.$data.expire = response.data["time"]
                 }
             }).catch(e => {
                 alert(e);
             })
         }
     }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
  text-decoration: none;
 }

 input {
   padding-left: 1em;
   width: 20%;
   height: 40px;
   font-size: 100%;
 }
 
 input[type="text"] {
   border: 1px solid #999;
 }
 input[type="text"]:focus {
   border: 1px solid #ff9900;
   outline: 0;
 }
 button {
   font-size: 1.2em;
   padding-top: 10px;
   padding-left: 15px;
   padding-right: 15px;
   padding-bottom: 8px;
   border-style: none;
   color: white;
   background-color: #ff9900;
 }
 
</style>
