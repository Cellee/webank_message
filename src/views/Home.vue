<template>
  <div class="home">
    <div class="bg-white">
      <van-cell-group>
        <van-cell title="文章标题文章标题文章标题文章标题文章标题文章标题文章标题文章标题文章标题文章标题文章标题" class="title" />
      </van-cell-group>

      <van-cell-group>
        <van-field
          v-model="message"
          label-width="0"
          rows="1"
          autosize
          label
          @input="inpbackups"
          type="textarea"
          placeholder="请输入留言"
        />
        <div class="p30">
          <van-icon name="smile-o" @click="onshow" />
        </div>
      </van-cell-group>

      <div class="emoji-box" v-if="show">
        <span class="cut" @click="onshow">收起</span>
        <VEmojiPicker :pack="pack" @select="selectEmoji" />
      </div>

      <div class="refer">
        <van-button
          :loading="loading"
          type="primary"
          loading-text="加载中..."
          @click="sushow = true"
        >留言</van-button>
      </div>
    </div>

    <!-- 留言信息 -->
    <div class="info">
      <div class="top">精选留言</div>

      <!-- 单一一个 -->
      <div class="list">
        <!-- 头像 -->
        <van-image class="head" round fit="cover" src="https://img.yzcdn.cn/vant/cat.jpeg" />

        <div class="main">
          <!-- 用户留言内容 -->
          <div class="user">
            <!-- 用户名和点赞 -->
            <div class="netname">
              <li>
                <!-- 用户名会超一定宽度 -->
                <span>某个用户</span>
                <span class="roof">置顶</span>
              </li>
              <div class="give">
                <van-icon name="good-job-o" />
                <span>80</span>
              </div>
            </div>
            <!-- 留言内容 -->
            <div
              class="say"
            >一叶扁舟轻帆卷。暂泊楚江南岸。孤城暮角，引胡笳怨。水茫茫，平沙雁、旋惊散。烟敛寒林簇，画屏展。天际遥山小，黛眉浅。旧赏轻抛，到此成游宦。觉客程劳，年光晚。异乡风物，忍萧索、当愁眼。帝城赊，秦楼阻，旅魂乱。芳草连空阔，残照满。佳人无消息，断云远。</div>

            <!-- 作者回复 -->
            <div class="netname">
              <li class="reply">
                <span>作者</span>
              </li>
              <!-- 点赞  加 active  icon 去掉 -o  -->
              <div class="give active">
                <van-icon name="good-job" />
                <span>81</span>
              </div>
            </div>
            <!-- 回复内容 -->
            <div class="say">nice</div>
          </div>
        </div>
      </div>

      <!-- 单一一个 -->
      <div class="list">
        <!-- 头像 -->
        <van-image class="head" round fit="cover" src="https://img.yzcdn.cn/vant/cat.jpeg" />

        <div class="main">
          <!-- 用户留言内容 -->
          <div class="user">
            <!-- 用户名和点赞 -->
            <div class="netname">
              <li>
                <!-- 用户名会超一定宽度 -->
                <span>某个用户</span>
              </li>
              <div class="give">
                <van-icon name="good-job-o" />
                <span>80</span>
              </div>
            </div>
            <!-- 留言内容 -->
            <div
              class="say"
            >一叶扁舟轻帆卷。暂泊楚江南岸。孤城暮角，引胡笳怨。水茫茫，平沙雁、旋惊散。烟敛寒林簇，画屏展。天际遥山小，黛眉浅。旧赏轻抛，到此成游宦。觉客程劳，年光晚。异乡风物，忍萧索、当愁眼。帝城赊，秦楼阻，旅魂乱。芳草连空阔，残照满。佳人无消息，断云远。</div>
          </div>
        </div>
      </div>
    </div>

    <!-- 留言成功 -->
    <van-popup v-model="sushow" class="success">
      <img alt="wx-phone" src="../assets/success.jpg" />
      <div class="tip">
        <li>留言成功</li>
        <p>留言通过审核后将对所有人可见</p>
        <p>精彩的留言会置顶哦~</p>
      </div>
      <div class="ok">
        <van-button round block type="info" @click="sushow = false">返回</van-button>
      </div>
    </van-popup>
  </div>
</template>

<script>
// @ is an alias to /src
import Vue from "vue";
import { Button, Cell, CellGroup, Field, Icon, Image, Popup } from "vant";

Vue.use(Button)
  .use(Cell)
  .use(CellGroup)
  .use(Field)
  .use(Icon)
  .use(Image)
  .use(Popup);

import VEmojiPicker from "v-emoji-picker";
import packData from "v-emoji-picker/data/emojis.json";

export default {
  name: "home",
  components: {
    VEmojiPicker
  },
  Props: {
    pack: { type: Array, required: true },
    labelSearch: { type: String, default: "Pesquisar..." },
    showCategory: { type: Boolean, default: true },
    emojisByRow: { type: Number, default: 5 }
  },
  data() {
    return {
      pack: packData,
      message: "", // 表情字符和留言内容

      backups: "", // 储存表情数组和留言内容
      show: false,
      loading: false,
      sushow: false
    };
  },
  methods: {
    selectEmoji(emoji) {
      console.log(emoji);
      this.message = this.message + emoji.emoji;
    },

    onshow() {
      this.show = !this.show;
    },

    inpbackups(val) {
      console.log(val);
    }
  }
};
</script>

<style lang="less">
.home {
  min-height: 100vh;
  background: #f4f4f4;
}
.bg-white {
  background: #fff;
  .p30 {
    padding: 10px 30px 0;
    color: #b1b1b1;
  }
  .title {
    .van-cell__title {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
  }
  #EmojiPicker {
    width: 750px;
  }
  #InputSearch {
    display: none !important;
  }
  .van-cell:not(:last-child)::after {
    border-bottom: 0;
  }
  .emoji-box {
    position: relative;
    span.cut {
      vertical-align: middle;
      position: absolute;
      right: 28px;
      top: -56px;
      font-size: 28px;
      color: #409eff;
    }
  }
  .refer {
    padding: 35px 0;
    text-align: center;
  }
  .van-button {
    padding: 0 30px;
    height: 40px;
    line-height: 38px;
  }
}

// 留言内容
.info {
  padding: 28px;
  .top {
    color: #909090;
    font-size: 30px;
    padding-bottom: 28px;
  }

  .list {
    position: relative;
    padding-left: 142px;
    padding-bottom: 50px;
    // 头像
    .head {
      position: absolute;
      left: 0;
      top: 2px;
      img {
        width: 112px;
        height: 112px;
      }
    }

    // 留言内容
    .main {
      font-size: 30px;
      color: #333;
      // 用户
      .user {
        // 用户名
        .netname {
          position: relative;
          padding-bottom: 18px;
          li {
            list-style: none;
            color: #717171;
            span {
              display: inline-block;
              max-width: 380px;
              overflow: hidden;
              height: 34px;
              line-height: 34px;
              vertical-align: middle;
            }
            span.roof {
              margin-left: 6px;
              padding: 3px 10px 1px;
              text-align: center;
              background: #b5b5b5;
              color: #fff;
              font-size: 24px;
            }
            &.reply {
              position: relative;
              padding-left: 20px;
              &::after {
                content: "";
                position: absolute;
                left: 0;
                width: 5px;
                height: 80%;
                top: 12%;
                background: #52a442;
              }
            }
          }
          // 点赞
          .give {
            position: absolute;
            right: 0;
            top: 0;
            i {
              font-size: 30px;
              vertical-align: middle;
            }
            span {
              vertical-align: middle;
            }
            &.active {
              color: #409eff;
            }
          }
        }

        .say {
          line-height: 48px;
          padding-bottom: 20px;
        }
      }
    }
  }
}

// 提交
.success {
  border-radius: 15px;
  img {
    width: 690px;
    display: block;
  }
  .tip {
    padding: 40px 0 20px;
    text-align: center;
    li {
      list-style: none;
      font-size: 40px;
      color: #000;
      margin-bottom: 15px;
    }
    p {
      margin: 0;
      font-size: 28px;
      color: #666;
      margin-bottom: 15px;
    }
  }
  .ok {
    padding: 0 30px 30px;
  }
}
</style>
