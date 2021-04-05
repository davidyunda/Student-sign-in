<template>
    <tr v-bind:key="student.starID" v-bind:class=" { present: student.present, absent:!student.present }">
        <td>{{ student.name }}</td>
        <td>{{ student.starID }}</td>
        <td>
            <input type="checkbox" v-bind:checked="student.present" v-on:change="arrivedORleft(student, $event.target.checked)">
        </td>
        <td v-show="edit"> <img src="@/assets/delete.png" v-on:click="deleteStudent"></td>
    </tr>
</template>

<script>
export default {
    name: 'StudentRow',
    props: {
        student: Object,
        edit: Boolean
    },
    methods: {
        arrivedORleft(student, present) {
            this.$emit('student-arrived-or-left', student, present)
        },
        deleteStudent() {
            if (confirm(`Delete ${this.student.name}?`)) {
                this.$emit('delete-student', this.student)
            }
        }
    }
}
</script>

<style scoped>
.present {
    color: grey;
    font-style: italic
}
.absent {
    color: black;
    font-weight: bold
}

img {
    height: 25px
}
</style>