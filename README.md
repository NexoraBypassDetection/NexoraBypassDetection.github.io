const express = require('express');
const fetch = require('node-fetch');
const path = require('path');
const app = express();

const PORT = process.env.PORT || 3000;

// Replace this with your actual Discord Webhook URL
const DISCORD_WEBHOOK_URL = 'https://discord.com/api/webhooks/your_webhook_id/your_token_here';

app.use(express.json());
app.use(express.static(path.join(__dirname))); // Serve index.html

app.post('/send-webhook', async (req, res) => {
  const { discordUsername, productName } = req.body;
  if (!discordUsername || !productName) {
    return res.status(400).json({ error: 'Missing data' });
  }

  const embed = {
    embeds: [
      {
        title: 'New Key Purchase',
        color: 0x3b82f6,
        fields: [
          { name: 'Discord Username', value: discordUsername, inline: true },
          { name: 'Product', value: productName, inline: true },
        ],
        timestamp: new Date().toISOString(),
      }
    ]
  };

  try {
    const response = await fetch(DISCORD_WEBHOOK_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(embed),
    });

    if (!response.ok) {
      console.error('Webhook error:', await response.text());
      return res.status(500).json({ error: 'Webhook failed' });
    }

    res.json({ success: true });
  } catch (err) {
    console.error('Server error:', err);
    res.status(500).json({ error: 'Server error' });
  }
});

app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
