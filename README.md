[nefra_deep_dialogues.html](https://github.com/user-attachments/files/22608122/nefra_deep_dialogues.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Nefra — AI Perfume Muse (Deep Dialogues)</title>
  <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='32' cy='32' r='30' fill='%23000'/%3E%3Ctext x='32' y='40' text-anchor='middle' font-size='32' fill='white'%3EN%3C/text%3E%3C/svg%3E">
  <meta property="og:title" content="Nefra — AI Perfume Muse">
  <meta property="og:description" content="Clickable prototype with deep multi-turn dialogues.">
  <meta property="og:type" content="website">
  <!-- Tailwind (CDN) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- React 18 UMD + Babel -->
  <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>
<body class="bg-gradient-to-b from-[#0b0b0c] to-[#161618] text-gray-900">
  <div id="root"></div>

  <script type="text/babel">
    const { useEffect, useRef, useState } = React;

    // --- Deep multi-turn dialogue scripts (conversational)
    const SCRIPTS = {
      romantic: {
        label: "Romantic Mood",
        turns: [
          { user: "I want something romantic.", nefra: "Romance can whisper close to the skin or bloom into the room. Do you want something \\u003cb\\u003eintimate\\u003c/b\\u003e or more \\u003cb\\u003eexpressive\\u003c/b\\u003e?" },
          { user: "Intimate.", nefra: "Then I’ll keep projection soft and textures creamy. Let me share three shades of romance—each with price, performance, seasonality, gender positioning, and a layering tip." },
          { user: "", nefra: "\\u003cb\\u003e1) Maison Francis Kurkdjian À la Rose (EDP)\\u003c/b\\u003e\\n\\u2022 Price: ~€200 (70ml)  \\n\\u2022 Performance: 6–7h, soft sillage (skin-close)  \\n\\u2022 Seasonality: Spring/Summer evenings  \\n\\u2022 Gender: Marketed feminine, \\u003ci\\u003etruly unisex in wear\\u003c/i\\u003e  \\n\\u2022 Layering: Rose lotion or Amyris body oil to extend the glow  \\n\\n\\u003ci\\u003eFeels like silk sheets at dawn, dew on rose petals—tender, luminous, elegant.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e2) BDK Parfums Gris Charnel (EDP)\\u003c/b\\u003e\\n\\u2022 Price: ~€190 (100ml)  \\n\\u2022 Performance: 7–8h, discreet/moderate  \\n\\u2022 Seasonality: Autumn/Spring dinners  \\n\\u2022 Gender: Unisex  \\n\\u2022 Layering: Vanilla body cream to boost sandalwood creaminess  \\n\\n\\u003ci\\u003eFeels like fig skin and warm tea in a dim café—modern, sensual, slightly playful.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e3) Chanel Coromandel (Les Exclusifs, EDP)\\u003c/b\\u003e\\n\\u2022 Price: ~€295 (75ml)  \\n\\u2022 Performance: 8–10h, moderate/room-halo if oversprayed  \\n\\u2022 Seasonality: Autumn/Winter nights  \\n\\u2022 Gender: Marketed feminine, commonly worn by men (truly unisex)  \\n\\u2022 Layering: Amber/vanilla cream to soften patchouli  \\n\\n\\u003ci\\u003eFeels like velvet curtains and lacquered wood—patchouli smoothed by vanilla/benzoin; a cashmere shawl for the soul.\\u003c/i\\u003e" },
          { user: "Which is best for a dinner date?", nefra: "For \\u003cb\\u003etender intimacy\\u003c/b\\u003e choose Gris Charnel. For \\u003cb\\u003eelegant delicacy\\u003c/b\\u003e choose À la Rose. If you want to be \\u003cb\\u003eremembered\\u003c/b\\u003e, Coromandel wraps you in quiet opulence." }
        ]
      },

      warmNight: {
        label: "Warm Night",
        turns: [
          { user: "I want something warm for the night.", nefra: "Warm can mean an \\u003cb\\u003eamber-spicy glow\\u003c/b\\u003e, \\u003cb\\u003esmoky mystery\\u003c/b\\u003e, or \\u003cb\\u003eboozy sweetness\\u003c/b\\u003e. Do you imagine modern lounge elegance or a classic, powerful aura?" },
          { user: "Modern lounge elegance.", nefra: "Then consider three paths—each warm, refined, and night-ready." },
          { user: "", nefra: "\\u003cb\\u003e1) Parfums de Marly Herod\\u003c/b\\u003e\\n\\u2022 Price: ~€220 (125ml)  \\n\\u2022 Performance: 8–9h, moderate  \\n\\u2022 Seasonality: Autumn/Winter nights  \\n\\u2022 Gender: Marketed masculine, comfortably unisex  \\n\\u2022 Layering: Vanilla lotion to smooth tobacco nuances  \\n\\n\\u003ci\\u003eTobacco leaf wrapped in vanilla/cinnamon—like sipping spiced whisky by a fire.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e2) Amouage Interlude Black Iris\\u003c/b\\u003e\\n\\u2022 Price: ~€320 (100ml)  \\n\\u2022 Performance: 10–12h, strong  \\n\\u2022 Seasonality: Cool evenings, formal nights  \\n\\u2022 Gender: Masculine-marketed, often worn by women  \\n\\u2022 Layering: Woody body cream to tame the incense/leather  \\n\\n\\u003ci\\u003eSmoky amber with iris—mysterious, smooth, cathedral twilight in a bottle.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e3) Kilian Angels’ Share\\u003c/b\\u003e\\n\\u2022 Price: ~€195 (50ml)  \\n\\u2022 Performance: 7–8h, moderate  \\n\\u2022 Seasonality: Autumn festive nights  \\n\\u2022 Gender: Unisex  \\n\\u2022 Layering: Amber body cream to amplify the gourmand warmth  \\n\\n\\u003ci\\u003eCognac, cinnamon, praline—silky, edible warmth; candlelit dessert and conversation.\\u003c/i\\u003e" },
          { user: "Which is most elegant for lounge dining?", nefra: "For a \\u003cb\\u003esmooth modern glow\\u003c/b\\u003e choose Angels’ Share. For a \\u003cb\\u003eclassic, reassuring warmth\\u003c/b\\u003e choose Herod. For \\u003cb\\u003emysterious, commanding elegance\\u003c/b\\u003e choose Interlude Black Iris." }
        ]
      },

      freshWork: {
        label: "Fresh for Work",
        turns: [
          { user: "I need something fresh for work.", nefra: "Shall we keep it \\u003cb\\u003ediscreet and professional\\u003c/b\\u003e for close quarters, or \\u003cb\\u003efresh but dynamic\\u003c/b\\u003e for open spaces?" },
          { user: "Discreet and professional.", nefra: "Here are three office-perfect choices, each polished and respectful." },
          { user: "", nefra: "\\u003cb\\u003e1) Acqua di Parma Colonia Essenza\\u003c/b\\u003e\\n\\u2022 Price: ~€140 (100ml)  \\n\\u2022 Performance: ~6h, discreet  \\n\\u2022 Seasonality: Spring/Summer mornings  \\n\\u2022 Gender: Masculine-marketed, citrus-musk is unisex  \\n\\u2022 Layering: Citrus lotion to brighten the opening  \\n\\n\\u003ci\\u003eCitrus, neroli, woods—like a perfectly pressed white shirt.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e2) MFK Aqua Universalis Forte\\u003c/b\\u003e\\n\\u2022 Price: ~€215 (70ml)  \\n\\u2022 Performance: ~8h, polite  \\n\\u2022 Seasonality: Year-round; shines in spring/autumn  \\n\\u2022 Gender: Unisex  \\n\\u2022 Layering: Citrus shower gel underneath for extra sparkle  \\n\\n\\u003ci\\u003eClean laundry in a summer breeze—crisp, composed, impeccable.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e3) Creed Aventus Cologne\\u003c/b\\u003e\\n\\u2022 Price: ~€245 (100ml)  \\n\\u2022 Performance: 8–9h, moderate  \\n\\u2022 Seasonality: Spring/Autumn  \\n\\u2022 Gender: Masculine-marketed; modern unisex appeal  \\n\\u2022 Layering: Vetiver cream to emphasize the green facet  \\n\\n\\u003ci\\u003eJuicy mandarin, ginger, vetiver—dynamic, confident, but office-friendly.\\u003c/i\\u003e" },
          { user: "Which suits long days?", nefra: "For \\u003cb\\u003eendurance\\u003c/b\\u003e choose Aventus Cologne. For \\u003cb\\u003esubtle elegance\\u003c/b\\u003e choose Aqua Universalis Forte. For \\u003cb\\u003eclassic safe professionalism\\u003c/b\\u003e choose Colonia Essenza." }
        ]
      },

      discontinued: {
        label: "Plum Japonais Alternatives",
        turns: [
          { user: "My favourite, Tom Ford Plum Japonais, is discontinued.", nefra: "Plum Japonais was dark fruit with spice (plum, cinnamon), amber, and oud—bold projection. I’ll suggest three alternatives across smoky, tropical, and spicy-amber moods." },
          { user: "", nefra: "\\u003cb\\u003e1) Serge Lutens Fille en Aiguilles\\u003c/b\\u003e\\n\\u2022 Price: ~€180 (100ml)  \\n\\u2022 Performance: ~8h, strong  \\n\\u2022 Seasonality: Autumn/Winter nights  \\n\\u2022 Gender: Unisex  \\n\\u2022 Layering: Incense oil to deepen resins  \\n\\n\\u003ci\\u003ePlum with pine and spice—smokier, resinous; a forest at dusk after rain.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e2) Memo Tamarindo\\u003c/b\\u003e\\n\\u2022 Price: ~€230 (75ml)  \\n\\u2022 Performance: ~7h, moderate  \\n\\u2022 Seasonality: Spring/Summer evenings  \\n\\u2022 Gender: Unisex  \\n\\u2022 Layering: Sandalwood lotion for creamier drydown  \\n\\n\\u003ci\\u003eTropical fruit (pineapple) with cardamom—brighter, still opulent; golden dusk on the beach.\\u003c/i\\u003e" },
          { user: "", nefra: "\\u003cb\\u003e3) Masque Milano Tango\\u003c/b\\u003e\\n\\u2022 Price: ~€135 (35ml)  \\n\\u2022 Performance: 7–8h, moderate  \\n\\u2022 Seasonality: Evenings year-round  \\n\\u2022 Gender: Unisex  \\n\\u2022 Layering: Vanilla cream to heighten warmth  \\n\\n\\u003ci\\u003eAmber, cumin, benzoin—translates the spicy-amber soul of Plum Japonais in a smoother, intimate way.\\u003c/i\\u003e" },
          { user: "Which is closest in spirit?", nefra: "For \\u003cb\\u003eDNA proximity\\u003c/b\\u003e choose Fille en Aiguilles (smoky-plum). For a \\u003cb\\u003etropical reinterpretation\\u003c/b\\u003e choose Tamarindo. For a \\u003cb\\u003esmoother spicy-amber soul\\u003c/b\\u003e choose Tango." }
        ]
      },
    };

    // --- Helpers
    const uid = () => Math.random().toString(36).slice(2);

    function Bubble({ role, text }) {
      const isUser = role === "user";
      return (
        <div className={"w-full flex " + (isUser ? "justify-end" : "justify-start")}>
          <div
            className={
              "max-w-[80%] rounded-2xl px-4 py-3 shadow " +
              (isUser
                ? "bg-gray-900 text-white rounded-br-md"
                : "bg-[#fcfbf7] text-gray-900 border border-[#ece7df] rounded-bl-md")
            }
          >
            <p className="leading-relaxed whitespace-pre-line" dangerouslySetInnerHTML={{__html: text}}></p>
            <div className="mt-1 text-[10px] opacity-60 text-right">
              {isUser ? "You" : "Nefra"}
            </div>
          </div>
        </div>
      );
    }

    function NefraPrototype() {
      const [messages, setMessages] = useState([
        { id: uid(), role: "nefra", text: "Hello, I’m Nefra — your AI perfume muse. Tap a scenario below and I’ll guide you with deep, boutique-style advice." },
      ]);
      const [isPlaying, setIsPlaying] = useState(false);
      const logRef = useRef(null);

      useEffect(() => {
        if (logRef.current) {
          logRef.current.scrollTo({ top: logRef.current.scrollHeight, behavior: "smooth" });
        }
      }, [messages]);

      const sleep = (ms) => new Promise((r) => setTimeout(r, ms));

      const typewriterAppend = async (full) => {
        const id = uid();
        let current = "";
        setMessages((m) => [...m, { id, role: "nefra", text: current }]);
        for (const ch of full) {
          current += ch;
          setMessages((m) => m.map((msg) => (msg.id === id ? { ...msg, text: current } : msg)));
          await sleep(6);
        }
      };

      const playScript = async (key) => {
        if (isPlaying) return;
        setIsPlaying(true);
        const seq = SCRIPTS[key].turns;
        for (const t of seq) {
          if (t.user) setMessages((m) => [...m, { id: uid(), role: "user", text: t.user }]);
          await sleep(380);
          await typewriterAppend(t.nefra);
          await sleep(300);
        }
        setIsPlaying(false);
      };

      const reset = () => {
        setMessages([{ id: uid(), role: "nefra", text: "Hello, I’m Nefra — your AI perfume muse. Tap a scenario below and I’ll guide you with deep, boutique-style advice." }]);
      };

      return (
        <div className="min-h-screen w-full p-6">
          <div className="mx-auto max-w-3xl">
            {/* Header */}
            <div className="mb-4 flex items-center justify-between">
              <div className="flex items-center gap-3">
                <div className="h-10 w-10 rounded-2xl bg-gray-900 text-white grid place-items-center font-semibold">N</div>
                <div>
                  <h1 className="text-xl font-semibold text-white">Nefra — AI Perfume Muse</h1>
                  <p className="text-sm text-gray-300">Clickable prototype • deep multi-turn dialogues with prices, performance, seasonality, gender & layering</p>
                </div>
              </div>
              <button onClick={reset} className="px-3 py-2 rounded-xl bg-white border border-gray-200 text-sm shadow hover:shadow-md">Reset</button>
            </div>

            {/* Chat Card */}
            <div className="rounded-2xl bg-white shadow-lg border border-[#ece7df] overflow-hidden">
              <div ref={logRef} className="h-[60vh] overflow-y-auto p-4 space-y-3 bg-white">
                {messages.map((m) => (
                  <Bubble key={m.id} role={m.role} text={m.text} />
                ))}
              </div>

              {/* Controls */}
              <div className="border-t border-[#ece7df] p-4">
                <div className="grid grid-cols-2 md:grid-cols-4 gap-2">
                  {Object.entries(SCRIPTS).map(([key, cfg]) => (
                    <button
                      key={key}
                      onClick={() => playScript(key)}
                      disabled={isPlaying}
                      className={
                        "rounded-xl px-3 py-2 text-sm shadow " +
                        (isPlaying ? "bg-gray-100 text-gray-400 border border-gray-200" : "bg-gray-900 text-white hover:shadow-md")
                      }
                    >
                      {cfg.label}
                    </button>
                  ))}
                </div>
                <div className="mt-3 text-xs text-gray-500">
                  Tip: You can edit prices, names, and copy inside the <code>SCRIPTS</code> object above.
                </div>
              </div>
            </div>

            {/* Footer notes */}
            <div className="mt-6 text-[12px] text-gray-300">
              <p>Disclaimer: Prices are indicative EUR boutique pricing; performance varies by skin, weather, and application. Gender labels reflect marketing, not wearability.</p>
            </div>
          </div>
        </div>
      );
    }

    const root = ReactDOM.createRoot(document.getElementById("root"));
    root.render(<NefraPrototype />);
  </script>
</body>
</html>
