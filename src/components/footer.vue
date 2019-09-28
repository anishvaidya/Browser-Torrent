<template>
  <footer class="footer">
    <div class="container">
      <div class="content has-text-centered">
        <p>
          <strong>BrowserTorrent</strong> by Dhiraj, Umesh, and Anish.
        </p>
        <p>
          This program is <strong>open source</strong>.<a href="https://github.com/dhirajs1997/BrowserTorrent" target="_blank"> Help us improve this program on Github.</a>
        </p>
        <p id="donate">Donate us on Ethereum at</p>
        <p id="donateLink"><a>0x87B560DbE9958839995f33B773cd389B666e11fD</a></p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'footerdetails'
}
</script>

<style>
  footer .content{
    margin: 10px 0 10px 0;
    padding: 10px;
  }
  #donate{
    margin-bottom: 0;
  }
  #donateLink{
    font-size: 12px;
  }
</style>
