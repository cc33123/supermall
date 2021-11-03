<template>
  <div class="recommends">
    <div v-for="item in recommends" class="recommends-item">
      <a :href="item.link">
        <img :src="item.image">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
  export default {
    name: "HomeRecommendView",
    props:{
      recommends:{
        type:Array,
        default() {
          return [];
        }
      }
    }
  }
</script>

<style scoped>
.recommends{
  display: flex;
  text-align: center;
  font-size: 12px;
  padding: 10px 0 20px;
  border-bottom: 8px solid #eee;
}
.recommends-item{
  flex:1;

}
.recommends-item img{
  width: 65px;
  height: 65px;
  margin-bottom: 10px;
}
</style>
