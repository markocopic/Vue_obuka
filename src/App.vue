<template>
  <div id="main">

    <div v-if="showModal" class="edit-modal">
      <input v-model="singlePost.title" type="text"><br>
      <textarea v-model="singlePost.body" name="" id="" cols="50" rows="10"></textarea><br>
      <button @click="closeModal()">cancel</button>
      <button @click="updatePost()">save</button>

    </div>

    <div class="filters">
      <select name="" id="" v-model="userId">
        <option v-for="user in users" :value="user.id" :key="user.id">
          {{user.name}}
        </option>
      </select>
      
      <button @click="createPost()">Create Post</button>
    </div>

    <div class="posts-region">
      <div @click="selectPost(post)" v-for="post in posts" :key="post.id">
        <h3>{{post.title}}</h3>
        <p>{{post.body}}</p>
        <button @click="editPost(post)">edit</button>
        <button @click="deletePost(post)">delete</button>
      </div>
    </div>

    <div class="single-post">
     <h2>Post info:</h2>
     <hr>
     <h3>{{singlePost.title}}</h3>
     <p>{{singlePost.body}}</p>
     <hr>
     <h4>Comments:</h4>
     <ul>
       <li v-for="comment in comments" :key="comment.id"> 
        <p> {{comment.name}}</p>
        <span>{{comment.body}}</span><br>
        <small>email: {{comment.email}}</small>
        <hr>
      </li>
     </ul>
    </div>

  </div>
</template>

<script>
 import axios from 'axios'

export default {
  data(){
    return{
      title: 'VUE OBUKA',
      userId:1,
      posts:[],
      users:[],
      comments:[],
      singlePost:{},
      showModal:false,
      newPost:false
    }
  },
  mounted(){
    this.getData()
    this.getUsers()
  },
  watch:{
    userId(){
      this.getData()
    }
  },
  computed:{
  },
  methods:{
    createPost(){
      this.showModal = true
      this.newPost = true
    },
    updatePost(){
      console.log(this.selectPost);
      if (this.newPost) {
        axios.post('https://jsonplaceholder.typicode.com/posts',{
          title: this.singlePost.title,
          body: this.singlePost.body,
          userId: this.userId,
        }).then(res=>{
          console.log(res.data);
          this.newPost = false
          this.showModal = false
          this.singlePost = {}
          alert('Post created')
        })
      } else {
        axios.put('https://jsonplaceholder.typicode.com/posts/'+this.singlePost.id,this.singlePost)
        .then(res=>{
          console.log(res.data)
          this.showModal = false
          this.singlePost = {}
          alert('Post updated')
        })
      }
      
    },
    closeModal(){
      this.showModal = false
    },
    deletePost(post){
      axios.delete('https://jsonplaceholder.typicode.com/posts/'+post.id)
      .then(res=>{
        console.log(res.data);
      })
    },
    editPost(){
      this.showModal = true
    },
    getComments(){
      axios.get('https://jsonplaceholder.typicode.com/comments',{
        params:{
          postId: this.singlePost.id
        }
      }).then(
        res=>{
          this.comments = res.data
          console.log(this.comments);
        }
      )
    },
    selectPost(post){
      this.singlePost = post
      this.getComments()
    },
    getUsers(){
      axios.get('https://jsonplaceholder.typicode.com/users',{
        params:{
        }
      }).then(
        res=>{
          this.users = res.data
          console.log(this.users);

        }
      )
    },
    getData(){
      this.posts = []
      axios.get('https://jsonplaceholder.typicode.com/posts',{
        params:{
          userId:this.userId
        }
      }).then(
        res=>{
          this.posts = res.data
          console.log(res);

        }
      )
      // .catch(e=>{
      //   if (e.response.status == 404) {
      //     console.log(e.response.status);
      //   } else {
      //     console.log(e);
          
      //   }
      //   alert('Serevr error')
      // })
    }
  }
}
</script>

<style>
#main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.post{
  border: 1px solid grey;
  margin: 20px;
  cursor: pointer;
}
.posts-region{
  max-height: 40vh;
  overflow: auto;
  border: 1px solid grey;
  margin-top: 10px;
}
.single-post{
  max-height: 40vh;
  border: 1px solid grey;
  margin-top:20px;
  overflow: auto;

}
.edit-modal{
  position: absolute;
  top: 30%;
  left:30%;
  z-index: 1000;
  background-color: lightgrey;
  padding: 20px;
}
</style>
