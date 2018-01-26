<template>
  <div id="app">
    <router-view/>
  </div>
</template>
<script>
export default {
  name: 'App'
}

</script>
<style>
body,
ul {
  margin: 0;
  padding: 0
}

a,
a.link-dark,
a.link-light {
  color: inherit;
  position: relative;
  text-decoration: none;
  transition: all .3s ease
}

a.link-dark:before,
a.link-light:before,
a:before {
  bottom: -2px;
  right: 0;
  content: "";
  position: absolute;
  transform: scale(1);
  transition: all .3s ease;
  width: 100%;
  height: 2px
}

a.link-dark:hover:before,
a.link-light:hover:before,
a:hover:before {
  transform: scale(0)
}

a.link-light:hover {
  color: #4fc3f7
}

a.link-light:before {
  background-color: #f5f5f5
}

a.link-dark:hover {
  color: #f5f5f5
}

a.link-dark:before {
  background-color: #4fc3f7
}

button {
  align-self: center;
  background-color: #f5f5f5;
  border: 2px solid #f5f5f5;
  border-radius: 190px;
  color: #0277bd;
  cursor: pointer;
  font-family: Quicksand, sans-serif;
  font-size: 1.25em;
  margin: .5em 0;
  outline: none;
  padding: 1em;
  transition: all .25s ease;
  max-width: 400px;
  width: 100%
}

button:disabled,
button:disabled:hover {
  cursor: auto;
  pointer-events: none
}

h2 {
  font-weight: 400
}

ul {
  list-style-type: none
}

@media (hover:hover) {
  button:active,
  button:hover {
    background-color: #4fc3f7;
    border: 2px solid #4fc3f7;
    color: #f5f5f5
  }
}

@media (max-width:600px) {
  body {
    font-size: .85em
  }
}

.flex-center-col {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center
}

.fade-enter-active,
.fade-leave-active {
  transition: all .3s ease
}

.fade-enter,
.fade-leave-to {
  opacity: 0
}

.score-high {
  color: #5cdb80
}

.score-low {
  color: #ff5593
}

@keyframes fade-in {
  0% {
    opacity: 0
  }
  to {
    opacity: 1
  }
}

@keyframes open {
  0% {
    max-height: 0;
    opacity: 0;
    margin-bottom: 0
  }
  to {
    max-height: 1000px;
    opacity: 1;
    margin-bottom: 2em
  }
}

@keyframes close {
  0% {
    max-height: 1000px;
    opacity: 1;
    margin-bottom: 2em
  }
  to {
    max-height: 0;
    opacity: 0;
    margin-bottom: 0
  }
}

body {
  background-color: #4481eb;
  background-image: linear-gradient(0deg, #4481eb 0, #04befe);
  background-repeat: no-repeat;
  display: flex;
  font-family: Quicksand, sans-serif;
  height: 100vh;
  justify-content: center;
  text-align: center
}

body,
header {
  color: #f5f5f5
}

header {
  transform: scale(1)
}

h1,
p {
  margin: 0
}

main {
  animation: fade-in 1.5s ease;
  flex-direction: column;
  justify-content: flex-start;
  height: 100%
}

.about-button,
main {
  align-items: center;
  display: flex
}

.about-button {
  background-color: #0277bd;
  border: 2px solid #4fc3f7;
  border-radius: 100%;
  cursor: pointer;
  justify-content: center;
  position: fixed;
  right: .5em;
  top: .25em;
  width: 40px;
  height: 40px;
  z-index: 1000
}

.container {
  width: 100%
}

.icon-close,
.icon-menu {
  transition: all .3s ease
}

.icon-close:hover,
.icon-menu:hover {
  color: #4fc3f7
}

.grow {
  animation: grow .5s ease forwards
}

.small {
  animation: squeeze .5s ease forwards
}

@keyframes grow {
  0% {
    transform: scale(.66);
    padding: .25em 0
  }
  to {
    transform: scale(1);
    padding: 1em
  }
}

@keyframes squeeze {
  0% {
    transform: scale(1);
    padding: 1em
  }
  to {
    transform: scale(.66);
    padding: .5em 0
  }
}

.expand-enter-active {
  animation: open .75s ease forwards
}

.expand-leave-active {
  animation: close .5s ease forwards
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}/*

body,
ul {
  margin: 0;
  padding: 0
}

a.link-dark,
a.link-light,
a {
  color: inherit;
  position: relative;
  text-decoration: none;
  transition: all .3s ease
}

a.link-dark:before,
a.link-light:before,
a:before {
  bottom: -2px;
  right: 0;
  content: "";
  position: absolute;
  transform: scale(1);
  transition: all .3s ease;
  width: 100%;
  height: 2px
}

a.link-dark:hover:before,
a.link-light:hover:before,
a:hover:before {
  transform: scale(0)
}

a.link-light:hover {
  color: #4fc3f7
}

a.link-light:before {
  background-color: #f5f5f5
}

a.link-dark:hover {
  color: #f5f5f5
}

a.link-dark:before {
  background-color: #4fc3f7
}

button {
  align-self: center;
  background-color: #f5f5f5;
  border: 2px solid #f5f5f5;
  border-radius: 190px;
  color: #0277bd;
  cursor: pointer;
  font-family: Quicksand, sans-serif;
  font-size: 1.25em;
  margin: .5em 0;
  outline: none;
  padding: 1em;
  transition: all .25s ease;
  max-width: 400px;
  width: 100%
}

button:disabled,
button:disabled:hover {
  cursor: auto;
  pointer-events: none
}

h2 {
  font-weight: 400
}

ul {
  list-style-type: none
}

@media (hover:hover) {
  button:active,
  button:hover {
    background-color: #4fc3f7;
    border: 2px solid #4fc3f7;
    color: #f5f5f5
  }
}

@media (max-width:600px) {
  body {
    font-size: .85em
  }
}

.flex-center-col {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center
}

.fade-enter-active,
.fade-leave-active {
  transition: all .3s ease
}

.fade-enter,
.fade-leave-to {
  opacity: 0
}

.score-high {
  color: #5cdb80
}

.score-low {
  color: #ff5593
}

@keyframes fade-in {
  0% {
    opacity: 0
  }
  to {
    opacity: 1
  }
}

@keyframes open {
  0% {
    max-height: 0;
    opacity: 0;
    margin-bottom: 0
  }
  to {
    max-height: 1000px;
    opacity: 1;
    margin-bottom: 2em
  }
}

@keyframes close {
  0% {
    max-height: 1000px;
    opacity: 1;
    margin-bottom: 2em
  }
  to {
    max-height: 0;
    opacity: 0;
    margin-bottom: 0
  }
}

h2 {
  font-weight: 700
}

section {
  max-width: 600px;
  position: relative
}

.turnDisplay {
  background-color: #f5f5f5;
  border-radius: 25px;
  color: #0277bd;
  margin-bottom: 2em;
  padding: .15em
}

@media (max-width:600px) {
  h2 {
    margin: 0
  }
  .turnDisplay {
    border-radius: 0;
    margin: 0
  }
}*/

</style>
