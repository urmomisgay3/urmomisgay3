- 👋 Hi, I’m @urmomisgay3
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
urmomisgay3/urmomisgay3 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

 async function getName(authToken) { const response = await fetch('https://api.blooket.com/api/users/verify-token?token=JWT+' + authToken); const data = await response.json();

return data.name
};

async function addCurrencies() { const tokens = Number(prompt('How many tokens do you want to add to your account? (10000 daily)')); const myToken = localStorage.token.split('JWT ')[1];

if (tokens > 10000) {
    alert('You can add up to 10000 tokens daily.')
}

const response = await fetch('https://api.blooket.com/api/users/add-rewards', {
    method: "PUT",
    headers: {
        "referer": "https://www.blooket.com/",
        "content-type": "application/json",
        "authorization": localStorage.token
    },
    body: JSON.stringify({
        addedTokens: tokens,
        addedXp: 300,
        name: await getName(myToken)
    })
});

if (response.status == 200) {
    alert(`${tokens} tokens and 300 XP added to your account!`);
} else {
    alert('An error occured.');
};
};

addCurrencies();
