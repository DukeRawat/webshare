<template>
  <div class="webshare-content">
    <div aria-live="polite" aria-atomic="true" class="position-fixed top-0 end-0">
      <div id="liveToastNotAvailable" class="toast align-items-center text-black bg-warning" role="alert" aria-live="assertive" aria-atomic="true">
          <div class="d-flex">
            <div  iv class="toast-body">
            Web Share api not available!
            </div>
            <button type="button" class="btn-close me-2 m-auto" data-bs-dismiss="toast" aria-label="Close"></button>
          </div>
      </div>
      <div id="liveToastSuccess" class="toast align-items-center text-black bg-light" role="alert" aria-live="assertive" aria-atomic="true">
          <div class="d-flex">
            <div  iv class="toast-body">
            Web Share complete!
            </div>
            <button type="button" class="btn-close me-2 m-auto" data-bs-dismiss="toast" aria-label="Close"></button>
          </div>
      </div>
      <div id="liveToastAbort" class="toast align-items-center text-white bg-danger" role="alert" aria-live="assertive" aria-atomic="true">
          <div class="d-flex">
            <div  iv class="toast-body">
            Web Share api Aborted!
            </div>
            <button type="button" class="btn-close me-2 m-auto" data-bs-dismiss="toast" aria-label="Close"></button>
          </div>
      </div>
    </div>
    <h1>{{ msg }}</h1>
    <hr/>
    <h2>Features and Limitations</h2>
    <h3>Features</h3>
    <br>
    <ul>
      <li> > Using Web Share, your web application can use the system-provided sharing capabilities just like a platform-specific app.</li>
      <li> > Users/Developers get a more comprehensive range of sharing options.</li>
      <li> > For Users it's possible to customize the preferred share targets on their devices. Reduce inconveniences and abuses</li>
      <li> > Web Share APIs help to share text, URLs, and files.</li>
      <li> > Improve page load times by doing away with third-party scripts from individual social platforms.</li>
      <li> > A single button is sufficient to trigger the device’s native sharing options.</li>
    </ul>
    <h3>Limitations</h3><br>
    <ul>
      <li> > It can only be used on a site that is accessed via HTTPS.</li>
      <li> > It must be invoked in response to a user action such as a click. Invoking it through the onload & setTimeout is not recommended.</li>
      <li> > As of January 2021, it is available on Safari, Android in Chromium forks, Chrome OS, and Chrome on Windows. Chrome on MacOS is still in development.</li>
    </ul>
    <h3>Browser support</h3><br>
    <ul>
      <li> > As of early 2021, using the API to share title, text, and URL is supported by: Safari 12 or later on macOS and iOS. Chrome 75 or later on Android, and 89 or later on Chrome OS and Windows.</li>
      <li> > Using the API to share files is supported by: Safari 15 or later on macOS and iOS. Chrome 75 or later on Android, and 89 or later on Chrome OS and Windows.</li>
      <li> > Most Chromium-based browsers, like Edge, have the same support for this feature as the corresponding version of Chrome.</li>
    </ul>
    <h3>Check feature availability using wpt.live</h3><br>
    <ul>
      <li><a href="https://wpt.live/web-share/" target="_blank" rel="noopener">Wpt.Live</a></li>
    </ul>
    <h3>3rd Party Share buttons libraries</h3><br>
    <ul>
      <li><a href="https://www.addthis.com/get/share/" target="_blank" rel="noopener">AddThis Share Buttons</a></li>
      <li><a href="https://sharingbuttons.io/" target="_blank" rel="noopener">Sharingbuttons.io Share Buttons</a></li>
    </ul>
    <h3>Web Share references</h3><br>
    <ul>
      <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Web_Share_API" target="_blank" rel="noopener">MDN Web Share API</a></li>
      <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/share" target="_blank" rel="noopener">MDN Navigator share</a></li>
      <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/canShare" target="_blank" rel="noopener">MDN Navigator canShare</a></li>
      <li><a href="https://www.w3.org/TR/web-share/" target="_blank" rel="noopener">w3c Web Share API</a></li>
    </ul>
    <h3>Some Other related references</h3><br>
    <ul>
      <li><a href="https://css-tricks.com/how-to-use-the-web-share-api/" target="_blank" rel="noopener">How to Use the Web Share API</a></li>
      <li><a href="https://web.dev/web-share/" target="_blank" rel="noopener">Integrate with the OS sharing UI</a></li>
      <li><a href="https://web.dev/web-share-target/" target="_blank" rel="noopener">Receiving shared data</a></li>
      <li><a href="https://alligator.io/js/web-share-api/" target="_blank" rel="noopener">The Web Share API</a></li>
      <li><a href="https://caniuse.com/web-share" target="_blank" rel="noopener">caniuse</a></li>
      <li><a href="https://mobiforge.com/design-development/sharing-buttons-and-the-web-share-api" target="_blank" rel="noopener">Sharing buttons</a></li>
    </ul>
    <button class="btn btn-warning share-btn position-fixed" @click="sharePage"><i class="bi bi-share-fill"></i></button>
  </div>
</template>

<script>
import {Toast} from "bootstrap";
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  mounted() {
  },
  methods: {
    sharePage() {
      let liveToastNotAvailable = document.querySelector('#liveToastNotAvailable');
      let liveToastSuccess = document.querySelector('#liveToastSuccess');
      let liveToastAbort = document.querySelector('#liveToastAbort');
      // const image = await fetch('img/logo.82b9c7a5.png')
      // .then((response) => response.blob())
      // .then((blob) => {
      //   var file = new File([blob], "picture.png", {type: 'image/png'});
      //   return([file]);
      // })
      // .catch(console.error);
      // if (navigator.share && navigator.canShare({file: image})) {
      if (navigator.share) {
        navigator.share({
          title: 'WebShare API Demo',
          text: 'Check out this WebShare Demo!',
          url: 'https://dukerawat.github.io/webshare/'
        }).then(() => {
          new Toast(liveToastSuccess).show();
          console.log('Thanks for sharing!');
        })
        .catch(() => {
          new Toast(liveToastAbort).show();
          console.error;
        });
      } else {
        let toast = new Toast(liveToastNotAvailable);
        toast.show();
        console.log('Web Share api not available!');
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  font-weight: 600;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.share-btn {
  bottom: 3%;
  right: 3%;
  border-color: black;
}
</style>
