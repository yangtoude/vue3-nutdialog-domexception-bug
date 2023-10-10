<template>
  <main>
    <div v-if="showContent === true">
      <button
        style="margin-right: 10px;"
        @click="showDialog = true"
      >open dialog</button>
      <button
        @click="handleToAbout"
      >to about</button>
      <div>open console, when click "to about" will throw error</div>
      <!-- with teleport="#app" will throw error below -->
      <!-- runtime-dom.esm-bundler.js:10 Uncaught (in promise) DOMException: Failed to execute 'insertBefore' on 'Node': The node before which the new node is to be inserted is not a child of this node. -->
      <nut-dialog
        teleport="#app"
        title="Title"
        content="Content..."
        ok-text="ok"
        cancel-text="cancel"
        v-model:visible="showDialog"
        :close-on-click-overlay="false"
        @ok="showDialog = false"
      >
      </nut-dialog>
      <!-- without teleport="#app" works fine -->
      <!-- <nut-dialog
        title="Title"
        content="Content..."
        ok-text="ok"
        cancel-text="cancel"
        v-model:visible="showDialog"
        :close-on-click-overlay="false"
        @ok="showDialog = false"
      >
      </nut-dialog> -->
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router';

const showDialog = ref(false)
const showContent = ref<boolean|null>(null)

setTimeout(() => {
  showContent.value = true
}, 100)

const router = useRouter()
const handleToAbout = () => {
  router.push({
    path: '/about'
  })
}

</script>
