<template>
  <div>
    <h2>{{ title }}</h2>
    <editor :cloudChannel="channel" :api-key="apiKey" :init="conf" :initialValue="snippet" />
  </div>
</template>
<script>
import Editor from '@tinymce/tinymce-vue';

export default {
  name: 'TinyEditor',
  props: {
    title: String,
    conf: Object,
    snippet: String,
    channel: String,
    apiKey: String
  },
  components: { editor: Editor },
  setup() {
    // Add code here, I mean if you want
    return {};
  },
}
</script>
