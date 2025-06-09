 🎉 Buzzer Quiz für 10 Spieler

Ein einfaches React-basiertes Buzzer-Quiz-System für bis zu 10 Spieler – inspiriert vom PietSmiet-Buzzer-System. Jeder Spieler kann seinen Namen eingeben, buzzern und Punkte bekommen/verloren haben.

## 🚀 Features
- Bis zu 10 Spieler
- Spieler können ihren Namen selbst eintragen
- Buzz-Mechanismus: nur ein Spieler kann gleichzeitig buzzern
- Punktevergabe (+1 / -1) pro Spieler
- Reset-Funktion für den Buzzer
- ✅ Beispielspielerliste
- ▶️ "Spiel starten"-Button setzt alle Scores und Buzzer zurück

## 🛠️ Installation

### Voraussetzungen
- Node.js (>= 18)
- npm

### Lokale Entwicklung
```bash
# Repository klonen
https://github.com/dein-benutzername/buzzer-quiz.git
cd buzzer-quiz

# Abhängigkeiten installieren
npm install

# Entwicklungsserver starten
npm run dev
```

Die App läuft dann unter `http://localhost:5173`

## ▶️ Spiel starten mit Beispielspielern
- Auf den Button **"Spiel starten"** klicken, um alle Namen auf Standardwerte zu setzen:
  - Spieler 1 bis Spieler 10
  - Punkte auf 0
  - Buzzer wird zurückgesetzt

### 🧩 Beispielcode für App.jsx (Start-Button & Initialisierung)
```jsx
import React, { useState } from 'react';

const initialPlayers = Array.from({ length: 10 }, (_, i) => ({
  name: `Spieler ${i + 1}`,
  score: 0,
  hasBuzzed: false,
}));

export default function App() {
  const [players, setPlayers] = useState(initialPlayers);
  const [buzzedPlayer, setBuzzedPlayer] = useState(null);

  const handleBuzz = (index) => {
    if (buzzedPlayer === null) {
      setBuzzedPlayer(index);
      const updated = [...players];
      updated[index].hasBuzzed = true;
      setPlayers(updated);
    }
  };

  const updateScore = (index, delta) => {
    const updated = [...players];
    updated[index].score += delta;
    setPlayers(updated);
  };

  const resetBuzz = () => {
    setPlayers(players.map(p => ({ ...p, hasBuzzed: false })));
    setBuzzedPlayer(null);
  };

  const startGame = () => {
    setPlayers(initialPlayers);
    setBuzzedPlayer(null);
  };

  return (
    <div className="p-4 max-w-4xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">🎉 Buzzer Quiz</h1>
      <button onClick={startGame} className="mb-4 px-4 py-2 bg-blue-500 text-white rounded">Spiel starten</button>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {players.map((player, index) => (
          <div key={index} className="p-4 border rounded shadow bg-white">
            <input
              className="font-bold text-lg mb-2 w-full border p-1"
              value={player.name}
              onChange={(e) => {
                const updated = [...players];
                updated[index].name = e.target.value;
                setPlayers(updated);
              }}
            />
            <p className="text-xl">Punkte: {player.score}</p>
            <div className="flex gap-2 mt-2">
              <button onClick={() => updateScore(index, 1)} className="bg-green-500 text-white px-2 py-1 rounded">+1</button>
              <button onClick={() => updateScore(index, -1)} className="bg-red-500 text-white px-2 py-1 rounded">-1</button>
              <button onClick={() => handleBuzz(index)} disabled={buzzedPlayer !== null} className="bg-yellow-500 text-white px-2 py-1 rounded">Buzz</button>
            </div>
            {player.hasBuzzed && <p className="text-pink-500 font-bold mt-2">Hat gebuzzert!</p>}
          </div>
        ))}
      </div>
      <button onClick={resetBuzz} className="mt-4 px-4 py-2 bg-gray-700 text-white rounded">Buzz zurücksetzen</button>
    </div>
  );
}
```

## 🧱 Projektstruktur
```
buzzer-quiz/
├── public/
├── src/
│   ├── App.jsx         # Hauptkomponente
│   ├── main.jsx        # Einstiegspunkt
│   ├── index.css       # Tailwind-Styling
├── index.html
├── package.json
├── tailwind.config.js
├── postcss.config.js
├── vite.config.js
├── .gitignore
└── README.md
```

## 🌐 Deployment

### GitHub Pages (automatisch mit GitHub Actions)

1. `vite.config.js` ist bereits vorbereitet mit dem `base`-Pfad.
2. GitHub Actions Workflow ist in `.github/workflows/deploy.yml` enthalten.
3. Push dein Projekt auf GitHub:
```bash
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/dein-benutzername/buzzer-quiz.git
git push -u origin main
```
4. GitHub Actions wird automatisch bauen und auf GitHub Pages deployen.

### Alternativ: Vercel oder Netlify
- Repository einfach importieren und deployen.

## 📸 Vorschau
![Vorschau Screenshot](https://via.placeholder.com/800x400?text=Buzzer+Quiz+Preview)

## 📄 Lizenz
MIT Lizenz.

---

Viel Spaß beim Buzzern! 🎉
