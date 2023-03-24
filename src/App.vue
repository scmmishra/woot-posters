<script lang="ts" setup>
import { ref } from "vue";
import InputWrapper from "./components/InputWrapper.vue";
import Checkmark from "./components/Checkmark.vue";

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

const selectedLayout = ref("left");
const selectedMesh = ref(meshOptions[0]);
</script>
<template>
  <div class="min-h-screen p-5 gap-8 grid grid-cols-3 bg-gray-100">
    <section class="bg-white p-5 rounded-md space-y-5">
      <h1 class="text-xl font-black uppercase tracking-tight">
        Chatwoot Posters
      </h1>
      <InputWrapper title="Heading">
        <input
          type="text"
          placeholder="A heading, two to three words"
          class="border-2 border-black rounded-md w-full text-lg px-4 py-2"
        />
      </InputWrapper>
      <InputWrapper title="Body">
        <textarea
          placeholder="A one or two liner description for this poster"
          class="border-2 border-black rounded-md w-full text-lg px-4 py-2"
        />
      </InputWrapper>
      <InputWrapper title="Layout">
        <div class="grid grid-cols-3 gap-2">
          <button
            @click="selectedLayout = 'left'"
            class="rounded-md shadow-lg transform duration-200 transition-transform hover:shadow-xl hover:-translate-y-px overflow-hidden relative"
          >
            <div class="h-[72px] bg-gray-200 grid grid-cols-2 gap-1 p-2">
              <div class="space-y-1 pt-1">
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
              </div>
              <div class="bg-gray-300 rounded-md w-full h-full"></div>
            </div>
            <div v-if="selectedLayout === 'left'">
              <Checkmark />
            </div>
          </button>
          <button
            @click="selectedLayout = 'right'"
            class="rounded-md shadow-lg transform duration-200 transition-transform hover:shadow-xl hover:-translate-y-px overflow-hidden relative"
          >
            <div class="h-[72px] bg-gray-200 grid grid-cols-2 gap-1 p-2">
              <div class="bg-gray-300 rounded-md w-full h-full"></div>
              <div class="space-y-1 pt-1">
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
              </div>
            </div>
            <div v-if="selectedLayout === 'right'">
              <Checkmark />
            </div>
          </button>
          <button
            @click="selectedLayout = 'center'"
            class="rounded-md shadow-lg transform duration-200 transition-transform hover:shadow-xl hover:-translate-y-px overflow-hidden relative"
          >
            <div class="h-[72px] bg-gray-200 flex flex-col gap-2 p-2 pb-0">
              <div class="space-y-1 pt-1">
                <div class="bg-gray-300 rounded-md w-1/2 h-2 mx-auto"></div>
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
              </div>
              <div
                class="bg-gray-300 rounded-md w-5/6 mx-auto h-full rounded-b-none"
              ></div>
            </div>
            <div v-if="selectedLayout === 'center'">
              <Checkmark />
            </div>
          </button>
          <button
            @click="selectedLayout = 'right-break'"
            class="rounded-md shadow-lg transform duration-200 transition-transform hover:shadow-xl hover:-translate-y-px overflow-hidden relative"
          >
            <div class="h-[72px] bg-gray-200 flex flex-col gap-1 p-2 pb-0 pr-0">
              <div class="space-y-1 pt-1 pr-2">
                <div class="bg-gray-300 rounded-md w-1/2 h-2"></div>
                <div class="bg-gray-300 rounded-md w-full h-2"></div>
              </div>
              <div class="bg-gray-300 rounded-tl-md w-full h-full"></div>
            </div>
            <div v-if="selectedLayout === 'right-break'">
              <Checkmark />
            </div>
          </button>
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
  </div>
</template>
