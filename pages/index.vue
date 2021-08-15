<template>
  <div>
    <div>
      <button class="btn btn-primary" @click="reload">reload</button>
    </div><br>
    <Video />
  </div>
</template>

<script>
import { defineComponent } from "@vue/composition-api";

export default defineComponent({
  name: "index",
  methods: {
    reload: function() {
      location.reload();
    }
  }
});
</script>
