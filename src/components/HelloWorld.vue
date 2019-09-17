<template>
  <div class="hello">
    <div><div class="loader"></div></div>
    <h1>{{ msg }}</h1>
    <!--<button>click me!</button>-->
    <select class="dogs-list" @change="get_data">
       <template  v-for="(lists, index) in list">
        <option :value="index">{{ index }}</option>
      </template>
    </select>
    <div class="img-main-div" v-if="images != ''">
      <template v-for="image in images">
          <img class="img-div" :src="image">
      </template>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
    data() {
    return {
      list: {},
      images: '',
    }
  },
  props: {
    msg: String
  },
  mounted: function() {
      document.querySelector('.loader').classList.add('load');
      axios.get('https://dog.ceo/api/breeds/list/all').then(response => {
        console.log(response.data);
        this.list = response.data.message;
        document.querySelector('.loader').classList.remove('load');
        console.log(this.list);
      }).catch(function (error) {
        // handle error
        console.log(error);
      });
  },
  methods: {
    get_data(e){
      document.querySelector('.loader').classList.add('load');
      console.log(e.target.value);
      axios.get('https://dog.ceo/api/breed/'+e.target.value+'/images').then(response => {
        console.log(response.data);
        this.images = response.data.message;
        document.querySelector('.loader').classList.remove('load');
      }).catch(function (error) {
        // handle error
        console.log(error);
      });
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
.dogs-list{
  padding: 5px 20px;
    border: 2px solid #918989;
    border-radius: 20px;
    outline: none;
    font-size: 25px;
}
.img-main-div{
  padding: 40px 40px;
}
.img-div{
    width: 45%;
    margin: 20px;
    height: 400px;
    border-radius: 20px;
    box-shadow: 0px 0px 40px 0px #173f3b;
}
.load{
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 6px solid black;
  border-top: 6px solid #fff;
  animation: animate 1.5s infinite linear;
}
.hello div{
    width: 100%;
    height: 1000px;
    opacity: 1;
    z-index: 2;
    background: #676a6954;
    position: fixed;
    margin: 0;
    padding: 0;
}

@keyframes animate{
  0%{
    transform: translate(-50%, -50%) rotate(0deg);
  }
  100%{
    transform: translate(-50%, -50%) rotate(360deg);
  }
}
  @media (min-width:320px) and (max-width:480px)  {
    .img-div{
      width: 85%;
      height: 200px;
    }
  }
</style>
