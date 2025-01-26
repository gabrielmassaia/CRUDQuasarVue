<template>
  <q-page padding>
    <q-table
      title="Treats"
      :rows="posts"
      :columns="columns"
      row-key="name"
    />
  </q-page>
</template>

<script>

import { defineComponent, ref, onMounted } from 'vue';
import { api } from 'boot/axios'

export default defineComponent({

  name: 'IndexPage',
  setup () {
    const posts = ref([])

    const columns = [

      { name: 'id', label: 'Id', field: 'id', sortable: true, align: 'left' },
      { name: 'title', label: 'Título', field: 'title', sortable: true, align: 'left' },
      { name: 'author', label: 'Autor', field: 'author', sortable: true, align: 'left' }

    ]

    onMounted(() => {
      getPosts()
    })

    const getPosts = async () => {
      try {
        const { data} = await api.get('p osts')
        posts.value = data
      } catch (error) {
        console.log(error)
      }
    }

    return {
      posts,
      columns
    }
  }
})
</script>
