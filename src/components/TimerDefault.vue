<template>
    <div class="timer">
        <div :class="this.isActive ? `timer__top_active` : ``" class="timer__top">
            <span v-if="this.hours" class="timer__text">
                {{ String(this.hours).padStart(2, '0')}}:
            </span>
            <span v-if="this.minutes" class="timer__text">
                {{ String(this.minutes).padStart(2, '0') }}:
            </span>
            <span class="timer__text">{{ String(this.seconds).padStart(2, '0') }}</span>
        </div>
        <div class="timer__buttons">
            <button @click="playPause" class="timer__btn timer__btn_play">
                <svg v-if="!this.isActive" width="17" height="20" viewBox="0 0 17 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E"/>
                </svg>
                <svg v-if="this.isActive" width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="7" width="3" height="20" :fill="this.isActive ? `#fff` : `#9E9E9E`" />
                    <rect width="3" height="20" :fill="this.isActive ? `#fff` : `#9E9E9E`"/>
                </svg>
            </button>
            <button @click="stop" class="timer__btn">
                <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect width="20" height="20" :fill="this.isActive ? `#fff` : `#9E9E9E`"/>
                </svg>
            </button>
        </div>
    </div>
</template>

<script>

export default {
  name: "TimerDefault",
  props: ["timer"],
  data() {
    return {
      ...this.timer,
    };
  },
  methods: {
    playPause() {
      this.isActive = !this.isActive;
      if (!this.isActive) {
        clearInterval(this.interval);
      } else {
        this.interval = setInterval(this.tick, 1000);
      }
    },
    stop() {
      clearInterval(this.interval);
      this.$emit("resetTimer", this.id);
    },
    tick() {
      this.seconds += 1;
      if (this.seconds > 59) {
        this.seconds = 0;
        this.minutes += 1;
      }
      if (this.minutes > 59) {
        this.hours += 1;
        this.minutes = 0;
      }
    },
  },
};

</script>

<style>
.timer {
  width: 225px;
  height: 120px;
  background: #696969;
  display: flex;
  flex-direction: column;
}
.timer__top {
 align-items: center;
 justify-content: center;
 display: flex;
 height: 50%;
}
.timer__top_active {
 color: #fff;
}
.timer__buttons {
 gap: 50px;
 border-top: 1px solid #9E9E9E;
 align-items: center;
 justify-content: center;
 display: flex;
 height: 50%;
}
.timer__btn {
  background: none;
  width: 20px;
}
.timer__text {
    font-size: 18px;
}
</style>
