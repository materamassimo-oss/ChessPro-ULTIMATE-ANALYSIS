# 🎯 QUICK REFERENCE: Unicode in HTML vs JavaScript

## LA REGOLA D'ORO

```
📌 HTML STATICO    → HTML Entities  (&#XXXX;)
📌 JAVASCRIPT CODE → Escape Codes   (\uXXXX)
```

---

## ✅ ESEMPI CORRETTI

### HTML Tags (File .html)
```html
<!-- ✅ CORRETTO -->
<h1>&#9812; Chess Game &#9818;</h1>
<button>&#9823; Play</button>
<p>Pieces: &#9817;&#9816;&#9815;</p>

<!-- ❌ SBAGLIATO - Non funziona! -->
<h1>\u2654 Chess Game \u265A</h1>
<button>\u265F Play</button>
```

### JavaScript Strings
```javascript
// ✅ CORRETTO
const piece = '\u2654'; // ♔
const annotation = '\u203C\u203C'; // ‼‼
console.log('\u2655'); // Output: ♕

// ❌ SBAGLIATO - Non necessario in JS
const piece = '&#9812;'; // Funziona ma non idiomatico
```

### Template Strings (JavaScript che genera HTML)
```javascript
// ✅ CORRETTO - Usa HTML entities perché genera HTML
function createHeader() {
    return `<h1>&#9812; Title &#9818;</h1>`;
}

// ✅ CORRETTO - Usa escape codes per textContent
function setText() {
    element.textContent = '\u2654'; // Browser interpreta come ♔
}

// ✅ ENTRAMBI FUNZIONANO per innerHTML
element.innerHTML = '&#9812;';  // HTML entity
element.innerHTML = '\u2654';   // JS escape → simbolo → HTML
```

---

## 📚 REFERENCE TABLE: Simboli Scacchi

| Simbolo | Nome | HTML Entity | JS Escape | Decimal |
|---------|------|-------------|-----------|---------|
| ♔ | White King | `&#9812;` | `\u2654` | 9812 |
| ♕ | White Queen | `&#9813;` | `\u2655` | 9813 |
| ♖ | White Rook | `&#9814;` | `\u2656` | 9814 |
| ♗ | White Bishop | `&#9815;` | `\u2657` | 9815 |
| ♘ | White Knight | `&#9816;` | `\u2658` | 9816 |
| ♙ | White Pawn | `&#9817;` | `\u2659` | 9817 |
| ♚ | Black King | `&#9818;` | `\u265A` | 9818 |
| ♛ | Black Queen | `&#9819;` | `\u265B` | 9819 |
| ♜ | Black Rook | `&#9820;` | `\u265C` | 9820 |
| ♝ | Black Bishop | `&#9821;` | `\u265D` | 9821 |
| ♞ | Black Knight | `&#9822;` | `\u265E` | 9822 |
| ♟ | Black Pawn | `&#9823;` | `\u265F` | 9823 |

---

## 🎯 DECISION TREE

```
Devo inserire un simbolo Unicode...
│
├─ In un tag HTML statico? (<h1>, <button>, <p>)
│  └─ ✅ Usa HTML Entity: &#9812;
│
├─ In una stringa JavaScript?
│  ├─ Per console.log o variabile?
│  │  └─ ✅ Usa Escape Code: '\u2654'
│  │
│  └─ Per generare HTML (template string)?
│     └─ ✅ Usa HTML Entity: `<h1>&#9812;</h1>`
│
└─ In CSS content?
   └─ ✅ Usa \2654 (CSS escape, no "u")
```

---

## 🔧 CONVERSIONE RAPIDA

### Simbolo → HTML Entity
```javascript
// Formula: Prendi codice hex, converti in decimal
'\u2654' → U+2654 → 9812 → &#9812;

// Tool online:
// https://www.unicodepedia.com/unicode/game-symbols/2654/white-chess-king/
```

### HTML Entity → JS Escape
```javascript
// Formula: Prendi decimal, converti in hex
&#9812; → 9812 → 0x2654 → \u2654

// Oppure usa:
String.fromCharCode(9812) === '\u2654' // true
```

---

## 💡 TIPS & TRICKS

### 1. Test Rapido in Console
```javascript
// Verifica che un escape code funzioni:
console.log('\u2654'); // Deve mostrare ♔

// Converti entity → char:
String.fromCharCode(9812); // ♔

// Converti char → code:
'♔'.charCodeAt(0); // 9812
```

### 2. Template String Safety
```javascript
// ✅ SAFE - HTML entity
const html = `<div>&#9812;</div>`;

// ⚠️ WORKS ma può confondere - escape viene interpretato
const html = `<div>\u2654</div>`; // Browser vede <div>♔</div>

// 🎯 BEST PRACTICE - usa entities per chiarezza
```

### 3. String Building
```javascript
// Opzione 1: Escape codes (più leggibile in JS)
const pieces = ['\u2654', '\u2655', '\u2656'];

// Opzione 2: Array di entities (per export HTML)
const htmlPieces = ['&#9812;', '&#9813;', '&#9814;'];

// Opzione 3: Misto (conversione runtime)
const pieces = ['\u2654', '\u2655'];
const htmlPieces = pieces.map(p => 
    `&#${p.charCodeAt(0)};`
);
```

---

## ⚠️ COMMON MISTAKES

### Errore #1: Escape codes in HTML
```html
<!-- ❌ SBAGLIATO -->
<h1>\u2654 Title</h1>
<!-- Browser mostra letteralmente: \u2654 Title -->

<!-- ✅ CORRETTO -->
<h1>&#9812; Title</h1>
```

### Errore #2: HTML entities in console.log
```javascript
// ❌ SBAGLIATO (funziona ma brutto)
console.log('&#9812;'); // Output: &#9812; (letterale)

// ✅ CORRETTO
console.log('\u2654'); // Output: ♔ (simbolo)
```

### Errore #3: Dimenticare il punto e virgola
```html
<!-- ❌ SBAGLIATO - manca ; -->
<h1>&#9812 Title</h1>

<!-- ✅ CORRETTO -->
<h1>&#9812; Title</h1>
```

---

## 🎓 ESEMPI REAL-WORLD

### Esempio 1: Header
```html
<!-- ChessPro v4.1.1 -->
<h1>&#9812; Chess Pro Ultimate &#9818;</h1>
```

### Esempio 2: Pulsante
```html
<button onclick="startGame()">
    &#9823; vs &#9812; AI
</button>
```

### Esempio 3: JavaScript Array
```javascript
const pieceSymbols = {
    k: '\u2654', // White King
    q: '\u2655', // White Queen
    r: '\u2656', // White Rook
    // ... etc
};
```

### Esempio 4: Export HTML
```javascript
function exportHTML() {
    const html = `
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="UTF-8">
            <title>Chess Report</title>
        </head>
        <body>
            <h1>&#9812; Analysis &#9818;</h1>
            <p>White pieces: &#9817;&#9816;&#9815;</p>
        </body>
        </html>
    `;
    return html;
}
```

### Esempio 5: PGN Annotations
```javascript
// In JavaScript strings - usa escape codes
if (brilliant) annotation = '\u203C\u203C'; // ‼‼
if (good) annotation = '\u0021'; // !
if (blunder) annotation = '\u003F\u003F'; // ??
```

---

## 🔍 DEBUG CHECKLIST

Quando i simboli non si vedono:

### Passo 1: Identifica il Contesto
```
Il simbolo è in:
[ ] HTML statico (<h1>, <div>, etc)
[ ] JavaScript string (const x = '...')
[ ] Template string (`<html>...</html>`)
[ ] CSS content property
```

### Passo 2: Verifica il Formato
```html
<!-- HTML? Deve avere &#XXXX; -->
<h1>&#9812;</h1> ✅
<h1>\u2654</h1> ❌

<!-- JavaScript? Deve avere \uXXXX -->
const x = '\u2654'; ✅
const x = '&#9812;'; ⚠️ (funziona ma non idiomatico)
```

### Passo 3: Controlla Encoding
```html
<!-- File deve essere UTF-8 -->
<meta charset="UTF-8"> ✅

<!-- VS Code: controlla bottom-right corner -->
UTF-8 ✅
ANSI ❌
```

---

## 📝 CHEAT SHEET

### Copy-Paste Ready

**White Pieces (HTML):**
```html
&#9812; &#9813; &#9814; &#9815; &#9816; &#9817;
```

**Black Pieces (HTML):**
```html
&#9818; &#9819; &#9820; &#9821; &#9822; &#9823;
```

**White Pieces (JavaScript):**
```javascript
'\u2654', '\u2655', '\u2656', '\u2657', '\u2658', '\u2659'
```

**Black Pieces (JavaScript):**
```javascript
'\u265A', '\u265B', '\u265C', '\u265D', '\u265E', '\u265F'
```

---

## ✅ QUICK TEST

Prova questo nel tuo file HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Unicode Test</title>
</head>
<body>
    <!-- HTML entities -->
    <h1>HTML: &#9812; &#9818;</h1>
    
    <!-- JavaScript -->
    <script>
        // JS escape codes
        console.log('JS:', '\u2654', '\u265A');
        
        // Insert into DOM with textContent
        document.body.innerHTML += 
            '<p>textContent: <span id="test1"></span></p>';
        document.getElementById('test1').textContent = '\u2654';
        
        // Insert into DOM with innerHTML
        document.body.innerHTML += 
            '<p>innerHTML: <span id="test2"></span></p>';
        document.getElementById('test2').innerHTML = '&#9818;';
    </script>
</body>
</html>
```

**Expected output:**
- HTML: ♔ ♚
- Console: JS: ♔ ♚
- textContent: ♔
- innerHTML: ♚

---

## 🎯 FINAL TIPS

1. **Consistency**: Pick one style per context and stick to it
2. **Comments**: Add comments showing the actual symbol
3. **Testing**: Always test in actual browser, not just editor
4. **Charset**: Always use UTF-8 encoding
5. **Reference**: Bookmark this guide!

---

## 🆘 STILL NOT WORKING?

**Checklist:**
- [ ] File encoding is UTF-8?
- [ ] `<meta charset="UTF-8">` presente?
- [ ] Using correct format (&#XXXX; in HTML, \uXXXX in JS)?
- [ ] Semicolon after HTML entity?
- [ ] Browser cache cleared?

**Se ancora non funziona:**
1. Apri Console (F12)
2. Ispeziona elemento con DevTools
3. Verifica che l'HTML contenga effettivamente il simbolo
4. Controlla Network tab per encoding issues

---

Made with ♔ by ChessPro v4.1.1
