<script setup>
import { reactive } from "vue";
const props = defineProps({
  information: {},
});

const generation = reactive({
  line: "",
});

if (props.information.beds) {
  generation.line =
    props.information.type + " . " + props.information.beds + " beds";
} else {
  generation.line = props.information.type;
}
</script>
<template>
  <div class="card">
    <img :src="props.information.photo" alt="Фото" class="card-img"/>
    <div class="card_second-line">
      <div class="card_second-line_first-part">
        <div v-show="props.information.superHost" class="font-700 card_super-host">SUPER HOST &#160</div>
        <div class="font-500 card_description">{{ generation.line }}</div>
      </div>
      <div class="font-500 card_second-line_second-part">
          &#9733
          <div class="card_rate">{{props.information.rating}}</div>
      </div>
    </div>
    <div class="font-700">{{props.information.title}}</div>
  </div>
</template>
<style scoped>
.card{
  width: 100%;
}
.card-img{
  width:100%;
  height:350px;
  border-radius: 24px;
  object-fit: fill;
}
.card_second-line{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
.card_second-line_first-part{
  display: flex;
  flex-direction: row;
}
.card_super-host{
  border-style: solid;
  border-width: 1px;
  border-radius: 12px;
  padding: 7px;
  font-size: 12px;
  margin-right: 10px;
  height: 15px;
  display:flex;
  align-self:center;
  color: #4F4F4F;
}
.card_description{
  display:flex;
  align-self:center;
  margin-top: 20px;
  margin-bottom: 20px;
  color: #828282;
}

.card_second-line_second-part{
  display: flex;
  flex-direction: row;
  gap: 7px;
  color: red;
}
.card_rate{
  color: #4F4F4F;
  display: flex;
  align-self: center;
}
</style>
