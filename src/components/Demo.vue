<template lang="html">
  <div>
    <tabs>
      <configuration title="Configure"></configuration>
      <search title="Search"></search>
      <stat title="Stat"></stat>
    </tabs>
  </div>
</template>

<script>
import Tab from './Tab.vue'
import Tabs from './Tabs.vue'
import Configuration from './Configuration.vue'
import Search from "./Search.vue"
import Stat from "./Stat.vue"
export default {
  components: {
    Configuration,
    Stat,
    Search,
    Tabs
  }
}
</script>