<script setup>
import { reactive, computed } from "vue";
const props = defineProps({
  places: {
    type: Array,
  },
});

const local = reactive({
  chosenPlace: "Add location",
  classLocation: "font-s-400 unpicked",

  classGuests: "font-s-400 unpicked",

  adultNumber: 0,
  childrenNumber: 0,
});

const emit = defineEmits(["search"])

function onSearch() {
  const result = {
    place : local.chosenPlace,
    people : chosenGuests.value
  }
  emit ("search", result)
}

const chosenGuests = computed(() => {
  if (local.adultNumber + local.childrenNumber == 1) {
    local.classGuests = "font-s-400";
    const a = String(local.adultNumber + local.childrenNumber) + " guest";
    return a;
  } else if (local.adultNumber + local.childrenNumber >= 1) {
    local.classGuests = "font-s-400";
    const a = String(local.adultNumber + local.childrenNumber) + " guests";
    return a;
  } else {
    local.classGuests = "font-s-400 unpicked";
    return "Add guests";
  }
});

function clearLocation() {
  local.chosenPlace = "Add location";
  local.classLocation = "font-s-400 unpicked";
}

function pickLocation(location) {
  local.chosenPlace = location;
  local.classLocation = "font-s-400";
}

function addAdult() {
  local.adultNumber += 1;
}
function removeAdult() {
  if (local.adultNumber != 0) {
    local.adultNumber -= 1;
  }
}
function addChildren() {
  local.childrenNumber += 1;
}
function removeChildren() {
  if (local.childrenNumber != 0) {
    local.childrenNumber -= 1;
  }
}
</script>
<template>
  <div>
    <div class="search">
      <div class="location">
        <div class="location_picked">
          <div class="font-s-800">LOCATION</div>
          <div :class="local.classLocation">
            {{ local.chosenPlace }}
          </div>
        </div>
        <div class="location_pick-block">
          <div v-for="element in props.places">
            <button
              @click="pickLocation(element)"
              class="location_pick font-s-400"
            >
              <img
                src="../assets/location.png"
                alt=""
                class="location_pick-img"
              />{{ element }}
            </button>
          </div>
          <button @click="clearLocation()" class="location_pick font-s-400">Clear location
          </button>
        </div>
      </div>
      <div class="guests">
        <div class="guests_picked">
          <div class="font-s-800">GUESTS</div>
          <div :class="local.classGuests">
            {{ chosenGuests }}
          </div>
        </div>
        <div class="guest_pick">
          <div class="guest_pick_elem">
            <div class="guests_pick_intro">
              <div class="guests_pick_intro-1 font-s-700">Adults</div>
              <div class="guests_pick_intro-2 font-s-400">Ages 13 or above</div>
            </div>
            <div class="guest_pick_man">
              <button @click="removeAdult()" class="guest_button">-</button>
              <div>{{ local.adultNumber }}</div>
              <button @click="addAdult()" class="guest_button">+</button>
            </div>
          </div>
          <div class="guest_pick_elem">
            <div class="guests_pick_intro">
              <div class="guests_pick_intro-1 font-s-700">Children</div>
              <div class="guests_pick_intro-2 font-s-400">Ages 2-12</div>
            </div>
            <div class="guest_pick_man">
              <button @click="removeChildren()" class="guest_button">-</button>
              <div>{{ local.childrenNumber }}</div>
              <button @click="addChildren()" class="guest_button">+</button>
            </div>
          </div>
        </div>
      </div>
      <button class="search_field" @click="onSearch">
        
        <img src="../assets/search.svg" alt="&#128269" class="search_icon">
        <div class="font-s-700">
          Search
        </div>
      </button>
    </div>
  </div>
</template>
<style scoped>
.search {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.search_field{
  display:flex;
  flex-direction: row;
  justify-content:space-between;
  align-items: center;
  gap: 5px;
  background-color: #EB5757;
  color: white;
  border: none;
  border-radius: 16px;
  height: 62px;
  padding: 12px 25px 12px 25px;
}
.search_field:hover{
  cursor: pointer;
}
.search_icon{
  height: 17px;
}

.location {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.location_picked {
  display: flex;
  flex-direction: column;
  box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  padding-top: 12px;
  padding-bottom: 10px;
  padding-left: 20px;
}
.location_pick-block {
  margin-top: 40px;
  gap: 30px;
}
.location_pick {
  background: none;
  border: none;
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 10px 20px 10px 20px;
  margin-bottom: 20px;
  height: 100%;
}
.location_pick:hover {
  cursor: pointer;
}
.location_pick-img {
  height: 20px;
}

.unpicked {
  color: #bdbdbd;
}

.guests {
  display: flex;
  flex-direction: column;
  width:100%;
}
.guests_picked {
  display: flex;
  flex-direction: column;
  box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  padding-top: 12px;
  padding-bottom: 10px;
  padding-left: 20px;
}
.guests_pick_intro {
  font-size: 14px;
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}
.guests_pick_intro-1 {
  color: #333333;
}
.guests_pick_intro-2 {
  color: #bdbdbd;
}
.guest_pick_man {
  display: flex;
  flex-direction: row;
  gap: 15px;
}
.guest_pick {
  margin-top: 50px;
  padding-left: 20px;
}
.guest_pick_elem {
  margin-bottom: 50px;
}
.guest_button {
  background-color: white;
  border-radius: 4px;
  border-color: #828282;
  border: width 1px;
  shadow: none;
}
</style>
