---
title: net command
category: CMD
tags: []
is_angular: false
---
<script>
function copytext() {
  /* Get the text field */
  var copyText = document.getElementById("netshare");

  /* Select the text field */
  copyText.select();

  /* Copy the text inside the text field */
  document.execCommand("copy");

  /* Alert the copied text */
  alert("Copied the text: " + copyText.value);
};

</script>

<pre id="netshare">
net share
<pre>



<!-- The button used to copy the text -->
<button onclick="copytext()">Copy text</button>





