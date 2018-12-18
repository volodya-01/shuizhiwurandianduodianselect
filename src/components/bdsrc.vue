<template>
  <div @click="home">
    <img :src="home_url" alt="..." style="height: 10vw">
  </div>
</template> 
       <script>
// 下面是导入两张图片的相对地址
/*   import home_no from '../static/icon/home_no.png'
  import home from '../static/icon/home.png' */
import jttop from "../assets/jttop.png";
import jtdown from "../assets/jtdown.png";
export default {
  name: "bdsrc",
  data() {
    return {
      home_url: jttop
    };
  },
  methods: {
    home() {
        if(this.home_url ==jtdown){
this.home_url = jttop
        }else if(this.home_url == jttop){
            this.home_url = jtdown
        }
      
    }
  }
};
</script>
