<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <div class="input">
      <input type="hidden" name="index" v-model="index_temp">
      <label>URL :</label>
      <input type="text" name="url" v-model="url_temp">
      <label>NAME :</label>
      <input type="text" name="name" class="name_input" v-model="name_temp">
      <label>DESC :</label>
      <input type="text" name="desc" class="desc_input" v-model="desc_temp">
      <input type="submit" name="submit" value="SUBMIT" v-on:click="addImage">
      <input type="submit" name="submit" value="DELETE" v-on:click="deleteImage">
    </div>
    <br>  
    <hr>
    <br>  
    <div class="gallery">
      <div>
        <button id="prev" v-on:click="prev"> << </button>
        <img v-bind:src="items[index_temp].url" style="max-width: 900px">
        <!-- <div style="width:500px;height:300px; margin: 0 auto;" :style="{ 'background-image': 'url(' + items[index_temp].url + ')'}"></div> -->
        <button id="next" v-on:click="next">>></button>
      </div>
      <div>
        <h1>{{items[index_temp].name}}</h1>
        <p>{{items[index_temp].desc}}</p>
      </div>
      <hr>
      <div>
        <!-- <span class="thumbnail-list" v-for="item in items" :key="item.name"> -->
        <span class="thumbnail-list" v-for="(item, index) in items" v-on:click="selectImage(index)">
          <img v-bind:src="item.url" class="thumbnail">
          <h5>{{item.name}}</h5>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Mini Gallery',
      name_temp: '',
      desc_temp: '',
      url_temp: '',
      index_temp: 0,
      items: [
        { name: 'tumblr',
          desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. ',
          url: 'https://m.ayobandung.com/images-bandung/post/articles/2018/12/26/42324/timblr.jpg' },
        { name: 'google',
          desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. ',
          url: 'https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_92x30dp.png' },
        { name: 'bing',
          desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. ',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/Bing_logo_%282016%29.svg/1200px-Bing_logo_%282016%29.svg.png' }      
      ]
    }
  },
    methods: {
      addImage(){
        this.items.push({name: this.name_temp, url: this.url_temp , desc: this.desc_temp});
        this.name_temp='';
        this.url_temp='';
        this.desc_temp='';
      },
      deleteImage(){
        if(this.index_temp!=0){
          this.items.splice(this.index_temp, 1);
          this.name_temp='';
          this.url_temp='';
          this.desc_temp='';
          this.index_temp--;
        }
      },
      selectImage(index){
        this.name_temp=this.items[index].name;
        this.url_temp=this.items[index].url;
        this.desc_temp=this.items[index].desc;
        this.index_temp=index;
      },
      prev(){
        if(this.index_temp > 0) this.index_temp--;
      },
      next(){
        if(this.index_temp < this.items.length-1) this.index_temp++;
      }      
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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
}

.thumbnail{
  max-width: 200px;
}

.thumbnail-list{
  display: inline-block;
  margin: 10px;
}
</style>
