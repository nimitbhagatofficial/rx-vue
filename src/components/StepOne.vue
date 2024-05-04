<template>
  <div class="col-md-6">
    <div class="form-group">
      <label for=""></label>
      <div v-for="(option, index) in options">
      </div>
      <select class="form-control" v-model="carModel" @change="carModalChanged()">
        <option v-for="(option, index) in options" :value="index">
          {{ option.code }}
        </option>
      </select>
    </div>

    <h2>{{ selectedModel.description }}</h2>

    <div class="d-flex">
      <div v-for="(color, index) in selectedModel.colors" :key="index" class="rounded-circle colours mr-5"
        :style="{ 'background-color': color.code }" @click="colorChanged(index)"
        :class="selectColor.code == color.code ? 'active' : ''">
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      carModel: 0,
      selectColor: '',
      selectedModel: false,
      options: [],
    }
  },
  async created() {
    try {
      if (!this.selectedModel) {
        const response = await axios.get('/modal', {
          headers: {
            Accept: "application/json"
          },
        }).then((result) => {
          this.options = result.data;
          this.selectedModel = this.options[0];
          this.selectColor = this.selectedModel.colors[0].code;
          this.ModalName = this.selectedModel.description;
          this.carModalChanged();
        });
      }

    } catch (err) {
      console.log(err);
    }
  },
  computed: {
    price() {
      return 0
    }
  },
  methods: {
    carModalChanged() {
      this.selectedModel = this.options[this.carModel];
      this.selectColor = this.selectedModel.colors[0]
      this.$emit('model-changed', this.selectedModel, this.selectedModel.colors[0]);
    },
    colorChanged(colorIndex) {
      this.selectColor = this.selectedModel.colors[colorIndex];
      this.$emit('model-changed', this.selectedModel, this.selectColor, false);
    }
  },
}
</script>
