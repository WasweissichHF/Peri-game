<!DOCTYPE html>
<html lang="de">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PERI-SPIEL - Elo, Duell, Dark Mode</title>

    <style>

        body {
            font-family: system-ui, sans-serif;
            background: #fff8f0;
            text-align: center;
            padding: 12px;
            margin: 0;
            transition: background 0.3s, color 0.3s;
            color: #111;
        }

        body.dark {
            background: #121212;
            color: #fff;
        }

        body.dark h1,
        body.dark h2,
        body.dark h3,
        body.dark p,
        body.dark div,
        body.dark span,
        body.dark label {
            color: #fff !important;
        }

        body.dark #frage,
        body.dark #rangliste,
        body.dark #ende,
        body.dark #accountBox,
        body.dark #modusBox,
        body.dark #duellBox {
            background: #1e1e1e !important;
            color: #fff !important;
            border: 1px solid #333;
        }

        body.dark input {
            background: #2a2a2a !important;
            color: #fff !important;
            border-color: #555 !important;
        }

        body.dark input::placeholder {
            color: #aaa !important;
        }

        body.dark .langBtn {
            background: #2a2a2a !important;
            color: #fff !important;
            border-color: #555 !important;
        }

        body.dark .langBtn.aktiv {
            background: #fff !important;
            color: #111 !important;
        }

        body.dark .nameVorschlag {
            background: #333 !important;
            color: #fff !important;
        }

        body.dark .rang-row {
            border-color: #333 !important;
        }

        body.dark .tabBtn {
            background: #333 !important;
            color: #fff !important;
        }

        body.dark .tabBtn.aktiv {
            background: #fff !important;
            color: #111 !important;
        }

        h1 {
            font-size: 22px;
            margin: 6px;
        }

        #frage {
            font-size: 26px;
            font-weight: 800;
            background: white;
            padding: 14px;
            border-radius: 14px;
            color: #111;
        }

        #info {
            margin: 10px;
            font-size: 15px;
        }

        #fortschritt {
            height: 14px;
            background: #eee;
            border-radius: 10px;
            max-width: 700px;
            margin: 10px auto;
            overflow: hidden;
        }

        #balken {
            height: 100%;
            background: #22c55e;
            width: 0%;
            transition: width .3s;
        }

        #timerBox {
            font-size: 22px;
            font-weight: 900;
            margin: 8px;
        }

        #timerBox.schnell {
            color: #22c55e;
        }

        #timerBox.lamgsam {
            color: #ef4444;
        }

        #grid {
            display: grid;
            grid-template-columns: repeat(18, 1fr);
            gap: 4px;
            max-width: 700px;
            margin: 12px auto;
        }

        .el {
            aspect-ratio: 1 / 1;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 15px;
            font-weight: 800;
            border: 1px solid rgba(0, 0, 0, .1);
            color: #111;
        }

        .leer {
            background: transparent;
            border: none;
            cursor: default;
        }

        .alkali {
            background: #ff9a8a;
        }

        .erdalkali {
            background: #ffcf7a;
        }

        .uebergang {
            background: #ffe27a;
        }

        .metall {
            background: #a8d8a8;
        }

        .halbmetall {
            background: #7fcdbb;
        }

        .nichtmetall {
            background: #7ec8e3;
        }

        .halogen {
            background: #c3a6e0;
        }

        .edelgas {
            background: #f7b733;
        }

        .lanth {
            background: #f4a9c4;
        }

        .acti {
            background: #f28bb1;
        }

        .richtig {
            background: #22c55e !important;
            color: white !important;
        }

        .falsch {
            background: #ef4444 !important;
            color: white !important;
        }

        button {
            background: #1e1e3a;
            color: white;
            border: none;
            padding: 14px;
            border-radius: 12px;
            width: 100%;
            max-width: 700px;
            font-size: 18px;
            margin: 6px auto;
            display: block;
            cursor: pointer;
        }

        body.dark button {
            background: #333;
            border: 1px solid #555;
            color: #fff;
        }

        input {
            padding: 14px;
            border-radius: 12px;
            border: 1px solid #ccc;
            width: 100%;
            max-width: 700px;
            font-size: 18px;
            text-align: center;
            box-sizing: border-box;
        }

        #meldung {
            font-size: 19px;
            font-weight: 800;
            min-height: 28px;
        }

        #rangliste {
            background: white;
            border-radius: 16px;
            padding: 14px;
            max-width: 700px;
            margin: 12px auto;
            text-align: left;
            color: #111;
        }

        #rangliste h3 {
            margin: 0 0 8px;
            text-align: center;
        }

        .rang-row {
            display: flex;
            justify-content: space-between;
            padding: 6px 0;
            border-bottom: 1px solid #eee;
        }

        #ende {
            background: white;
            border-radius: 16px;
            padding: 20px;
            max-width: 700px;
            margin: 12px auto;
            display: none;
            color: #111;
        }

        .langBtn {
            background: white !important;
            color: #1e1e3a !important;
            border: 2px solid #1e1e3a !important;
            width: auto !important;
            display: inline-block !important;
            padding: 8px 16px !important;
            font-size: 16px !important;
            margin: 4px !important;
        }

        .langBtn.aktiv {
            background: #1e1e3a !important;
            color: white !important;
        }

        .modusBtn {
            width: auto !important;
            display: inline-block !important;
            padding: 10px 18px !important;
            margin: 4px !important;
            background: #666 !important;
        }

        .modusBtn.aktiv {
            background: #22c55e !important;
        }

        .nameVorschlag {
            background: #e0f2fe !important;
            color: #1e1e3a !important;
            width: auto !important;
            display: inline-block !important;
            padding: 8px 14px !important;
            font-size: 15px !important;
            margin: 4px !important;
        }

        .box {
            background: white;
            border-radius: 16px;
            padding: 14px;
            max-width: 700px;
            margin: 12px auto;
            color: #111;
        }

        .tabBtn {
            width: 48% !important;
            display: inline-block !important;
            background: #ddd !important;
            color: #111 !important;
        }

        .tabBtn.aktiv {
            background: #1e1e3a !important;
            color: white !important;
        }

        #countdownOverlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            color: white;
            z-index: 999;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }

        #countdownZahl {
            font-size: 120px;
            font-weight: 900;
        }

    </style>
</head>

<body>

    <div id="countdownOverlay">
        <div id="countdownTitel" style="font-size: 24px;">DUELL STARTET IN</div>
        <div id="countdownZahl">3</div>
        <div id="countdownText" style="font-size: 18px;">Mach dich bereit!</div>
    </div>

    <h1>
        PERI-SPIEL ⚛️
    </h1>

    <div>
        <button class="langBtn aktiv" id="btnDE" onclick="setLang('de')">
            Deutsch
        </button>

        <button class="langBtn" id="btnEN" onclick="setLang('en')">
            English
        </button>

        <button class="langBtn" id="btnDark" onclick="toggleDark()">
            🌙 Dark Mode
        </button>
    </div>

    <div id="accountBox" class="box">

        <h2 style="margin: 0;" id="willkommenTitel">
            Willkommen! 👋
        </h2>

        <p id="accountText">
            Erstelle einen Account oder spiel als Gast!
        </p>

        <div>
            <button class="tabBtn aktiv" id="tabLogin" onclick="zeigeTab('login')">
                Einloggen
            </button>

            <button class="tabBtn" id="tabReg" onclick="zeigeTab('reg')">
                Account erstellen
            </button>
        </div>

        <div id="loginForm" style="margin-top: 10px;">

            <input id="loginName" placeholder="Benutzername" maxlength="20">

            <br>
            <br>

            <input id="loginPass" placeholder="Passwort" type="password">

            <br>
            <br>

            <button id="loginBtn" onclick="einloggen()">
                Einloggen ✅
            </button>

            <p id="loginStatus" style="font-weight: 700; font-size: 14px;"></p>

        </div>

        <div id="regForm" style="display: none; margin-top: 10px;">

            <input id="regName" placeholder="Neuer Benutzername" maxlength="20">

            <br>
            <br>

            <input id="regPass" placeholder="Passwort wählen (min. 4 Zeichen)" type="password">

            <br>
            <br>

            <p style="font-size: 14px; font-weight: 700;" id="vorschlaegeTitel">
                Vorschläge für dich:
            </p>

            <div id="vorschlaege"></div>

            <button id="neueVorschlaegeBtn" onclick="neueVorschlaege()">
                🔄 Neue Vorschläge
            </button>

            <button id="regBtn" onclick="registrieren()" style="background: #22c55e;">
                Account erstellen ✨
            </button>

            <p id="regStatus" style="font-weight: 700; font-size: 14px;"></p>

        </div>

        <hr>

        <button id="gastBtn" onclick="alsGast()" style="background: #f59e0b;">
            👤 Als Gast spielen (ohne Account)
        </button>

        <p style="font-size: 13px;" id="gastHinweis">
            Als Gast wird dein Elo NICHT gespeichert. Mit Account kannst du dich überall einloggen!
        </p>

        <button onclick="ausloggen()" id="logoutBtn" style="display: none; background: #ef4444;">
            Ausloggen
        </button>

    </div>

    <div id="modusBox" style="display: none;">

        <p style="font-size: 18px; font-weight: 700;" id="modusTitel">
            Welchen Modus willst du?
        </p>

        <button class="modusBtn aktiv" id="btnModusName" onclick="setModus('name')">
            🏷️ Name -> Zahl finden
        </button>

        <button class="modusBtn" id="btnModusZahl" onclick="setModus('zahl')">
            🔢 Zahl -> Element finden
        </button>

        <button id="soloBtn" onclick="startSolo()">
            ▶️ Solo spielen (Elo)
        </button>

        <button id="duellModusBtn" onclick="zeigeDuell()" style="background: #7c3aed;">
            ⚔️ Duell-Modus
        </button>

    </div>

    <div id="duellBox" class="box" style="display: none;">

        <h2 id="duellTitel">
            ⚔️ DUELL - 2 Minuten, gleichzeitig!
        </h2>

        <p id="duellBeschreibung">
            Fordere jemanden heraus! Ihr startet gleichzeitig mit 3,2,1 LOS!
            Wer in 2 Minuten mehr richtig hat, gewinnt +25 Elo!
            Verlierer -25 Elo!
        </p>

        <input id="gegnerInput" placeholder="Name vom Gegner (genau wie im Spiel)">

        <button id="herausfordernBtn" onclick="herausfordern()">
            Herausfordern ⚔️
        </button>

        <p id="duellStatus"></p>

        <hr>

        <h3 id="offeneTitel">📩 Offene Herausforderungen für dich:</h3>

        <div id="eingehendeDuellBox">
            Keine offenen Herausforderungen.
        </div>

        <button id="duellAktualisierenBtn" onclick="ladeEingehendeDuell()" style="padding: 8px; font-size: 14px; background: #666;">
            🔄 Aktualisieren
        </button>

        <hr>

        <button id="duellZurueckBtn" onclick="zurueckZumModus()" style="background: #666;">
            ⬅️ Zurück
        </button>

    </div>

    <div id="spielBox" style="display: none;">

        <div id="frage">
            Laedt...
        </div>

        <div id="timerBox">
            ⏱️ <span id="timerText">15</span>s
        </div>

        <div id="fortschritt">
            <div id="balken"></div>
        </div>

        <div id="meldung"></div>

        <div id="info"></div>

        <div id="grid"></div>

        <button id="weiterBtn" onclick="weiter()">
            Naechste Frage
        </button>

        <button onclick="neustart()" id="neustartBtn">
            Neues Spiel
        </button>

        <button id="beendenBtn" onclick="durchlaufBeenden()" style="background: #ef4444;">
            ⏹️ Durchlauf beenden
        </button>

        <div id="ende"></div>

    </div>

    <div id="rangliste">

        <h3 id="rangTitel">
            🏆 Elo-Rangliste - Top 10
        </h3>

        <div id="ranglisteInhalt">
            Laedt Rangliste...
        </div>

        <button onclick="ladeRangliste()" style="padding: 8px; font-size: 14px;" id="aktualisierenBtn">
            Aktualisieren
        </button>

    </div>

    <script>

        // ================= DARK MODE =================

        function toggleDark() {
            document.body.classList.toggle('dark');

            try {
                localStorage.setItem('periDark', document.body.classList.contains('dark') ? '1' : '0');
            } catch (e) {}
        }

        try {
            if (localStorage.getItem('periDark') === '1') {
                document.body.classList.add('dark');
            }
        } catch (e) {}

        // ================= SPRACHE - JETZT ALLES ÜBERSETZT! =================

        let lang = 'de';

        try {
            lang = localStorage.getItem('periLang') || 'de';
        } catch (e) {}

        const TEXTE = {

            de: {
                woIst: "Wo ist ",
                frageZeichen: " ?",
                findeZahl: "Finde das Element mit der Ordnungszahl ",
                ausrufe: " !",
                naechste: "Naechste Frage",
                neustart: "Neues Spiel",
                beenden: "⏹️ Durchlauf beenden",
                haupt: "Hauptrunde",
                wiederholung: "WIEDERHOLUNG",
                wiederholungMsg: "Wiederholungsrunde! Jetzt deine Fehler nochmal!",
                hallo: "Hallo ",
                punkte: "Punkte",
                fehler: "Fehler",
                zumWiederholen: "Zum Wiederholen",
                rekord: "Rekord",
                deinRekord: "Dein Rekord",
                frageVon: "Frage",
                von: "von",
                richtig: "RICHTIG! ",
                ist: " ist ",
                falsch: "Falsch! Das war ",
                klickRichtig: ". Klick jetzt das Richtige!",
                erstRichtig: "Erst das Richtige anklicken!",
                fertig: "FERTIG!",
                neuerRekord: "NEUER REKORD!",
                stark: "Stark gespielt, ",
                deinePunkte: "Deine Punkte",
                hochgeladen: "Dein Elo wurde gespeichert!",
                rangTitel: "🏆 Elo-Rangliste - Top 10",
                aktualisieren: "Aktualisieren",
                keineEintraege: "Noch keiner da - sei der Erste! 🔥",
                fehlerLaden: "Rangliste konnte nicht geladen werden.",
                du: " - DU",
                alleGeschafft: "Du hast alle Elemente + Wiederholungen geschafft.",
                // NEU: UI Übersetzungen
                willkommen: "Willkommen! 👋",
                accountText: "Erstelle einen Account oder spiel als Gast!",
                einloggenTab: "Einloggen",
                regTab: "Account erstellen",
                loginNamePh: "Benutzername",
                loginPassPh: "Passwort",
                loginBtn: "Einloggen ✅",
                regNamePh: "Neuer Benutzername",
                regPassPh: "Passwort wählen (min. 4 Zeichen)",
                vorschlaegeTitel: "Vorschläge für dich:",
                neueVorschlaege: "🔄 Neue Vorschläge",
                regBtn: "Account erstellen ✨",
                gastBtn: "👤 Als Gast spielen (ohne Account)",
                gastHinweis: "Als Gast wird dein Elo NICHT gespeichert. Mit Account kannst du dich überall einloggen!",
                logoutBtn: "Ausloggen",
                modusTitel: "Welchen Modus willst du?",
                modusName: "🏷️ Name -> Zahl finden",
                modusZahl: "🔢 Zahl -> Element finden",
                soloBtn: "▶️ Solo spielen (Elo)",
                duellModusBtn: "⚔️ Duell-Modus",
                duellTitel: "⚔️ DUELL - 2 Minuten, gleichzeitig!",
                duellBeschreibung: "Fordere jemanden heraus! Ihr startet gleichzeitig mit 3,2,1 LOS! Wer in 2 Minuten mehr richtig hat, gewinnt +25 Elo! Verlierer -25 Elo!",
                gegnerPh: "Name vom Gegner (genau wie im Spiel)",
                herausfordernBtn: "Herausfordern ⚔️",
                offeneTitel: "📩 Offene Herausforderungen für dich:",
                keineHerausforderung: "Keine offenen Herausforderungen.",
                duellAktualisieren: "🔄 Aktualisieren",
                duellZurueck: "⬅️ Zurück",
                darkMode: "🌙 Dark Mode",
                zuLangsam: "⏰ ZU LANGSAM! Kein Elo für diese Frage!",
                gastText: " 👤 GAST (Elo wird nicht gespeichert)",
                schonGruen: "Schon grün: ",
                duellVs: "⚔️ DUELL vs ",
                duellRichtig: "Richtig: ",
                duellPunkteLabel: "Punkte: ",
                countdownTitel: "DUELL STARTET IN",
                countdownBereit: "Mach dich bereit!",
                countdownGegner: "Gegner gefunden! Gleich geht es los!",
                zeitUmTitel: "⏰ ZEIT UM! 2 Minuten vorbei!",
                warteAuf: "Warte auf ",
                duHastRichtig: "Du hast ",
                richtigAusrufe: " richtig!",
                duellVorbei: "⚔️ DUELL VORBEI!",
                duGewonnen: "🏆 DU HAST GEWONNEN!",
                duVerloren: " HAT GEWONNEN!",
                unentschieden: "🤝 UNENTSCHIEDEN!",
                duBekommst: "Du bekommst +25 Elo! 😈 Dein neues Elo: ",
                duVerlierst: "Du verlierst 25 Elo! Dein neues Elo: ",
                keinerBekommt: "Keiner bekommt Elo. Dein Elo bleibt: ",
                zurueckMenu: "Zurück zum Menü",
                gastEnde: "Als Gast wurde dein Elo NICHT gespeichert. Mach einen Account, um es zu speichern!"
            },

            en: {
                woIst: "Where is ",
                frageZeichen: " ?",
                findeZahl: "Find the element with atomic number ",
                ausrufe: " !",
                naechste: "Next question",
                neustart: "New game",
                beenden: "⏹️ End run",
                haupt: "Main round",
                wiederholung: "REVIEW",
                wiederholungMsg: "Review round! Now your mistakes again!",
                hallo: "Hello ",
                punkte: "Points",
                fehler: "Mistakes",
                zumWiederholen: "To review",
                rekord: "Record",
                deinRekord: "Your record",
                frageVon: "Question",
                von: "of",
                richtig: "CORRECT! ",
                ist: " is ",
                falsch: "Wrong! That was ",
                klickRichtig: ". Now click the correct one!",
                erstRichtig: "Click the correct one first!",
                fertig: "DONE!",
                neuerRekord: "NEW RECORD!",
                stark: "Well played, ",
                deinePunkte: "Your points",
                hochgeladen: "Your Elo was saved!",
                rangTitel: "🏆 Elo Leaderboard - Top 10",
                aktualisieren: "Refresh",
                keineEintraege: "Nobody yet - be the first! 🔥",
                fehlerLaden: "Could not load leaderboard.",
                du: " - YOU",
                alleGeschafft: "You completed all elements + reviews.",
                // NEU: UI Übersetzungen - ALLES!
                willkommen: "Welcome! 👋",
                accountText: "Create an account or play as guest!",
                einloggenTab: "Log in",
                regTab: "Create account",
                loginNamePh: "Username",
                loginPassPh: "Password",
                loginBtn: "Log in ✅",
                regNamePh: "New username",
                regPassPh: "Choose password (min. 4 chars)",
                vorschlaegeTitel: "Suggestions for you:",
                neueVorschlaege: "🔄 New suggestions",
                regBtn: "Create account ✨",
                gastBtn: "👤 Play as guest (no account)",
                gastHinweis: "As a guest your Elo will NOT be saved. With an account you can log in anywhere!",
                logoutBtn: "Log out",
                modusTitel: "Which mode do you want?",
                modusName: "🏷️ Name -> Find number",
                modusZahl: "🔢 Number -> Find element",
                soloBtn: "▶️ Play Solo (Elo)",
                duellModusBtn: "⚔️ Duel Mode",
                duellTitel: "⚔️ DUEL - 2 minutes, at the same time!",
                duellBeschreibung: "Challenge someone! You both start at the same time with 3,2,1 GO! Whoever gets more correct in 2 minutes wins +25 Elo! Loser -25 Elo!",
                gegnerPh: "Opponent name (exactly as in game)",
                herausfordernBtn: "Challenge ⚔️",
                offeneTitel: "📩 Open challenges for you:",
                keineHerausforderung: "No open challenges.",
                duellAktualisieren: "🔄 Refresh",
                duellZurueck: "⬅️ Back",
                darkMode: "🌙 Dark Mode",
                zuLangsam: "⏰ TOO SLOW! No Elo for this question!",
                gastText: " 👤 GUEST (Elo will not be saved)",
                schonGruen: "Already green: ",
                duellVs: "⚔️ DUEL vs ",
                duellRichtig: "Correct: ",
                duellPunkteLabel: "Points: ",
                countdownTitel: "DUEL STARTS IN",
                countdownBereit: "Get ready!",
                countdownGegner: "Opponent found! Starting soon!",
                zeitUmTitel: "⏰ TIME UP! 2 minutes over!",
                warteAuf: "Waiting for ",
                duHastRichtig: "You got ",
                richtigAusrufe: " correct!",
                duellVorbei: "⚔️ DUEL OVER!",
                duGewonnen: "🏆 YOU WON!",
                duVerloren: " WON!",
                unentschieden: "🤝 DRAW!",
                duBekommst: "You get +25 Elo! 😈 Your new Elo: ",
                duVerlierst: "You lose 25 Elo! Your new Elo: ",
                keinerBekommt: "Nobody gets Elo. Your Elo stays: ",
                zurueckMenu: "Back to menu",
                gastEnde: "As a guest your Elo was NOT saved. Make an account to save it!"
            }

        };

        function t(key) {
            return TEXTE[lang][key] || key;
        }

        function setLang(neu) {

            lang = neu;

            try {
                localStorage.setItem('periLang', lang);
            } catch (e) {}

            document.getElementById('btnDE').classList.toggle('aktiv', lang === 'de');
            document.getElementById('btnEN').classList.toggle('aktiv', lang === 'en');

            // Spiel-Buttons
            document.getElementById('weiterBtn').textContent = t('naechste');
            document.getElementById('neustartBtn').textContent = t('neustart');
            document.getElementById('beendenBtn').textContent = t('beenden');
            document.getElementById('rangTitel').textContent = t('rangTitel');
            document.getElementById('aktualisierenBtn').textContent = t('aktualisieren');

            // NEU: ALLE UI-Elemente übersetzen!
            document.getElementById('willkommenTitel').textContent = t('willkommen');
            document.getElementById('accountText').textContent = t('accountText');
            document.getElementById('tabLogin').textContent = t('einloggenTab');
            document.getElementById('tabReg').textContent = t('regTab');
            document.getElementById('loginName').placeholder = t('loginNamePh');
            document.getElementById('loginPass').placeholder = t('loginPassPh');
            document.getElementById('loginBtn').textContent = t('loginBtn');
            document.getElementById('regName').placeholder = t('regNamePh');
            document.getElementById('regPass').placeholder = t('regPassPh');
            document.getElementById('vorschlaegeTitel').textContent = t('vorschlaegeTitel');
            document.getElementById('neueVorschlaegeBtn').textContent = t('neueVorschlaege');
            document.getElementById('regBtn').textContent = t('regBtn');
            document.getElementById('gastBtn').textContent = t('gastBtn');
            document.getElementById('gastHinweis').textContent = t('gastHinweis');
            document.getElementById('logoutBtn').textContent = t('logoutBtn');
            document.getElementById('modusTitel').textContent = t('modusTitel');
            document.getElementById('btnModusName').textContent = t('modusName');
            document.getElementById('btnModusZahl').textContent = t('modusZahl');
            document.getElementById('soloBtn').textContent = t('soloBtn');
            document.getElementById('duellModusBtn').textContent = t('duellModusBtn');
            document.getElementById('duellTitel').textContent = t('duellTitel');
            document.getElementById('duellBeschreibung').textContent = t('duellBeschreibung');
            document.getElementById('gegnerInput').placeholder = t('gegnerPh');
            document.getElementById('herausfordernBtn').textContent = t('herausfordernBtn');
            document.getElementById('offeneTitel').textContent = t('offeneTitel');
            document.getElementById('duellAktualisierenBtn').textContent = t('duellAktualisieren');
            document.getElementById('duellZurueckBtn').textContent = t('duellZurueck');
            document.getElementById('btnDark').textContent = t('darkMode');
            document.getElementById('countdownTitel').textContent = t('countdownTitel');
            document.getElementById('countdownText').textContent = t('countdownBereit');

            // Wenn keine Herausforderungen da sind, Text auch übersetzen
            let eingehendeBox = document.getElementById('eingehendeDuellBox');
            if (eingehendeBox && eingehendeBox.textContent.trim() === "Keine offenen Herausforderungen." || eingehendeBox.textContent.trim() === "No open challenges.") {
                eingehendeBox.textContent = t('keineHerausforderung');
            }

            if (ziel) {
                zeigeFrage();
            }

            updateInfo(phase === "wiederholung" ? t('wiederholung') : t('haupt'));
            ladeRangliste();

        }

        const EN_NAMEN = {
            1: "Hydrogen",
            2: "Helium",
            3: "Lithium",
            4: "Beryllium",
            5: "Boron",
            6: "Carbon",
            7: "Nitrogen",
            8: "Oxygen",
            9: "Fluorine",
            10: "Neon",
            11: "Sodium",
            12: "Magnesium",
            13: "Aluminium",
            14: "Silicon",
            15: "Phosphorus",
            16: "Sulfur",
            17: "Chlorine",
            18: "Argon",
            19: "Potassium",
            20: "Calcium",
            21: "Scandium",
            22: "Titanium",
            23: "Vanadium",
            24: "Chromium",
            25: "Manganese",
            26: "Iron",
            27: "Cobalt",
            28: "Nickel",
            29: "Copper",
            30: "Zinc",
            31: "Gallium",
            32: "Germanium",
            33: "Arsenic",
            34: "Selenium",
            35: "Bromine",
            36: "Krypton",
            37: "Rubidium",
            38: "Strontium",
            39: "Yttrium",
            40: "Zirconium",
            41: "Niobium",
            42: "Molybdenum",
            43: "Technetium",
            44: "Ruthenium",
            45: "Rhodium",
            46: "Palladium",
            47: "Silver",
            48: "Cadmium",
            49: "Indium",
            50: "Tin",
            51: "Antimony",
            52: "Tellurium",
            53: "Iodine",
            54: "Xenon",
            55: "Caesium",
            56: "Barium",
            57: "Lanthanum",
            58: "Cerium",
            59: "Praseodymium",
            60: "Neodymium",
            61: "Promethium",
            62: "Samarium",
            63: "Europium",
            64: "Gadolinium",
            65: "Terbium",
            66: "Dysprosium",
            67: "Holmium",
            68: "Erbium",
            69: "Thulium",
            70: "Ytterbium",
            71: "Lutetium",
            72: "Hafnium",
            73: "Tantalum",
            74: "Tungsten",
            75: "Rhenium",
            76: "Osmium",
            77: "Iridium",
            78: "Platinum",
            79: "Gold",
            80: "Mercury",
            81: "Thallium",
            82: "Lead",
            83: "Bismuth",
            84: "Polonium",
            85: "Astatine",
            86: "Radon",
            87: "Francium",
            88: "Radium",
            89: "Actinium",
            90: "Thorium",
            91: "Protactinium",
            92: "Uranium",
            93: "Neptunium",
            94: "Plutonium",
            95: "Americium",
            96: "Curium",
            97: "Berkelium",
            98: "Californium",
            99: "Einsteinium",
            100: "Fermium",
            101: "Mendelevium",
            102: "Nobelium",
            103: "Lawrencium",
            104: "Rutherfordium",
            105: "Dubnium",
            106: "Seaborgium",
            107: "Bohrium",
            108: "Hassium",
            109: "Meitnerium",
            110: "Darmstadtium",
            111: "Roentgenium",
            112: "Copernicium",
            113: "Nihonium",
            114: "Flerovium",
            115: "Moscovium",
            116: "Livermorium",
            117: "Tennessine",
            118: "Oganesson"
        };

        function elementName(el) {
            return lang === 'en' ? (EN_NAMEN[el[0]] || el[2]) : el[2];
        }

        // ================= MOCKAPI - NUR 1 RESOURCE =================

        const MOCKAPI_URL = "https://6b071ccc57fa1297bb56cb2e.mockapi.io/Leaderboard";

        let username = "";
        let elo = 1000;
        let istGast = false;
        let eingeloggt = false;

        function hashPass(p) {
            let h = 0;

            for (let i = 0; i < p.length; i++) {
                h = (h * 31 + p.charCodeAt(i)) >>> 0;
            }

            return "h" + h.toString(36);
        }

        function holeLokaleUsers() {
            try {
                let raw = localStorage.getItem('periUsers');
                if (!raw) {
                    return [];
                }
                return JSON.parse(raw);
            } catch (e) {
                return [];
            }
        }

        function speichereLokaleUsers(users) {
            try {
                localStorage.setItem('periUsers', JSON.stringify(users));
            } catch (e) {}
        }

        function direktEinloggen(name, eloWert) {
            username = name;
            elo = eloWert || 1000;
            istGast = false;
            eingeloggt = true;

            try {
                localStorage.setItem('periUsername', username);
                localStorage.setItem('periElo', String(elo));
            } catch (e) {}

            document.getElementById('accountBox').style.display = 'none';
            document.getElementById('modusBox').style.display = 'block';
            document.getElementById('logoutBtn').style.display = 'block';
        }

        function zeigeTab(welcher) {

            document.getElementById('loginForm').style.display = welcher === 'login' ? 'block' : 'none';
            document.getElementById('regForm').style.display = welcher === 'reg' ? 'block' : 'none';

            document.getElementById('tabLogin').classList.toggle('aktiv', welcher === 'login');
            document.getElementById('tabReg').classList.toggle('aktiv', welcher === 'reg');

            if (welcher === 'reg') {
                neueVorschlaege();
            }

        }

        async function registrieren() {

            let n = document.getElementById('regName').value.trim();
            let p = document.getElementById('regPass').value;

            if (!n) {
                alert(lang === 'en' ? "Please enter a name!" : "Bitte Name eingeben!");
                return;
            }

            if (p.length < 4) {
                alert(lang === 'en' ? "Password must be at least 4 characters!" : "Passwort muss mindestens 4 Zeichen haben!");
                return;
            }

            document.getElementById('regStatus').textContent = lang === 'en' ? "Creating account... ⏳" : "Account wird erstellt... ⏳";

            let lokaleUsers = holeLokaleUsers();

            if (lokaleUsers.find(u => u.name.toLowerCase() === n.toLowerCase())) {
                document.getElementById('regStatus').textContent = lang === 'en' ? "❌ Name already taken!" : "❌ Name schon vergeben! Nimm einen anderen!";
                return;
            }

            lokaleUsers.push({
                name: n,
                pass: hashPass(p),
                elo: 1000
            });

            speichereLokaleUsers(lokaleUsers);

            fetch(MOCKAPI_URL, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    type: "user",
                    name: n,
                    pass: hashPass(p),
                    elo: 1000,
                    punkte: 0,
                    fehler: 0
                })
            }).catch(e => {});

            document.getElementById('regStatus').textContent = lang === 'en' ? "✅ Account created! Logging you in..." : "✅ Account erstellt! Du wirst eingeloggt...";

            setTimeout(function() {
                direktEinloggen(n, 1000);
                alert(lang === 'en' ? "Welcome, " + n + "! You are now logged in! 🏆" : "Willkommen, " + n + "! Du bist jetzt eingeloggt! 🏆");
            }, 500);

        }

        async function einloggen() {

            let n = document.getElementById('loginName').value.trim();
            let p = document.getElementById('loginPass').value;

            if (!n || !p) {
                alert(lang === 'en' ? "Enter name and password!" : "Name und Passwort eingeben!");
                return;
            }

            document.getElementById('loginStatus').textContent = lang === 'en' ? "Logging in... ⏳" : "Logge ein... ⏳";

            let lokaleUsers = holeLokaleUsers();
            let user = lokaleUsers.find(u => u.name.toLowerCase() === n.toLowerCase());

            if (!user) {
                try {
                    let r = await fetch(MOCKAPI_URL);
                    let alle = await r.json();
                    let cloudUser = alle.find(u => u.type === "user" && u.name && u.name.toLowerCase() === n.toLowerCase());

                    if (cloudUser) {
                        user = cloudUser;
                        lokaleUsers.push(cloudUser);
                        speichereLokaleUsers(lokaleUsers);
                    }
                } catch (e) {}
            }

            if (!user) {
                document.getElementById('loginStatus').textContent = lang === 'en' ? "❌ Account not found! Create it first!" : "❌ Account nicht gefunden! Erst erstellen!";
                return;
            }

            if (user.pass !== hashPass(p)) {
                document.getElementById('loginStatus').textContent = lang === 'en' ? "❌ Wrong password!" : "❌ Falsches Passwort!";
                return;
            }

            direktEinloggen(user.name, Number(user.elo) || 1000);

            alert(lang === 'en' ? "Welcome back, " + user.name + "! Your Elo: " + elo + " 🏆" : "Willkommen zurück, " + user.name + "! Dein Elo: " + elo + " 🏆");

        }

        function alsGast() {

            username = "Gast" + Math.floor(100 + Math.random() * 900);
            if (lang === 'en') {
                username = "Guest" + Math.floor(100 + Math.random() * 900);
            }
            elo = 1000;
            istGast = true;
            eingeloggt = false;

            document.getElementById('accountBox').style.display = 'none';
            document.getElementById('modusBox').style.display = 'block';

            alert(lang === 'en' ? "You play as " + username + "! Your Elo will NOT be saved. With an account it will!" : "Du spielst als " + username + "! Dein Elo wird NICHT gespeichert. Mit Account schon!");

        }

        function ausloggen() {

            username = "";
            elo = 1000;
            istGast = false;
            eingeloggt = false;

            try {
                localStorage.removeItem('periUsername');
            } catch (e) {}

            document.getElementById('accountBox').style.display = 'block';
            document.getElementById('modusBox').style.display = 'none';
            document.getElementById('spielBox').style.display = 'none';
            document.getElementById('duellBox').style.display = 'none';
            document.getElementById('logoutBtn').style.display = 'none';

            stoppeDuellPolling();

        }

        function speichereElo() {

            try {
                localStorage.setItem('periElo', String(elo));
            } catch (e) {}

            if (username && !istGast) {
                let users = holeLokaleUsers();
                let u = users.find(x => x.name === username);
                if (u) {
                    u.elo = elo;
                    speichereLokaleUsers(users);
                }
            }

        }

        // ================= NAMENS-VORSCHLÄGE =================

        const VOR_NAMEN = [
            "Shadow", "Quantum", "Neon", "Turbo",
            "Cosmic", "Hyper", "Pixel", "Blitz",
            "Nitro", "Ghost", "Atomic", "Lunar",
            "Solar", "Vortex", "Phantom", "Rocket",
            "Cyber", "Mega"
        ];

        const VOR_TIERE = [
            "Fox", "Wolf", "Tiger", "Dragon",
            "Eagle", "Shark", "Lion", "Falcon",
            "Viper", "Rex", "Bear", "Hawk",
            "Panda", "Cobra"
        ];

        async function neueVorschlaege() {

            let vorschlaege = [];

            while (vorschlaege.length < 3) {
                let n = VOR_NAMEN[Math.floor(Math.random() * VOR_NAMEN.length)];
                let t = VOR_TIERE[Math.floor(Math.random() * VOR_TIERE.length)];
                let z = Math.floor(10 + Math.random() * 90);
                let name = n + t + z;

                if (!vorschlaege.includes(name)) {
                    vorschlaege.push(name);
                }
            }

            document.getElementById('vorschlaege').innerHTML = vorschlaege.map(n =>
                '<button class="nameVorschlag" onclick="waehleName(\'' + n + '\')">' + n + '</button>'
            ).join('');

        }

        function waehleName(n) {
            document.getElementById('regName').value = n;
        }

        // ================= MODUS =================

        let modus = "name";
        let spielModus = "solo";

        function setModus(m) {
            modus = m;
            document.getElementById('btnModusName').classList.toggle('aktiv', m === 'name');
            document.getElementById('btnModusZahl').classList.toggle('aktiv', m === 'zahl');
        }

        function startSolo() {
            spielModus = "solo";
            document.getElementById('modusBox').style.display = 'none';
            document.getElementById('duellBox').style.display = 'none';
            document.getElementById('spielBox').style.display = 'block';
            neustart();
        }

        function zurueckZumModus() {
            document.getElementById('duellBox').style.display = 'none';
            document.getElementById('modusBox').style.display = 'block';
            stoppeDuellPolling();
        }

        function zeigeDuell() {
            document.getElementById('modusBox').style.display = 'none';
            document.getElementById('duellBox').style.display = 'block';
            ladeEingehendeDuell();
            starteDuellPolling();
        }

        // ================= DUELL-SYSTEM - GLEICHZEITIG, 2 MINUTEN =================

        let aktuellesDuellId = null;
        let aktuellesDuell = null;
        let gegnerName = "";
        let duellPollInterval = null;
        let duellCountdownLaeuft = false;
        let duellGestartet = false;
        let duellMeineRichtigen = 0;
        let duellMeineFehler = 0;
        let duellErgebnisGezeigt = false;

        function starteDuellPolling() {
            stoppeDuellPolling();
            duellPollInterval = setInterval(function() {
                if (aktuellesDuellId) {
                    checkeDuellStatus();
                } else {
                    ladeEingehendeDuell();
                }
            }, 2000);
        }

        function stoppeDuellPolling() {
            if (duellPollInterval) {
                clearInterval(duellPollInterval);
                duellPollInterval = null;
            }
        }

        async function herausfordern() {

            gegnerName = document.getElementById('gegnerInput').value.trim();

            if (!gegnerName) {
                alert(lang === 'en' ? "Enter the opponent name!" : "Gib den Namen vom Gegner ein!");
                return;
            }

            if (gegnerName.toLowerCase() === username.toLowerCase()) {
                alert(lang === 'en' ? "You can't challenge yourself!" : "Du kannst dich nicht selbst herausfordern!");
                return;
            }

            document.getElementById('duellStatus').textContent = lang === 'en' ? "Sending challenge... ⏳" : "Herausforderung wird geschickt... ⏳";

            try {
                let r = await fetch(MOCKAPI_URL, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        type: "duell",
                        challenger: username,
                        opponent: gegnerName,
                        status: "wartet",
                        startZeit: 0,
                        challengerScore: -1,
                        opponentScore: -1,
                        challengerRichtig: 0,
                        opponentRichtig: 0,
                        erstelltAm: Date.now()
                    })
                });

                let neu = await r.json();
                aktuellesDuellId = neu.id;
                aktuellesDuell = neu;

                document.getElementById('duellStatus').textContent = lang === 'en' ? "✅ Challenge sent to " + gegnerName + "! Wait until he accepts... (keep this page open!)" : "✅ Herausforderung an " + gegnerName + " geschickt! Warte bis er annimmt... (Seite offen lassen!)";
                starteDuellPolling();

            } catch (e) {
                document.getElementById('duellStatus').textContent = lang === 'en' ? "❌ Could not send. Try again!" : "❌ Konnte nicht geschickt werden. Versuch es nochmal!";
            }

        }

        async function ladeEingehendeDuell() {

            if (!username || istGast) {
                return;
            }

            try {
                let r = await fetch(MOCKAPI_URL);
                let alle = await r.json();

                if (!Array.isArray(alle)) {
                    return;
                }

                let meine = alle.filter(d => d.type === "duell" && d.opponent && d.opponent.toLowerCase() === username.toLowerCase() && d.status === "wartet");

                let box = document.getElementById('eingehendeDuellBox');

                if (!box) {
                    return;
                }

                if (meine.length === 0) {
                    if (!aktuellesDuellId) {
                        box.innerHTML = t('keineHerausforderung');
                    }
                    return;
                }

                box.innerHTML = meine.map(d => {
                    let acceptText = lang === 'en' ? "✅ Accept - 3,2,1 GO!" : "✅ Annehmen - 3,2,1 LOS!";
                    let declineText = lang === 'en' ? "❌ Decline" : "❌ Ablehnen";
                    let fordertText = lang === 'en' ? " challenges you!" : " fordert dich heraus!";
                    let infoText = lang === 'en' ? "2 minutes - who gets more correct wins +25 Elo!" : "2 Minuten - wer mehr richtig hat, gewinnt +25 Elo!";
                    return '<div style="border: 2px solid #7c3aed; padding: 10px; border-radius: 12px; margin: 8px 0;">' +
                        '<b>' + d.challenger + '</b>' + fordertText + '<br>' +
                        infoText + '<br>' +
                        '<button onclick="duellAnnehmen(\'' + d.id + '\')" style="background: #22c55e;">' + acceptText + '</button> ' +
                        '<button onclick="duellAblehnen(\'' + d.id + '\')" style="background: #ef4444;">' + declineText + '</button>' +
                        '</div>';
                }).join('');

            } catch (e) {}

        }

        async function duellAnnehmen(duellId) {

            try {
                let startZeit = Date.now() + 5000;

                await fetch(MOCKAPI_URL + "/" + duellId, {
                    method: 'PUT',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        type: "duell",
                        challenger: aktuellesDuell ? aktuellesDuell.challenger : "",
                        opponent: username,
                        status: "countdown",
                        startZeit: startZeit,
                        challengerScore: -1,
                        opponentScore: -1,
                        challengerRichtig: 0,
                        opponentRichtig: 0,
                        erstelltAm: Date.now()
                    })
                });

                let r = await fetch(MOCKAPI_URL + "/" + duellId);
                let d = await r.json();

                aktuellesDuellId = duellId;
                aktuellesDuell = d;
                gegnerName = d.challenger;

                document.getElementById('duellStatus').textContent = lang === 'en' ? "✅ Accepted! Starting soon - 3,2,1!" : "✅ Angenommen! Gleich geht es los - 3,2,1!";
                starteDuellPolling();
                starteCountdown(d);

            } catch (e) {
                alert(lang === 'en' ? "Could not accept!" : "Konnte nicht angenommen werden!");
            }

        }

        async function duellAblehnen(duellId) {
            try {
                await fetch(MOCKAPI_URL + "/" + duellId, {
                    method: 'DELETE'
                });
                ladeEingehendeDuell();
            } catch (e) {}
        }

        async function checkeDuellStatus() {

            if (!aktuellesDuellId) {
                return;
            }

            try {
                let r = await fetch(MOCKAPI_URL + "/" + aktuellesDuellId);
                if (!r.ok) {
                    aktuellesDuellId = null;
                    return;
                }

                let d = await r.json();
                aktuellesDuell = d;

                if (d.status === "countdown" && !duellCountdownLaeuft && !duellGestartet) {
                    if (d.challenger === username) {
                        gegnerName = d.opponent;
                    } else {
                        gegnerName = d.challenger;
                    }
                    starteCountdown(d);
                }

                if (d.status === "fertig" && !duellErgebnisGezeigt) {
                    zeigeDuellErgebnis(d);
                }

            } catch (e) {}
        }

        function starteCountdown(duell) {

            duellCountdownLaeuft = true;

            document.getElementById('duellBox').style.display = 'none';
            document.getElementById('modusBox').style.display = 'none';

            let overlay = document.getElementById('countdownOverlay');
            overlay.style.display = 'flex';

            let startZeit = duell.startZeit;

            let countdownInterval = setInterval(function() {

                let jetzt = Date.now();
                let diff = startZeit - jetzt;
                let sekunden = Math.ceil(diff / 1000);

                if (sekunden > 3) {
                    document.getElementById('countdownZahl').textContent = lang === 'en' ? "Ready?" : "Bereit?";
                    document.getElementById('countdownText').textContent = t('countdownGegner');
                } else if (sekunden === 3) {
                    document.getElementById('countdownZahl').textContent = "3";
                    document.getElementById('countdownText').textContent = t('countdownBereit');
                } else if (sekunden === 2) {
                    document.getElementById('countdownZahl').textContent = "2";
                } else if (sekunden === 1) {
                    document.getElementById('countdownZahl').textContent = "1";
                } else if (sekunden <= 0) {
                    clearInterval(countdownInterval);
                    document.getElementById('countdownZahl').textContent = lang === 'en' ? "GO! ⚡" : "LOS! ⚡";
                    document.getElementById('countdownText').textContent = lang === 'en' ? "2 minutes - GO GO GO!" : "2 Minuten - GO GO GO!";

                    setTimeout(function() {
                        overlay.style.display = 'none';
                        starteDuellGleichzeitig();
                    }, 700);
                }

            }, 200);

        }

        function starteDuellGleichzeitig() {

            spielModus = "duell";
            duellGestartet = true;
            duellMeineRichtigen = 0;
            duellMeineFehler = 0;
            duellErgebnisGezeigt = false;

            document.getElementById('duellBox').style.display = 'none';
            document.getElementById('spielBox').style.display = 'block';

            queue = mischen(E);
            index = 0;
            punkte = 0;
            fehler = 0;
            falschListe = [];
            phase = "haupt";
            schonErraten = [];

            document.getElementById('ende').style.display = 'none';
            document.getElementById('grid').style.display = 'grid';
            document.getElementById('weiterBtn').style.display = 'block';

            neueFrage();
            starteDuellTimer2Minuten();

            if (aktuellesDuellId && aktuellesDuell && aktuellesDuell.status === "countdown") {
                fetch(MOCKAPI_URL + "/" + aktuellesDuellId, {
                    method: 'PUT',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        type: "duell",
                        challenger: aktuellesDuell.challenger,
                        opponent: aktuellesDuell.opponent,
                        status: "laeuft",
                        startZeit: aktuellesDuell.startZeit,
                        challengerScore: -1,
                        opponentScore: -1,
                        challengerRichtig: 0,
                        opponentRichtig: 0,
                        erstelltAm: aktuellesDuell.erstelltAm
                    })
                }).catch(e => {});
            }

        }

        function starteDuellTimer2Minuten() {

            clearInterval(duellInterval);
            clearInterval(timerInterval);

            let duellZeit = 120;

            document.getElementById('timerText').textContent = "DUELL: " + duellZeit + "s | " + t('duellRichtig') + "0";

            duellInterval = setInterval(function() {

                duellZeit--;

                let min = Math.floor(duellZeit / 60);
                let sek = duellZeit % 60;
                let sekText = sek < 10 ? "0" + sek : "" + sek;

                document.getElementById('timerText').textContent = "DUELL: " + min + ":" + sekText + " | " + t('duellRichtig') + duellMeineRichtigen;

                if (duellZeit <= 10) {
                    document.getElementById('timerBox').classList.add('lamgsam');
                }

                if (duellZeit <= 0) {
                    clearInterval(duellInterval);
                    duellZeitUm();
                }

            }, 1000);

        }

        async function duellZeitUm() {

            clearInterval(duellInterval);
            clearInterval(timerInterval);

            document.getElementById('grid').style.display = 'none';
            document.getElementById('ende').style.display = 'block';
            document.getElementById('ende').innerHTML = "<h2>" + t('zeitUmTitel') + "</h2><p>" + t('duHastRichtig') + "<b>" + duellMeineRichtigen + "</b>" + t('richtigAusrufe') + "<br>" + t('warteAuf') + gegnerName + "...</p><p>" + (lang === 'en' ? "Result will show soon!" : "Ergebnis wird gleich angezeigt!") + "</p>";

            if (aktuellesDuellId && aktuellesDuell) {

                try {
                    let r = await fetch(MOCKAPI_URL + "/" + aktuellesDuellId);
                    let d = await r.json();

                    let binChallenger = (d.challenger === username);

                    let neuesDuell = {
                        type: "duell",
                        challenger: d.challenger,
                        opponent: d.opponent,
                        status: d.status,
                        startZeit: d.startZeit,
                        challengerScore: d.challengerScore,
                        opponentScore: d.opponentScore,
                        challengerRichtig: d.challengerRichtig,
                        opponentRichtig: d.opponentRichtig,
                        erstelltAm: d.erstelltAm
                    };

                    if (binChallenger) {
                        neuesDuell.challengerScore = punkte;
                        neuesDuell.challengerRichtig = duellMeineRichtigen;
                    } else {
                        neuesDuell.opponentScore = punkte;
                        neuesDuell.opponentRichtig = duellMeineRichtigen;
                    }

                    if (neuesDuell.challengerScore !== -1 && neuesDuell.opponentScore !== -1) {
                        neuesDuell.status = "fertig";
                    } else {
                        neuesDuell.status = "warten_auf_ergebnis";
                    }

                    await fetch(MOCKAPI_URL + "/" + aktuellesDuellId, {
                        method: 'PUT',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(neuesDuell)
                    });

                    if (neuesDuell.status === "fertig") {
                        zeigeDuellErgebnis(neuesDuell);
                    } else {
                        let warteInterval = setInterval(async function() {
                            try {
                                let rr = await fetch(MOCKAPI_URL + "/" + aktuellesDuellId);
                                let dd = await rr.json();
                                if (dd.status === "fertig") {
                                    clearInterval(warteInterval);
                                    zeigeDuellErgebnis(dd);
                                }
                            } catch (e) {}
                        }, 2000);
                    }

                } catch (e) {
                    document.getElementById('ende').innerHTML = "<h2>" + t('zeitUmTitel') + "</h2><p>" + t('duHastRichtig') + duellMeineRichtigen + t('richtigAusrufe') + "</p>";
                }

            }

        }

        function zeigeDuellErgebnis(d) {

            if (duellErgebnisGezeigt) {
                return;
            }

            duellErgebnisGezeigt = true;
            stoppeDuellPolling();

            let binChallenger = (d.challenger === username);
            let meinRichtig = binChallenger ? d.challengerRichtig : d.opponentRichtig;
            let gegnerRichtig = binChallenger ? d.opponentRichtig : d.challengerRichtig;
            let meinPunkte = binChallenger ? d.challengerScore : d.opponentScore;
            let gegnerPunkte = binChallenger ? d.opponentScore : d.challengerScore;

            let gewinnerText = "";
            let eloText = "";

            if (meinRichtig > gegnerRichtig) {
                gewinnerText = t('duGewonnen');
                elo += 25;
                eloText = t('duBekommst') + elo;
            } else if (meinRichtig < gegnerRichtig) {
                gewinnerText = "😭 " + gegnerName + t('duVerloren');
                elo -= 25;
                if (elo < 0) elo = 0;
                eloText = t('duVerlierst') + elo;
            } else {
                gewinnerText = t('unentschieden');
                eloText = t('keinerBekommt') + elo;
            }

            speichereElo();
            sendeScore();

            document.getElementById('grid').style.display = 'none';
            document.getElementById('ende').style.display = 'block';

            let youLabel = lang === 'en' ? "You" : "Du";
            let richtigLabel = lang === 'en' ? " correct" : " richtig";

            document.getElementById('ende').innerHTML =
                "<h2>" + t('duellVorbei') + "</h2>" +
                "<p style='font-size: 22px;'><b>" + gewinnerText + "</b></p>" +
                "<p style='font-size: 20px;'>" +
                youLabel + " (" + username + "): <b>" + meinRichtig + richtigLabel + "</b> | " + meinPunkte + " " + t('punkte') + "<br>" +
                gegnerName + ": <b>" + gegnerRichtig + richtigLabel + "</b> | " + gegnerPunkte + " " + t('punkte') + "<br><br>" +
                eloText +
                "</p>" +
                "<button onclick='duellZurueck()' style='background: #22c55e;'>" + t('zurueckMenu') + "</button>";

            setTimeout(function() {
                try {
                    fetch(MOCKAPI_URL + "/" + aktuellesDuellId, { method: 'DELETE' }).catch(e => {});
                } catch (e) {}
                aktuellesDuellId = null;
                aktuellesDuell = null;
                duellGestartet = false;
                duellCountdownLaeuft = false;
            }, 5000);

        }

        function duellZurueck() {
            document.getElementById('spielBox').style.display = 'none';
            document.getElementById('ende').style.display = 'none';
            document.getElementById('modusBox').style.display = 'block';
            document.getElementById('grid').style.display = 'grid';
            spielModus = "solo";
            aktuellesDuellId = null;
            aktuellesDuell = null;
            duellGestartet = false;
            duellCountdownLaeuft = false;
        }

        // ================= RANGLISTE =================

        async function ladeRangliste() {

            const box = document.getElementById('ranglisteInhalt');

            try {

                let r = await fetch(MOCKAPI_URL);
                let alle = await r.json();

                if (!Array.isArray(alle)) {
                    alle = [];
                }

                let scores = alle.filter(e => e.type === "score" || !e.type);

                scores.sort((a, b) => (Number(b.elo) || 1000) - (Number(a.elo) || 1000));

                let top = scores.slice(0, 10);

                if (top.length === 0) {
                    box.innerHTML = t('keineEintraege');
                    return;
                }

                box.innerHTML = top.map((e, i) => {
                    let mark = e.name === username ? t('du') : "";
                    return '<div class="rang-row"><span>' + (i + 1) + '. ' + e.name + mark + '</span><span><b>' + (e.elo || 1000) + ' Elo</b> | ' + t('punkte') + ': ' + (e.punkte || 0) + '</span></div>';
                }).join('');

            } catch (e) {
                box.innerHTML = t('fehlerLaden');
            }

        }

        async function sendeScore() {

            if (istGast) {
                return;
            }

            try {

                let r = await fetch(MOCKAPI_URL);
                let alle = await r.json();

                if (!Array.isArray(alle)) {
                    alle = [];
                }

                let vorhanden = alle.find(d => d.type === "score" && d.name === username);

                if (vorhanden) {
                    if (elo > (Number(vorhanden.elo) || 1000)) {
                        await fetch(MOCKAPI_URL + "/" + vorhanden.id, {
                            method: 'PUT',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify({
                                type: "score",
                                name: username,
                                elo: elo,
                                punkte: punkte,
                                fehler: fehler
                            })
                        });
                    }
                } else {
                    await fetch(MOCKAPI_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            type: "score",
                            name: username,
                            elo: elo,
                            punkte: punkte,
                            fehler: fehler
                        })
                    });
                }

                try {
                    let userEintrag = alle.find(x => x.type === "user" && x.name === username);
                    if (userEintrag) {
                        await fetch(MOCKAPI_URL + "/" + userEintrag.id, {
                            method: 'PUT',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify({
                                type: "user",
                                name: username,
                                pass: userEintrag.pass,
                                elo: elo,
                                punkte: 0,
                                fehler: 0
                            })
                        });
                    }
                } catch (e) {}

            } catch (e) {}

            ladeRangliste();

        }

        function leseRekord() {
            try {
                return parseInt(localStorage.getItem('periRekord') || '0') || 0;
            } catch (e) {
                return 0;
            }
        }

        function speichereRekord(w) {
            try {
                localStorage.setItem('periRekord', String(w));
            } catch (e) {}
        }

        // ================= ELEMENTE - ALLE 118 =================

        const E = [
            [1, "H", "Wasserstoff", 1, 1, "nichtmetall"],
            [2, "He", "Helium", 1, 18, "edelgas"],
            [3, "Li", "Lithium", 2, 1, "alkali"],
            [4, "Be", "Beryllium", 2, 2, "erdalkali"],
            [5, "B", "Bor", 2, 13, "halbmetall"],
            [6, "C", "Kohlenstoff", 2, 14, "nichtmetall"],
            [7, "N", "Stickstoff", 2, 15, "nichtmetall"],
            [8, "O", "Sauerstoff", 2, 16, "nichtmetall"],
            [9, "F", "Fluor", 2, 17, "halogen"],
            [10, "Ne", "Neon", 2, 18, "edelgas"],
            [11, "Na", "Natrium", 3, 1, "alkali"],
            [12, "Mg", "Magnesium", 3, 2, "erdalkali"],
            [13, "Al", "Aluminium", 3, 13, "metall"],
            [14, "Si", "Silicium", 3, 14, "halbmetall"],
            [15, "P", "Phosphor", 3, 15, "nichtmetall"],
            [16, "S", "Schwefel", 3, 16, "nichtmetall"],
            [17, "Cl", "Chlor", 3, 17, "halogen"],
            [18, "Ar", "Argon", 3, 18, "edelgas"],
            [19, "K", "Kalium", 4, 1, "alkali"],
            [20, "Ca", "Calcium", 4, 2, "erdalkali"],
            [21, "Sc", "Scandium", 4, 3, "uebergang"],
            [22, "Ti", "Titan", 4, 4, "uebergang"],
            [23, "V", "Vanadium", 4, 5, "uebergang"],
            [24, "Cr", "Chrom", 4, 6, "uebergang"],
            [25, "Mn", "Mangan", 4, 7, "uebergang"],
            [26, "Fe", "Eisen", 4, 8, "uebergang"],
            [27, "Co", "Cobalt", 4, 9, "uebergang"],
            [28, "Ni", "Nickel", 4, 10, "uebergang"],
            [29, "Cu", "Kupfer", 4, 11, "uebergang"],
            [30, "Zn", "Zink", 4, 12, "uebergang"],
            [31, "Ga", "Gallium", 4, 13, "metall"],
            [32, "Ge", "Germanium", 4, 14, "halbmetall"],
            [33, "As", "Arsen", 4, 15, "halbmetall"],
            [34, "Se", "Selen", 4, 16, "nichtmetall"],
            [35, "Br", "Brom", 4, 17, "halogen"],
            [36, "Kr", "Krypton", 4, 18, "edelgas"],
            [37, "Rb", "Rubidium", 5, 1, "alkali"],
            [38, "Sr", "Strontium", 5, 2, "erdalkali"],
            [39, "Y", "Yttrium", 5, 3, "uebergang"],
            [40, "Zr", "Zirconium", 5, 4, "uebergang"],
            [41, "Nb", "Niob", 5, 5, "uebergang"],
            [42, "Mo", "Molybdaen", 5, 6, "uebergang"],
            [43, "Tc", "Technetium", 5, 7, "uebergang"],
            [44, "Ru", "Ruthenium", 5, 8, "uebergang"],
            [45, "Rh", "Rhodium", 5, 9, "uebergang"],
            [46, "Pd", "Palladium", 5, 10, "uebergang"],
            [47, "Ag", "Silber", 5, 11, "uebergang"],
            [48, "Cd", "Cadmium", 5, 12, "uebergang"],
            [49, "In", "Indium", 5, 13, "metall"],
            [50, "Sn", "Zinn", 5, 14, "metall"],
            [51, "Sb", "Antimon", 5, 15, "halbmetall"],
            [52, "Te", "Tellur", 5, 16, "halbmetall"],
            [53, "I", "Iod", 5, 17, "halogen"],
            [54, "Xe", "Xenon", 5, 18, "edelgas"],
            [55, "Cs", "Caesium", 6, 1, "alkali"],
            [56, "Ba", "Barium", 6, 2, "erdalkali"],
            [57, "La", "Lanthan", 6, 3, "lanth"],
            [72, "Hf", "Hafnium", 6, 4, "uebergang"],
            [73, "Ta", "Tantal", 6, 5, "uebergang"],
            [74, "W", "Wolfram", 6, 6, "uebergang"],
            [75, "Re", "Rhenium", 6, 7, "uebergang"],
            [76, "Os", "Osmium", 6, 8, "uebergang"],
            [77, "Ir", "Iridium", 6, 9, "uebergang"],
            [78, "Pt", "Platin", 6, 10, "uebergang"],
            [79, "Au", "Gold", 6, 11, "uebergang"],
            [80, "Hg", "Quecksilber", 6, 12, "uebergang"],
            [81, "Tl", "Thallium", 6, 13, "metall"],
            [82, "Pb", "Blei", 6, 14, "metall"],
            [83, "Bi", "Bismut", 6, 15, "metall"],
            [84, "Po", "Polonium", 6, 16, "metall"],
            [85, "At", "Astat", 6, 17, "halogen"],
            [86, "Rn", "Radon", 6, 18, "edelgas"],
            [87, "Fr", "Francium", 7, 1, "alkali"],
            [88, "Ra", "Radium", 7, 2, "erdalkali"],
            [89, "Ac", "Actinium", 7, 3, "acti"],
            [104, "Rf", "Rutherfordium", 7, 4, "uebergang"],
            [105, "Db", "Dubnium", 7, 5, "uebergang"],
            [106, "Sg", "Seaborgium", 7, 6, "uebergang"],
            [107, "Bh", "Bohrium", 7, 7, "uebergang"],
            [108, "Hs", "Hassium", 7, 8, "uebergang"],
            [109, "Mt", "Meitnerium", 7, 9, "uebergang"],
            [110, "Ds", "Darmstadtium", 7, 10, "uebergang"],
            [111, "Rg", "Roentgenium", 7, 11, "uebergang"],
            [112, "Cn", "Copernicium", 7, 12, "uebergang"],
            [113, "Nh", "Nihonium", 7, 13, "metall"],
            [114, "Fl", "Flerovium", 7, 14, "metall"],
            [115, "Mc", "Moscovium", 7, 15, "metall"],
            [116, "Lv", "Livermorium", 7, 16, "metall"],
            [117, "Ts", "Tenness", 7, 17, "halogen"],
            [118, "Og", "Oganesson", 7, 18, "edelgas"],
            [58, "Ce", "Cer", 8, 4, "lanth"],
            [59, "Pr", "Praseodym", 8, 5, "lanth"],
            [60, "Nd", "Neodym", 8, 6, "lanth"],
            [61, "Pm", "Promethium", 8, 7, "lanth"],
            [62, "Sm", "Samarium", 8, 8, "lanth"],
            [63, "Eu", "Europium", 8, 9, "lanth"],
            [64, "Gd", "Gadolinium", 8, 10, "lanth"],
            [65, "Tb", "Terbium", 8, 11, "lanth"],
            [66, "Dy", "Dysprosium", 8, 12, "lanth"],
            [67, "Ho", "Holmium", 8, 13, "lanth"],
            [68, "Er", "Erbium", 8, 14, "lanth"],
            [69, "Tm", "Thulium", 8, 15, "lanth"],
            [70, "Yb", "Ytterbium", 8, 16, "lanth"],
            [71, "Lu", "Lutetium", 8, 17, "lanth"],
            [90, "Th", "Thorium", 9, 4, "acti"],
            [91, "Pa", "Protactinium", 9, 5, "acti"],
            [92, "U", "Uran", 9, 6, "acti"],
            [93, "Np", "Neptunium", 9, 7, "acti"],
            [94, "Pu", "Plutonium", 9, 8, "acti"],
            [95, "Am", "Americium", 9, 9, "acti"],
            [96, "Cm", "Curium", 9, 10, "acti"],
            [97, "Bk", "Berkelium", 9, 11, "acti"],
            [98, "Cf", "Californium", 9, 12, "acti"],
            [99, "Es", "Einsteinium", 9, 13, "acti"],
            [100, "Fm", "Fermium", 9, 14, "acti"],
            [101, "Md", "Mendelevium", 9, 15, "acti"],
            [102, "No", "Nobelium", 9, 16, "acti"],
            [103, "Lr", "Lawrencium", 9, 17, "acti"]
        ];

        // ================= SPIEL LOGIK =================

        let queue = [];
        let index = 0;
        let ziel = null;
        let geloest = false;
        let punkte = 0;
        let fehler = 0;
        let falschListe = [];
        let phase = "haupt";
        let rekord = leseRekord();
        let schonErraten = [];

        let timerInterval = null;
        let zeitUebrig = 15;
        let frageStartZeit = 0;
        let duellInterval = null;

        function mischen(arr) {

            let a = [...arr];

            for (let i = a.length - 1; i > 0; i--) {
                let j = Math.floor(Math.random() * (i + 1));
                [a[i], a[j]] = [a[j], a[i]];
            }

            return a;

        }

        function neustart() {

            document.getElementById('ende').style.display = 'none';
            document.getElementById('grid').style.display = 'grid';
            document.getElementById('weiterBtn').style.display = 'block';

            queue = mischen(E);
            index = 0;
            punkte = 0;
            fehler = 0;
            falschListe = [];
            phase = "haupt";
            schonErraten = [];

            neueFrage();

        }

        function durchlaufBeenden() {

            if (spielModus === "duell") {
                if (confirm(lang === 'en' ? "Really end the duel early? You will lose the duel!" : "Duell wirklich vorzeitig beenden? Du verlierst dann das Duell!")) {
                    clearInterval(duellInterval);
                    clearInterval(timerInterval);
                    duellMeineRichtigen = 0;
                    duellZeitUm();
                }
                return;
            }

            clearInterval(timerInterval);
            spielEnde();

        }

        function zeigeFrage() {

            if (modus === "name") {
                document.getElementById('frage').textContent = t('woIst') + elementName(ziel) + t('frageZeichen');
            } else {
                document.getElementById('frage').textContent = t('findeZahl') + ziel[0] + t('ausrufe');
            }

        }

        function neueFrage() {

            geloest = false;
            document.getElementById('meldung').textContent = '';

            if (index >= queue.length) {

                if (phase === "haupt" && falschListe.length > 0 && spielModus !== "duell") {
                    phase = "wiederholung";
                    queue = mischen(falschListe);
                    falschListe = [];
                    index = 0;
                    document.getElementById('meldung').textContent = t('wiederholungMsg');
                } else if (spielModus === "duell") {
                    queue = mischen(E);
                    index = 0;
                    schonErraten = [];
                } else {
                    spielEnde();
                    return;
                }

            }

            ziel = queue[index];

            zeigeFrage();

            updateInfo(phase === "wiederholung" ? t('wiederholung') : t('haupt'));

            bauen();

            if (spielModus !== "duell") {
                starteTimer();
            }

        }

        function starteTimer() {

            clearInterval(timerInterval);

            if (spielModus === "duell") {
                return;
            }

            zeitUebrig = 15;
            frageStartZeit = Date.now();

            document.getElementById('timerText').textContent = zeitUebrig;

            timerInterval = setInterval(() => {

                zeitUebrig--;

                document.getElementById('timerText').textContent = zeitUebrig;

                let box = document.getElementById('timerBox');

                box.classList.remove('schnell', 'lamgsam');

                if (zeitUebrig <= 5) {
                    box.classList.add('lamgsam');
                } else {
                    box.classList.add('schnell');
                }

                if (zeitUebrig <= 0) {

                    clearInterval(timerInterval);

                    document.getElementById('meldung').textContent = t('zuLangsam');

                    fehler++;

                    if (!falschListe.find(x => x[0] === ziel[0])) {
                        falschListe.push(ziel);
                    }

                    geloest = true;

                    updateInfo(phase === "wiederholung" ? t('wiederholung') : t('haupt'));

                }

            }, 1000);

        }

        function updateInfo(phasenText) {

            if (!ziel) {
                return;
            }

            let pct = phase === "haupt" ? Math.round((index / 118) * 100) : 100;

            document.getElementById('balken').style.width = pct + '%';

            let gastText = istGast ? t('gastText') : "";

            if (spielModus === "duell") {
                document.getElementById('info').innerHTML =
                    t('duellVs') + gegnerName + " | " + t('duellRichtig') + "<b>" + duellMeineRichtigen + "</b> | " + t('fehler') + ": " + fehler + " | " + t('punkte') + ": " + punkte;
                return;
            }

            document.getElementById('info').innerHTML =
                t('hallo') + username + ' | Elo: <b>' + elo + '</b>' + gastText + ' | ' + phasenText + ' | ' + t('frageVon') + ' ' + (index + 1) + ' ' + t('von') + ' ' + queue.length + '<br>' +
                t('punkte') + ': ' + punkte + ' | ' + t('fehler') + ': ' + fehler + ' | ' + t('zumWiederholen') + ': ' + falschListe.length + '<br>' +
                t('deinRekord') + ': ' + rekord + ' ' + t('punkte') + ' | ' + t('schonGruen') + schonErraten.length;

        }

        function bauen() {

            const grid = document.getElementById('grid');

            grid.innerHTML = '';

            for (let r = 1; r <= 9; r++) {

                for (let c = 1; c <= 18; c++) {

                    const el = E.find(e => e[3] === r && e[4] === c);
                    const d = document.createElement('div');

                    if (!el) {
                        d.className = 'el leer';
                        grid.appendChild(d);
                        continue;
                    }

                    d.className = 'el ' + el[5];

                    if (modus === "name") {
                        d.textContent = el[0];
                    } else {
                        d.textContent = el[1];
                    }

                    if (schonErraten.includes(el[0])) {
                        d.classList.add('richtig');
                        d.style.pointerEvents = 'none';
                        d.style.opacity = '0.85';
                        d.style.cursor = 'default';
                    } else {
                        d.onclick = () => klick(el, d);
                    }

                    grid.appendChild(d);

                }

            }

        }

        function klick(el, div) {

            if (geloest && spielModus !== "duell") {
                return;
            }

            if (schonErraten.includes(el[0])) {
                return;
            }

            if (el[0] === ziel[0]) {

                if (!schonErraten.includes(el[0])) {
                    schonErraten.push(el[0]);
                }

                clearInterval(timerInterval);

                let sekunden = Math.floor((Date.now() - frageStartZeit) / 1000);
                let eloGewinn = 0;

                if (spielModus === "duell") {
                    eloGewinn = 0;
                    duellMeineRichtigen++;
                    punkte += 10;
                    setTimeout(function() {
                        index++;
                        neueFrage();
                    }, 400);
                } else if (sekunden <= 5) {
                    eloGewinn = 15;
                } else if (sekunden <= 10) {
                    eloGewinn = 10;
                } else if (sekunden <= 15) {
                    eloGewinn = 5;
                } else {
                    eloGewinn = 0;
                }

                if (spielModus !== "duell") {
                    elo += eloGewinn;
                    speichereElo();
                    punkte += 10;
                    geloest = true;
                }

                div.classList.add('richtig');
                div.style.pointerEvents = 'none';

                if (spielModus === "duell") {
                    document.getElementById('meldung').textContent = (lang === 'en' ? "CORRECT! ⚡ Correct: " : "RICHTIG! ⚡ Richtig: ") + duellMeineRichtigen;
                } else {
                    document.getElementById('meldung').textContent =
                        t('richtig') + elementName(ziel) + t('ist') + ziel[0] + ' (' + ziel[1] + ') + ' + eloGewinn + ' Elo! ⚡ (' + sekunden + 's)';
                }

            } else {

                div.classList.add('falsch');

                if (spielModus !== "duell") {
                    elo -= 10;
                    if (elo < 0) elo = 0;
                    speichereElo();
                    fehler++;

                    if (!falschListe.find(x => x[0] === ziel[0])) {
                        falschListe.push(ziel);
                    }

                    document.getElementById('meldung').textContent =
                        t('falsch') + elementName(el) + t('klickRichtig') + " -10 Elo 😭";
                } else {
                    fehler++;
                    document.getElementById('meldung').textContent = t('falsch') + elementName(el) + (lang === 'en' ? " - keep going!" : " - weiter!");
                    setTimeout(function() {
                        div.classList.remove('falsch');
                    }, 600);
                }

            }

            updateInfo(phase === "wiederholung" ? t('wiederholung') : t('haupt'));

        }

        function weiter() {

            if (spielModus === "duell") {
                index++;
                neueFrage();
                return;
            }

            if (!geloest) {
                document.getElementById('meldung').textContent = t('erstRichtig');
                return;
            }

            index++;
            neueFrage();

        }

        function spielEnde() {

            clearInterval(timerInterval);

            document.getElementById('grid').style.display = 'none';
            document.getElementById('weiterBtn').style.display = 'none';
            document.getElementById('frage').textContent = t('fertig');

            let neuerRekord = false;

            if (punkte > rekord) {
                rekord = punkte;
                speichereRekord(rekord);
                neuerRekord = true;
            }

            document.getElementById('balken').style.width = '100%';
            document.getElementById('ende').style.display = 'block';

            let gastHinweis = istGast
                ? "<br><br>" + t('gastEnde')
                : "<br><br>" + t('hochgeladen');

            document.getElementById('ende').innerHTML =
                '<h2>' + (neuerRekord ? t('neuerRekord') : t('stark') + username + '!') + '</h2>' +
                '<p style="font-size: 24px">' + t('deinePunkte') + ': <b>' + punkte + '</b><br>' + t('fehler') + ': ' + fehler + '<br>Elo: ' + elo + '<br>' + t('rekord') + ': ' + rekord + '</p>' +
                '<p>' + gastHinweis + '</p><p>' + t('alleGeschafft') + '</p>' +
                '<button onclick="zurueckNachEnde()" style="background: #22c55e;">' + t('zurueckMenu') + '</button>';

            document.getElementById('info').textContent = 'Elo: ' + elo + ' | ' + t('rekord') + ': ' + rekord + ' ' + t('punkte');

            sendeScore();

        }

        function zurueckNachEnde() {
            document.getElementById('spielBox').style.display = 'none';
            document.getElementById('ende').style.display = 'none';
            document.getElementById('modusBox').style.display = 'block';
            document.getElementById('grid').style.display = 'grid';
        }

        setLang(lang);
        ladeRangliste();
        neueVorschlaege();

    </script>

</body>

</html>
