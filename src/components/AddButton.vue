<template>
   <div class="add" >
      <button @click="addTimer" class="add__btn">+</button>
    </div>
</template>

<script>
export default {
  name: "AddButton",
  methods: {
    addTimer() {
      this.$emit("add-timer");
    },
  },
};

</script>

<style>
.add {
  width: 225px;
  height: 120px;
  background: #696969;
  display: flex;
}
.add__btn {
  font-size: 30px;
  background: none;
  color: #9E9E9E;
  align-items: center;
  margin: 0 auto;
}
</style>
