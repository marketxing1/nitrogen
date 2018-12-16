<template>
  <div>
    <div class="message-header" v-if="showHeader">
      <div class="message-header-time">{{dayAgo}}</div>
      <div class="message-header-close">
        <i class="fa fa-times-circle" aria-hidden="true"></i>
      </div>
    </div>
    <notice class="message-notice">
      <template slot="notice-header-icon">
        <img class="notice-header-icon-img" :src="icon"/>
      </template>
      <template slot="notice-header-title">
        <span class="message-tip">{{tip}}</span>
        <span class="message-time">
          <span class="message-time-text">{{timeAgo}}</span>
          <i class="fa fa-times-circle message-time-close" aria-hidden="true"></i>
        </span>
      </template>
      <template slot="notice-body">
        <div class="message-item">
          <div class="message-title" v-html="title"></div>
          <div class="message-body" v-html="body"></div>
        </div>
      </template>
    </notice>
  </div>
</template>

<script>
  import Notice from './Notice';
  import Calendar from './Calendar';

  export default {
    name: "MessageNotice",
    components: {
      Notice
    },
    props: {
      showHeader: Boolean,
      icon: String,
      tip: String,
      title: String,
      body: String,
      time: Date
    },
    computed: {
      timeAgo: function () {
        return Calendar.timeAgo(this.time);
      },
      dayAgo: function () {
        return Calendar.dayAgo(this.time);
      }

    }
  }
</script>

<style scoped>

  .message-header, .message-tip {
    color: #4e4e4e;
  }

  .message-header-time {
    font-size: 20px;
    display: inline-block;
    padding: 5px 20px 0 20px;
    width: 110px;
  }

  .message-header-close {
    display: inline-block;
    width: 140px;
    text-align: right;
  }

  .message-header-close i {
    margin-right: 8px;
    font-size: 15px;
  }

  .message-item {
    padding: 10px 20px;
  }

  .message-item .message-title {
    font-weight: 600;
    font-size: 15px;
  }

  .message-item .message-body {
    font-size: 10px;
    color: #4e4e4e;
  }

  .message-time {
    float: right;
    margin-right: 10px;
    line-height: 22px;
    color: #4e4e4e;
  }

  .message-notice:hover .message-time-text, .message-notice .message-time-close {
    display: none;
  }

  .message-notice:hover .message-time-close, .message-notice .message-time-text {
    display: unset;
  }

  .message-time-close {
    font-size: 15px;
  }

</style>