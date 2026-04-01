<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <ul id='channels'>
    <li v-for='channel in channels' :key='channel.value'>
      <div >
        <a :href='baseUrl + "?channel=" + channel.value + "&api-key=" + apiKey' >{{ channel.name }}</a>
      </div>
    </li>
  </ul>
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.classic" :snippet="snippets.full" title="Classic Editor"/>
  <tiny-editor :apiKey="apiKey" :channel="channel" :conf="conf.inline" :snippet="snippets.full" title="Inline Editor"/>
</template>

<script>
import { full } from './settings/settings';
import { generateConfig } from './configs/config';
import TinyEditorVue from './components/TinyEditor.vue';

export default {
  name: 'App',
  components: {
    'tiny-editor': TinyEditorVue
  },
  setup() {
    const configParams = {
      jwtServerURL: 'https://demo.api.tiny.cloud',
      apiKey: 'prsghhxax677rv082a1zj9b7cgjuoaqysf7h8ayxi5ao43ha'
    };
    const baseUrl = window.location.href.indexOf('?') > 0 ? window.location.href.substring(0, window.location.href.indexOf('?')) : window.location.href;
    const params = new URLSearchParams(window.location.search);
    const channel = params.get('channel') || '8-dev';
    const apiKey = params.get('api-key') || configParams.apiKey;
    const conf = {
      classic: generateConfig(configParams, { excludePlugins: ['tinydrive', 'uploadcare']}),
      inline: generateConfig(configParams, { excludePlugins: ['tinydrive', 'editimage', 'image' ], overrideConfig: { inline: true }})
    }

    const snippets = {
      full
    };

    const channels = [
    { name: '8 Development', value: '8-dev' },
    { name: '8 Testing', value: '8-testing' },
    { name: '8 Stable', value: '8-stable' },
    { name: '7 Development', value: '7-dev' },
    { name: '7 Testing', value: '7-testing' },
    { name: '7 Stable', value: '7-stable' },
    { name: '6 Development', value: '6-dev' },
    { name: '6 Testing', value: '6-testing' },
    { name: '6 Stable', value: '6-stable' },
    ];

    console.log('base url ', baseUrl)

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
