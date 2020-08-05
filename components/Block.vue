<template>
  <div class="block" :class="{good: mining && block.verified, bad: mining && !block.verified}">
    <div class="form-group">
      <label for="previous-hash">Previous Hash</label>
      <input id="previous-hash" type="text" :value="block.previousHash" disabled>
    </div>
    <div v-if="mining" class="form-group">
      <label for="nonce">Nonce</label>
      <input id="nonce" v-model="nonce" type="number" min="0" :disabled="lock">
    </div>
    <div class="form-group">
      <label for="data">Data</label>
      <textarea id="data" v-model="value" rows="3" :disabled="lock" />
    </div>
    <div class="form-group">
      <label for="hash">Hash</label>
      <input id="hash" type="text" :value="block.hash" disabled>
    </div>
    <div class="form-group buttons">
      <button v-if="mining" type="button" class="button mine-block-button" :disabled="lock" @click="mine">
        Mine
      </button>
      <button type="button" class="button delete-block-button" :disabled="lock" @click="destroy">
        Destroy
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    mining: {
      type: Boolean,
      default: true
    },
    lock: {
      type: Boolean,
      default: true
    },
    block: {
      type: Object,
      default: () => ({
        previousHash: '0000000000000000000000000000000000000000000000000000000000000000',
        nonce: 0,
        value: '',
        verified: false
      })
    }
  },
  computed: {
    nonce: {
      get () {
        return this.block.nonce;
      },
      set (value) {
        this.$emit('changeNonce', parseInt(value));
      }
    },
    value: {
      get () {
        return this.block.value;
      },
      set (value) {
        this.$emit('changeValue', value);
      }
    }
  },
  methods: {
    destroy () {
      this.$emit('destroy');
    },
    mine () {
      this.$emit('mine');
    }
  }
};
</script>
