<template>
  <div>
    <component v-for="(comp, compIndex) in topicComponents"
               :is="comp.type"
               class="topic-component"
               :slots="comp.slots"
               :options="comp.options"
               :item="item"
               :key="getCompKey(key, compIndex)"
    />
  </div>
</template>

<script>
  import generateUniqueId from '../util/unique-id';

  import Badge from './Badge.vue';
  import ButtonComp from './ButtonComp.vue';
  import Callout from './Callout.vue';
  import CollectionSummary from './CollectionSummary.vue';
  import Division from './Division.vue';
  import ePayForm from './ePayForm.vue';
  import HorizontalTable from './HorizontalTable.vue';
  import Image_ from './Image.vue';
  import VerticalTable from './VerticalTable.vue';
  import OverlayToggleGroup from './OverlayToggleGroup.vue';
  import Paragraph from './Paragraph.vue';
  import List from './List.vue';
  import TabGroup from './TabGroup.vue';
  import HorizontalTableGroup from './HorizontalTableGroup.vue';
  import BadgeCustom from './BadgeCustom.vue';
  import Topic from './Topic.vue';
  import TopicSet from './TopicSet.vue';
  // console.log('in TopicComponentGroup.vue script, BadgeCustom:', BadgeCustom, 'Badge:', Badge, 'TabGroup:', TabGroup, 'Callout:', Callout, 'CollectionSummary:', CollectionSummary, 'HorizontalTable:', HorizontalTable);

  export default {
    name: 'TopicComponentGroup',
    props: ['topicComponents', 'item', 'filterData'],
    components: {
      Badge,
      ButtonComp,
      Callout,
      CollectionSummary,
      Division,
      ePayForm,
      HorizontalTable,
      Image_,
      VerticalTable,
      OverlayToggleGroup,
      Paragraph,
      List,
      HorizontalTableGroup,
    },
    beforeCreate() {
      // console.log('TopicComponentGroup beforeCreate is running');
      this.$options.components.TabGroup = TabGroup;
      this.$options.components.BadgeCustom = BadgeCustom;
      this.$options.components.Topic = Topic;
      this.$options.components.TopicSet = TopicSet;
    },
    data() {
      return {
        // generate a (basically) unique id for the group. the go-to npm packages
        // for uuid generation aren't available as umd builds on unpkg and
        // therefore won't work with the examples. this is good enough :)
        key: generateUniqueId()
      };
    },
    methods: {
      getCompKey(compGroupKey, compIndex) {
        return `topic-comp-${compGroupKey}-${compIndex}`;
      }
    }
  };
</script>

<style scoped>
  .topic-component {
    /* margin-bottom: 10px !important; */
  }
</style>
