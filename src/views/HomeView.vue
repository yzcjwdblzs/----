<template>
  <div class="admin_box">
    <div class="head_top">
      <p class="head_text">任务列表</p>
      <div class="nav_box">
        <div class="left_nav">
          <div :class="ids == item.id ? 'admap_box' : 'map_box'"  @click="addNav(item.id)" v-for="(item) in data.head_list" :key="item.id">
            {{ item.name }}
          </div>
        </div>
        <div class="right_nav">
          <el-input v-model="input2" style="width: 240px" placeholder="输入任务名称" :suffix-icon="Search" class="inp" />
          <el-button style="margin-left: 2px;">高级搜索</el-button>
          <el-button type="primary" style="background-color: #0559A1;">新增任务</el-button>
        </div>
      </div>
    </div>

    <div class="select_box">
      排序
      <el-select v-model="value" placeholder="Select" size="small" style="width: 150px;margin-right: 10px;" >
        <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value" />
      </el-select>
      状态
      <el-select v-model="value" placeholder="Select" size="small" style="width: 150px" >
          <el-option v-for="item in option" :key="item.value" :label="item.label" :value="item.value" />
      </el-select>
    </div>

    <div class="foot_list">
      <div class="left_top" style="width: 42%;margin-right: 12px;margin-bottom: 7px;">
        <div class="herad_ltop">
          <p style="font-size: 18px;font-weight: 500;">重要不紧急</p>
          <p>更多</p>
        </div>
        <div class="foot_lbotm">
          <el-tree
            v-if="datas"
            style="max-width: 600px"
            :data="datas"
            :props="defaultProps"
            @node-expand="handleNodeExpand"
            @node-collapse="handleNodeCollapse"
            :expand-on-click-node="false"
          >
          <template #default="{ node, data }">
            <span class="custom-tree-node">
              <span style="font-size: 20px;display: inline-block;display: flex;align-items: center;">
                <p @click="linkParticulars(data.imgShow)">{{ node.label }}</p>
                <img src="../assets/龙江银行切图/pic_2.png" v-if="data.imgShow" @click="handleNodeClick(data)" alt=""  />
                <img src="../assets/龙江银行切图/pic_3.png" v-if="!data.imgShow" @click="handleNodeClick(data)" alt="" />
              </span>
              <div v-if="data.flag||!data.children" style="width: 330px;display: flex;font-size: 16px;">
                <el-progress :percentage="Number(data.value)"  />
                {{ data.name }}
                {{ data.time }}
              </div>
            </span>
          </template>
          </el-tree>
          <div v-else style="width: 40%;height: 100px;position: absolute;left: calc(50% - 20%);top: calc(50% - 50px); text-align: center;">
            <img src="../assets/龙江银行切图/pic_4.png" alt="">
            <p>无任务</p>
          </div>
        </div>
        <!-- <p style="text-align: center;line-height: 167px;">无任务</p> -->
      </div>

      <div class="left_bottom" style="width: 42%;margin-right: 12px;margin-top: 7px;">
        <div class="herad_ltop">
          <p style="font-size: 18px;font-weight: 500;">不紧急不重要</p>
          <p>更多</p>
        </div>
        <div class="foot_lbotm">
          <el-tree
            v-if="datas"
            style="max-width: 600px"
            :data="datas"
            :props="defaultProps"
            @node-expand="handleNodeExpand"
            @node-collapse="handleNodeCollapse"
            :expand-on-click-node="false"
          >
          <template #default="{ node, data }">
            <span class="custom-tree-node">
              <span style="font-size: 18px;display: inline-block;display: flex;align-items: center;">
                <p @click="linkParticulars(data.imgShow)">{{ node.label }}</p>
                <img src="../assets/龙江银行切图/pic_2.png" v-if="data.imgShow" @click="handleNodeClick(data)" alt=""  />
                <img src="../assets/龙江银行切图/pic_3.png" v-if="!data.imgShow" @click="handleNodeClick(data)" alt="" />
              </span>
              <div v-if="data.flag||!data.children" style="width: 330px;display: flex;font-size: 16px;">
                <el-progress :percentage="Number(data.value)"  />
                {{ data.name }}
                {{ data.time }}
              </div>
            </span>
          </template>
          </el-tree>
          <div v-else style="width: 40%;height: 100px;position: absolute;left: calc(50% - 20%);top: calc(50% - 50px); text-align: center;">
            <img src="../assets/龙江银行切图/pic_4.png" alt="">
            <p>无任务</p>
          </div>
        </div>
      </div>

      <div class="right_top" style="width: 42%;margin-left: 12px;margin-bottom: 7px;">
        <div class="herad_ltop">
          <p style="font-size: 18px;font-weight: 500;">重要且紧急</p>
          <p>更多</p>
        </div>
        <div class="foot_lbotm">
          <el-tree
            v-if="datas"
            style="max-width: 600px"
            :data="datas"
            :props="defaultProps"
            @node-expand="handleNodeExpand"
            @node-collapse="handleNodeCollapse"
            :expand-on-click-node="false"
          >
          <template #default="{ node, data }">
            <span class="custom-tree-node">
              <span style="font-size: 18px;display: inline-block;display: flex;align-items: center;">
                <p @click="linkParticulars(data.imgShow)">{{ node.label }}</p>
                <img src="../assets/龙江银行切图/pic_2.png" v-if="data.imgShow" @click="handleNodeClick(data)" alt=""  />
                <img src="../assets/龙江银行切图/pic_3.png" v-if="!data.imgShow" @click="handleNodeClick(data)" alt="" />
              </span>
              <div v-if="data.flag||!data.children" style="width: 330px;display: flex;font-size: 16px;">
                <el-progress :percentage="Number(data.value)"  />
                {{ data.name }}
                {{ data.time }}
              </div>
            </span>
          </template>
          </el-tree>
          <div v-else style="width: 40%;height: 100px;position: absolute;left: calc(50% - 20%);top: calc(50% - 50px); text-align: center;">
            <img src="../assets/龙江银行切图/pic_4.png" alt="">
            <p>无任务</p>
          </div>
        </div>
        <!-- <p style="text-align: center;line-height: 167px;">无任务</p> -->
      </div>

      <div class="right_bottom" style="width: 42%;margin-left: 12px;margin-top: 7px;">
        <div class="herad_ltop">
          <p style="font-size: 18px;font-weight: 500;">紧急不重要</p>
          <p>更多</p>
        </div>
        <div class="foot_lbotm" >
          <el-tree
            v-if="datas"
            style="max-width: 600px"
            :data="datas"
            :props="defaultProps"
            @node-expand="handleNodeExpand"
            @node-collapse="handleNodeCollapse"
            :expand-on-click-node="false"
          >
          <template #default="{ node, data }">
            <span class="custom-tree-node">
              <span style="font-size: 18px;display: inline-block;display: flex;align-items: center;">
                <p @click="linkParticulars(data.imgShow)">{{ node.label }}</p>
                <img src="../assets/龙江银行切图/pic_2.png" v-if="data.imgShow" @click="handleNodeClick(data)" alt=""  />
                <img src="../assets/龙江银行切图/pic_3.png" v-if="!data.imgShow" @click="handleNodeClick(data)" alt="" />
              </span>
              <div v-if="data.flag||!data.children" style="width: 330px;display: flex;font-size: 16px;">
                <el-progress :percentage="Number(data.value)"  />
                {{ data.name }}
                {{ data.time }}
              </div>
            </span>
          </template>
          </el-tree>
          <div v-else style="width: 40%;height: 100px;position: absolute;left: calc(50% - 20%);top: calc(50% - 50px); text-align: center;">
            <img src="../assets/龙江银行切图/pic_4.png" alt="">
            <p>无任务</p>
          </div>
        </div>
      </div>

      <!-- <div class="yz">
        <div class="yz_top">
          <p>重要</p>
        </div>
        <div class="yz_bottom">
          <p>不重要</p>
        </div>
      </div>
      <div class="xz">
        <div class="xz_left">
          <p>不紧急</p>
        </div>
        <div class="xz_right">
          <p>紧急</p>
        </div>
      </div> -->
    </div>
  </div>
</template>
<script setup>

import { useRouter, useRoute } from "vue-router";
import { useStore } from "vuex";
import { ref, reactive, computed, watch } from "vue";
import { Search } from '@element-plus/icons-vue'
// 引入路由
const router = useRouter();
// 路由对象
const route = useRoute();
// 引入仓库
const store = useStore();
// 父传子
const props = defineProps({});

const ids = ref(0);
const input2 = ref('');
const value = ref('');
const show = ref(false);

// 声明响应式数据
const data = reactive({
  head_list: [
    { id: 0, name: "我负责的" },
    { id: 1, name: "我协办的" },
    { id: 2, name: "我分配的" },
    { id: 3, name: "通知我的" },
  ],
});
const addNav = (e) => {
  ids.value = e;
};
const options = [
  {
    label: '结束时间倒叙',
    value: '',
  },
  {
    label: '结束时间正序',
    value: 'Option2',
  },
  {
    label: '开始时间倒叙',
    value: 'Option3',
  },
  {
    label: '开始事件正序',
    value: 'Option4',
  },
]
const option = [
  {
    label: '进行中',
    value: '',
  },
  {
    label: '已完成',
    value: 'Option2',
  },
  {
    label: '全部',
    value: 'Option3',
  },
]



const handleNodeClick = (data) => {
  // console.log(data);
  if(data.imgShow) {
    data.imgShow = 0
  }else {
    data.imgShow = 1
  }
}

const handleNodeExpand = (data) => {
  // console.log('我展开了:',data);
  data.flag = true
}
const linkParticulars = (e) => {
  console.log('我要跳转');
  let url = `https://www.baidu.com?id=${e}`;
  window.open(url);
}
const handleNodeCollapse = (data) => {
  data.flag = false
}

const datas = [
  {
    label: '清除缓存',
    value:'60',
    name:'张三',
    time:'2023-01-13',
    flag:false,
    imgShow:0,
    children: [
      {
        label: 'Level two 1-1',
        value:'56',
        name:'张三',
        time:'2023-01-13',
        flag:false,
        imgShow:0,
        children: [
          {
            label: 'Level three 1-1-1',
            value:'56',
            name:'张三',
            time:'2023-01-13',
            flag:false,
            imgShow:0,
          },
        ],
      },
    ],
  },
]



</script>
<style lang="scss" scoped>
.el-progress--line {
  width: 250px;
}
::v-deep .el-tree-node__content {
  height: 50px;
}
.admin_box {
  width: 100%;
  height: 100%;
}
.head_top {
  width: 100%;
  font-size: 26px;
  padding: 0 95px;
  height: 140px;
  background-color:  #F5F7FB;
}
.head_text {
  width: 100%;
  height: 50%;
  line-height: 70px;
}
.nav_box {
  width: 100%;
  height: 50%;
  display: flex;
  justify-content: space-between;
}
.left_nav {
  width: 35%;
  height: 100%;
  line-height: 70px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.map_box,
.admap_box {
  width: 22%;
  height: 100%;
  text-align: center;
  font-size: 18px;
  // line-height: 40px;
  cursor: pointer;
}
.admap_box {
  color: #00a9ff;
  border-bottom: 3px solid #00a9ff;
}
.right_nav {
  width: 30%;
  display: flex;
  align-items: center;
}
.inp {
  height: 35px;
}
.select_box {
  width: 50%;
  margin-top: 8px;
  font-size: 18px;
  padding-left: 95px;
}
.foot_list {
  width: 75%;
  margin: 0 auto;
  height: 100%;
  margin-top: 10px;
  position: relative;
  display: flex;
  align-content: center;
  flex-wrap: wrap;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-image: url(../assets/龙江银行切图/pic_1.png);
  background-repeat: no-repeat;
  background-size: 100% 100%;
}
.left_top {
  background: #E98339;
}
.left_bottom {
  background: #39B29A;
}
.right_top {
  background: #E65F5F;
}
.right_bottom {
  background: #5FA3FE;
}
.left_top,
.left_bottom,
.right_top,
.right_bottom {
  height: 38%;
  border-radius: 10px;
  border: 1px solid #ccc;
  overflow: hidden;
  // margin: 7px 0 0;
}
.herad_ltop {
  width: 100%;
  height: 40px;
  display: flex;
  padding: 5px 14px;
  font-family: PingFang SC;
  color: #fff;
  align-items: center;
  justify-content: space-between;
  // border-bottom: 1px solid #a08e66;
}
.foot_lbotm {
  position: relative;
  width: 100%;
  height: calc(100% - 40px);
  overflow-y: scroll;
  padding-top: 5px;
  border-radius: 0 0 10px 10px;
  background-color: #fff;
}

.yz {
  width: 3px;
  height: 91%;
  margin-top: 23px;
  background-color: #797979;
  position: absolute;
}
.yz_top {
  position: absolute;
  top: -18px;
  left: -8px;
  border-left:10px solid transparent;
  border-right:10px solid transparent;
  border-bottom:25px solid #797979;
  width:0;
  height:0;
  p {
    width: 50px;
    text-align: center;
    font-size: 20px;
    position: absolute;
    top: -25px;
    left: -25px;
  }
}
.yz_bottom {
  position: absolute;
  bottom: -18px;
  left: -8px;
  border-left:10px solid transparent;
  border-right:10px solid transparent;
  border-top:25px solid #797979;
  width:0;
  height:0;
  p {
    width: 60px;
    text-align: center;
    position: absolute;
    left: -30px;
    font-size: 20px;
  }
}
.xz {
  width: 82%;
  height: 3px;
  position: absolute;
  top: calc(52% - 3px);
  background-color: #797979;
}
.xz_left {
  position: absolute;
  bottom: -8px;
  left: -10px;
  border-bottom:10px solid transparent;
  border-top:10px solid transparent;
  border-right:25px solid #797979;
  width:0;
  height:0;
  p {
    position: absolute;
    font-size: 20px;
    left: -25px;
    top: -40px;
  }
}
.xz_right {
  position: absolute;
  bottom: -8px;
  right: -10px;
  border-bottom:10px solid transparent;
  border-top:10px solid transparent;
  border-left:25px solid #797979;
  width:0;
  height:0;
  p {
    position: absolute;
    font-size: 20px;
    left: 3px;
    top: -28px;
  }
}
</style> 