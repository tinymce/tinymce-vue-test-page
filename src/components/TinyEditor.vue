<template>
  <div>
    <h2>{{ title }}</h2>
    <editor :api-key="apiKey" :init="conf" :initialValue="snippet" />
  </div>
</template>
<script>
import Editor from '@tinymce/tinymce-vue';

export default {
  name: 'TinyEditor',
  props: {
    title: String,
    conf: Object,
    snippet: String
  },
  components: { editor: Editor },
  setup() {
    const apiKey = 'b1g4d59rwwqxx1vj7mci23rjj8ubgb46i4xsio6ieig6fkps';
    return {
      apiKey,
    };
  },
}
</script>
