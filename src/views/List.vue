<template>
  <v-list
    subheader
    flat
  >

    <v-text-field @keyup.enter="addNewItem()" @click:append="addNewItem()" v-model="newItemTitle" class="ma-3"
      solo
      label="New item" clearable
    ></v-text-field>
    <div v-for="item in shoppingList"
         :key="item.id">
      <v-list-item
        @click="doneBought(item.id)" :class="{ 'blue lighten-5' : item.bought }">
        <template>
          <v-list-item-action>
            <v-checkbox
              :input-value="item.bought"
              color="primary"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title :class="{ 'text-decoration-line-through' : item.bought }">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn icon @click.stop="deleteItem(item.id)" stop>
              <v-icon color="grey lighten-1">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </template>
      </v-list-item>
      <v-divider />
    </div>
  </v-list>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'List',
  data: () => {
    return (
      {
        newItemTitle: '',
        shoppingList: [
          {
            id: 1,
            title: 'Title 1',
            bought: false
          },
          {
            id: 2,
            title: 'Title 2',
            bought: false
          },
          {
            id: 3,
            title: 'Title 3',
            bought: false
          }
        ]
      })
  },
  methods: {
    generateId () {
      return 5
    },
    doneBought (id) {
      const item = this.shoppingList.filter(value => value.id === id)[0]
      item.bought = !item.bought
    },
    deleteItem (id) {
      const index = this.shoppingList.indexOf(this.shoppingList.filter(value => value.id === id)[0])
      this.shoppingList.splice(index, 1)
    },
    addNewItem () {
      const id = this.shoppingList[this.shoppingList.length - 1].id
      const item = { id: id, title: this.newItemTitle, bought: false }
      this.shoppingList.push(item)
      this.newItemTitle = ''
    }
  }
}

</script>
