<template>
  <div
    class="flex flex-col items-center justify-between px-8 py-8 gap-8 text-light-text dark:text-dark-text bg-light-layer-0 dark:bg-dark-layer-0"
  >
    <Head>
      <Title>{{ organization.name }} </Title>
    </Head>
    <div class="w-3/4 h-[260px] mx-auto">
      <ImageOrganization :imgURL="organization?.imageURL" />
    </div>
    <div class="flex flex-col items-center gap-2">
      <h1
        class="text-3xl font-bold responsive-h1 text-light-text dark:text-dark-text"
      >
        {{ organization.name }}
      </h1>
      <h2
        class="text-lg font-bold text-center responsive-h2 text-light-distinct-text dark:text-dark-distinct-text"
      >
        {{ organization.tagline }}
      </h2>
    </div>
    <div class="flex flex-col items-center w-full gap-4">
      <MenuLinkWrapper
        v-for="button in organizationButtons"
        :key="button.id"
        :to="localePath(button.routeURL)"
        :selected="button.selected"
      >
        <div
          class="flex items-center w-full text-sm font-medium text-left space-x-2"
        >
          <span class="width-1/6"
            ><Icon
              v-if="button.iconURL"
              :name="button.iconURL"
              class="flex-shrink-0 w-5 h-5"
          /></span>
          <p
            class="text-lg font-bold select-none width-5/6 whitespace-nowrap hover:light-menu-selection"
          >
            <span class="sr-only">{{ $t("_global.navigate-to") }}</span>
            {{ $t(button.label) }}
          </p>
        </div>
      </MenuLinkWrapper>
      <BtnRouteInternal
        class="w-max"
        :cta="true"
        linkTo="/"
        label="components.btn-route-internal.offer-to-help"
        fontSize="base"
        rightIcon="bi:arrow-right"
        iconSize="1.25em"
        ariaLabel="components.btn-route-internal.offer-to-help-aria-label"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from "vue";
import type { MenuSelector } from "~/types/menu-selector";
import type { Organization } from "~/types/organization";

definePageMeta({
  layout: "sidebar",
});

const { id } = useRoute().params;
const localePath = useLocalePath();
const organization: Organization = {
  name: "tech from below",
  status: "approved",
  tagline: "Technologie von und für soziale Bewegungen",
  location: "Berlin",
  description: "This is the description of tech from below",
  topic: "Technology and Privacy",
  members: 3,
  supporters: 30,
  imageURL: "/images/tech-from-below.svg",
};

const organizationButtons: MenuSelector[] = [
  {
    id: 1,
    label: "_global.about",
    routeURL: "/organizations/" + id + "/about",
    iconURL: "bi:card-text",
    selected: useRoute().path.split("/").pop() === "about" ? true : true,
  },
  {
    id: 2,
    label: "_global.events",
    routeURL: "/organizations/" + id + "/events",
    iconURL: "bi:calendar-check",
    selected: useRoute().path.split("/").pop() === "events" ? true : true,
  },
  {
    id: 3,
    label: "_global.groups",
    routeURL: "/organizations/" + id + "/groups",
    iconURL: "IconGroup",
    selected: useRoute().path.split("/").pop() === "groups" ? true : true,
  },
  {
    id: 4,
    label: "_global.resources",
    routeURL: "/organizations/" + id + "/resources",
    iconURL: "IconResource",
    selected: useRoute().path.split("/").pop() === "resources" ? true : true,
  },
  {
    id: 5,
    label: "_global.faq",
    routeURL: "/organizations/" + id + "/faq",
    iconURL: "IconFAQ",
    selected: useRoute().path.split("/").pop() === "faq" ? true : true,
  },
  {
    id: 6,
    label: "_global.settings",
    routeURL: "/organizations/" + id + "/settings",
    iconURL: "bi:gear",
    selected: useRoute().path.split("/").pop() === "settings" ? true : true,
  },
  // {
  //    id: 7,
  //   label: "_global.affiliates",
  //   routeURL: "/organizations/" + id + "/affiliates",
  //   iconURL: "IconSupport",
  //   selected: useRoute().path.split("/").pop() === "affiliates" ? true : true,
  // },
  // {
  //    id: 8,
  //   label: "_global.tasks",
  //   routeURL: "/organizations/" + id + "/tasks",
  //   iconURL: "bi:check-square",
  //   selected: useRoute().path.split("/").pop() === "tasks" ? true : true,
  // },
  // {
  //    id: 9,
  //   label: "_global.discussions",
  //   routeURL: "/organizations/" + id + "/discussions",
  //   iconURL: "octicon:comment-discussion-24",
  //   selected: useRoute().path.split("/").pop() === "discussions" ? true : true,
  // },
];

const handleResize = () => {
  if (window.innerWidth > 640) {
    window.removeEventListener("resize", handleResize);
    navigateTo(`${id}/about`);
  }
};

onMounted(() => {
  // Add event listener to handle resizing.
  window.addEventListener("resize", handleResize);

  // Verify that the user is on a mobile device.
  handleResize();
});
</script>
