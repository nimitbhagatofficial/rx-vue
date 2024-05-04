<template>
    <div class="col-md-6">

        <div class="form-group">
            <label for=""></label>
            <select class="form-control" v-model="config" @change="settingsChanged">
                <option v-for="(config, index) in configurations.configs" :value="index">
                    {{ config.description }} - ${{ config.price }}
                </option>
            </select>
        </div>

        <ul>
            <li>Color - {{ selectedColor.description }} - ${{ selectedColor.price }}</li>
            <li>
                Range/Speed - {{ selectedConfig.range }}/{{ selectedConfig.speed }} - ${{ selectedConfig.price }}
            </li>
            <li>Tow Hitch - {{ configurations.towHitch ? "YES" : "No" }}</li>
            <li>Yoke - {{ configurations.yoke ? "YES" : "No" }}</li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    props: ["selectedModal", "selectedColor"],
    data() {
        return {
            configurations: false,
            config: "",
            selectedConfig: {},
        }
    },
    computed: {},
    methods: {
        getConfigurations() {
            try {
                const response = axios.get('/modal/' + this.selectedModal.code, {
                    headers: {
                        Accept: "application/json"
                    },
                }).then((result) => {
                    this.config = 0;
                    this.configurations = result.data;
                    this.selectedConfig = this.configurations.configs[0];
                });
            } catch (err) {
                console.log(err);
            }
        },
        configChange() {
            this.$emit('config-changed', this.configurations, this.selectedConfig);
        },
        settingsChanged() {
            this.selectedConfig = this.configurations.configs[this.config];
            this.configChange();
        }
    },
}
</script>