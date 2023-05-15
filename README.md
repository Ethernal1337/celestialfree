<html>
<head>
  <title>Pasted emojies Encoder/Decoder</title>
  <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      background-color: #f1f1f1;
    }

    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
    }

    h1 {
      margin-bottom: 20px;
    }

    input[type="text"] {
      width: 300px;
      padding: 10px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
      resize: both;
      overflow: auto;
      border: none;
      outline: none;
    }

    button {
      padding: 10px 20px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
      margin-top: 10px;
      border: none;
      outline: none;
    }

    .outputBox {
      margin-top: 10px;
      padding: 10px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
      background-color: #f9f9f9;
      width: 300px;
      text-align: center;
    }
  </style>
  <script>
    function decode() {
      var emojiString = document.getElementById("inputDecode").value;
      const utf8EmojiString = emojiString.replace(/([\uD800-\uDBFF][\uDC00-\uDFFF])/g, (match) => {
        const codePoint = (match.charCodeAt(0) - 0xD800) * 0x400 + match.charCodeAt(1) - 0xDC00 + 0x10000;
        return String.fromCharCode(codePoint);
      });
      const base64Url = Array.from(utf8EmojiString).map((char) => String.fromCharCode(char.charCodeAt(0) - 0x1f337)).join('');
      const rawUrl = decodeURIComponent(escape(atob(base64Url)));
      document.getElementById("outputDecode").textContent = rawUrl;
    }

    function encode() {
      var url = document.getElementById("inputEncode").value;
      const utf8Url = unescape(encodeURIComponent(url));
      const base64Url = btoa(utf8Url);
      const emojiString = Array.from(base64Url).map((char) => String.fromCodePoint(0x1f337 + char.charCodeAt(0))).join('');
      document.getElementById("outputEncode").textContent = emojiString;
    }
  </script>
</head>
<body>
  <div class="container">
    <h1>P1337 Encoder/Decoder</h1>

    <h2>Decode</h2>
    <input type="text" id="inputDecode" placeholder="Enter encoded string">
    <button onclick="decode()">Decode</button>
    <div class="outputBox" id="outputDecode"></div>

    <h2>Encode</h2>
    <input type="text" id="inputEncode" placeholder="Enter text to encode">
    <button onclick="encode()">Encode</button>
    <div class="outputBox" id="outputEncode"></div>
  </div>

  <script>
  </script>
</body>
</html>
