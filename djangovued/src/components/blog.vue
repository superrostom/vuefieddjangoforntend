<template>
  <div class="main" >

     <div class="body" >
    <div v-for="post in posts" v-bind:key="post.id"  >
      <h2>{{post.title}}</h2>
      <h3>{{post.body}}</h3>
      <br/>
      <br/>
      <br/>
      <button v-on:click="deletePostHandle(post.id)" > delete </button>

    </div>
    <div class="div" >
      <button v-if="!showForm"   v-on:click="showFormHandel"  > add post </button>
      <button v-on:click="logoutHandle" > sign out </button>
    </div >
    <div class="divf"  v-if="showForm">
      <textarea rows="3" cols="5" placeholder="  post's title "  v-model="title" @keyup.enter="addPostHandel" ></textarea>
      <textarea rows="5" cols="10" placeholder="your post" v-model="body" @keyup.enter="addPostHandel" ></textarea>
      <button type="button" v-on:click="addPostHandel"  @click="showFormHandel" >submit</button>

    </div>
     </div>
    </div>

</template>

<script>

  import {mapState} from 'vuex'

  export default {
    name: "blog",
    props:{

    },


    computed: {
      ...mapState([
        'posts',
        'showForm'
      ]),

    },

    data() {
      return {
        id:0,
        title: '',
        body: ''
        }

      },


    created() {
        this.$store.dispatch('retrievePosts').then(response=>
        {

        })


    },
    methods: {
      showFormHandel(){

        this.$store.commit('showForm')
      },


      deletePostHandle(id) {
        this.$store.dispatch('deletePost',id).then(response=>
        {


        })


      },

      logoutHandle() {
        this.$store.commit('destroyToken');

        this.$router.push({name: 'home'});

      },

      addPostHandel(){
        this.id= this.$store.state.posts.length;
        this.$store.dispatch('addPost',{
          'id':this.$store.state.posts.length,
          'title': this.title,
          'body': this.body}).then(response=>{


        })

      },



    },

  }




</script>

<style scoped>

  .body{
    display: grid;
    grid-template-columns: 1fr;
    justify-self: center;

    box-sizing: border-box;
    transition: all 3s ease-in-out 0s;
    -webkit-transition: width 2s, height 4s;
    box-shadow: 1px 1px 25px rgba(0, 0, 0, 0.35);
    border-radius: 10px;
    justify-items: center;
    padding: 10px 10px 10px 10px;

  }

  h2{


  }

  .div {
    display: flex;
    flex-direction: row;
    justify-items: self-end;
  }


  button {


    width: 60px;
    height: 30px;
    background-color: rgba(0, 0, 0, 0.3);
    border: none;
    text-align: center;
    margin-top: 10px;
    display: inline-block;
    color: white;
    font-family: inherit;
    box-shadow: 1px 1px 25px rgba(0, 0, 0, 0.35);
    border-radius: 10px;
    cursor: pointer;
  }

  button:hover {background-color: black}

  button:active {
    background-color: black;
    box-shadow: 0 5px #666;
    transform: translateY(4px);

  }
  .divf{
    display: grid;
    grid-template-columns: 1fr;
    justify-self: center;

  }
  textarea {
    margin-top: 10px;
    -moz-border-bottom-colors: none;
    -moz-border-left-colors: none;
    -moz-border-right-colors: none;
    -moz-border-top-colors: none;
    background: none repeat scroll 0 0 rgba(0, 0, 0, 0.07);
    border-color: silver;
    border-image: none;
    border-radius: 6px 6px 6px 6px;
    border-style: none solid solid none;
    border-width: medium 1px 1px medium;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.12) inset;
    color: #555555;
    font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
    font-size: 1em;
    line-height: 1.4em;
    padding: 5px 8px;
    transition: background-color 0.2s ease 0s;
  }


  textarea:focus {
    background: none repeat scroll 0 0 #FFFFFF;
    outline-width: 0;
  }
</style>
