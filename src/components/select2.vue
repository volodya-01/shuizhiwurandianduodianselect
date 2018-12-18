<template>
  <div class="select">
    <div class="outbox">
      <div class="outbox1">
        <div class="outbox1-1">最大历时</div>
        <div class="outbox1-2">
          <div class="maxtimeinput">
            <el-input placeholder="请输入内容" v-model="input10" clearable></el-input>
          </div>
          <div class="hourfont">小时</div>
        </div>
      </div>
      <div class="outbox2">
        <div class="outbox2-1">发现污染点</div>
        <div class="outbox2-2">
          <div class="inbox2-1">
            <div class="wrdiput">
              <div v-for="(item0,index0) in list0" :key="index0" class="wrdiputoutbox">
                <div class="wrdiputinbox">
                  <span>{{item0.name.label}}</span>
                  <span
                    class="delet0 iconfont icon-shanchu"
                    @click="selectapi0(index0)"
                    style="color:#729a18"
                  ></span>
                </div>
              </div>
            </div>
            <div class="jiahao" @click="showselct">
              <img :src="imgurl" alt style="width:12px;height:12px">
            </div>
          </div>
          <div class="szdfont" @click="selectfun">水质点</div>
          <div class="searchpoint">.&nbsp;.&nbsp;.</div>
        </div>
      </div>
      <div class="outbox3">
        <div class="outbox3-1">污染发生时间</div>
        <div class="outbox3-2">
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </div>
      </div>
    </div>

    <!-- 下拉框部分 -->
    <div class="drapedwon" v-show="drap1">
      <div
        v-for="(item,index) in list1"
        :key="index"
        :class="{'active': list1[index].forhide == true}"
        class="drapedwonlist1"
        @click="selectapi(index)"
      >
        <div class="listinboix1">
          <span>{{list1[index].name.label}}{{list1[index].forhide}}</span>
        </div>
      </div>
    </div>

    <div class="drapedwon2" v-show="drap2">
      <div v-for="(item2,index2) in list0" :key="index2" class="drapedwonlist2">
        <div class="listinboix2">
          <span>{{item2.name.label}}</span>
          <span
            class="delet iconfont icon-shanchu"
            @click="selectapi2(index2)"
            style="color:#729a18"
          ></span>
        </div>
      </div>
    </div>

    <!-- 下拉框部分结束 -->
  </div>
</template>

<script>
import jttop from "../assets/jttop.png";
import jtdown from "../assets/jtdown.png";
import "../assets/iconfont/iconfont.css";
export default {
  name: "select2",
  data() {
    return {
      imgurl: jtdown,
      //ele-input
      input10: "",
      //ele-select
      options: [
        {
          value: "选项1",
          label: "黄金糕"
        },
        {
          value: "选项2",
          label: "双皮奶"
        },
        {
          value: "选项3",
          label: "蚵仔煎"
        },
        {
          value: "选项4",
          label: "龙须面"
        },
        {
          value: "选项5",
          label: "北京烤鸭"
        }
      ],
      value: "",
      drap1: false,
      drap2: false,
      nowIndex: 0,
      listnum0: [],
      list0: [],
      list1: []
    };
  },
  mounted() {
    var arr1 = [];
    for (var i = 0; i < 20; i++) {
      var label = "szxxc00" + i;
      var value = i;
      var a = { label, value };
      arr1.push({
        name: a,
        forhide: false
      });
    }
    this.list1 = arr1;
    console.log(this.list1);
  },
  methods: {
    selectfun() {
      if (this.drap1 == false) {
        this.drap1 = true;
        this.drap2 = false;
      } else {
        this.drap1 = false;
      }
    },
    showselct() {
      if (this.drap2 == false) {
        this.drap2 = true;
        this.drap1 = false;
      } else {
        this.drap2 = false;
      }
      if (this.imgurl == jtdown) {
        this.imgurl = jttop;
      } else if (this.imgurl == jttop) {
        this.imgurl = jtdown;
      }
    },
    selectapi(val) {
      // list1[index].forhide
      var a = val;
      var that = this;
      this.$set(that.list1[a], "forhide", !that.list1[a].forhide);
      console.log(this.list1[val]);
      var list0 = this.list0;
      if (list0.indexOf(this.list1[val]) == -1) {
        list0.push(this.list1[val]);
      } else {
        list0.splice(list0.indexOf(this.list1[val]), 1);
      }
      this.list0 = list0;
      console.log(this.list0);
    },
    selectapi2(val2) {
      var that = this;
      for (var i = 0; i < this.list1.length; i++) {
        if (this.list1[i].name == this.list0[val2].name) {
          that.$set(that.list1[i], "forhide", false);
        }
      }
      this.list0.splice(val2, 1);
    },
    selectapi0(val0) {
      var that = this;
      for (var i = 0; i < this.list1.length; i++) {
        if (this.list1[i].name == this.list0[val0].name) {
          that.$set(that.list1[i], "forhide", false);
        }
      }
      this.list0.splice(val0, 1);
    }
  }
};
</script>
<style>
.el-input__inner {
  height: 24px;
  line-height: 24px;
  padding: 0 5px;
}
.el-input__icon {
  line-height: 24px;
}
.el-input {
  font-size: 12px;
}
.el-select .el-input__inner:focus {
  border-color: #dcdfe6;
}
.el-select:hover .el-input__inner {
  border-color: #dcdfe6;
}

.el-input.is-active .el-input__inner,
.el-input__inner:focus {
  border-color: #dcdfe6;
  outline: 0;
}
.el-select .el-input.is-focus .el-input__inner {
  border-color: #dcdfe6;
}
.el-select-dropdown__item {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
}
.el-select-dropdown__item.selected {
  color: #729a18;
  font-weight: 700;
}
</style>
<style scoped>
.select {
  margin: 60px 400px;
}
.outbox {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  width: 378px;
  height: 192px;
  border: 1px #d1d1da solid;
}
.outbox1 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  /* justify-content: space-between; */
  align-items: center;
  width: 335px;
  height: 25px;
}
.outbox1-1 {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
}
.outbox1-2 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  margin-left: 56px;
}
.maxtimeinput {
  width: 172px;
  height: 24px;
  /*  border: 1px solid #dcdfe6;
border-radius: 5px; */
}
input {
  text-align: start;
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  border: none;
  outline: none;
}
input::-webkit-input-placeholder {
  padding-left: 5px;
  color: #acb3ba;
}
input:-moz-placeholder {
  margin-left: 5px;
  color: #acb3ba;
}
input::-moz-placeholder {
  margin-left: 5px;
  color: #acb3ba;
}
input:-ms-input-placeholder {
  margin-left: 5px;
  color: #acb3ba;
}

.hourfont {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  margin-left: 35px;
}
.outbox2 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  width: 335px;
  height: 25px;
  margin-top: 30px;
}
.outbox2-1 {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  width: 60px;
  height: 24px;
  line-height: 24px;
}
.outbox2-2 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
}
.inbox2-1 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  border: 1px solid #dcdfe6;
  border-radius: 4px;
}
.wrdiput {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: center;
  width: 112px;
  height: 24px;
  /*  background-color: #f0f0f1; */
  overflow: hidden;
}
.wrdiputoutbox {
  width: 142px;
  height: 24px;
}
.wrdiputinbox {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  width: 80px;
  height: 24px;
  line-height: 24px;
}

.jiahao {
  width: 20px;
  height: 24px;
  line-height: 24px;
  padding-left: -4px;
  /*  background-color: #f0f0f1; */
  /* margin-left: 10px; */
  cursor: pointer;
}
.delet0 {
  margin-left: 5px;
}
.iconfont {
  font-size: 12px;
}
.szdfont {
  width: 48px;
  height: 22px;
  line-height: 22px;
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  border: 1px solid #dcdfe6;
  border-radius: 4px;
  margin-left: 10px;
  cursor: pointer;
}
.searchpoint {
  width: 26px;
  height: 22px;
  line-height: 16px;
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  border: 1px solid #dcdfe6;
  border-radius: 4px;
  margin-left: 10px;
  cursor: pointer;
}
.outbox3 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  /* justify-content: space-between; */
  align-items: center;
  width: 335px;
  height: 25px;
  margin-top: 30px;
}
.outbox3-1 {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  width: 75px;
  height: 24px;
  line-height: 24px;
  margin-left: -3px;
}
.outbox3-2 {
  width: 172px;
  height: 24px;
  border-radius: 2px;
  margin-right: 5px;
  outline: none;
  border: none;
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  cursor: pointer;
  margin-left: 30px;
}

/* 下拉框部分样式 */
.drapedwon {
  width: 151px;
  height: 163px;
  border: 1px #e4e4ec solid;
  /*  background-color: #d1d1da; */
  position: relative;
  top: -80px;
  left: 271px;
  overflow: auto;
  background-color: #fff;
}

.drapedwonlist1 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  color: #818d9a;
}
/* .drapedwonlist1:nth-child(even){
    background-color: #818d9a
} */
.listinboix1 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: center;
  height: 30px;
  width: 108px;
  /*  margin-left: 20px; */
}
.listinboix1 > span {
  font-size: 12px;
  font-family: "微软雅黑";
  /* color: #818d9a; */
  cursor: pointer;
}

.drapedwon2 {
  width: 130px;
  height: 110px;
  border: 1px #e4e4ec solid;
  /*  background-color: #d1d1da; */
  position: relative;
  top: -80px;
  left: 127px;
  overflow: auto;
  background-color: #fff;
}
.drapedwonlist2:hover {
  background-color: #f0f0f1;
}
.listinboix2 {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  height: 30px;
  width: 90px;
  margin: 0 15px;
}
.listinboix2 > span {
  font-size: 12px;
  font-family: "微软雅黑";
  color: #818d9a;
  cursor: pointer;
}
.delet {
  margin-left: 20px;
}
.active {
  background-color: #f0f0f1;
  color: #729a18;
  /*  border-bottom: 1px #d1d1da solid; */
}

select {
  border: none;
  outline: none;
}
</style>
