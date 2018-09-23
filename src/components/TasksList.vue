<template>
    <div class="tasks-container">
        <h5>{{ title }}</h5>
        <b-list-group>
            <b-list-group-item
                v-for="(task, index) in taskList" 
                :key="index">
                {{ task.name }}
                    <b-button variant="outline-success" :size="'sm'"
                    type="button" 
                    @click="toggleTask(task)" 
                    v-if="!task.done">
                    Completar
                    </b-button>
                </b-list-group-item>
        </b-list-group>
    </div>
    
</template>

<script>
    export default {
        props: {
            title: {
                type: String,
                required: true
            },
            taskList: {
                type: Array,
                required: true
            }
        },
        data() {
            return {}
        },
        methods: {
            toggleTask(task) {
                this.$emit('complete', task);
            }
        }
    }
</script>
<style scoped>
.tasks-container {
    margin-top: 2rem;
}
</style>

