<template>
    <div class="component">
        <h1>The User Component</h1>
        <p>I'm an awesome User! My name is {{ name }} am my age is {{ age }}</p>
        <button @click="changeName">Change my name</button>
        <input type="number" v-model.number="age">
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-6">
                <app-user-detail
                    :name="name"
                    @nameWasReset="name = $event"
                    :resetFn="resetName"
                    :userAge="age"
                ></app-user-detail>
            </div>
            <div class="col-xs-12 col-sm-6">
                <app-user-edit
                    :userAge="age"
                    @ageWasEdited="age = $event"
                ></app-user-edit>
            </div>
        </div>
    </div>
</template>

<script>
    import UserDetail from './UserDetail.vue';
    import UserEdit from './UserEdit.vue';
    import { eventBus } from '../main'

    export default {
        data() {
            return {
                name: 'Max',
                age: 27
            }
        },
        methods: {
            changeName() {
                this.name = 'Anna'
            },
            resetName() {
                this.name = 'Cristina'
            }
        },
        components: {
            appUserDetail: UserDetail,
            appUserEdit: UserEdit
        },
        created() {
            eventBus.$on('ageWasEdited', age => {
                this.age = age
            })
        }
    }
</script>

<style scoped>
    div {
        background-color: lightblue;
    }
</style>
