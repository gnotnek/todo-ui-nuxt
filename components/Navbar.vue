<template>
<div class="navbar bg-base-100">
  <div class="flex-1">
    <a class="btn btn-ghost text-xl"><router-link to="#">A Note App</router-link></a>
  </div>
  <div class="flex-none">
    <ul class="menu menu-horizontal px-1">
      <li><router-link to="signup">Sign Up</router-link></li>
      <li><router-link to="login">Log In</router-link></li>
    </ul>
  </div>
</div>
</template>