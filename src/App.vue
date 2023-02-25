<template>
  <header class="site-header">
    <nav class="navbar">
  <div class="container">

    <div class="navbar-header">
      <button class="navbar-toggler" data-toggle="open-navbar1">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <router-link to="/">
        <a href="#">
        <h4>Net<span>Movie</span></h4>
      </a>
      </router-link>
    </div>

    <div class="navbar-menu" id="open-navbar1">
      <ul class="navbar-nav">
        <li class="fav">
          <router-link to="/favorite">
            <a href="#">Saved Movies</a>
          </router-link>
        </li>
        <li disabled ><a href="#">Signin</a></li>
      </ul>
    </div>
  </div>
</nav>
  </header>

  <main class="container">
    <router-view />
  </main>
</template>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira sans', sans-serif;

  &::selection{
    background: transparentsize(#42B883, 0.5)
  }

  body{
    background-color: #1F1B24;
  }

  a{
    text-decoration: none;
    color: #b2b4b5;

    &:hover{
      opacity: .9;
      color: #b2b4b5;
    }
  }

  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap');

  $font-family: 'Roboto', sans-serif;
  $font-size-base: 0.925rem;
  $base-color: #66f;
  $text-dark: #3c4250;
  $border-color: #eceef3;

  $navbar-body-color: #fff;
  // $navbar-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.035);
  $navbar-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  $navbar-padding-y: 1rem;
  $navbar-padding-x: 1.15rem;

  $navbar-link-hover: $base-color;
  $navbar-link-padding-y: 0.5rem;
  $navbar-link-padding-x: 1rem;

  $navbar-dropdown-padding-y: 0.5rem;
  $navbar-dropdown-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.1);
  $navbar-dropdown-radius: 0.75rem;

  $navbar-dropdown-item-padding-y: 0.25rem;
  $navbar-dropdown-item-padding-x: 1rem;

  $navbar-dropdown-separator-margin-y: 9px;
  $navbar-dropdown-separator-color: $border-color;

  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }

  body {
    font-family: $font-family;
    font-size: $font-size-base;
  }

  a {
    text-decoration: none;
  }

  .container {
    width: 70%;
    position: relative;
    margin: {
      left: auto;
      right: auto;
    }

    padding: {
      left: 15px;
      right: 15px;
    }
  }


  .container {
    @media (min-width: 250px) {
      width: 90%;
    }
    @media (min-width: 576px) {
      width: 90%;
    }
  }

// Start navbar
  .navbar,
  .navbar > .container {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    @media (max-width: 768px) {
      display: block;
    }
  }

.navbar {
  box-shadow: $navbar-shadow;
  background-color: $navbar-body-color;
  padding: $navbar-padding-y $navbar-padding-x;
  border-bottom: 1px solid $border-color;

  .container {
    @media (min-width: 576px) {
      max-width: 540px;
    }
    @media (min-width: 768px) {
      max-width: 720px;
    }
    @media (min-width: 992px) {
      max-width: 960px;
    }
    @media (min-width: 1200px) {
      max-width: 1140px;
    }
  }

  .navbar-header {
    display: flex;
    align-items: center;

    @media (max-width: 768px) {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-direction: row-reverse;
    }

    .navbar-toggler {
      cursor: pointer;
      border: none;
      display: none;
      outline: none;

      @media (max-width: 768px) { display: block }

      span {
        height: 2px;
        width: 22px;
        background-color: lighten($text-dark, 35%);
        display: block;
      }
      span:not(:last-child) {
        margin-bottom: 0.2rem;
      }
    }

    > a {
      font-weight: 500;
      color: $text-dark;
    }
  }

  .navbar-menu {
    display: flex;
    align-items: center;
    flex-basis: auto;
    flex-grow: 1;

    @media (max-width: 768px) {
      display: none;
      text-align: center;
    }
 
    &.active {
      display: flex !important;
    }

    .fav{
      border-right: 2px solid #626060;
    }
    
    .navbar-nav {
      margin-left: auto;
      flex-direction: row;
      display: flex;
      padding-left: 0;
      margin-bottom: 0;
      list-style: none;

      @media (max-width: 768px) {
        width: 100%;
        display: block;
        border-top: 1px solid #EEE;
        margin-top: 1rem;
      }

      > li {
        
        > a {
          color: $text-dark;
          text-decoration: none;
          font-size: 17px;
          // font-weight: bold;
          display: inline-block;
          padding: $navbar-link-padding-y $navbar-link-padding-x;
          &:hover {
            color: $navbar-link-hover;
          }
          @media (max-width: 768px) {
            border-bottom: 1px solid $border-color;
          }
        }
        &.active {
          a {
            color: $base-color;
          }
        }
      }
    }
  }

  .navbar-dropdown {
    position: relative;
  }
}


// Custom
.navbar .navbar-header > a span {
  color: white;
}
.navbar .navbar-header h4 {
  color: #42B883;
  font-weight: 500;
  font-size: 1.25rem;
  @media (max-width: 768px) {
    font-size: 1.05rem;
  }
}

}
</style>
