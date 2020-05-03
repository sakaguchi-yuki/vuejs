<template>
  <div>
    <p>
      <img class="logo" src="../images/logo.jpg" alt="ロゴ">
      <span class="sample">チャット</span>
    </p>
    <form @submit="onSubmit">
      名前:<input v-model="$data.texta" type="text">
      テキスト:<input v-model="$data.textb" type="text">
      <button type="submit">送信</button>
    </form>
    <!-- <MyComponent :message="$data.message" /> -->
    <ul v-for="m in $data.message" :key="m.text">{{m.text}}</ul>
  </div>
</template>

<script>
import Vue from 'vue';
import socket from './utils/socket';

// components
import MyComponent from './components/MyComponent.vue';

export default Vue.extend({
  components: {
    MyComponent
  },
  data() {
    return {
      message: [{ text: 'サンプル太郎　テキストテキストテキスト' }],
      texta: '',
      textb: ''
    };
  },
  created() {
    socket.on('connect', () => {
      console.log('connected!');
    });

    socket.on('send', (a, b) => {
      console.log(`${a}`);
      this.$data.message.unshift(
        a
      );
    });
  },
  methods: {
    /**
     * Enterボタンを押したとき
     */
    onSubmit(e) {
      e.preventDefault();
      socket.emit('send', { text: `${this.$data.texta} ${this.$data.textb}` });
    }
  }
});
</script>

<style lang="scss" scoped>
.logo {
  width: 40px;
}

.sample {
  color: $black;
}
</style>
