<template>
  <!-- Sidebar -->
  <aside class="fixed h-screen w-[20vw] pt-5 pl-16 text-black">
    <!-- Logo -->
    <img class="w-12 ml-[-10px] mb-2" src="../assets/logo.png" alt="Logo" />
    <!-- List (unordered) of icons and corresponding texts in the sidebar -->
    <ul class="links">
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/home.svg"
          alt="Home Icon"
        />
        <p>Home</p>
      </li>
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/explore.svg"
          alt="Explore Icon"
        />
        <p>Explore</p>
      </li>
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/messages.svg"
          alt="Messages Icon"
        />
        <p>Messages</p>
      </li>
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/notifications.svg"
          alt="Notifications Icon"
        />
        <p>Notifications</p>
      </li>
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/bookmarks.svg"
          alt="Bookmarks Icon"
        />
        <p>Bookmarks</p>
      </li>
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/lists.svg"
          alt="Lists Icon"
        />
        <p>Lists</p>
      </li>
      <!-- Mini profile image and text -->
      <li>
        <img
          class="w-7 h-7 mr-2 border-[3px] border-opacity-80 border-white rounded-full"
          src="../assets/Profile.png"
          alt="Profile Image"
        />
        <p>Profile</p>
      </li>
      <li>
        <img
          class="w-6 h-6 mr-2"
          src="../assets/icons/more.svg"
          alt="More Icon"
        />
        <p>More</p>
      </li>
    </ul>

    <!-- Tweet button -->
    <button
      class="bg-blue-500 text-white w-[90%] h-10 border-none rounded-full mt-5 ml-[-9px]"
    >
      Tweet
    </button>
  </aside>
</template>

<style>
.links li {
  display: flex;
  align-items: center;
  padding: 12px 0;
  cursor: pointer;
}

.links li:hover {
  color: #60a0ff;
}
</style>

<script>
export default {
  name: "SideBar",
};
</script>
