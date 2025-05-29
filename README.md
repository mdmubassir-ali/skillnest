# skillnest
const { app, BrowserWindow } = require('electron');
const path = require('path');

function createWindow() {
  const win = new BrowserWindow({
    width: 1200,
    height: 800,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js'),
      contextIsolation: true,
      nodeIntegration: false,
    }
  });

  win.loadFile(path.join(__dirname, 'build', 'index.html'));
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit();
});
🔹 preload.js
javascript
Copy
Edit
window.addEventListener('DOMContentLoaded', () => {
  // You can expose APIs to renderer here securely if needed
});
🔹 package.json
json
Copy
Edit
{
  "name": "skillnest-desktop",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "electron": "electron .",
    "dist": "electron-builder"
  },
  "devDependencies": {
    "electron": "^25.3.0",
    "electron-builder": "^23.6.0"
  },
  "build": {
    "appId": "com.skillnest.app",
    "files": [
      "build/**/*",
      "main.js",
      "preload.js",
      "package.json"
    ],
    "mac": {
      "target": "dmg"
    },
    "win": {
      "target": "nsis"
    },
    "linux": {
      "target": "AppImage"
    }
  }
}
🔹 src/App.js
javascript
Copy
Edit
import React from 'react';

export default function App() {
  return <h1>Welcome to Skillnest Desktop App</h1>;
}
🔹 src/index.js
javascript
Copy
Edit
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
🔹 public/index.html
html
Copy
Edit
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Skillnest Desktop</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
