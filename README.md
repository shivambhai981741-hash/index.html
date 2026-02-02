index.html
<script>
const API_KEY = "YAHAN_APNI_API_KEY_DAALO"; // 🔑

async function send(){
  let m = document.getElementById('msg');
  let c = document.getElementById('chat');
  if(m.value.trim()==='') return;

  let userText = m.value;
  c.innerHTML += `<div class='user'>${userText}</div>`;
  m.value = "";

  c.innerHTML += `<div class='bot'>Soch raha hoon 🤔...</div>`;
  c.scrollTop = c.scrollHeight;

  const response = await fetch("https://api.openai.com/v1/chat/completions", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": "Bearer " + API_KEY
    },
    body: JSON.stringify({
      model: "gpt-4o-mini",
      messages: [
        {
          role: "system",
          content: "Tum ek Smart Teacher ho jo Navy MR (12th level) Hindi me padhata hai."
        },
        {
          role: "user",
          content: userText
        }
      ]
    })
  });

  const data = await response.json();
  c.lastChild.remove();
  c.innerHTML += `<div class='bot'>${data.choices[0].message.content}</div>`;
  c.scrollTop = c.scrollHeight;
}
</script>


