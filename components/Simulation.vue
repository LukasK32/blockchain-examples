<template>
  <div>
    <div v-if="mining">
      <div class="inline-form-group">
        <label for="difficulty">Difficulty</label>
        <input
          id="difficulty"
          v-model="difficulty"
          type="number"
          min="1"
          max="64"
          :disabled="lock"
        >
      </div>
    </div>

    <Block
      v-for="(b, i) in blocks"
      :key="i"
      :block="b"
      :mining="mining"
      :lock="lock"
      @changeNonce="v => updateBlockNonce(i, v)"
      @changeValue="v => updateBlockValue(i, v)"
      @destroy="v => destroyBlock(i)"
      @mine="v => mineBlock(i)"
    />

    <button type="button" class="button add-block-button" :disabled="lock" @click="addBlock">
      Add block
    </button>
  </div>
</template>

<script>
import { sha256 } from 'js-sha256';

export default {
  props: {
    mining: {
      type: Boolean,
      default: true
    }
  },
  data: () => ({
    values: [
      {
        nonce: 0,
        value: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
      },
      {
        nonce: 0,
        value: 'Aenean suscipit at tellus ut blandit. Curabitur dolor lectus, congue eget leo ac, vestibulum pharetra risus.'
      }
    ],
    lock: false,
    difficulty: 1
  }),
  computed: {
    blocks () {
      const blocks = [];
      let previousHash = '0000000000000000000000000000000000000000000000000000000000000000';

      for (let i = 0; i < this.values.length; i++) {
        const block = {
          previousHash,
          ...this.values[i]
        };

        const hash = sha256(JSON.stringify(block));

        block.hash = hash;
        block.verified = this.verifyHash(hash);
        previousHash = hash;

        blocks.push(block);
      }

      return blocks;
    }
  },
  methods: {
    updateBlockNonce (n, value) {
      this.values[n].nonce = value;
    },
    updateBlockValue (n, value) {
      this.values[n].value = value;
    },
    destroyBlock (n) {
      this.values.splice(n, 1);
    },
    addBlock () {
      this.values.push({
        nonce: 0,
        value: ''
      });
    },
    mineBlock (n) {
      this.lock = true;

      setTimeout(() => {
        let previousHash = '0000000000000000000000000000000000000000000000000000000000000000';
        let block = {};

        for (let i = 0; i < this.values.length && i <= n; i++) {
          block = {
            previousHash,
            ...this.values[i]
          };

          const hash = sha256(JSON.stringify(block));

          block.hash = hash;
          previousHash = hash;
        }

        block.nonce = 0;
        delete block.hash;
        let hash = sha256(JSON.stringify(block));

        while (block.nonce < Number.MAX_VALUE && !this.verifyHash(hash)) {
          block.nonce++;
          hash = sha256(JSON.stringify(block));
        }

        this.values[n].nonce = block.nonce;
        this.lock = false;
      }, 1);
    },
    verifyHash (hash) {
      for (let i = 0; i < this.difficulty && i < hash.length; i++) {
        if (hash[i] !== '0') {
          return false;
        }
      }

      return true;
    }
  }
};
</script>

<style lang="scss">
.button {
  display: block;
  border: none;
  border-radius: 0;
  color: white;
  cursor: pointer;
  outline: none;
  font-size: 1em;
  padding: 0.3em 0.7em;
}

.add-block-button {
  font-size: 1.2em;
  padding: 0.4em 1em;
  margin: 0 auto;
  background-color: #3eca7a;

  &:hover {
    background-color: darken(#3eca7a, 7%);
  }

  &:disabled {
    background-color: darken(#3eca7a, 14%);
    cursor: initial;
  }
}

.delete-block-button {
  background-color: #ca3e47;

  &:hover {
    background-color: darken(#ca3e47, 7%);
  }

  &:disabled {
    background-color: darken(#ca3e47, 14%);
    cursor: initial;
  }
}

.mine-block-button {
  background-color: #3e7cca;

  &:hover {
    background-color: darken(#3e7cca, 7%);
  }

  &:disabled {
    background-color: darken(#3e7cca, 14%);
    cursor: initial;
  }
}

  label, input, textarea {
    display: block;
    width: 100%;
  }

  input, textarea {
    font-family: 'Roboto Mono', monospace;
    border-radius: 0;
    border: none;
    font-size: 0.9em;
    padding: 0.6em;
  }

  .inline-form-group {
    display: flex;
    flex-direction: row;
    justify-content:flex-end;
  align-content: stretch;
  align-items: center;

    input, label {
      display: inline-block;
      width: auto;
    }

    label {
      margin-right: 10px;
    }
  }
</style>
