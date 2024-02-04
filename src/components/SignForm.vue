<template>
  <form @submit="(event) => handleFormSubmit(event)">
    <div class="inp-wrap">
      <label for="">Enter your email</label>
      <div class="input-style text-inp">
        <input v-model="formValue.email" />
      </div>
    </div>
    <div class="inp-wrap">
      <label for="">Enter your password</label>
      <div class="input-style text-inp">
        <input v-model="formValue.password" />
      </div>
    </div>
    <div class="inp-wrap">
      <label for="">Select your language</label>
      <div class="select-wrap">
        <div class="input-style select-inp" @click="toggleDropdown">
          <p>
            {{
              formValue.languages.length ? selectedLangages : "Choose languages"
            }}
          </p>
          <img
            src="@/assets/arrow-down.svg"
            :class="showDropdown ? 'img-up' : ''"
            alt=""
          />
        </div>
        <div class="options" v-show="showDropdown">
          <div v-for="language in languages" class="option">
            <input
              type="checkbox"
              :value="language"
              v-model="formValue.languages"
              id=""
            />
            <p>{{ language[0].toUpperCase() + language.substring(1) }}</p>
          </div>
        </div>
      </div>
    </div>

    <div class="sub-wrap">
      <button
        class="sub-btn"
        :disabled="!readyForm"
        :class="!readyForm ? 'low-opacity' : ''"
      >
        Get Started
      </button>
    </div>
  </form>
</template>

<script setup>
import { onMounted, ref, watch } from "vue";

// const {openSuccess} = props
const props = defineProps(['opendialog'])

import { isValidEmail, isValidPassword } from "./Validations.vue";
const formValue = ref({
  email: "",
  password: "",
  languages: ["english"],
});
console.log({ isValidEmail });

const showDropdown = ref(false);

const languages = ["english", "kannada", "malayalam", "telugu", "tamil"];
const toggleDropdown = () => {
  showDropdown.value = !showDropdown.value;
};

const selectedLangages = ref("");

const readyForm = ref(false);

watch(
  () => formValue.value.languages,
  (newValue, oldValue) => {
    GenetateSelectedLangText(newValue);
  }
);

watch(formValue.value, (newValue, oldValue) => {
  if (
    isValidEmail(newValue.email) &&
    isValidPassword(newValue.password) &&
    newValue.languages.length
  ) {
    readyForm.value = true;
  } else {
    readyForm.value = false;
  }
});

function GenetateSelectedLangText(newValue) {
  selectedLangages.value = "";
  newValue.forEach((e, i) => {
    selectedLangages.value += `${e[0].toUpperCase()}${e.substring(1)}${
      newValue.length !== i + 1 ? "," : ""
    } `;
  });
}

onMounted(() => {
  GenetateSelectedLangText(formValue.value.languages);
});

document.addEventListener("click", (event) => {
  const dropdown = document.querySelector(".select-wrap");
  if (dropdown && !dropdown.contains(event.target)) {
    showDropdown.value = false;
  }
});

function handleFormSubmit(e) {
  e.preventDefault();
  props.opendialog()
//   document.querySelector('#successDialog').showModal()
}
</script>
