<template>
  <div id="app">
    <h2>タスク一覧</h2>
    <ul>
      <li v-for="task in tasks" v-bind:key="task.id">
        <input type="checkbox" v-bind:checked="task.done" v-on:change="toggleTasksStatus(task)">
        {{ task.name }}

        <span v-for="id in task.LabelIds" v-bind:key="id">
          {{ getLabelText(id) }}
        </span>
      </li>
    </ul>

    <form v-on:submit.prevent="addTask">
      <input type="text" v-model="newTaskName" placeholder="新しいタスク">
    </form>

    <h2>ラベル一覧</h2>
    <ul>
      <li v-for="label in labels" v-bind:key="label.id">
        <input type="checkbox" v-bind:value="label.id" v-model="newTaskLabelIds">
          {{ label.text }}
      </li>
    </ul>

    <form v-on:submit.prevent="addLabel">
      <input type="text" v-model="newLabelText" placeholder="新しいラベル">
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 入力中の新しいタスク名を一時的に保管する
      newTaskName: '',

      // 新しいタスクに紐づくラベル一覧を一時的に保管する
      newTaskLabelIds: [],

      // 入力中の新しいラベル名を一時的に保管する
      newLabelText: ''
    }
  },
  computed: {
    tasks() {
      return this.$store.state.tasks
    },
    labels() {
      return this.$store.state.labels
    },
  },
  methods: {
    addTask () {
      // 'addTask'ミューテーションをコミットする
      this.$store.commit('addTask', {
        name: this.newTaskName,
        labelIds: this.newTaskLabelIds
      })
      this.newTaskName = ''
      this.newTaskLabelIds = []
    },
    toggleTaskStatus (task) {
      // 'toggleTaskStatus'ミューテーションをコミットする
      this.$store.commit('toggleTaskStatus', {
        id: task.id
      })
    },
    addLabel () {
      // 'addLabel'ミューテーションをコミットする
      this.$store.commit('addLabel', {
        text: this.newLabelText
      })
      this.newLabelText = ''
    },
    getLabelText (id) {
      const label = this.labels.filter(label => label.id === id)[0]
      return label ? label.text : ''
    },
  }
}
</script>

<style>
</style>
