# index.html
My mint chat
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mint Friends Chat</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: sans-serif;
  background: #effaf6;
  color: #496c60;
}
.container {
  max-width: 480px;
  margin: 35px auto;
  padding: 20px;
}
h1 {
  text-align: center;
  color: #76bba4;
  font-size: 28px;
}
.card {
  background: white;
  border-radius: 22px;
  padding: 22px;
  box-shadow: 0 5px 20px #b8ded033;
}
input {
  width: 100%;
  padding: 13px;
  margin: 8px 0;
  border: 1px solid #cce9df;
  border-radius: 12px;
  font-size: 15px;
}
button {
  border: none;
  background: #91ceb9;
  color: white;
  padding: 13px;
  border-radius: 13px;
  cursor: pointer;
  font-size: 15px;
}
#join { width: 100%; margin-top: 10px; }
#chat { display: none; }
#messages {
  height: 350px;
  overflow-y: auto;
  background: #f5fbf8;
  border-radius: 15px;
  padding: 12px;
  margin: 15px 0;
}
.message {
  background: #dff3eb;
  padding: 10px 13px;
  border-radius: 14px;
  margin: 8px 0;
  overflow-wrap: anywhere;
}
.name {
  font-size: 12px;
  color: #79a999;
  margin-bottom: 4px;
}
.send {
  display: flex;
  gap: 7px;
}
.send input { margin: 0; }
.send button { min-width: 65px; }
#typing {
  font-size: 12px;
  color: #8bb8a8;
  min-height: 20px;
}
.note {
  text-align: center;
  font-size: 12px;
  color: #91aaa1;
  margin-top: 18px;
}
</style>
</head>
<body>
<div class="container">
  <h1>♡ Mint Friends Chat ♡</h1>

  <div class="card" id="login">
    <h3>お部屋に入ろう 🌿</h3>
    <input id="nickname" placeholder="ニックネーム">
    <input id="room" placeholder="みんなで決めた合言葉">
    <button id="join">入室する ♡</button>
  </div>

  <div class="card" id="chat">
    <h3 id="roomTitle"></h3>
    <div id="messages"></div>
    <div id="typing"></div>
    <div class="send">
      <input id="message" placeholder="メッセージを入力...">
      <button id="send">送信</button>
    </div>
    <p class="note">Mint Friends Chat ♡</p>
  </div>
</div>

<script>
const $ = id => document.getElementById(id);
let nickname = "";

$("join").onclick = () => {
  nickname = $("nickname").value.trim();
  const room = $("room").value.trim();

  if (!nickname || !room) {
    alert("ニックネームと合言葉を入力してね！");
    return;
  }

  $("login").style.display = "none";
  $("chat").style.display = "block";
  $("roomTitle").textContent = "🌿 " + room + " のお部屋";
};

function sendMessage() {
  const input = $("message");
  const value = input.value.trim();
  if (!value) return;

  const item = document.createElement("div");
  item.className = "message";

  const name = document.createElement("div");
  name.className = "name";
  name.textContent = nickname;

  const body = document.createElement("div");
  body.textContent = value;

  item.append(name, body);
  $("messages").appendChild(item);
  $("messages").scrollTop = $("messages").scrollHeight;

  input.value = "";
  $("typing").textContent = "";
}

$("send").onclick = sendMessage;

$("message").addEventListener("keydown", event => {
  if (event.key === "Enter") sendMessage();
});

$("message").addEventListener("input", () => {
  $("typing").textContent =
    $("message").value.length > 0 ? "入力中..." : "";
});
</script>
</body>
</html>
