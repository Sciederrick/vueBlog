<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>List Blog Titles</h1>
    <input type="text" v-model="search" placeholder="search blogs"/>
    <div v-for="blog in filteredBlogs" class="single-blog">
      <h2 v-rainbow>{{ blog.title|to-uppercase }}</h2>
    </div>
	</div>
</template>

<script>
import searchMixin from '../mixins/searchMixin';

export default {
  data () {
    return {
      blogs:[],
      search:''
    }

  },
  methods:{

  },
  created(){
    this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
      console.log(data);
      console.log(Math.random().toString().slice(2,8));
      this.blogs=data.body.slice(0,10);
    });
  },
  computed:{

  },
  // Registering filters locally
  filters:{
    'to-uppercase': function(value){
      return value.toUpperCase();
    }
  },
  //Registering directives locally
  directives:{
    'rainbow': {
      bind(el, binding, vnode){
        el.style.color="#" + Math.random().toString(16).slice(2,8);
      }
    }
  },
  mixins:[searchMixin] //registering searchMixin
}
</script>

<style scoped>
  #show-blogs{
    max-width:800px;
    margin:0 auto;
  }
  .single-blog{
    padding:20px;
    margin:20px 0;
    box-sizing:border-box;
    background:#eee;
  }
</style>
