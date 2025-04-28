<script setup>
const props = defineProps({
  id: {
    type: Number,
    required: true,
  },
  createdDate: {
    type: String,
    required: true,
  },
  editedDate: {
    type: [String, null],
    required: true,
  },
  author: {
    type: Object,
    required: true,
    validator: (value) => {
      return typeof value.handle === 'string' && typeof value.imageUrl === 'string'
    },
  },
  content: {
    type: String,
    required: true,
  },
  likes: {
    type: Number,
    default: 0,
  },
  dislikes: {
    type: Number,
    default: 0,
  },
  reactions: {
    type: Array,
    default: () => [],
    validator: (value) => {
      const allowedTypes = ['heart', 'laugh', 'wow']
      return value.every(
        (reaction) =>
          reaction &&
          typeof reaction.type === 'string' &&
          allowedTypes.includes(reaction.type) &&
          typeof reaction.count === 'number',
      )
    },
  },
  // Array of reply ids
  replies: {
    type: Array,
    default: () => [],
    validator: (value) => {
      return value.every((reply) => {
        return typeof reply === Number
      })
    },
  },
  onLike: {
    type: Function,
    default: () => {},
  },
  onDislike: {
    type: Function,
    default: () => {},
  },
  onReaction: {
    type: Function,
    default: () => {},
  },
  onReply: {
    type: Function,
    default: () => {},
  },
})
</script>
<template>
  <div class="comment">
    <div class="comment-header">
      <img :src="props.author.imageUrl" alt="Author's avatar" class="avatar" />
      <div class="author-info">
        <span class="author-handle">{{ props.author.handle }}</span>
        <span class="comment-date">{{ props.createdDate }}</span>
      </div>
    </div>
    <p class="comment-content">{{ props.content }}</p>
    <div class="comment-actions">
      <button @click="props.onLike">Like ({{ props.likes }})</button>
      <button @click="props.onDislike">Dislike ({{ props.dislikes }})</button>
      <button @click="props.onReply">Reply</button>
    </div>
    <div class="comment-reactions">
      <span v-for="reaction in props.reactions" :key="reaction.type">
        {{ reaction.type }}: {{ reaction.count }}
      </span>
    </div>
    <div class="comment-replies">
      <a href="#" @click.prevent>
        {{ props.replies.length > 0 ? props.replies.length + ' replies' : 'no replies' }}
      </a>
    </div>
  </div>
</template>
<style scoped>
.comment {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 0;
}
.comment-header {
  display: flex;
  align-items: center;
}
.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin-right: 10px;
}
.author-info {
  display: flex;
  flex-direction: column;
}
.author-handle {
  font-weight: bold;
}
.comment-date {
  font-size: 0.8em;
  color: #666;
}
.comment-content {
  margin: 10px 0;
}
.comment-actions {
  display: flex;
  gap: 10px;
}
.comment-reactions {
  margin: 10px 0;
}
.comment-replies {
  margin-top: 10px;
}
.comment-replies ul {
  list-style-type: none;
  padding: 0;
}
.comment-replies li {
  margin: 5px 0;
}
</style>
