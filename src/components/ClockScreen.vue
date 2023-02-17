<template>
  <div class="container">
    <div class="clock">
      <div class="date">
        <p>{{ year }}/{{ month }}/{{ day }}</p>
      </div>
      <div class="time">
        <p>
          {{ hours }}:{{ minutes }}<span class="seconds">:{{ seconds }}</span>
        </p>
      </div>
      <div class="button" v-on:click="showMessage()">
        <p>5秒後にアラームを設定</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      //現在の日時を保持
      date: new Date(),
    };
  },
  computed: {
    // 年
    year() {
      return this.date.getFullYear();
    },
    // 月
    month() {
      return this.date.getMonth() + 1;
    },
    // 日
    day() {
      return this.dateTimePadding(this.date.getDate());
    },
    // 時
    hours() {
      return this.dateTimePadding(this.date.getHours());
    },
    // 分
    minutes() {
      return this.dateTimePadding(this.date.getMinutes());
    },
    // 秒
    seconds() {
      return this.dateTimePadding(this.date.getSeconds());
    },
  },
  mounted() {
    // 現在の日時をセット
    this.setDate();
    // 1秒毎にsetDate()を実行
    setInterval(() => this.setDate(), 1000);
  },
  methods: {
    // 日時を二桁に変換
    dateTimePadding(num) {
      return ("0" + num).slice(-2);
    },
    setDate() {
      this.date = new Date();
    },
    showMessage() {
      setTimeout(() => {
        alert("5秒経過しました。");
      }, 5000);
    },
  },
};
</script>

<style scoped>
.container {
  height: 100%;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-content: center;
  background-color: #262626;
}
p {
  margin: 0px;
}
.clock {
  margin: 0 auto;
}
.date,
.time {
  font-weight: 700;
  color: #00ff01;
}
.date {
  font-size: 16px;
  text-align: right;
}
.time {
  font-size: 70px;
}
.seconds {
  font-size: 30px;
}
.button {
  border: 1px solid #fcfcfc;
  text-align: center;
  padding: 10px 0;
  color: #fcfcfc;
  cursor: pointer;
}
</style>
