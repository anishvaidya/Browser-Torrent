<template>
  <div class="container content is-fluid">
    <!-- Pop up for how-to guide using modal -->
    <div class="modal" :class="{'is-active': modalVisible}">
      <div class="modal-background" v-on:click="toggleModal"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title has-text-centered">Beginners guide to torrenting</p>
        </header>
        <section class="modal-card-body">
          <ul>
            <li>Choose the torrent of your liking.</li>
            <li>Copy the magnet link or the infohash of your torrent.</li>
            <blockquote>
              eg.
              <a href="magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent" target="_blank">Copy my address.</a> (Magnet link to Sintel, a free movie.)
            </blockquote>
            <li>Paste the link in the given input box.</li>
            <li>Click on download.</li>
            <li>Relax while the files are being downloaded.</li>
            <li>The downloaded files will be displayed on your browser window.</li>
            <li>Click to download instantaneously.</li>
          </ul>
        </section>
        <footer class="modal-card-foot">
          <button class="button is-success" v-on:click="toggleModal">OK</button>
        </footer>
      </div>
    </div>
    <div v-if="!downloadStarted">
      <form action="/torrent" method="post">
        <div class="field has-text-centered">
          <label class="label">Enter torrent ID or magnetURI</label>
          <div class="field is-horizontal has-addons has-addons-centered">
            <div class="control">
              <input class="input is-medium" name="torrentid" v-model="magnetURI" required>
            </div>
            <div class="control">
              <button class="button is-info is-outlined is-medium" type="submit" name="torrent-submit" v-on:click.prevent="download">Download</button>
            </div>
          </div>
        </div>
      </form>
    </div>
    <div class="container is-fluid has-text-centered"  v-if="downloadStarted">
      <p id="progressText">Downloading...</p>
      <p id="fileLength"></p>
      <p id="downloadSpeed"></p>
      <progress id="progressBar" class="progress is-danger is-medium" value="0" max="100"></progress>
    </div>

    <div class="has-text-centered">
      <p id="logs"></p>
    </div>

    <div class="container has-text-centered" style="margin-top: 40px;">
      <p>Not sure how to download using BrowserTorrent.</p>
      <a v-on:click="toggleModal">Click here to learn.</a>
    </div>
  </div>
</template>

<script>
import webtorrent from 'webtorrent'
export default {
  name: 'download-form',
  data() {
    return{
      modalVisible: false,
      downloadStarted: false,
      magnetURI: null
    }
  },
  methods:{
    toggleModal: function(){
      this.modalVisible = !this.modalVisible;
    },
    toggleProgressbar: function(){
      this.downloadStarted = !this.downloadStarted;
    },
    download: function(){
      if(this.magnetURI == null || this.magnetURI == "" || this.magnetURI == " "){
        alert("Please give INPUT");
      }
      else{
        this.toggleProgressbar();
        console.log('Clicked me!');
        var client = new webtorrent();
        client.destroy();
        var client = new webtorrent();
        console.log(client);
        // var link = this.magnetURI;
        // var magnetURI = 'magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent';
        // var magnetURI = "magnet:?xt=urn:btih:54dca0477d74d88ed051a9cd62fe5359151e7823&dn=elementaryos-0.4.1-stable.20180214.iso&tr=https%3A%2F%2Fashrise.com%3A443%2Fphoenix%2Fannounce&tr=udp%3A%2F%2Fopen.demonii.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.ccc.de%3A80%2Fannounce&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80%2Fannounce&tr=udp%3A%2F%2Ftracker.publicbt.com%3A80%2Fannounce&ws=http://ams3.dl.elementary.io/download/MTUyMTM3NjM3OA==/elementaryos-0.4.1-stable.20180214.iso";
        client.add(this.magnetURI, function(torrent){
          console.log('above ready');
          document.getElementById("fileLength").innerHTML = "File Size: <strong>" + ((client.torrents[0].length)/(1024*1024)).toFixed(2) + "MB</strong>";
          var interval = setInterval(function () {
            // log('Progress: ' + (torrent.progress * 100).toFixed(1) + '%');
            document.getElementById("progressBar").value = (torrent.progress * 100);
            document.getElementById("downloadSpeed").innerHTML = "Download Speed: <strong>" + (torrent.downloadSpeed / 1024) + "KBps</strong>";
            document.getElementById("progressText").innerHTML = " Progress: <strong>" + (torrent.progress * 100).toFixed(1) + "%</strong>";
          }, 5000)

          torrent.on('ready', function(){
            console.log('test');
          });

          torrent.on('done', function() {
            console.log('Done downloading');
            document.getElementById("progressBar").value = 100;
            document.getElementById("progressText").innerHTML = " Progress: 100%. <strong>Click on files below to download.</strong>";
            var counter = 0;
            clearInterval(interval);
            torrent.files.forEach(function (file) {
              console.log(file.name);
              // file.appendTo('#logs');
              // log('(Blob URLs only work if the file is loaded from a server. "http//localhost" works. "file://" does not.)')
              file.getBlobURL(function (err, url) {
                if (err) return log(err.message);
                // log('File done.');
                log('<a href="' + url + '" download="' + file.name + '">Download full file: ' + file.name + '</a>');
              });
            }
          )
        })
      });

      function log (str) {
        var p = document.getElementById("logs");
        logs.innerHTML += str + '<br />';
      }
    }
  }
}
}
</script>


<style scoped>
.content{
  margin-top: 140px;
}

progress{
  width: 60%;
  margin: 0 auto;
}
</style>
