<template>
  <div class="appbar">
    <div>
      <h2 class="appname">{{ appName }}</h2>
      <p class="tagline">{{ tagline }}</p>
    </div>

    <span></span>
    <span class="username">
      <cdx-icon :icon="cdxIconUserActive" size="medium"></cdx-icon>
      <h3>
        {{ username }}
      </h3>
    </span>
  </div>
</template>

<script>
import { inject } from "vue";
import { CdxIcon } from "@wikimedia/codex";
import { cdxIconUserActive } from "@wikimedia/codex-icons";

export default {
  name: "AppBar",
  data() {
    return {
      appName: inject("appName"),
      username: inject("username"),
      tagline: inject("tagline"),
    };
  },
  setup() {
    return {
      cdxIconUserActive,
    };
  },
  components: {
    CdxIcon,
  },
};
</script>

<style scoped>
.appbar {
  border-bottom: 5px;
  border-bottom-style: solid;
  border-bottom-color: #172861;
  border-top: 4px solid #172861;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 1rem;
  align-items: center;
  font-family: Arial, Helvetica, sans-serif;
  background-color: #4056a1;
  color: white;
}
.appname {
  margin-left: 1rem;
}
.username {
  padding-right: 1rem;
  display: flex;
  flex-direction: row;
  color: "white";
  align-items: center;
}
.tagline {
  color: white;
  font-weight: bold;
  margin-left: 1rem;
}
.cdx-icon {
  fill: white !important;
  margin-right: 1rem;
}
</style>
