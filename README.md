<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Anonymous School Feedback</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <!-- Opt-in to light/dark color schemes for native UI surfaces -->
  <meta name="color-scheme" content="light dark" />
  <style>
    :root {
      /* Let the UA render appropriate form controls in light/dark */
      color-scheme: light dark;

      /* Theming via CSS custom properties (variables) */
      --bg: #f7f8fb;
      --text: #0b1220;
      --muted: #5b6577;
      --card: rgba(255, 255, 255, 0.85);
      --card-border: rgba(15, 23, 42, 0.08);
      --accent: #2563eb;   /* blue-600 */
      --accent-2: #7c3aed; /* purple-600 */
      --ring: #93c5fd;     /* blue-300 */
      --shadow: 0 12px 40px rgba(2, 6, 23, 0.12);
      --blur: 14px;

      --radius: 16px;
      --gap: 14px;
      --pad: 18px;

      --transition: 160ms;
    }

    @media (prefers-color-scheme: dark) {
      :root {
        --bg: #0b1020;
        --text: #e6e8ef;
        --muted: #a2a9ba;
        --card: rgba(17, 24, 39, 0.60);
        --card-border: rgba(255, 255, 255, 0.10);
        --accent: #60a5fa;   /* blue-400 */
        --accent-2: #a78bfa; /* violet-400 */
        --ring: #60a5fa;
        --shadow: 0 12px 40px rgba(0, 0, 0, 0.45);
      }
    }

    /* Respect users who prefer less motion */
    @media (prefers-reduced-motion: reduce) {
      * {
        animation: none !important;
        transition: none !important;
        scroll-behavior: auto !important;
      }
    }

    /* Background and layout */
    html, body {
      height: 100%;
    }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto,
                   "Helvetica Neue", Arial, "Noto Sans", "Liberation Sans", sans-serif;
      color: var(--text);
      background: radial-gradient(1200px 800px at 80% -10%, rgba(124, 58, 237, 0.18), transparent 60%),
                  radial-gradient(1000px 700px at -10% 20%, rgba(37, 99, 235, 0.18), transparent 55%),
                  var(--bg);
      display: grid;
      place-items: center;
      padding: 32px 18px;
    }

    .card {
      width: min(680px, 100%);
      border-radius: calc(var(--radius) + 2px);
      background: var(--card);
      border: 1px solid var(--card-border);
      box-shadow: var(--shadow);
      backdrop-filter: blur(var(--blur));
      -webkit-backdrop-filter: blur(var(--blur));
      overflow: clip;
    }

    .header {
      padding: 22px 22px 8px;
    }
    .title {
      margin: 0 0 6px;
      font-weight: 700;
      letter-spacing: -0.01em;
      font-size: clamp(1.25rem, 1rem + 1vw, 1.6rem);
    }
    .subtitle {
      margin: 0;
      color: var(--muted);
      font-size: 0.975rem;
      line-height: 1.45;
    }

    form {
      display: grid;
      gap: var(--gap);
      padding: 10px 22px 22px;
    }

    label {
      font-size: 0.95rem;
      font-weight: 600;
      margin-bottom: 6px;
      display: block;
    }

    .field {
      display: grid;
      gap: 6px;
    }

    select,
    textarea,
    button {
      font: inherit;
    }

    select,
    textarea {
      width: 100%;
      color: var(--text);
      background: rgba(255, 255, 255, 0.6);
      border: 1px solid var(--card-border);
      border-radius: var(--radius);
      padding: var(--pad);
      outline: none;
      transition: box-shadow var(--transition) ease, border-color var(--transition) ease, background var(--transition) ease;
      backdrop-filter: blur(2px);
      -webkit-backdrop-filter: blur(2px);
    }

    @media (prefers-color-scheme: dark) {
      select,
      textarea {
        background: rgba(2, 6, 23, 0.35);
      }
    }

    textarea {
      min-height: 170px;
      resize: vertical;
    }

    select:focus-visible,
    textarea:focus-visible {
      border-color: transparent;
      box-shadow: 0 0 0 3px var(--ring);
    }

    .note {
      color: var(--muted);
      font-size: 0.92rem;
      margin-top: -2px;
      margin-bottom: 8px;
    }

    .actions {
      display: grid;
      gap: 10px;
      margin-top: 6px;
    }

    button[type="submit"] {
      cursor: pointer;
      border: none;
      border-radius: calc(var(--radius) + 2px);
      padding: 14px 18px;
      color: white;
      font-weight: 700;
      letter-spacing: 0.02em;
      background-image: linear-gradient(135deg, var(--accent), var(--accent-2));
      box-shadow: 0 8px 20px rgba(37, 99, 235, 0.35);
      transition: transform var(--transition) ease, box-shadow var(--transition) ease, opacity var(--transition) ease;
    }

    button[type="submit"]:hover {
      transform: translateY(-1px);
      box-shadow: 0 12px 28px rgba(37, 99, 235, 0.40);
    }

    button[type="submit"]:active {
      transform: translateY(0);
      box-shadow: 0 6px 16px rgba(37, 99, 235, 0.32);
    }

    button[type="submit"]:focus-visible {
      outline: none;
      box-shadow: 0 0 0 4px rgba(147, 197, 253, 0.85), 0 8px 20px rgba(37, 99, 235, 0.35);
    }

    .footer {
      padding: 16px 22px 22px;
      border-top: 1px solid var(--card-border);
      color: var(--muted);
      font-size: 0.92rem;
      display: flex;
      align-items: center;
      gap: 10px;
      justify-content: space-between;
    }

    .tip {
      font-size: 0.9rem;
    }
  </style>
</head>
<body>
  <main class="card" aria-labelledby="title">
    <header class="header">
      <h1 class="title" id="title">Anonymous Feedback</h1>
      <p class="subtitle">Share honest complaints or suggestions to help improve the school experience—no name or email collected.</p>
    </header>

    <!-- Replace ACTION_URL with the Apps Script Web App URL -->
    <!-- target="_blank" opens the thank‑you page in a new tab -->
    <form action="https://script.google.com/macros/s/AKfycbyYHMqb337ImwMTu_5Qr1baOZ0IaunY5ekQzLlNGhaA2Gl7WsLUBcVx-ZtjUBt5vja5/exec" method="post" target="_blank">
      <div class="field">
        <label for="category">Category (optional)</label>
        <select id="category" name="category">
          <option>General</option>
          <option>Facilities</option>
          <option>Academics</option>
          <option>Safety</option>
          <option>Other</option>
        </select>
      </div>

      <div class="field">
        <label for="message">Message</label>
        <textarea id="message" name="message" required placeholder="Write feedback or a complaint…"></textarea>
        <p class="note">Avoid personal identifiers to keep this fully anonymous.</p>
      </div>

      <div class="actions">
        <button type="submit">Send Anonymously</button>
      </div>
    </form>

    <div class="footer">
      <span class="tip">Dark mode and reduced‑motion are supported automatically.</span>
    </div>
  </main>
</body>
</html>
