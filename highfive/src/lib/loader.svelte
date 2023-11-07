<div id="loader"></div>

<style>
#loader {
    z-index: 1;
    width: 80px;
    height: 80px;
    border: 8px solid rgba(0,0,0,.2);
    border-radius: 50%;
    border-top: 8px solid #000;
    -webkit-animation: spin 2s linear infinite;
    animation: spin 2s linear infinite;
}

@-webkit-keyframes spin {
  0% { -webkit-transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>