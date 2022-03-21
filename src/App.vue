<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <ul id='channels'>
    <li v-for='channel in channels' :key='channel.value'>
      <div >
        <a :href='baseUrl + "?channel=" + channel.value'>{{ channel.name }}</a>
      </div>
    </li>
  </ul>
  <tiny-editor :channel="channel" :conf="conf.classic" :snippet="snippets.basic" title="Classic Editor" />
  <tiny-editor :channel="channel" :conf="conf.inline" :snippet="snippets.basic" title="Inline Editor" />
  <tiny-editor :channel="channel" :conf="conf.quickbars" :snippet="snippets.basic" title="Quickbars Editor" />
  <tiny-editor :channel="channel" :conf="conf.bottom" :snippet="snippets.basic" title="Bottom Toolbar Editor" />
  <tiny-editor :channel="channel" :conf="conf.resize" :snippet="snippets.full" title="Resize Editor" />
  <tiny-editor :channel="channel" :conf="conf.template" :snippet="snippets.template" title="Template Editor" />
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
    { name: '6 Development', value: '6-dev' },
    { name: '6 Testing', value: '6-testing' },
    { name: '6 Stable', value: '6-stable' },
    { name: '5 Stable', value: '5' }
    ];

    return {
      channels,
      baseUrl,
      channel,
      conf,
      snippets
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
