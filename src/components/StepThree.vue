<template>
    <div class="col-md-6">
        <h1>Summary</h1>
        <table border="1">
            <tr>
                <td colspan="2">
                    <h2>
                        {{ selectedModal.description }}
                    </h2>
                </td>
            </tr>
            <tr>
                <td>
                    {{ selectedConfig.description }}
                    <br>
                    Speed - {{ selectedConfig.speed }}
                    <br>
                    Range - {{ selectedConfig.range }}
                    <br>
                    Yoke - {{ configurations.yoke ? 'Yes' : 'No' }}
                    <br>
                    Toe - {{ configurations.towHitch ? 'Yes' : 'No' }}
                </td>
                <td>${{ selectedConfig.price }}</td>
            </tr>
            <tr>
                <td>Color - {{ selectedColor.description }}</td>
                <td>${{ selectedColor.price }}</td>
            </tr>
            <tr>
                <td>Total</td>
                <td>${{ selectedColor.price + selectedConfig.price }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    props: ["selectedModal", "selectedColor", "selectedConfig", "configurations"],
    data() {
        return {}
    },
    computed: {},
    methods: {},
}
</script>