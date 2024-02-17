<template>
  <button class="group-mapping-add" type="button" @click="$emit('add')">
    {{ t(appName, 'Add group mapping') }}
  </button>
  <div v-for="(mapping, mappingIdx) in groupMapping" :key="mapping">
  <!-- Only for discord checklist with names-->
  <template v-if="appName === 'discord'">
    <select class="foreign-group" v-model="mapping.foreign">
      <option v-for="(name, id) in getGroupsForDiscord()" :key="id" :value="id">
        {{ name }}
      </option>
    </select>
  <!-- else -->
  </template>
  <template v-else>
    <input type="text" class="foreign-group" v-model="mapping.foreign" />
  </template>
    <select class="local-group" :name="mapping.foreign ? inputNamePrefix + '['+mapping.foreign+']' : ''">
      <option v-for="group in groups" :key="group" :value="group" :selected="mapping.local === group">
        {{ group }}
      </option>
    </select>
    <span class="group-mapping-remove" @click="$emit('remove', mappingIdx)">x</span>
  </div>
</template>

<script>
export default {
  props: ['groups', 'groupMapping', 'inputNamePrefix']
}

// Function to get names and IDs of all groups_for_discord as dictionary
function getGroupsForDiscord() {
  return {131232:"Role1"};
}

</script>

<style scoped>
  .group-mapping-add {
    width: 100%;
    display: block;
  }
  .foreign-group, .local-group {
    width: 133px;
  }
  .group-mapping-remove {
    cursor: pointer;
    font-weight: bold;
  }
</style>
