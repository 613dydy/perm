const express = require('express');
const fs = require('fs');
const app = express();

// アクセスがあった時にログを記録する
app.get('/', (req, res) => {
  const log = {
    ip: req.headers['x-forwarded-for'] || req.connection.remoteAddress,
    userAgent: req.headers['user-agent'],
    time: new Date().toISOString(),
  };

  fs.appendFileSync('logs.txt', JSON.stringify(log) + '\n');
  res.send('アクセスが記録されました。');
});

// ポート設定（Renderでは必要）
const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
