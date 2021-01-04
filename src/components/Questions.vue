<template>
  <div class="container">
    <div class="holder">
      <p>Question: {{ question }}</p>
      <p
        @click="$emit('actionFoo', 'a')"
        v-on:click="selectItem"
        class="changeColorArr"
      >
        a: {{ first }}
      </p>
      <p
        @click="$emit('actionFoo', 'b')"
        class="changeColorArr"
        v-on:click="selectItem"
      >
        b: {{ second }}
      </p>
      <p
        @click="$emit('actionFoo', 'c')"
        class="changeColorArr"
        v-on:click="selectItem"
      >
        c: {{ third }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Questions",
  props: {
    question: null,
    first: null,
    second: null,
    third: null,
  },
  methods: {
    selectItem(el) {
      const changeColorArr = document.querySelectorAll(".changeColorArr");
      changeColorArr.forEach((e) => {
        e.style.backgroundColor = "cornsilk";
      });
      if (el) {
        el.currentTarget.style.backgroundColor = "green";
      }
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

.holder {
  width: 500px;
}

p {
  padding: 10px;
  background-color: cornsilk;
  margin-bottom: 10px;
  cursor: pointer;
}
</style>
