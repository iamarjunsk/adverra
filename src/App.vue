<script setup>
import { ref } from "vue";
import SignForm from "./components/SignForm.vue";

const selectedOptions = ref([]);
const openSuccess = ref(false)
const options = ref([
  { value: "option1", label: "Option 1" },
  { value: "option2", label: "Option 2" },
  { value: "option3", label: "Option 3" },
  // Add more options as needed
]);

const handleOptionChange = () => {
  // Handle option change if needed
};
const openDialog = () => {
  debugger
  openSuccess.value = true;
};

const closeDialog = () => {
  openSuccess.value = false;
};

</script>

<template>
  <div class="login-sec">
    <div class="left-side"><img src="@/assets/back.png" alt="" /></div>
    <div class="right-side">
      <div class="sec-wrap">
        <div class="title-logo">
          <img src="@/assets/logo.svg" class="logo" alt="" />
        </div>
        <div class="welcome-wrap">
          <h4>Welcome</h4>
          <p>Please enter the details provided by your clinic</p>
        </div>
        <SignForm :opendialog="openDialog"/>
      </div>
    </div>
  </div>
  <dialog class="successDialog_" :open="openSuccess" @close="closeDialog">
    <div class="active">
      <div>
        <img src="@/assets/logo.svg" alt="" />
      </div>
      <p>You're suceessfully logged in</p>
      <div class="closeSec">
        <button id="closeSuccess" @click="closeDialog()">Close</button>
      </div>

    </div>
  </dialog>
</template>

<style lang="scss">
@import url("./assets/style.scss");

.dropdown {
  position: relative;
  display: inline-block;
}

.selected {
  border: 1px solid #ccc;
  padding: 5px;
  cursor: pointer;
}

.options {
  position: absolute;
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 5px;
  max-height: 200px;
  overflow-y: auto;
  z-index: 1000;
}

.options div {
  margin-bottom: 5px;
}

input[type="checkbox"] {
  margin-right: 5px;
}
</style>
