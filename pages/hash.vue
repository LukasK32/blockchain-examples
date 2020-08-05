<template>
  <div>
    <h1>Cryptographic hash function</h1>
    <div class="block">
      <div class="form-group">
        <label for="data">Data</label>
        <textarea id="data" v-model="value" rows="3" />
      </div>
      <div class="form-group">
        <label for="hash">Hash</label>
        <input id="hash" type="text" :value="hash" disabled>
      </div>
    </div>
  </div>
</template>

<script>
import { sha256 } from 'js-sha256';

export default {
  data: () => ({
    value: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
  }),
  computed: {
    hash () {
      return sha256(this.value);
    }
  }
};
</script>
