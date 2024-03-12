<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <ul id='channels'>
    <li v-for='channel in channels' :key='channel.value'>
      <div >
        <a :href='baseUrl + "?channel=" + channel.value + "&api-key=" + apiKey' >{{ channel.name }}</a>
      </div>
    </li>
  </ul>
  <p><label><input type="checkbox" id="streaming" /> Stream response</label></p>
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.classic" :snippet="snippets.basic" title="Classic Editor" />
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.inline" :snippet="snippets.basic" title="Inline Editor" />
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.quickbars" :snippet="snippets.basic" title="Quickbars Editor" />
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.bottom" :snippet="snippets.basic" title="Bottom Toolbar Editor" />
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.resize" :snippet="snippets.full" title="Resize Editor" />
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.template" :snippet="snippets.template" title="Template Editor" />
</template>

<script>
import { basic, full, template } from './settings/settings.ts';
import { classic, inline, quickbars, bottom, resize, templateConf } from './settings/configurations.ts';
import TinyEditorVue from './components/TinyEditor.vue';

export default {
  name: 'App',
  components: {
    'tiny-editor': TinyEditorVue
  },
  setup() {
    const baseUrl = window.location.href.indexOf('?') > 0 ? window.location.href.substring(0, window.location.href.indexOf('?')) : window.location.href;
    const params = new URLSearchParams(window.location.search);
    const channel = params.get('channel') || '6-dev';
    const apiKey = params.get('api-key') || 'b1g4d59rwwqxx1vj7mci23rjj8ubgb46i4xsio6ieig6fkps';
    const conf = {
      classic,
      inline,
      quickbars,
      bottom,
      resize,
      template: templateConf
    }

    const snippets = {
      basic,
      full,
      template
    };

    const channels = [
    { name: '7 Development', value: '7-dev' },
    { name: '7 Testing', value: '7-testing' },
    { name: '7 Stable', value: '7-stable' },
    { name: '6 Development', value: '6-dev' },
    { name: '6 Testing', value: '6-testing' },
    { name: '6 Stable', value: '6-stable' },
    ];

    return {
      channels,
      baseUrl,
      channel,
      apiKey,
      conf,
      snippets,
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
