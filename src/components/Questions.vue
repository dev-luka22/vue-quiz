<template>
  <div class="container">
    <div class="holder">
      <p class="holder-question">{{ question }}</p>
      <p
        @click="$emit('actionFoo', 'a')"
        v-on:click="selectItem"
        class="changeColorArr"
      >
        {{ first }}
      </p>
      <p
        @click="$emit('actionFoo', 'b')"
        class="changeColorArr"
        v-on:click="selectItem"
      >
        {{ second }}
      </p>
      <p
        @click="$emit('actionFoo', 'c')"
        class="changeColorArr"
        v-on:click="selectItem"
      >
        {{ third }}
      </p>
      <p
        @click="$emit('actionFoo', 'd')"
        class="changeColorArr"
        v-on:click="selectItem"
      >
        {{ fourth }}
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
    fourth: null,
  },
  methods: {
    selectItem(el) {
      const changeColorArr = document.querySelectorAll(".changeColorArr");
      changeColorArr.forEach((e) => {
        e.style.backgroundColor = "#ffffff";
        e.style.color = "#000000";
      });
      if (el) {
        el.currentTarget.style.backgroundColor = "#01be01";
        el.currentTarget.style.color = "#ffffff";
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
}

.holder {
  width: 500px;
  position: relative;
  z-index: 3;
}

p {
  padding: 10px;
  background-color: #ffffff;
  margin-bottom: 15px;
  cursor: pointer;
  text-align: center;
  width: 500px;
  border-radius: 10px;
}

.holder-question {
  color: #f02121;
  font-weight: 700;
}

@media only screen and (max-width: 500px) {
  .holder {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  p {
    width: 400px;
  }
}

@media only screen and (max-width: 400px) {
  p {
    width: 310px;
  }
}
</style>
