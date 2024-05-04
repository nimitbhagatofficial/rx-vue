<template>
  <div class="container mt-1">
    <div class="row">
      <div class="col-md-6">
        <img :src="image" class="img-fluid" alt="Product Image" />
      </div>
      <StepOne ref="sOne" :selectedModal="selectedModal" :selectedColor="selectedColor" v-show="active1 == true"
        @model-changed="modelChanged" />

      <StepTwo ref="sTwo" :selectedModal="selectedModal" :selectedColor="selectedColor" v-show="active2 == true"
        @config-changed="configChanged" />

      <StepThree ref="sThree" :selectedModal="selectedModal" :selectedColor="selectedColor"
        :selectedConfig="selectedConfig" v-show="active3 == true" />
    </div>
  </div>
</template>

<script>
import StepOne from '../components/StepOne.vue'
import StepTwo from '../components/StepTwo.vue'
import StepThree from '../components/StepThree.vue'
export default {
  props: ["active1", "active2", "active3"],
  components: { StepOne, StepTwo, StepThree },
  data() {
    return {
      image: '',
      selectedModal: false,
      selectedColor: false,
      selectedConfig: false,
    }
  },
  computed: {
  },
  methods: {
    modelChanged(modal, color,) {
      this.selectedModal = modal;
      this.selectedColor = color;
      this.$refs.sTwo.getConfigurations();
      this.image = "https://interstate21.com/tesla-app/images/" + modal.code + '/' + color.code + '.jpg';
    },
    configChanged(selectedConfig) {
      
      this.selectedConfig = selectedConfig;
    }
  }
}
</script>

<style>
.colours {
  height: 25px;
  width: 25px;
  box-shadow: 1px 1px 2px 1px;
}

.colours.active {
  border: 3px solid;
}
</style>
