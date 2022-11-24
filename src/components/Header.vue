<script setup>
import { computed } from "vue";
const props = defineProps({
  place: "",
  people: "",
});

const emit = defineEmits(["searchOn"])

const classPlace = computed(() => {
  if (props.place == "Add location") {
    return "button-element font-s-400 unpicked"
  } else{
    return "button-element font-s-400"
  }
})
const classPeople = computed(() => {
  if (props.people == "Add guests") {
    return "button-element font-s-400 unpicked"
  } else{
    return "button-element font-s-400"
  }
})

function turnSearchOn() {
  emit("searchOn")
}

</script>

<template>
  <div class="header">
    <div class="logo">
      <img src="../assets/logo.png" alt="windbnb" />
    </div>
    <button class="header-button" @click="turnSearchOn()">
      <div :class="classPlace">{{ props.place }}</div>
      <div :class="classPeople">{{ props.people }}</div>
      <div class="button-element"><img src="../assets/search.svg" alt="&#128269" class="icon"></div>
    </button>
  </div>
</template>

<style scoped>
.header{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  height: 45px;
}
.logo{
  height: 100%;
}
.header-button{
  width: 30%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  border: none;
  border-radius: 16px;
  background: none;
  box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
}

.header-button:hover{
  cursor:pointer;

}

.button-element{
  display: flex;
  justify-content: center;
  text-align: center;
}
.unpicked{
  color: #BDBDBD;
}
.icon{
  height:17px;
}
</style>
