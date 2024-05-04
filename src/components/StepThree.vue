<template>
    <div class="col-md-6">
        <h1>Summary</h1>
        <table>
            <tr>
                <td>{{ selectedConfig }}</td>
                <td></td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    props: ["selectedModal", "selectedColor", "selectedConfig"],
    data() {
        return {}
    },
    computed: {},
    methods: {},
}
</script>