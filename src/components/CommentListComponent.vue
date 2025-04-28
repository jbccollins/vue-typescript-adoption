<script setup>
import CommentComponent from './CommentComponent.vue'
</script>

<template>
  <div>
    <CommentComponent
      id="1"
      createdDate="2025-04-25"
      :editedDate="null"
      :author="{ handle: 'alice', imageUrl: 'https://randomuser.me/api/portraits/women/1.jpg' }"
      content="This is a great post! 🎉"
      :likes="5"
      :dislikes="0"
      :reactions="[
        { type: 'heart', count: 2 },
        { type: 'laugh', count: 1 },
      ]"
      :replies="[3, 4, 5]"
    />
    <CommentComponent
      id="2"
      createdDate="2025-04-26"
      editedDate="2025-04-27"
      :author="{ handle: 'bob', imageUrl: 'https://randomuser.me/api/portraits/men/2.jpg' }"
      content="Thanks for sharing this information."
      :likes="2"
      :dislikes="1"
      :reactions="[{ type: 'wow', count: 3 }]"
      :replies="[]"
    />
  </div>
</template>
