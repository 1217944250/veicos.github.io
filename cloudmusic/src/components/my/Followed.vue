<template>
  <div>
    <van-nav-bar
      title="您的粉丝"
      left-text="返回"
      left-arrow
      @click-left="$router.push('/my')"
    />
  </div>
  <van-list>
    <van-cell
      v-for="item in list"
      :key="item"
      :title="item.nickname"
    ></van-cell>
  </van-list>
</template>
<script>
import { getUserFolloweds } from "@/request/api/my.js";
export default {
  template: {},
  data() {
    return {
      user: {},
      list: [],
    };
  },
  async created() {
    try {
      //从本地获取userDetail信息
      let tempUser = JSON.parse(localStorage.getItem("user"));
      if (tempUser != null) {
        this.user = tempUser;
        let followed = await getUserFolloweds(this.user.profile.userId);
        this.list = followed.data.followeds;
        // console.log(this.list);
        console.log(followed);
      }
      //   console.log(tempUser);
    } catch (error) {
      console.error("获取本地user出错");
    }
  },
  methods: {},
};
</script>
