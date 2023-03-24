<script lang="ts" setup>
import { ref } from "vue";
import InputWrapper from "./components/InputWrapper.vue";
import Checkmark from "./components/Checkmark.vue";
import Left from "./components/LayoutOptions/Left.vue";
import Right from "./components/LayoutOptions/Right.vue";
import Center from "./components/LayoutOptions/Center.vue";
import RightBreak from "./components/LayoutOptions/RightBreak.vue";
import Poster from "./components/Poster.vue";
import DownloadButton from "./components/DownloadButton.vue";

const meshOptions = [
  "mesh-bg-1.png",
  "mesh-bg-2.png",
  "mesh-bg-3.png",
  "mesh-bg-4.png",
  "mesh-bg-5.png",
  "mesh-bg-6.png",
  "mesh-bg-7.png",
  "mesh-bg-8.png",
];

const currentImage = ref<string | ArrayBuffer | null>("null");
const title = ref("Launching Heatmaps");
const body = ref(
  `This report provides a peek into the busiest hours of the day for a week, helping you identify patterns in customer conversations. So, you can account for your busiest and laziest hours.`
);
const selectedLayout = ref("left");
const selectedMesh = ref(meshOptions[0]);

function setImage() {
  const inputFile = document.getElementById("imageInput") as HTMLInputElement;
  if (inputFile.files) {
    const image = inputFile.files[0];
    const reader = new FileReader();

    reader.readAsDataURL(image);
    reader.onload = () => {
      currentImage.value = reader.result;
    };
  }
}
</script>
<template>
  <div class="min-h-screen p-5 gap-8 grid grid-cols-3 bg-gray-100">
    <section class="bg-white p-5 rounded-lg space-y-5">
      <h1 class="text-xl font-black uppercase tracking-tight">
        Chatwoot Posters
      </h1>
      <InputWrapper title="Heading">
        <input
          v-model="title"
          type="text"
          placeholder="A heading, two to three words"
          class="border-2 border-black rounded-md w-full text-lg px-4 py-2"
        />
      </InputWrapper>
      <InputWrapper title="Body">
        <textarea
          v-model="body"
          placeholder="A one or two liner description for this poster"
          class="border-2 border-black rounded-md w-full text-lg px-4 py-2"
        />
      </InputWrapper>
      <InputWrapper title="Layout">
        <div class="grid grid-cols-3 gap-2">
          <Left
            :selected="selectedLayout === 'left'"
            @select="selectedLayout = 'left'"
          />
          <Right
            :selected="selectedLayout === 'right'"
            @select="selectedLayout = 'right'"
          />
          <Center
            :selected="selectedLayout === 'center'"
            @select="selectedLayout = 'center'"
          />
          <RightBreak
            :selected="selectedLayout === 'right-break'"
            @select="selectedLayout = 'right-break'"
          />
        </div>
      </InputWrapper>
      <InputWrapper title="Select background">
        <div class="grid grid-cols-3 gap-2">
          <button
            v-for="mesh in meshOptions"
            @click="selectedMesh = mesh"
            class="rounded-md shadow-lg transform duration-200 transition-transform hover:shadow-xl hover:-translate-y-px overflow-hidden relative"
          >
            <img
              :src="`/mesh/${mesh}`"
              alt="mesh"
              :class="{
                'opacity-50': mesh === selectedMesh,
              }"
            />
            <div v-if="mesh === selectedMesh">
              <Checkmark />
            </div>
          </button>
        </div>
      </InputWrapper>
    </section>
    <section class="col-span-2 space-y-4">
      <Poster
        :title="title"
        :body="body"
        :image="currentImage"
        :layout="selectedLayout"
        :background="selectedMesh"
      />
      <div class="flex justify-between w-full">
        <div>
          <input
            class="relative m-0 block w-full min-w-0 flex-auto rounded border border-solid border-gray-300 bg-clip-padding py-[0.32rem] px-3 text-base font-normal text-black transition duration-300 ease-in-out file:-mx-3 file:-my-[0.32rem] file:overflow-hidden file:rounded-none file:border-0 file:border-solid file:border-inherit file:bg-gray-100 file:px-3 file:py-[0.32rem] file:text-black-700 file:transition file:duration-150 file:ease-in-out file:[margin-inline-end:0.75rem] file:[border-inline-end-width:1px] hover:file:bg-gray-200 focus:border-primary focus:text-gray-900 focus:shadow-[0_0_0_1px] focus:shadow-primary focus:outline-none"
            type="file"
            @change="setImage"
            id="imageInput"
            accept="image/*"
          />
        </div>
        <DownloadButton />
      </div>
    </section>
  </div>
</template>
