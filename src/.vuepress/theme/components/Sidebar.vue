<template>
  <aside class="sidebar">
    <NavLinks />

    <slot name="top" />

    <SidebarLinks :depth="0" :items="items" />
    <slot name="bottom" />
    <div class="current" v-if="current">
      {{ current }}
    </div>
    <div class="current">
      Want more?
      <a href="https://sanicbook.com" target="_blank">
        sanicbook.com
        <span
          ><svg
            xmlns="http://www.w3.org/2000/svg"
            aria-hidden="true"
            focusable="false"
            x="0px"
            y="0px"
            viewBox="0 0 100 100"
            width="15"
            height="15"
            class="icon outbound"
          >
            <path
              fill="currentColor"
              d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"
            ></path>
            <polygon
              fill="currentColor"
              points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"
            ></polygon>
          </svg>
          <span class="sr-only">(opens new window)</span></span
        >
      </a>
    </div>
  </aside>
</template>

<script>
import SidebarLinks from "@theme/components/SidebarLinks.vue";
import NavLinks from "@theme/components/NavLinks.vue";
export default {
  name: "Sidebar",

  components: { SidebarLinks, NavLinks },

  props: ["items"],
  computed: {
    current() {
      return this.$root.$localeConfig.current || "";
    },
  },
};
</script>

<style lang="stylus">
.sidebar {
  ul {
    padding: 0;
    margin: 0;
    list-style-type: none;
  }

  a {
    display: inline-block;
  }

  .nav-links {
    display: none;
    border-bottom: 1px solid $borderColor;
    padding: 0.5rem 0 0.75rem 0;

    a {
      font-weight: 600;
    }

    .nav-item, .repo-link {
      display: block;
      line-height: 1.25rem;
      font-size: 1.1em;
      padding: 0.5rem 0 0.5rem 1.5rem;
    }
  }

  .current {
    padding: 1rem;
    border-top: 1px solid $borderColor;
  }

  & > .sidebar-links {
    padding: 1.5rem 0;

    & > li > a.sidebar-link {
      font-size: 1.1em;
      line-height: 1.7;
      font-weight: bold;
    }

    & > li:not(:first-child) {
      margin-top: 0.75rem;
    }
  }
}

@media (max-width: $MQMobile) {
  .sidebar {
    .nav-links {
      display: block;

      .dropdown-wrapper .nav-dropdown .dropdown-item a.router-link-active::after {
        top: calc(1rem - 2px);
      }
    }

    & > .sidebar-links {
      padding: 1rem 0;
    }
  }
}
</style>
