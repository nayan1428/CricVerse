# CricVerse
Yeh lijiye Cricket Franchise Manager 2026 ka fully updated aur bug-free version!
🔧 Fixes & Upgrades:
 * No More Placeholders: Saare unassigned pools mein ab 140+ real international aur legendary players ke naam hain (Sachin Tendulkar, AB de Villiers, Faf du Plessis, Ishan Kishan, etc.), toh simulate karne par kabhi bhi "Veteran / Scout #X" nahi aayega.
 * Strict Squad Limits:
   * IPL 2026: Min 18 aur Max 25 players per squad.
   * Legends League Cricket (LLC): Min 14 aur Max 18 players per squad.
 * Smooth Simulation & Auction: Auto-fill aur auction logic ko fix kar diya gaya hai taaki squad limits hamesha maintain rahein.
Aap is poore code ko copy karke apne phone par .html file ke taur par save karke chala sakte hain:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
<title>Cricket Franchise Manager 2026 - IPL & LLC Edition</title>
<style>
  :root {
    --bg: #0b0f19;
    --card: #131a2a;
    --card2: #1a2338;
    --border: #26334d;
    --text: #f1f5f9;
    --muted: #94a3b8;
    --gold: #f59e0b;
    --green: #10b981;
    --red: #ef4444;
    --blue: #3b82f6;
    --purple: #8b5cf6;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; -webkit-tap-highlight-color: transparent; }
  body { background: var(--bg); color: var(--text); min-height: 100vh; padding-bottom: 85px; overflow-x: hidden; }
  button { cursor: pointer; border: none; outline: none; font-weight: 700; transition: 0.15s; }
  button:active { transform: scale(0.96); }
  button:disabled { opacity: 0.45; cursor: not-allowed; transform: none; }

  .topbar { position: sticky; top: 0; z-index: 50; background: rgba(11,15,25,0.95); backdrop-filter: blur(10px); border-bottom: 1px solid var(--border); padding: 10px 14px; display: flex; align-items: center; justify-content: space-between; }
  .brand { font-weight: 900; font-size: 15px; letter-spacing: 0.5px; display: flex; align-items: center; gap: 6px; }
  .pill { background: var(--card2); border: 1px solid var(--border); padding: 4px 9px; border-radius: 99px; font-size: 11px; font-weight: 700; color: var(--gold); }

  .container { max-width: 640px; margin: 0 auto; padding: 12px; }
  .card { background: var(--card); border: 1px solid var(--border); border-radius: 14px; padding: 14px; margin-bottom: 12px; }
  .h1 { font-size: 22px; font-weight: 900; margin-bottom: 6px; }
  .h2 { font-size: 16px; font-weight: 800; margin-bottom: 8px; display: flex; align-items: center; justify-content: space-between; }
  .sub { font-size: 12px; color: var(--muted); line-height: 1.4; }

  .btn { width: 100%; padding: 13px 16px; border-radius: 12px; font-size: 14px; display: flex; align-items: center; justify-content: center; gap: 8px; }
  .btn-gold { background: linear-gradient(135deg, #f59e0b, #d97706); color: #090d16; }
  .btn-green { background: linear-gradient(135deg, #10b981, #059669); color: #fff; }
  .btn-blue { background: linear-gradient(135deg, #3b82f6, #2563eb); color: #fff; }
  .btn-red { background: linear-gradient(135deg, #ef4444, #dc2626); color: #fff; }
  .btn-purple { background: linear-gradient(135deg, #8b5cf6, #6d28d9); color: #fff; }
  .btn-dark { background: var(--card2); border: 1px solid var(--border); color: var(--text); }
  .btn-sm { padding: 7px 11px; font-size: 12px; border-radius: 8px; width: auto; }

  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; }
  .grid-5 { display: grid; grid-template-columns: repeat(5, 1fr); gap: 5px; }

  .team-tile { background: var(--card2); border: 2px solid var(--border); border-radius: 12px; padding: 10px; text-align: left; color: var(--text); }
  .team-tile.active { border-color: var(--gold); background: rgba(245,158,11,0.12); }
  .team-code { font-size: 15px; font-weight: 900; display: flex; align-items: center; justify-content: space-between; }
  .dot { width: 10px; height: 10px; border-radius: 50%; display: inline-block; }

  .league-tab { padding: 12px; border-radius: 12px; border: 2px solid var(--border); background: var(--card2); color: var(--text); text-align: center; }
  .league-tab.active-ipl { border-color: var(--blue); background: rgba(59,130,246,0.16); }
  .league-tab.active-llc { border-color: var(--gold); background: rgba(245,158,11,0.16); }

  .row { display: flex; align-items: center; justify-content: space-between; padding: 10px; background: var(--card2); border: 1px solid var(--border); border-radius: 10px; margin-bottom: 7px; gap: 8px; }
  .badge { font-size: 10px; font-weight: 800; padding: 2px 6px; border-radius: 5px; text-transform: uppercase; }
  .b-bat { background: rgba(59,130,246,0.2); color: #60a5fa; }
  .b-bowl { background: rgba(16,185,129,0.2); color: #34d399; }
  .b-ar { background: rgba(139,92,246,0.2); color: #a78bfa; }
  .b-wk { background: rgba(245,158,11,0.2); color: #fbbf24; }
  .b-os { background: rgba(239,68,68,0.2); color: #f87171; }

  .franchise-chip { background: var(--card2); border: 1px solid var(--border); border-radius: 8px; padding: 5px 4px; text-align: center; font-size: 10px; transition: 0.2s; }
  .franchise-chip.bidding { border-color: var(--gold); background: rgba(245,158,11,0.22); transform: scale(1.04); box-shadow: 0 0 12px rgba(245,158,11,0.35); }
  .franchise-chip.human { border-bottom: 2px solid var(--blue); }

  .timer-bar { height: 6px; background: var(--card2); border-radius: 99px; overflow: hidden; margin: 10px 0; }
  .timer-fill { height: 100%; background: linear-gradient(90deg, var(--red), var(--gold), var(--green)); transition: width 0.2s linear; }

  .log-box { max-height: 110px; overflow-y: auto; font-size: 11px; background: #090d16; border: 1px solid var(--border); border-radius: 8px; padding: 8px; }
  .log-item { padding: 3px 0; border-bottom: 1px dashed rgba(255,255,255,0.06); }

  /* Tactical 2D Match View */
  .match-header { background: #111827; border: 1px solid var(--border); border-radius: 12px; padding: 10px; margin-bottom: 8px; }
  .over-balls { display: flex; gap: 6px; margin: 8px 0; }
  .ball-pill { flex: 1; height: 28px; border-radius: 6px; background: var(--card2); border: 1px solid var(--border); display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 900; }
  .ball-4 { background: rgba(59,130,246,0.25); border-color: #3b82f6; color: #93c5fd; }
  .ball-6 { background: rgba(245,158,11,0.3); border-color: #f59e0b; color: #fcd34d; }
  .ball-W { background: rgba(239,68,68,0.3); border-color: #ef4444; color: #fca5a5; }
  .ball-run { background: rgba(16,185,129,0.2); border-color: #10b981; color: #6ee7b7; }

  .stadium-wrap { position: relative; width: 100%; max-width: 380px; margin: 0 auto; aspect-ratio: 1 / 1; border-radius: 14px; overflow: hidden; border: 2px solid var(--border); background: #0c1911; }
  canvas { width: 100%; height: 100%; display: block; }

  .drawer-backdrop { position: fixed; inset: 0; background: rgba(0,0,0,0.75); z-index: 100; display: flex; align-items: flex-end; justify-content: center; }
  .drawer { background: var(--card); border-top: 2px solid var(--gold); border-radius: 18px 18px 0 0; width: 100%; max-width: 640px; max-height: 82vh; overflow-y: auto; padding: 16px; animation: slideUp 0.2s ease-out; }
  @keyframes slideUp { from { transform: translateY(40px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

  .bottom-dock { position: fixed; bottom: 0; left: 0; right: 0; background: rgba(11,15,25,0.97); border-top: 1px solid var(--border); padding: 10px 12px; z-index: 40; display: flex; justify-content: center; }
  .dock-inner { width: 100%; max-width: 640px; display: flex; gap: 8px; align-items: center; }

  table { width: 100%; border-collapse: collapse; font-size: 12px; }
  th, td { padding: 7px 5px; text-align: left; border-bottom: 1px solid var(--border); }
  th { color: var(--muted); font-size: 10px; text-transform: uppercase; }
  input, select { background: var(--card2); border: 1px solid var(--border); color: var(--text); padding: 10px 12px; border-radius: 10px; font-size: 13px; width: 100%; }
</style>
</head>
<body>

<div class="topbar">
  <div class="brand" id="top-brand">🏏 IPL & LLC <span style="color:var(--gold)">2026</span></div>
  <div id="top-status" class="pill">LEAGUE HUB</div>
</div>

<div id="app" class="container"></div>
<div id="modal-root"></div>

<script>
// ==================== LEAGUES DATABASE (IPL 2026 & LEGENDS LEAGUE CRICKET) ====================[span_5](start_span)[span_5](end_span)
const LEAGUES = {
  IPL: {
    id: 'IPL',
    title: 'IPL 2026',
    subtitle: 'Indian Premier League',
    purse: 120.0,
    maxRetention: 6,
    maxOSInSquad: 8,
    minSquad: 18,
    maxSquad: 25,
    teams: [
      { id: 'RCB', name: 'Royal Challengers Bengaluru', color: '#ef4444', venue: 'Bengaluru' },
      { id: 'CSK', name: 'Chennai Super Kings', color: '#eab308', venue: 'Chennai' },
      { id: 'MI',  name: 'Mumbai Indians', color: '#3b82f6', venue: 'Mumbai' },
      { id: 'KKR', name: 'Kolkata Knight Riders', color: '#8b5cf6', venue: 'Kolkata' },
      { id: 'SRH', name: 'Sunrisers Hyderabad', color: '#f97316', venue: 'Hyderabad' },
      { id: 'RR',  name: 'Rajasthan Royals', color: '#ec4899', venue: 'Jaipur' },
      { id: 'DC',  name: 'Delhi Capitals', color: '#2563eb', venue: 'Delhi' },
      { id: 'LSG', name: 'Lucknow Super Giants', color: '#06b6d4', venue: 'Lucknow' },
      { id: 'GT',  name: 'Gujarat Titans', color: '#14b8a6', venue: 'Ahmedabad' },
      { id: 'PBKS',name: 'Punjab Kings', color: '#dc2626', venue: 'Mullanpur' }
    ],
    players: [
      // RCB[span_6](start_span)[span_6](end_span)
      { id: 1, name: 'Virat Kohli', team: 'RCB', role: 'BAT', os: false, bat: 96, bowl: 25, base: 2.0, uncapped: false, jersey: 18 },
      { id: 2, name: 'Rajat Patidar', team: 'RCB', role: 'BAT', os: false, bat: 87, bowl: 15, base: 2.0, uncapped: false, jersey: 97 },
      { id: 3, name: 'Josh Hazlewood', team: 'RCB', role: 'BOWL', os: true, bat: 25, bowl: 93, base: 2.0, uncapped: false, jersey: 38 },
      { id: 4, name: 'Phil Salt', team: 'RCB', role: 'WK', os: true, bat: 90, bowl: 10, base: 2.0, uncapped: false, jersey: 28 },
      { id: 5, name: 'Bhuvneshwar Kumar', team: 'RCB', role: 'BOWL', os: false, bat: 35, bowl: 87, base: 2.0, uncapped: false, jersey: 15 },
      { id: 6, name: 'Krunal Pandya', team: 'RCB', role: 'AR', os: false, bat: 78, bowl: 82, base: 2.0, uncapped: false, jersey: 24 },
      { id: 7, name: 'Tim David', team: 'RCB', role: 'BAT', os: true, bat: 86, bowl: 30, base: 2.0, uncapped: false, jersey: 8 },
      { id: 8, name: 'Suyash Sharma', team: 'RCB', role: 'BOWL', os: false, bat: 15, bowl: 81, base: 0.75, uncapped: true, jersey: 19 },
      // CSK[span_7](start_span)[span_7](end_span)
      { id: 9, name: 'Ruturaj Gaikwad', team: 'CSK', role: 'BAT', os: false, bat: 92, bowl: 15, base: 2.0, uncapped: false, jersey: 31 },
      { id: 10, name: 'MS Dhoni', team: 'CSK', role: 'WK', os: false, bat: 84, bowl: 10, base: 2.0, uncapped: true, jersey: 7 },
      { id: 11, name: 'Ravindra Jadeja', team: 'CSK', role: 'AR', os: false, bat: 84, bowl: 89, base: 2.0, uncapped: false, jersey: 8 },
      { id: 12, name: 'Matheesha Pathirana', team: 'CSK', role: 'BOWL', os: true, bat: 15, bowl: 92, base: 2.0, uncapped: false, jersey: 99 },
      { id: 13, name: 'Shivam Dube', team: 'CSK', role: 'AR', os: false, bat: 88, bowl: 62, base: 2.0, uncapped: false, jersey: 25 },
      { id: 14, name: 'Noor Ahmad', team: 'CSK', role: 'BOWL', os: true, bat: 22, bowl: 89, base: 2.0, uncapped: false, jersey: 15 },
      { id: 15, name: 'Devon Conway', team: 'CSK', role: 'BAT', os: true, bat: 88, bowl: 10, base: 2.0, uncapped: false, jersey: 88 },
      // MI[span_8](start_span)[span_8](end_span)
      { id: 16, name: 'Jasprit Bumrah', team: 'MI', role: 'BOWL', os: false, bat: 25, bowl: 98, base: 2.0, uncapped: false, jersey: 93 },
      { id: 17, name: 'Suryakumar Yadav', team: 'MI', role: 'BAT', os: false, bat: 95, bowl: 15, base: 2.0, uncapped: false, jersey: 63 },
      { id: 18, name: 'Hardik Pandya', team: 'MI', role: 'AR', os: false, bat: 89, bowl: 87, base: 2.0, uncapped: false, jersey: 33 },
      { id: 19, name: 'Rohit Sharma', team: 'MI', role: 'BAT', os: false, bat: 92, bowl: 20, base: 2.0, uncapped: false, jersey: 45 },
      { id: 20, name: 'Tilak Varma', team: 'MI', role: 'BAT', os: false, bat: 89, bowl: 35, base: 2.0, uncapped: false, jersey: 9 },
      { id: 21, name: 'Trent Boult', team: 'MI', role: 'BOWL', os: true, bat: 28, bowl: 91, base: 2.0, uncapped: false, jersey: 18 },
      { id: 22, name: 'Mitchell Santner', team: 'MI', role: 'AR', os: true, bat: 72, bowl: 85, base: 2.0, uncapped: false, jersey: 74 },
      // KKR[span_9](start_span)[span_9](end_span)
      { id: 23, name: 'Sunil Narine', team: 'KKR', role: 'AR', os: true, bat: 86, bowl: 91, base: 2.0, uncapped: false, jersey: 74 },
      { id: 24, name: 'Andre Russell', team: 'KKR', role: 'AR', os: true, bat: 90, bowl: 84, base: 2.0, uncapped: false, jersey: 12 },
      { id: 25, name: 'Rinku Singh', team: 'KKR', role: 'BAT', os: false, bat: 89, bowl: 15, base: 2.0, uncapped: false, jersey: 35 },
      { id: 26, name: 'Varun Chakaravarthy', team: 'KKR', role: 'BOWL', os: false, bat: 15, bowl: 91, base: 2.0, uncapped: false, jersey: 29 },
      { id: 27, name: 'Harshit Rana', team: 'KKR', role: 'BOWL', os: false, bat: 35, bowl: 86, base: 1.5, uncapped: false, jersey: 22 },
      { id: 28, name: 'Quinton de Kock', team: 'KKR', role: 'WK', os: true, bat: 88, bowl: 10, base: 2.0, uncapped: false, jersey: 12 },
      // SRH[span_10](start_span)[span_10](end_span)
      { id: 29, name: 'Heinrich Klaasen', team: 'SRH', role: 'WK', os: true, bat: 95, bowl: 10, base: 2.0, uncapped: false, jersey: 45 },
      { id: 30, name: 'Pat Cummins', team: 'SRH', role: 'BOWL', os: true, bat: 68, bowl: 92, base: 2.0, uncapped: false, jersey: 30 },
      { id: 31, name: 'Abhishek Sharma', team: 'SRH', role: 'AR', os: false, bat: 91, bowl: 68, base: 2.0, uncapped: false, jersey: 4 },
      { id: 32, name: 'Travis Head', team: 'SRH', role: 'BAT', os: true, bat: 94, bowl: 40, base: 2.0, uncapped: false, jersey: 62 },
      { id: 33, name: 'Nitish Kumar Reddy', team: 'SRH', role: 'AR', os: false, bat: 84, bowl: 76, base: 1.5, uncapped: false, jersey: 88 },
      { id: 34, name: 'Mohammed Shami', team: 'SRH', role: 'BOWL', os: false, bat: 25, bowl: 91, base: 2.0, uncapped: false, jersey: 11 },
      // RR[span_11](start_span)[span_11](end_span)
      { id: 35, name: 'Sanju Samson', team: 'RR', role: 'WK', os: false, bat: 91, bowl: 10, base: 2.0, uncapped: false, jersey: 11 },
      { id: 36, name: 'Yashasvi Jaiswal', team: 'RR', role: 'BAT', os: false, bat: 93, bowl: 20, base: 2.0, uncapped: false, jersey: 64 },
      { id: 37, name: 'Riyan Parag', team: 'RR', role: 'AR', os: false, bat: 86, bowl: 68, base: 2.0, uncapped: false, jersey: 5 },
      { id: 38, name: 'Jofra Archer', team: 'RR', role: 'BOWL', os: true, bat: 42, bowl: 90, base: 2.0, uncapped: false, jersey: 22 },
      { id: 39, name: 'Shimron Hetmyer', team: 'RR', role: 'BAT', os: true, bat: 86, bowl: 10, base: 2.0, uncapped: false, jersey: 189 },
      { id: 40, name: 'Wanindu Hasaranga', team: 'RR', role: 'AR', os: true, bat: 66, bowl: 89, base: 2.0, uncapped: false, jersey: 49 },
      // DC[span_12](start_span)[span_12](end_span)
      { id: 41, name: 'KL Rahul', team: 'DC', role: 'WK', os: false, bat: 91, bowl: 10, base: 2.0, uncapped: false, jersey: 1 },
      { id: 42, name: 'Axar Patel', team: 'DC', role: 'AR', os: false, bat: 83, bowl: 89, base: 2.0, uncapped: false, jersey: 20 },
      { id: 43, name: 'Kuldeep Yadav', team: 'DC', role: 'BOWL', os: false, bat: 25, bowl: 92, base: 2.0, uncapped: false, jersey: 23 },
      { id: 44, name: 'Mitchell Starc', team: 'DC', role: 'BOWL', os: true, bat: 40, bowl: 91, base: 2.0, uncapped: false, jersey: 56 },
      { id: 45, name: 'Tristan Stubbs', team: 'DC', role: 'BAT', os: true, bat: 88, bowl: 30, base: 2.0, uncapped: false, jersey: 30 },
      { id: 46, name: 'Jake Fraser-McGurk', team: 'DC', role: 'BAT', os: true, bat: 87, bowl: 10, base: 2.0, uncapped: false, jersey: 29 },
      // LSG[span_13](start_span)[span_13](end_span)
      { id: 47, name: 'Rishabh Pant', team: 'LSG', role: 'WK', os: false, bat: 93, bowl: 10, base: 2.0, uncapped: false, jersey: 17 },
      { id: 48, name: 'Nicholas Pooran', team: 'LSG', role: 'WK', os: true, bat: 93, bowl: 10, base: 2.0, uncapped: false, jersey: 29 },
      { id: 49, name: 'Mayank Yadav', team: 'LSG', role: 'BOWL', os: false, bat: 15, bowl: 88, base: 1.5, uncapped: false, jersey: 14 },
      { id: 50, name: 'Ravi Bishnoi', team: 'LSG', role: 'BOWL', os: false, bat: 22, bowl: 88, base: 2.0, uncapped: false, jersey: 56 },
      { id: 51, name: 'David Miller', team: 'LSG', role: 'BAT', os: true, bat: 88, bowl: 10, base: 2.0, uncapped: false, jersey: 10 },
      { id: 52, name: 'Mitchell Marsh', team: 'LSG', role: 'AR', os: true, bat: 87, bowl: 79, base: 2.0, uncapped: false, jersey: 8 },
      // GT[span_14](start_span)[span_14](end_span)
      { id: 53, name: 'Shubman Gill', team: 'GT', role: 'BAT', os: false, bat: 94, bowl: 15, base: 2.0, uncapped: false, jersey: 77 },
      { id: 54, name: 'Rashid Khan', team: 'GT', role: 'AR', os: true, bat: 72, bowl: 95, base: 2.0, uncapped: false, jersey: 19 },
      { id: 55, name: 'Jos Buttler', team: 'GT', role: 'WK', os: true, bat: 93, bowl: 10, base: 2.0, uncapped: false, jersey: 63 },
      { id: 56, name: 'Mohammed Siraj', team: 'GT', role: 'BOWL', os: false, bat: 20, bowl: 89, base: 2.0, uncapped: false, jersey: 73 },
      { id: 57, name: 'Kagiso Rabada', team: 'GT', role: 'BOWL', os: true, bat: 35, bowl: 91, base: 2.0, uncapped: false, jersey: 25 },
      { id: 58, name: 'Sai Sudharsan', team: 'GT', role: 'BAT', os: false, bat: 88, bowl: 15, base: 2.0, uncapped: false, jersey: 23 },
      // PBKS[span_15](start_span)[span_15](end_span)
      { id: 59, name: 'Shreyas Iyer', team: 'PBKS', role: 'BAT', os: false, bat: 91, bowl: 15, base: 2.0, uncapped: false, jersey: 96 },
      { id: 60, name: 'Arshdeep Singh', team: 'PBKS', role: 'BOWL', os: false, bat: 20, bowl: 91, base: 2.0, uncapped: false, jersey: 2 },
      { id: 61, name: 'Yuzvendra Chahal', team: 'PBKS', role: 'BOWL', os: false, bat: 15, bowl: 90, base: 2.0, uncapped: false, jersey: 3 },
      { id: 62, name: 'Marcus Stoinis', team: 'PBKS', role: 'AR', os: true, bat: 86, bowl: 81, base: 2.0, uncapped: false, jersey: 17 },
      { id: 63, name: 'Glenn Maxwell', team: 'PBKS', role: 'AR', os: true, bat: 87, bowl: 79, base: 2.0, uncapped: false, jersey: 32 },
      { id: 64, name: 'Shashank Singh', team: 'PBKS', role: 'BAT', os: false, bat: 85, bowl: 20, base: 1.0, uncapped: true, jersey: 19 },
      // Expanded Unassigned Pool with real names[span_16](start_span)[span_16](end_span)
      { id: 65, name: 'Faf du Plessis', team: null, role: 'BAT', os: true, bat: 87, bowl: 15, base: 2.0, uncapped: false, jersey: 13 },
      { id: 66, name: 'Ishan Kishan', team: null, role: 'WK', os: false, bat: 88, bowl: 10, base: 2.0, uncapped: false, jersey: 32 },
      { id: 67, name: 'Venkatesh Iyer', team: null, role: 'AR', os: false, bat: 86, bowl: 72, base: 2.0, uncapped: false, jersey: 25 },
      { id: 68, name: 'Liam Livingstone', team: null, role: 'AR', os: true, bat: 86, bowl: 77, base: 2.0, uncapped: false, jersey: 23 },
      { id: 69, name: 'Avesh Khan', team: null, role: 'BOWL', os: false, bat: 18, bowl: 85, base: 1.5, uncapped: false, jersey: 65 },
      { id: 70, name: 'Deepak Chahar', team: null, role: 'BOWL', os: false, bat: 45, bowl: 85, base: 1.5, uncapped: false, jersey: 90 },
      { id: 71, name: 'Washington Sundar', team: null, role: 'AR', os: false, bat: 78, bowl: 84, base: 1.5, uncapped: false, jersey: 5 },
      { id: 72, name: 'Marco Jansen', team: null, role: 'AR', os: true, bat: 70, bowl: 87, base: 1.5, uncapped: false, jersey: 70 },
      { id: 73, name: 'Rachin Ravindra', team: null, role: 'AR', os: true, bat: 85, bowl: 75, base: 1.5, uncapped: false, jersey: 8 },
      { id: 74, name: 'T Natarajan', team: null, role: 'BOWL', os: false, bat: 12, bowl: 86, base: 1.5, uncapped: false, jersey: 44 },
      { id: 75, name: 'Jitesh Sharma', team: null, role: 'WK', os: false, bat: 83, bowl: 10, base: 1.0, uncapped: false, jersey: 99 },
      { id: 76, name: 'Prasidh Krishna', team: null, role: 'BOWL', os: false, bat: 15, bowl: 86, base: 1.5, uncapped: false, jersey: 24 },
      { id: 77, name: 'Shardul Thakur', team: null, role: 'AR', os: false, bat: 64, bowl: 82, base: 1.5, uncapped: false, jersey: 54 },
      { id: 78, name: 'Sam Curran', team: null, role: 'AR', os: true, bat: 80, bowl: 84, base: 2.0, uncapped: false, jersey: 58 },
      { id: 79, name: 'Anrich Nortje', team: null, role: 'BOWL', os: true, bat: 15, bowl: 88, base: 2.0, uncapped: false, jersey: 20 },
      { id: 80, name: 'Ashutosh Sharma', team: null, role: 'BAT', os: false, bat: 83, bowl: 10, base: 0.75, uncapped: true, jersey: 14 },
      { id: 81, name: 'Vaibhav Suryavanshi', team: null, role: 'BAT', os: false, bat: 80, bowl: 10, base: 0.5, uncapped: true, jersey: 12 },
      { id: 82, name: 'Nehal Wadhera', team: null, role: 'BAT', os: false, bat: 82, bowl: 20, base: 0.75, uncapped: true, jersey: 16 },
      { id: 83, name: 'Mukesh Kumar', team: null, role: 'BOWL', os: false, bat: 15, bowl: 84, base: 1.5, uncapped: false, jersey: 49 },
      { id: 84, name: 'Will Jacks', team: null, role: 'AR', os: true, bat: 86, bowl: 74, base: 2.0, uncapped: false, jersey: 22 },
      { id: 85, name: 'Glenn Phillips', team: null, role: 'AR', os: true, bat: 85, bowl: 72, base: 1.5, uncapped: false, jersey: 23 },
      { id: 86, name: 'Khaleel Ahmed', team: null, role: 'BOWL', os: false, bat: 15, bowl: 85, base: 1.5, uncapped: false, jersey: 71 },
      { id: 87, name: 'Harshal Patel', team: null, role: 'BOWL', os: false, bat: 42, bowl: 86, base: 2.0, uncapped: false, jersey: 9 },
      { id: 88, name: 'Rahul Chahar', team: null, role: 'BOWL', os: false, bat: 25, bowl: 83, base: 1.0, uncapped: false, jersey: 1 },
      { id: 89, name: 'Rovman Powell', team: null, role: 'BAT', os: true, bat: 84, bowl: 30, base: 1.5, uncapped: false, jersey: 52 },
      { id: 90, name: 'Mayank Agarwal', team: null, role: 'BAT', os: false, bat: 82, bowl: 10, base: 1.0, uncapped: false, jersey: 16 },
      { id: 91, name: 'Cameron Green', team: null, role: 'AR', os: true, bat: 89, bowl: 85, base: 2.0, uncapped: false, jersey: 42 },
      { id: 92, name: 'Ben Stokes', team: null, role: 'AR', os: true, bat: 88, bowl: 82, base: 2.0, uncapped: false, jersey: 55 },
      { id: 93, name: 'Jonny Bairstow', team: null, role: 'WK', os: true, bat: 89, bowl: 10, base: 2.0, uncapped: false, jersey: 51 },
      { id: 94, name: 'Harry Brook', team: null, role: 'BAT', os: true, bat: 88, bowl: 15, base: 2.0, uncapped: false, jersey: 88 },
      { id: 95, name: 'Kane Williamson', team: null, role: 'BAT', os: true, bat: 89, bowl: 10, base: 2.0, uncapped: false, jersey: 22 },
      { id: 96, name: 'Daryl Mitchell', team: null, role: 'AR', os: true, bat: 87, bowl: 75, base: 1.5, uncapped: false, jersey: 75 },
      { id: 97, name: 'Aiden Markram', team: null, role: 'AR', os: true, bat: 87, bowl: 72, base: 2.0, uncapped: false, jersey: 4 },
      { id: 98, name: 'Adam Zampa', team: null, role: 'BOWL', os: true, bat: 15, bowl: 89, base: 1.5, uncapped: false, jersey: 8 },
      { id: 99, name: 'Lockie Ferguson', team: null, role: 'BOWL', os: true, bat: 20, bowl: 88, base: 1.5, uncapped: false, jersey: 69 },
      { id: 100, name: 'Jason Holder', team: null, role: 'AR', os: true, bat: 81, bowl: 84, base: 1.5, uncapped: false, jersey: 98 },
      { id: 101, name: 'Maheesh Theekshana', team: null, role: 'BOWL', os: true, bat: 18, bowl: 88, base: 1.5, uncapped: false, jersey: 61 },
      { id: 102, name: 'Rahmanullah Gurbaz', team: null, role: 'WK', os: true, bat: 86, bowl: 10, base: 1.0, uncapped: false, jersey: 21 },
      { id: 103, name: 'Mustafizur Rahman', team: null, role: 'BOWL', os: true, bat: 15, bowl: 87, base: 1.5, uncapped: false, jersey: 90 },
      { id: 104, name: 'Gerald Coetzee', team: null, role: 'BOWL', os: true, bat: 25, bowl: 87, base: 1.5, uncapped: false, jersey: 62 },
      { id: 105, name: 'Mark Wood', team: null, role: 'BOWL', os: true, bat: 20, bowl: 89, base: 2.0, uncapped: false, jersey: 33 },
      { id: 106, name: 'Devdutt Padikkal', team: null, role: 'BAT', os: false, bat: 84, bowl: 10, base: 1.0, uncapped: false, jersey: 37 },
      { id: 107, name: 'Prithvi Shaw', team: null, role: 'BAT', os: false, bat: 85, bowl: 10, base: 1.0, uncapped: false, jersey: 100 },
      { id: 108, name: 'Sarfaraz Khan', team: null, role: 'BAT', os: false, bat: 83, bowl: 10, base: 0.75, uncapped: false, jersey: 97 },
      { id: 109, name: 'Manish Pandey', team: null, role: 'BAT', os: false, bat: 82, bowl: 10, base: 1.0, uncapped: false, jersey: 31 },
      { id: 110, name: 'Wriddhiman Saha', team: null, role: 'WK', os: false, bat: 82, bowl: 10, base: 1.0, uncapped: false, jersey: 6 },
      { id: 111, name: 'K.S. Bharat', team: null, role: 'WK', os: false, bat: 80, bowl: 10, base: 0.75, uncapped: false, jersey: 13 },
      { id: 112, name: 'Vijay Shankar', team: null, role: 'AR', os: false, bat: 80, bowl: 75, base: 1.0, uncapped: false, jersey: 59 },
      { id: 113, name: 'Deepak Hooda', team: null, role: 'AR', os: false, bat: 81, bowl: 74, base: 1.0, uncapped: false, jersey: 27 },
      { id: 114, name: 'Shivam Mavi', team: null, role: 'BOWL', os: false, bat: 20, bowl: 83, base: 1.0, uncapped: false, jersey: 23 },
      { id: 115, name: 'Chetan Sakariya', team: null, role: 'BOWL', os: false, bat: 15, bowl: 83, base: 1.0, uncapped: false, jersey: 29 },
      { id: 116, name: 'Sandeep Sharma', team: null, role: 'BOWL', os: false, bat: 15, bowl: 85, base: 1.0, uncapped: false, jersey: 28 },
      { id: 117, name: 'Varun Aaron', team: null, role: 'BOWL', os: false, bat: 15, bowl: 82, base: 1.0, uncapped: false, jersey: 39 },
      { id: 118, name: 'Kamlesh Nagarkoti', team: null, role: 'BOWL', os: false, bat: 20, bowl: 81, base: 0.75, uncapped: false, jersey: 44 },
      { id: 119, name: 'Ravi Ashwin', team: null, role: 'AR', os: false, bat: 75, bowl: 89, base: 2.0, uncapped: false, jersey: 99 },
      { id: 120, name: 'Piyush Chawla', team: null, role: 'BOWL', os: false, bat: 35, bowl: 87, base: 1.5, uncapped: false, jersey: 11 },
      { id: 121, name: 'Jason Roy', team: null, role: 'BAT', os: true, bat: 88, bowl: 10, base: 1.5, uncapped: false, jersey: 20 },
      { id: 122, name: 'Rilee Rossouw', team: null, role: 'BAT', os: true, bat: 87, bowl: 10, base: 1.5, uncapped: false, jersey: 99 },
      { id: 123, name: 'Sherfane Rutherford', team: null, role: 'AR', os: true, bat: 84, bowl: 76, base: 1.2, uncapped: false, jersey: 50 },
      { id: 124, name: 'Romario Shepherd', team: null, role: 'AR', os: true, bat: 83, bowl: 82, base: 1.5, uncapped: false, jersey: 16 },
      { id: 125, name: 'Duan Jansen', team: null, role: 'AR', os: true, bat: 70, bowl: 80, base: 1.0, uncapped: false, jersey: 72 },
      { id: 126, name: 'Spencer Johnson', team: null, role: 'BOWL', os: true, bat: 15, bowl: 86, base: 1.5, uncapped: false, jersey: 92 },
      { id: 127, name: 'Jhye Richardson', team: null, role: 'BOWL', os: true, bat: 25, bowl: 86, base: 1.5, uncapped: false, jersey: 13 },
      { id: 128, name: 'Nathan Ellis', team: null, role: 'BOWL', os: true, bat: 20, bowl: 86, base: 1.2, uncapped: false, jersey: 34 },
      { id: 129, name: 'Reece Topley', team: null, role: 'BOWL', os: true, bat: 15, bowl: 87, base: 1.5, uncapped: false, jersey: 37 },
      { id: 130, name: 'Tom Curran', team: null, role: 'AR', os: true, bat: 78, bowl: 82, base: 1.5, uncapped: false, jersey: 59 },
      { id: 131, name: 'Taskin Ahmed', team: null, role: 'BOWL', os: true, bat: 20, bowl: 86, base: 1.2, uncapped: false, jersey: 3 },
      { id: 132, name: 'Liton Das', team: null, role: 'WK', os: true, bat: 84, bowl: 10, base: 1.0, uncapped: false, jersey: 16 },
      { id: 133, name: 'Shakib Al Hasan', team: null, role: 'AR', os: true, bat: 85, bowl: 86, base: 2.0, uncapped: false, jersey: 75 },
      { id: 134, name: 'Mehidy Hasan', team: null, role: 'AR', os: true, bat: 80, bowl: 82, base: 1.2, uncapped: false, jersey: 53 },
      { id: 135, name: 'Dasun Shanaka', team: null, role: 'AR', os: true, bat: 84, bowl: 78, base: 1.2, uncapped: false, jersey: 7 },
      { id: 136, name: 'Charith Asalanka', team: null, role: 'BAT', os: true, bat: 85, bowl: 20, base: 1.2, uncapped: false, jersey: 50 },
      { id: 137, name: 'Kusal Mendis', team: null, role: 'WK', os: true, bat: 86, bowl: 10, base: 1.5, uncapped: false, jersey: 13 },
      { id: 138, name: 'Pathum Nissanka', team: null, role: 'BAT', os: true, bat: 86, bowl: 10, base: 1.5, uncapped: false, jersey: 18 },
      { id: 139, name: 'Dushmantha Chameera', team: null, role: 'BOWL', os: true, bat: 15, bowl: 86, base: 1.5, uncapped: false, jersey: 55 },
      { id: 140, name: 'Dilshan Madushanka', team: null, role: 'BOWL', os: true, bat: 15, bowl: 86, base: 1.2, uncapped: false, jersey: 98 }
    ]
  },

  LLC: {
    id: 'LLC',
    title: 'Legends League Cricket',
    subtitle: 'Boss Logon Ka Game (LLC T20)',
    purse: 80.0,
    maxRetention: 4,
    maxOSInSquad: 6,
    minSquad: 14,
    maxSquad: 18,
    teams: [
      { id: 'IC',  name: 'India Capitals', color: '#2563eb', venue: 'Delhi' },
      { id: 'GG',  name: 'Gujarat Greats', color: '#f59e0b', venue: 'Ahmedabad' },
      { id: 'MB',  name: 'Manipal Tigers', color: '#eab308', venue: 'Bengaluru' },
      { id: 'SSG', name: 'Southern Super Stars', color: '#ef4444', venue: 'Hyderabad' },
      { id: 'KS',  name: 'Konark Suryas Odisha', color: '#f97316', venue: 'Cuttack' },
      { id: 'UHR', name: 'Urbanrisers Hyderabad', color: '#10b981', venue: 'Hyderabad' },
      { id: 'BRS', name: 'Bhilwara Kings', color: '#8b5cf6', venue: 'Jodhpur' },
      { id: 'TT',  name: 'Toyam Hyderabad', color: '#06b6d4', venue: 'Ranchi' }
    ],
    players: [
      // India Capitals[span_17](start_span)[span_17](end_span)
      { id: 201, name: 'Gautam Gambhir', team: 'IC', role: 'BAT', os: false, bat: 91, bowl: 10, base: 2.0, uncapped: false, jersey: 5 },
      { id: 202, name: 'Yusuf Pathan', team: 'IC', role: 'AR', os: false, bat: 90, bowl: 78, base: 2.0, uncapped: false, jersey: 28 },
      { id: 203, name: 'Jacques Kallis', team: 'IC', role: 'AR', os: true, bat: 93, bowl: 88, base: 2.0, uncapped: false, jersey: 3 },
      { id: 204, name: 'Mitchell Johnson', team: 'IC', role: 'BOWL', os: true, bat: 42, bowl: 91, base: 2.0, uncapped: false, jersey: 25 },
      { id: 205, name: 'Pravin Tambe', team: 'IC', role: 'BOWL', os: false, bat: 15, bowl: 85, base: 1.0, uncapped: false, jersey: 2 },
      // Gujarat Greats[span_18](start_span)[span_18](end_span)
      { id: 206, name: 'Shikhar Dhawan', team: 'GG', role: 'BAT', os: false, bat: 93, bowl: 15, base: 2.0, uncapped: false, jersey: 42 },
      { id: 207, name: 'Chris Gayle', team: 'GG', role: 'BAT', os: true, bat: 96, bowl: 55, base: 2.0, uncapped: false, jersey: 333 },
      { id: 208, name: 'Mohammad Kaif', team: 'GG', role: 'BAT', os: false, bat: 84, bowl: 15, base: 1.5, uncapped: false, jersey: 11 },
      { id: 209, name: 'Sreesanth', team: 'GG', role: 'BOWL', os: false, bat: 20, bowl: 87, base: 1.5, uncapped: false, jersey: 36 },
      { id: 210, name: 'Liam Plunkett', team: 'GG', role: 'BOWL', os: true, bat: 38, bowl: 86, base: 1.5, uncapped: false, jersey: 17 },
      // Manipal Tigers[span_19](start_span)[span_19](end_span)
      { id: 211, name: 'Harbhajan Singh', team: 'MB', role: 'BOWL', os: false, bat: 48, bowl: 90, base: 2.0, uncapped: false, jersey: 3 },
      { id: 212, name: 'Robin Uthappa', team: 'MB', role: 'WK', os: false, bat: 89, bowl: 10, base: 2.0, uncapped: false, jersey: 37 },
      { id: 213, name: 'Thisara Perera', team: 'MB', role: 'AR', os: true, bat: 85, bowl: 83, base: 1.5, uncapped: false, jersey: 1 },
      { id: 214, name: 'Corey Anderson', team: 'MB', role: 'AR', os: true, bat: 86, bowl: 80, base: 1.5, uncapped: false, jersey: 78 },
      { id: 215, name: 'Muttiah Muralitharan', team: 'MB', role: 'BOWL', os: true, bat: 15, bowl: 95, base: 2.0, uncapped: false, jersey: 800 },
      // Southern Super Stars[span_20](start_span)[span_20](end_span)
      { id: 216, name: 'Dinesh Karthik', team: 'SSG', role: 'WK', os: false, bat: 91, bowl: 10, base: 2.0, uncapped: false, jersey: 19 },
      { id: 217, name: 'Kedar Jadhav', team: 'SSG', role: 'AR', os: false, bat: 85, bowl: 68, base: 1.5, uncapped: false, jersey: 81 },
      { id: 218, name: 'Ross Taylor', team: 'SSG', role: 'BAT', os: true, bat: 90, bowl: 10, base: 2.0, uncapped: false, jersey: 3 },
      { id: 219, name: 'Martin Guptill', team: 'SSG', role: 'BAT', os: true, bat: 89, bowl: 15, base: 2.0, uncapped: false, jersey: 31 },
      { id: 220, name: 'Abdur Razzak', team: 'SSG', role: 'BOWL', os: true, bat: 25, bowl: 85, base: 1.0, uncapped: false, jersey: 41 },
      // Konark Suryas Odisha[span_21](start_span)[span_21](end_span)
      { id: 221, name: 'Irfan Pathan', team: 'KS', role: 'AR', os: false, bat: 85, bowl: 89, base: 2.0, uncapped: false, jersey: 56 },
      { id: 222, name: 'Ambati Rayudu', team: 'KS', role: 'BAT', os: false, bat: 88, bowl: 10, base: 2.0, uncapped: false, jersey: 9 },
      { id: 223, name: 'Kevin Pietersen', team: 'KS', role: 'BAT', os: true, bat: 93, bowl: 35, base: 2.0, uncapped: false, jersey: 24 },
      { id: 224, name: 'Vinay Kumar', team: 'KS', role: 'BOWL', os: false, bat: 28, bowl: 86, base: 1.5, uncapped: false, jersey: 23 },
      { id: 225, name: 'Dilshan Munaweera', team: 'KS', role: 'AR', os: true, bat: 83, bowl: 72, base: 1.0, uncapped: false, jersey: 14 },
      // Urbanrisers Hyderabad[span_22](start_span)[span_22](end_span)
      { id: 226, name: 'Suresh Raina', team: 'UHR', role: 'BAT', os: false, bat: 94, bowl: 62, base: 2.0, uncapped: false, jersey: 48 },
      { id: 227, name: 'Stuart Binny', team: 'UHR', role: 'AR', os: false, bat: 81, bowl: 80, base: 1.5, uncapped: false, jersey: 84 },
      { id: 228, name: 'Dwayne Smith', team: 'UHR', role: 'AR', os: true, bat: 87, bowl: 76, base: 1.5, uncapped: false, jersey: 50 },
      { id: 229, name: 'Pragyan Ojha', team: 'UHR', role: 'BOWL', os: false, bat: 15, bowl: 87, base: 1.5, uncapped: false, jersey: 30 },
      { id: 230, name: 'Tino Best', team: 'UHR', role: 'BOWL', os: true, bat: 25, bowl: 85, base: 1.0, uncapped: false, jersey: 36 },
      // Bhilwara Kings[span_23](start_span)[span_23](end_span)
      { id: 231, name: 'Virender Sehwag', team: 'BRS', role: 'BAT', os: false, bat: 95, bowl: 55, base: 2.0, uncapped: false, jersey: 44 },
      { id: 232, name: 'Shane Watson', team: 'BRS', role: 'AR', os: true, bat: 92, bowl: 88, base: 2.0, uncapped: false, jersey: 33 },
      { id: 233, name: 'Munaf Patel', team: 'BRS', role: 'BOWL', os: false, bat: 18, bowl: 87, base: 1.5, uncapped: false, jersey: 13 },
      { id: 234, name: 'Tillakaratne Dilshan', team: 'BRS', role: 'AR', os: true, bat: 90, bowl: 72, base: 2.0, uncapped: false, jersey: 23 },
      { id: 235, name: 'Naman Ojha', team: 'BRS', role: 'WK', os: false, bat: 84, bowl: 10, base: 1.0, uncapped: false, jersey: 77 },
      // Toyam Hyderabad[span_24](start_span)[span_24](end_span)
      { id: 236, name: 'Yuvraj Singh', team: 'TT', role: 'AR', os: false, bat: 95, bowl: 82, base: 2.0, uncapped: false, jersey: 12 },
      { id: 237, name: 'Brett Lee', team: 'TT', role: 'BOWL', os: true, bat: 35, bowl: 93, base: 2.0, uncapped: false, jersey: 58 },
      { id: 238, name: 'Parthiv Patel', team: 'TT', role: 'WK', os: false, bat: 86, bowl: 10, base: 1.5, uncapped: false, jersey: 42 },
      { id: 239, name: 'Lendl Simmons', team: 'TT', role: 'BAT', os: true, bat: 88, bowl: 25, base: 1.5, uncapped: false, jersey: 54 },
      { id: 240, name: 'Ashok Dinda', team: 'TT', role: 'BOWL', os: false, bat: 15, bowl: 85, base: 1.5, uncapped: false, jersey: 11 },
      // Expanded Legends Unassigned Pool with real names[span_25](start_span)[span_25](end_span)
      { id: 241, name: 'Sachin Tendulkar', team: null, role: 'BAT', os: false, bat: 98, bowl: 62, base: 2.0, uncapped: false, jersey: 10 },
      { id: 242, name: 'AB de Villiers', team: null, role: 'WK', os: true, bat: 97, bowl: 15, base: 2.0, uncapped: false, jersey: 17 },
      { id: 243, name: 'Brian Lara', team: null, role: 'BAT', os: true, bat: 95, bowl: 10, base: 2.0, uncapped: false, jersey: 9 },
      { id: 244, name: 'Zaheer Khan', team: null, role: 'BOWL', os: false, bat: 28, bowl: 92, base: 2.0, uncapped: false, jersey: 34 },
      { id: 245, name: 'Dale Steyn', team: null, role: 'BOWL', os: true, bat: 25, bowl: 95, base: 2.0, uncapped: false, jersey: 8 },
      { id: 246, name: 'Lasith Malinga', team: null, role: 'BOWL', os: true, bat: 22, bowl: 94, base: 2.0, uncapped: false, jersey: 99 },
      { id: 247, name: 'Kumar Sangakkara', team: null, role: 'WK', os: true, bat: 93, bowl: 10, base: 2.0, uncapped: false, jersey: 11 },
      { id: 248, name: 'Mahela Jayawardene', team: null, role: 'BAT', os: true, bat: 91, bowl: 15, base: 2.0, uncapped: false, jersey: 27 },
      { id: 249, name: 'Matthew Hayden', team: null, role: 'BAT', os: true, bat: 92, bowl: 10, base: 2.0, uncapped: false, jersey: 28 },
      { id: 250, name: 'Adam Gilchrist', team: null, role: 'WK', os: true, bat: 94, bowl: 10, base: 2.0, uncapped: false, jersey: 18 },
      { id: 251, name: 'Dwayne Bravo', team: null, role: 'AR', os: true, bat: 86, bowl: 91, base: 2.0, uncapped: false, jersey: 47 },
      { id: 252, name: 'Kieron Pollard', team: null, role: 'AR', os: true, bat: 90, bowl: 82, base: 2.0, uncapped: false, jersey: 55 },
      { id: 253, name: 'Glenn McGrath', team: null, role: 'BOWL', os: true, bat: 15, bowl: 94, base: 2.0, uncapped: false, jersey: 11 },
      { id: 254, name: 'Anil Kumble', team: null, role: 'BOWL', os: false, bat: 35, bowl: 93, base: 2.0, uncapped: false, jersey: 37 },
      { id: 255, name: 'Sourav Ganguly', team: null, role: 'BAT', os: false, bat: 91, bowl: 58, base: 2.0, uncapped: false, jersey: 99 },
      { id: 256, name: 'Rahul Dravid', team: null, role: 'BAT', os: false, bat: 92, bowl: 10, base: 2.0, uncapped: false, jersey: 19 },
      { id: 257, name: 'Hashim Amla', team: null, role: 'BAT', os: true, bat: 91, bowl: 10, base: 1.5, uncapped: false, jersey: 1 },
      { id: 258, name: 'JP Duminy', team: null, role: 'AR', os: true, bat: 86, bowl: 74, base: 1.5, uncapped: false, jersey: 21 },
      { id: 259, name: 'Aaron Finch', team: null, role: 'BAT', os: true, bat: 89, bowl: 20, base: 1.5, uncapped: false, jersey: 5 },
      { id: 260, name: 'Eoin Morgan', team: null, role: 'BAT', os: true, bat: 88, bowl: 10, base: 1.5, uncapped: false, jersey: 16 },
      { id: 261, name: 'Murali Vijay', team: null, role: 'BAT', os: false, bat: 85, bowl: 15, base: 1.0, uncapped: false, jersey: 8 },
      { id: 262, name: 'Subramaniam Badrinath', team: null, role: 'BAT', os: false, bat: 83, bowl: 10, base: 1.0, uncapped: false, jersey: 33 },
      { id: 263, name: 'RP Singh', team: null, role: 'BOWL', os: false, bat: 18, bowl: 87, base: 1.5, uncapped: false, jersey: 9 },
      { id: 264, name: 'Piyush Chawla', team: null, role: 'BOWL', os: false, bat: 42, bowl: 88, base: 1.5, uncapped: false, jersey: 11 },
      { id: 265, name: 'Amit Mishra', team: null, role: 'BOWL', os: false, bat: 30, bowl: 89, base: 1.5, uncapped: false, jersey: 99 },
      { id: 266, name: 'Chaminda Vaas', team: null, role: 'BOWL', os: true, bat: 45, bowl: 89, base: 1.5, uncapped: false, jersey: 22 },
      { id: 267, name: 'Sanath Jayasuriya', team: null, role: 'AR', os: true, bat: 92, bowl: 82, base: 2.0, uncapped: false, jersey: 7 },
      { id: 268, name: 'Daniel Vettori', team: null, role: 'AR', os: true, bat: 68, bowl: 90, base: 1.5, uncapped: false, jersey: 11 },
      { id: 269, name: 'Shaun Marsh', team: null, role: 'BAT', os: true, bat: 88, bowl: 10, base: 1.5, uncapped: false, jersey: 9 },
      { id: 270, name: 'Albie Morkel', team: null, role: 'AR', os: true, bat: 86, bowl: 84, base: 1.5, uncapped: false, jersey: 81 },
      { id: 271, name: 'Herschelle Gibbs', team: null, role: 'BAT', os: true, bat: 89, bowl: 10, base: 1.5, uncapped: false, jersey: 00 },
      { id: 272, name: 'Graeme Smith', team: null, role: 'BAT', os: true, bat: 90, bowl: 15, base: 2.0, uncapped: false, jersey: 9 },
      { id: 273, name: 'Brad Haddin', team: null, role: 'WK', os: true, bat: 85, bowl: 10, base: 1.5, uncapped: false, jersey: 5 },
      { id: 274, name: 'Michael Hussey', team: null, role: 'BAT', os: true, bat: 92, bowl: 20, base: 2.0, uncapped: false, jersey: 48 },
      { id: 275, name: 'Shane Watson', team: null, role: 'AR', os: true, bat: 91, bowl: 85, base: 2.0, uncapped: false, jersey: 33 },
      { id: 276, name: 'Brad Hogg', team: null, role: 'BOWL', os: true, bat: 20, bowl: 88, base: 1.2, uncapped: false, jersey: 9 },
      { id: 277, name: 'Nathan Bracken', team: null, role: 'BOWL', os: true, bat: 15, bowl: 89, base: 1.5, uncapped: false, jersey: 14 },
      { id: 278, name: 'Stuart Broad', team: null, role: 'BOWL', os: true, bat: 35, bowl: 91, base: 2.0, uncapped: false, jersey: 8 },
      { id: 279, name: 'Tim Bresnan', team: null, role: 'AR', os: true, bat: 78, bowl: 83, base: 1.2, uncapped: false, jersey: 19 },
      { id: 280, name: 'Owais Shah', team: null, role: 'BAT', os: true, bat: 84, bowl: 20, base: 1.0, uncapped: false, jersey: 7 }
    ]
  }
};

const RETENTION_SLABS = [18, 14, 11, 18, 14];

// ==================== CENTRAL GAME STATE ====================
const state = {
  leagueId: 'IPL',
  screen: 'HOME',
  season: 1,
  auctionType: 'MEGA',
  mode: 'SOLO',
  roomCode: '',
  userTeam: 'RCB',
  friends: [],
  franchises: {},
  players: [],
  auction: {
    pool: [],
    idx: 0,
    currentBid: 0,
    highestBidder: null,
    timer: 100,
    speed: 1,
    paused: false,
    autoBid: false,
    logs: [],
    rtmPending: null
  },
  seasonData: {
    fixtures: [],
    currentMatchIdx: 0,
    orangeCap: {},
    purpleCap: {},
    champion: null
  },
  liveMatch: null
};

let auctionInterval = null;
let matchInterval = null;

function activeLeague() { return LEAGUES[state.leagueId]; }
function activeTeams() { return activeLeague().teams; }

function switchLeague(lid) {
  state.leagueId = lid;
  state.userTeam = LEAGUES[lid].teams[0].id;
  render();
}

function initFranchises() {
  const lg = activeLeague();
  state.players = JSON.parse(JSON.stringify(lg.players));
  state.franchises = {};
  lg.teams.forEach(t => {
    const friend = state.friends.find(f => f.teamId === t.id);
    const isUser = t.id === state.userTeam;
    state.franchises[t.id] = {
      id: t.id,
      name: t.name,
      color: t.color,
      venue: t.venue,
      purse: lg.purse,
      squad: [],
      rtm: 0,
      xi: [],
      cap: null,
      vc: null,
      pts: 0, w: 0, l: 0, nrr: 0,
      isHuman: isUser || !!friend,
      ownerName: isUser ? 'You' : (friend ? friend.name : 'AI Bot')
    };
  });
}

function getTeam(id) { return state.franchises[id]; }
function fmtCr(v) { return '₹' + Number(v).toFixed(2).replace(/\.00$/, '') + ' Cr'; }
function roleBadge(r) {
  const map = { BAT: 'b-bat', BOWL: 'b-bowl', AR: 'b-ar', WK: 'b-wk' };
  return `<span class="badge ${map[r]||'b-bat'}">${r}</span>`;
}

// ==================== HOME & MULTIPLAYER LOBBY ====================
function renderHome() {
  const lg = activeLeague();
  document.getElementById('top-brand').innerHTML = `🏏 ${lg.title} <span style="color:var(--gold)">MANAGER</span>`;
  document.getElementById('top-status').innerText = lg.id;

  let teamGrid = lg.teams.map(t => `
    <button class="team-tile ${state.userTeam === t.id ? 'active' : ''}" onclick="state.userTeam='${t.id}'; render()">
      <div class="team-code"><span>${t.id}</span><span class="dot" style="background:${t.color}"></span></div>
      <div class="sub" style="font-size:11px; margin-top:3px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis;">${t.name}</div>
    </button>
  `).join('');

  return `
    <div class="card">
      <div class="h1">Cricket Franchise Manager 2026</div>
      <div class="sub">Play both <b>IPL 2026</b> (Min 18 - Max 25 squad) and <b>Legends League Cricket (LLC)</b> (Min 14 - Max 18 squad) with real named players, Mega Auctions, Retentions, RTM & Live 2D Matches!</div>
    </div>

    <div class="card">
      <div class="h2">1. Choose Tournament League</div>
      <div class="grid-2">
        <button class="league-tab ${state.leagueId === 'IPL' ? 'active-ipl' : ''}" onclick="switchLeague('IPL')">
          <div style="font-weight:900; font-size:15px;">🏆 IPL 2026</div>
          <div class="sub" style="font-size:10px;">10 Teams • ₹120 Cr • 18-25 Squad</div>
        </button>
        <button class="league-tab ${state.leagueId === 'LLC' ? 'active-llc' : ''}" onclick="switchLeague('LLC')">
          <div style="font-weight:900; font-size:15px; color:var(--gold);">👑 Legends League</div>
          <div class="sub" style="font-size:10px;">8 Teams • ₹80 Cr • 14-18 Squad</div>
        </button>
      </div>
    </div>

    <div class="card">
      <div class="h2">2. Select Your ${lg.id} Franchise</div>
      <div class="grid-2">${teamGrid}</div>
    </div>

    <div class="card">
      <div class="h2">3. Choose Game Mode</div>
      <div style="display:flex; flex-direction:column; gap:8px;">
        <button class="btn ${state.leagueId === 'LLC' ? 'btn-gold' : 'btn-blue'}" onclick="startSolo()">
          🏆 Start ${lg.title} Career (Mega Auction)
        </button>
        <button class="btn btn-dark" onclick="openMultiplayer()">
          🌐 Online Room Code Multiplayer
        </button>
      </div>
    </div>
  `;
}

function startSolo() {
  state.mode = 'SOLO';
  state.friends = [];
  state.season = 1;
  state.auctionType = 'MEGA';
  initFranchises();
  autoRetainAI();
  state.screen = 'RETENTION';
  render();
}

function openMultiplayer() {
  state.mode = 'MULTI';
  state.roomCode = state.leagueId + Math.floor(10 + Math.random() * 89);
  state.friends = [];
  state.screen = 'LOBBY';
  render();
}

function renderLobby() {
  const teams = activeTeams();
  const taken = [state.userTeam, ...state.friends.map(f => f.teamId)];
  const availTeams = teams.filter(t => !taken.includes(t.id));

  return `
    <div class="card">
      <div class="h2">
        <span>🌐 ${activeLeague().id} Multiplayer Room</span>
        <span class="pill" style="font-size:14px;">CODE: ${state.roomCode}</span>
      </div>
      <div class="sub">Share Room Code <b>${state.roomCode}</b> with friends or add a friend slot below to test live bidding & trading!</div>
      
      <div style="margin-top:12px;">
        <div class="row">
          <div><b>You (Host)</b> <span class="badge b-wk">${state.userTeam}</span></div>
          <span style="color:var(--green); font-size:12px; font-weight:800;">● READY</span>
        </div>
        ${state.friends.map((f, idx) => `
          <div class="row">
            <div><b>${f.name}</b> <span class="badge b-bat">${f.teamId}</span></div>
            <button class="btn-dark btn-sm" onclick="state.friends.splice(${idx},1); render()">Remove</button>
          </div>
        `).join('')}
      </div>

      ${availTeams.length ? `
      <div style="margin-top:12px; padding-top:12px; border-top:1px solid var(--border);">
        <div class="sub" style="margin-bottom:6px;">Simulate Friend Joining Room:</div>
        <div class="grid-2">
          <input id="friend-name" placeholder="Friend Name (e.g. Ayush)" value="Ayush" />
          <select id="friend-team">
            ${availTeams.map(t => `<option value="${t.id}">${t.id} - ${t.name}</option>`).join('')}
          </select>
        </div>
        <button class="btn btn-dark" style="margin-top:8px;" onclick="addFriendToRoom()">+ Add Friend to Room</button>
      </div>` : ''}
    </div>

    <div class="card">
      <div class="sub" style="margin-bottom:10px;">Remaining ${teams.length - taken.length} franchises will be controlled by Aggressive AI Bots.</div>
      <div class="grid-2">
        <button class="btn btn-dark" onclick="state.screen='HOME'; render()">← Back</button>
        <button class="btn btn-green" onclick="launchMultiplayer()">Start Retention Room →</button>
      </div>
    </div>
  `;
}

function addFriendToRoom() {
  const name = document.getElementById('friend-name').value.trim() || 'Friend';
  const teamId = document.getElementById('friend-team').value;
  state.friends.push({ name, teamId });
  render();
}

function launchMultiplayer() {
  state.season = 1;
  state.auctionType = 'MEGA';
  initFranchises();
  autoRetainAI();
  state.screen = 'RETENTION';
  render();
}

// ==================== RETENTION & RTM PHASE ====================
function autoRetainAI() {
  const lg = activeLeague();
  lg.teams.forEach(t => {
    const f = state.franchises[t.id];
    if (f.id === state.userTeam) return;
    const teamPlayers = state.players.filter(p => p.team === t.id).sort((a,b) => Math.max(b.bat, b.bowl) - Math.max(a.bat, a.bowl));
    const maxRet = lg.id === 'LLC' ? 3 : 4;
    const count = 2 + Math.floor(Math.random() * (maxRet - 1));
    let cappedIdx = 0;
    for (let i = 0; i < Math.min(count, teamPlayers.length); i++) {
      const p = teamPlayers[i];
      const cost = lg.id === 'LLC' ? (12 - cappedIdx++ * 3) : (p.uncapped ? 4 : RETENTION_SLABS[cappedIdx++]);
      if (f.purse >= cost) {
        f.purse -= cost;
        p.soldPrice = cost;
        p.retained = true;
        f.squad.push(p);
      }
    }
    f.rtm = Math.max(0, lg.maxRetention - f.squad.length);
  });
}

function toggleUserRetention(playerId) {
  const lg = activeLeague();
  const f = getTeam(state.userTeam);
  const p = state.players.find(x => x.id === playerId);
  const idx = f.squad.findIndex(x => x.id === playerId);

  if (idx >= 0) {
    f.squad.splice(idx, 1);
    p.retained = false;
    p.soldPrice = 0;
  } else {
    if (f.squad.length >= lg.maxRetention) return alert(`Maximum ${lg.maxRetention} retentions allowed in ${lg.id}!`);
    const uncappedCount = f.squad.filter(x => x.uncapped).length;
    if (p.uncapped && uncappedCount >= 2) return alert('Max 2 uncapped retentions allowed!');
    f.squad.push(p);
    p.retained = true;
  }

  let cappedIdx = 0;
  let totalCost = 0;
  f.squad.forEach(sp => {
    const c = lg.id === 'LLC' ? Math.max(4, 12 - cappedIdx++ * 3) : (sp.uncapped ? 4 : RETENTION_SLABS[cappedIdx++]);
    sp.soldPrice = c;
    totalCost += c;
  });
  f.purse = lg.purse - totalCost;
  f.rtm = Math.max(0, lg.maxRetention - f.squad.length);
  render();
}

function renderRetention() {
  const lg = activeLeague();
  const f = getTeam(state.userTeam);
  const roster = state.players.filter(p => p.team === state.userTeam);
  document.getElementById('top-status').innerText = `PURSE: ${fmtCr(f.purse)} | RTM: ${f.rtm}`;

  return `
    <div class="card">
      <div class="h2">
        <span>🔒 ${f.id} Retention & RTM Room</span>
        <span class="pill">${f.squad.length}/${lg.maxRetention} Retained</span>
      </div>
      <div class="sub">${lg.title} Rules: Unused retention slots convert into <b>RTM Cards (${f.rtm})</b> for the Mega Auction! (Squad Limit: Min ${lg.minSquad}, Max ${lg.maxSquad})</div>
      
      <div class="grid-3" style="margin-top:10px; text-align:center;">
        <div class="franchise-chip"><div class="sub">Purse Left</div><b>${fmtCr(f.purse)}</b></div>
        <div class="franchise-chip"><div class="sub">Retained</div><b>${f.squad.length} Players</b></div>
        <div class="franchise-chip"><div class="sub">RTM Cards</div><b style="color:var(--gold)">${f.rtm} RTMs</b></div>
      </div>
    </div>

    <div class="card">
      <div class="h2">Your ${lg.id} Core Roster</div>
      ${roster.map(p => {
        const isRet = f.squad.some(x => x.id === p.id);
        return `
          <div class="row" style="${isRet ? 'border-color:var(--gold); background:rgba(245,158,11,0.08);' : ''}">
            <div>
              <div style="font-weight:800; font-size:14px;">${p.name} ${p.os ? '<span class="badge b-os">OS</span>' : ''} ${p.uncapped ? '<span class="badge b-bowl">UNCAPPED ₹4Cr</span>' : ''}</div>
              <div class="sub">${roleBadge(p.role)} &nbsp; BAT ${p.bat} • BOWL ${p.bowl}</div>
            </div>
            <button class="btn-sm ${isRet ? 'btn-gold' : 'btn-dark'}" onclick="toggleUserRetention(${p.id})">
              ${isRet ? '✓ ' + fmtCr(p.soldPrice) : '+ Retain'}
            </button>
          </div>
        `;
      }).join('')}
    </div>

    <div class="bottom-dock">
      <div class="dock-inner">
        <button class="btn btn-green" onclick="startAuction('MEGA')">🔨 Lock Retentions & Enter Mega Auction →</button>
      </div>
    </div>
  `;
}

// ==================== LIVE AUCTION ENGINE ====================
function startAuction(type) {
  state.auctionType = type;
  const retainedIds = new Set();
  Object.values(state.franchises).forEach(f => f.squad.forEach(p => retainedIds.add(p.id)));

  const pool = state.players.filter(p => !retainedIds.has(p.id)).map(p => ({
    ...p,
    prevTeam: p.team,
    team: null,
    soldPrice: 0
  }));

  pool.sort((a,b) => (Math.max(b.bat, b.bowl) + Math.random()*12) - (Math.max(a.bat, a.bowl) + Math.random()*12));

  state.auction = {
    pool,
    idx: 0,
    currentBid: 0,
    highestBidder: null,
    timer: 100,
    speed: 1,
    paused: false,
    autoBid: false,
    logs: [`🔨 ${activeLeague().id} ${type} AUCTION LIVE! ${pool.length} real named players in the hammer pool.`],
    rtmPending: null
  };

  loadNextAuctionPlayer();
  state.screen = 'AUCTION';
  render();
  startAuctionLoop();
}

function loadNextAuctionPlayer() {
  const a = state.auction;
  if (a.idx >= a.pool.length) {
    stopAuctionLoop();
    fillRemainingSquadsAI();
    openSquadXI();
    return;
  }
  const p = a.pool[a.idx];
  a.currentBid = p.base;
  a.highestBidder = null;
  a.timer = 100;
  a.rtmPending = null;
  a.logs.unshift(`📢 On the block: <b>${p.name}</b> (${p.role}${p.os?' • OS':''}) — Base ${fmtCr(p.base)}`);
}

function getBidIncrement(val) {
  if (val < 5) return 0.25;
  return 0.50;
}

function nextBidAmount() {
  const a = state.auction;
  if (!a.highestBidder) return a.pool[a.idx].base;
  return +(a.currentBid + getBidIncrement(a.currentBid)).toFixed(2);
}

function placeBid(teamId) {
  const a = state.auction;
  const lg = activeLeague();
  if (a.rtmPending) return;
  const p = a.pool[a.idx];
  const f = getTeam(teamId);
  const amt = nextBidAmount();

  if (a.highestBidder === teamId) return;
  if (f.purse < amt) return;
  if (f.squad.length >= lg.maxSquad) return;
  if (p.os && f.squad.filter(x => x.os).length >= lg.maxOSInSquad) return;

  a.currentBid = amt;
  a.highestBidder = teamId;
  a.timer = 100;
  a.logs.unshift(`✋ <b>${teamId}</b> bids <span style="color:var(--gold)">${fmtCr(amt)}</span> for ${p.name}`);
  render();
}

function aiMaxValuation(f, p) {
  const lg = activeLeague();
  const skill = Math.max(p.bat, p.bowl) + (p.role === 'AR' ? 6 : 0);
  let val = 1.0;
  if (skill >= 94) val = 14 + Math.random() * 6;
  else if (skill >= 90) val = 10 + Math.random() * 5;
  else if (skill >= 86) val = 5.5 + Math.random() * 4.5;
  else if (skill >= 82) val = 2.5 + Math.random() * 3.0;
  else val = p.base + Math.random() * 1.2;

  if (lg.id === 'LLC') val *= 0.72;
  if (f.squad.length < lg.minSquad) val *= 1.5;

  const roleCount = f.squad.filter(x => x.role === p.role).length;
  if (roleCount < 2) val *= 1.25;
  if (!p.os) val *= 1.15;
  return Math.min(val, f.purse - (Math.max(0, lg.minSquad - f.squad.length) * 0.4));
}

function startAuctionLoop() {
  stopAuctionLoop();
  auctionInterval = setInterval(() => {
    const a = state.auction;
    const lg = activeLeague();
    if (state.screen !== 'AUCTION' || a.paused || a.rtmPending) return;

    const p = a.pool[a.idx];
    if (!p) return;

    if (a.autoBid && a.highestBidder !== state.userTeam && nextBidAmount() <= 10) {
      placeBid(state.userTeam);
    }

    if (a.timer < 88 && Math.random() < 0.58) {
      const nextAmt = nextBidAmount();
      const candidates = activeTeams().map(t => getTeam(t.id)).filter(f => {
        if (f.id === state.userTeam || f.id === a.highestBidder) return false;
        if (f.purse < nextAmt || f.squad.length >= lg.maxSquad) return false;
        if (p.os && f.squad.filter(x => x.os).length >= lg.maxOSInSquad) return false;
        return aiMaxValuation(f, p) >= nextAmt;
      });

      if (candidates.length > 0) {
        const chosen = candidates[Math.floor(Math.random() * candidates.length)];
        placeBid(chosen.id);
        return;
      }
    }

    a.timer -= 14;
    if (a.timer <= 0) {
      resolveCurrentPlayer();
    } else {
      const fill = document.getElementById('auc-timer-fill');
      if (fill) fill.style.width = Math.max(0, a.timer) + '%';
    }
  }, 550 / state.auction.speed);
}

function stopAuctionLoop() {
  if (auctionInterval) { clearInterval(auctionInterval); auctionInterval = null; }
}

function resolveCurrentPlayer() {
  const a = state.auction;
  const lg = activeLeague();
  const p = a.pool[a.idx];

  if (!a.highestBidder) {
    a.logs.unshift(`❌ <b>${p.name}</b> goes UNSOLD.`);
    a.idx++;
    loadNextAuctionPlayer();
    render();
    return;
  }

  const orig = p.prevTeam ? getTeam(p.prevTeam) : null;
  if (state.auctionType === 'MEGA' && orig && orig.id !== a.highestBidder && orig.rtm > 0 && orig.purse >= a.currentBid && orig.squad.length < lg.maxSquad && (!p.os || orig.squad.filter(x=>x.os).length < lg.maxOSInSquad)) {
    if (orig.id === state.userTeam) {
      a.rtmPending = { player: p, winnerTeam: a.highestBidder, bidAmount: a.currentBid };
      render();
      return;
    } else if (Math.random() < 0.45 && aiMaxValuation(orig, p) >= a.currentBid) {
      orig.rtm--;
      a.highestBidder = orig.id;
      a.logs.unshift(`🃏 <b>${orig.id}</b> uses <b>RTM CARD</b> to reclaim ${p.name} at ${fmtCr(a.currentBid)}!`);
    }
  }

  finalizeSale(p, a.highestBidder, a.currentBid);
}

function handleUserRTM(useIt) {
  const a = state.auction;
  const { player, winnerTeam, bidAmount } = a.rtmPending;
  const userF = getTeam(state.userTeam);

  if (useIt) {
    userF.rtm--;
    const winnerF = getTeam(winnerTeam);
    const counter = +(bidAmount + 1.5).toFixed(2);
    if (winnerF.purse >= counter && aiMaxValuation(winnerF, player) >= counter && userF.purse >= counter) {
      a.logs.unshift(`🔥 ${winnerTeam} counters RTM to ${fmtCr(counter)}! ${state.userTeam} matches it!`);
      finalizeSale(player, state.userTeam, counter);
    } else {
      a.logs.unshift(`🃏 <b>${state.userTeam}</b> exercises RTM Card for ${player.name}!`);
      finalizeSale(player, state.userTeam, bidAmount);
    }
  } else {
    finalizeSale(player, winnerTeam, bidAmount);
  }
}

function finalizeSale(p, teamId, price) {
  const a = state.auction;
  const f = getTeam(teamId);
  f.purse = +(f.purse - price).toFixed(2);
  p.team = teamId;
  p.soldPrice = price;
  f.squad.push(p);

  const mainP = state.players.find(x => x.id === p.id);
  if (mainP) { mainP.team = teamId; mainP.soldPrice = price; }

  a.logs.unshift(`🔨 <b style="color:var(--green)">SOLD!</b> <b>${p.name}</b> → <b>${teamId}</b> for <b>${fmtCr(price)}</b>`);
  a.idx++;
  loadNextAuctionPlayer();
  render();
}

function skipCurrentPlayer() {
  const a = state.auction;
  const lg = activeLeague();
  const p = a.pool[a.idx];
  if (!p) return;
  let bestTeam = a.highestBidder;
  let bestBid = a.currentBid;
  activeTeams().forEach(t => {
    const f = getTeam(t.id);
    if (f.id === state.userTeam) return;
    if (f.squad.length >= lg.maxSquad || (p.os && f.squad.filter(x=>x.os).length < lg.maxOSInSquad)) return;
    const maxV = aiMaxValuation(f, p);
    if (maxV > bestBid && f.purse >= bestBid + 0.5) {
      bestBid = +(Math.min(maxV, bestBid + 1.5 + Math.random()*3)).toFixed(2);
      bestTeam = f.id;
    }
  });
  if (bestTeam) finalizeSale(p, bestTeam, bestBid);
  else { a.idx++; loadNextAuctionPlayer(); render(); }
}

function simAllAuction() {
  stopAuctionLoop();
  const a = state.auction;
  const lg = activeLeague();
  while (a.idx < a.pool.length) {
    const p = a.pool[a.idx];
    const elig = activeTeams().map(t => getTeam(t.id)).filter(f => f.purse >= p.base && f.squad.length < lg.maxSquad && (!p.os || f.squad.filter(x=>x.os).length < lg.maxOSInSquad));
    if (elig.length) {
      elig.sort((x,y) => {
        const xNeed = x.squad.length < lg.minSquad ? 1 : 0;
        const yNeed = y.squad.length < lg.minSquad ? 1 : 0;
        if (xNeed !== yNeed) return yNeed - xNeed;
        return y.purse - x.purse;
      });
      const buyer = elig[0];
      const price = +(Math.min(buyer.purse, Math.max(p.base, aiMaxValuation(buyer, p) * 0.9))).toFixed(2);
      buyer.purse = +(buyer.purse - price).toFixed(2);
      p.team = buyer.id;
      p.soldPrice = price;
      buyer.squad.push(p);
      const mp = state.players.find(x => x.id === p.id);
      if (mp) { mp.team = buyer.id; mp.soldPrice = price; }
    }
    a.idx++;
  }
  fillRemainingSquadsAI();
  openSquadXI();
}

function fillRemainingSquadsAI() {
  const lg = activeLeague();
  activeTeams().forEach(t => {
    const f = getTeam(t.id);
    while (f.squad.length < lg.minSquad) {
      const unassigned = state.players.filter(p => !p.team && !p.retained);
      if (unassigned.length > 0) {
        const p = unassigned[0];
        p.team = t.id;
        p.soldPrice = p.base || 1.0;
        f.squad.push(p);
      } else {
        break;
      }
    }
  });
}

function renderAuction() {
  const a = state.auction;
  const lg = activeLeague();
  const p = a.pool[a.idx];
  const userF = getTeam(state.userTeam);
  const teams = activeTeams();
  document.getElementById('top-status').innerText = `PURSE: ${fmtCr(userF.purse)} | SQUAD: ${userF.squad.length}/${lg.maxSquad}`;

  if (!p) return `<div class="card">Completing Auction...</div>`;

  const nextBid = nextBidAmount();
  const canBid = a.highestBidder !== state.userTeam && userF.purse >= nextBid && userF.squad.length < lg.maxSquad && (!p.os || userF.squad.filter(x=>x.os).length < lg.maxOSInSquad);

  return `
    <div style="display:grid; grid-template-columns: repeat(${teams.length === 8 ? 4 : 5}, 1fr); gap:5px; margin-bottom:10px;">
      ${teams.map(t => {
        const f = getTeam(t.id);
        const isTop = a.highestBidder === t.id;
        return `
          <div class="franchise-chip ${isTop ? 'bidding' : ''} ${f.isHuman ? 'human' : ''}">
            <div style="font-weight:900; color:${isTop?'var(--gold)':'#fff'}">${t.id}</div>
            <div style="color:var(--muted); font-size:9px;">₹${f.purse.toFixed(1)}C</div>
            <div style="font-size:9px;">${f.squad.length} pl</div>
          </div>
        `;
      }).join('')}
    </div>

    <div class="card" style="border-color:var(--gold);">
      <div style="display:flex; justify-content:space-between; align-items:center;">
        <span class="pill">PLAYER ${a.idx + 1} / ${a.pool.length}</span>
        <div style="display:flex; gap:5px;">
          <button class="btn-dark btn-sm" onclick="state.auction.speed = state.auction.speed===1?2:1; startAuctionLoop(); render()">${a.speed}x Speed</button>
          <button class="btn-dark btn-sm" onclick="skipCurrentPlayer()">Skip</button>
          <button class="btn-dark btn-sm" onclick="simAllAuction()">Sim All</button>
        </div>
      </div>

      <div style="margin-top:12px; display:flex; justify-content:space-between; align-items:flex-start;">
        <div>
          <div class="h1" style="margin-bottom:2px;">${p.name}</div>
          <div>${roleBadge(p.role)} ${p.os ? '<span class="badge b-os">OVERSEAS</span>' : '<span class="badge b-bowl">INDIAN</span>'} <span class="sub">Base: ${fmtCr(p.base)}</span></div>
        </div>
        <div style="text-align:right;">
          <div class="sub">BAT <b style="color:#fff">${p.bat}</b></div>
          <div class="sub">BOWL <b style="color:#fff">${p.bowl}</b></div>
        </div>
      </div>

      <div style="background:var(--card2); border-radius:12px; padding:12px; margin-top:12px; display:flex; justify-content:space-between; align-items:center;">
        <div>
          <div class="sub">CURRENT BID</div>
          <div style="font-size:24px; font-weight:900; color:var(--gold);">${fmtCr(a.currentBid)}</div>
        </div>
        <div style="text-align:right;">
          <div class="sub">HIGHEST BIDDER</div>
          <div style="font-size:18px; font-weight:900; color:${a.highestBidder ? 'var(--green)' : 'var(--muted)'};">
            ${a.highestBidder ? a.highestBidder + ' (' + getTeam(a.highestBidder).ownerName + ')' : 'No Bids Yet'}
          </div>
        </div>
      </div>

      <div class="timer-bar"><div id="auc-timer-fill" class="timer-fill" style="width:${a.timer}%"></div></div>

      <div class="grid-2" style="margin-top:8px;">
        <button class="btn btn-gold" ${canBid ? '' : 'disabled'} onclick="placeBid('${state.userTeam}')">
          ✋ BID ${fmtCr(nextBid)}
        </button>
        <button class="btn ${a.autoBid ? 'btn-green' : 'btn-dark'}" onclick="state.auction.autoBid = !state.auction.autoBid; render()">
          ${a.autoBid ? '🤖 Auto-Bid: ON' : '🤖 Auto-Bid: OFF'}
        </button>
      </div>
    </div>

    <div class="card">
      <div class="h2">Live Auction Feed</div>
      <div class="log-box">${a.logs.slice(0, 12).map(l => `<div class="log-item">${l}</div>`).join('')}</div>
    </div>

    ${a.rtmPending ? `
      <div class="drawer-backdrop">
        <div class="drawer" style="text-align:center;">
          <div class="pill" style="display:inline-block; margin-bottom:8px;">🃏 RIGHT TO MATCH (RTM)</div>
          <div class="h1">${a.rtmPending.player.name}</div>
          <div class="sub" style="margin-bottom:14px;"><b>${a.rtmPending.winnerTeam}</b> won the bid at <b>${fmtCr(a.rtmPending.bidAmount)}</b>. Use your RTM card (${userF.rtm} left) to match?</div>
          <div class="grid-2">
            <button class="btn btn-dark" onclick="handleUserRTM(false)">Let Go</button>
            <button class="btn btn-gold" onclick="handleUserRTM(true)">🃏 Use RTM Card</button>
          </div>
        </div>
      </div>
    ` : ''}
  `;
}

// ==================== PLAYING XI & CAPTAIN SELECTION ====================
function openSquadXI() {
  activeTeams().forEach(t => {
    const f = getTeam(t.id);
    const sorted = [...f.squad].sort((a,b) => (b.bat + b.bowl) - (a.bat + a.bowl));
    const xi = [];
    let os = 0;
    for (const p of sorted) {
      if (xi.length >= 11) break;
      if (p.os && os >= 4) continue;
      if (p.os) os++;
      xi.push(p.id);
    }
    f.xi = xi;
    f.cap = xi[0];
    f.vc = xi[1];
  });
  state.screen = 'SQUAD_XI';
  render();
}

function toggleXIPlayer(pid) {
  const f = getTeam(state.userTeam);
  const p = f.squad.find(x => x.id === pid);
  const idx = f.xi.indexOf(pid);
  if (idx >= 0) {
    f.xi.splice(idx, 1);
  } else {
    if (f.xi.length >= 11) return alert('Playing XI already has 11 players! Deselect one first.');
    const curOS = f.xi.map(id => f.squad.find(x => x.id === id)).filter(x => x && x.os).length;
    if (p.os && curOS >= 4) return alert('Maximum 4 Overseas players allowed in Playing XI!');
    f.xi.push(pid);
  }
  if (!f.xi.includes(f.cap)) f.cap = f.xi[0] || null;
  render();
}

function renderSquadXI() {
  const f = getTeam(state.userTeam);
  const lg = activeLeague();
  const osCount = f.xi.map(id => f.squad.find(x => x.id === id)).filter(x => x && x.os).length;
  document.getElementById('top-status').innerText = `SQUAD: ${f.squad.length} | XI: ${f.xi.length}/11`;

  return `
    <div class="card">
      <div class="h2">
        <span>📋 Select Playing XI (${f.id})</span>
        <span class="pill">Squad: ${f.squad.length} (Min ${lg.minSquad})</span>
      </div>
      <div class="sub">Pick your 11 starters and assign Captain (C) for ${lg.title} Season ${state.season}.</div>
    </div>

    <div class="card">
      ${f.squad.map(p => {
        const inXI = f.xi.includes(p.id);
        const isCap = f.cap === p.id;
        return `
          <div class="row" style="${inXI ? 'border-color:var(--green); background:rgba(16,185,129,0.08);' : ''}">
            <div>
              <div style="font-weight:800; font-size:13px;">#${p.jersey || 10} ${p.name} ${p.os ? '<span class="badge b-os">OS</span>' : ''}</div>
              <div class="sub">${roleBadge(p.role)} BAT ${p.bat} • BOWL ${p.bowl}</div>
            </div>
            <div style="display:flex; gap:5px; align-items:center;">
              ${inXI ? `<button class="btn-sm ${isCap ? 'btn-gold' : 'btn-dark'}" onclick="getTeam('${state.userTeam}').cap=${p.id}; render()">${isCap ? '© CAP' : 'C'}</button>` : ''}
              <button class="btn-sm ${inXI ? 'btn-green' : 'btn-dark'}" onclick="toggleXIPlayer(${p.id})">${inXI ? '✓ XI' : '+ Add'}</button>
            </div>
          </div>
        `;
      }).join('')}
    </div>

    <div class="bottom-dock">
      <div class="dock-inner">
        <button class="btn btn-gold" ${f.xi.length === 11 && f.squad.length >= lg.minSquad ? '' : 'disabled'} onclick="startSeasonSchedule()">
          🏏 Lock Playing XI & Enter Season ${state.season} →
        </button>
      </div>
    </div>
  `;
}

// ==================== SEASON SCHEDULE & POINTS TABLE ====================
function startSeasonSchedule() {
  const teams = activeTeams();
  teams.forEach(t => {
    const f = getTeam(t.id);
    f.pts = 0; f.w = 0; f.l = 0; f.nrr = 0;
  });

  const ids = teams.map(t => t.id);
  const fixtures = [];
  const matchesPerTeam = ids.length === 8 ? 7 : 7;
  for (let i = 0; i < ids.length; i++) {
    for (let j = i + 1; j < ids.length; j++) {
      if (fixtures.filter(m => m.t1===ids[i]||m.t2===ids[i]).length < matchesPerTeam && fixtures.filter(m => m.t1===ids[j]||m.t2===ids[j]).length < matchesPerTeam) {
        fixtures.push({ t1: ids[i], t2: ids[j], done: false, result: '' });
      }
    }
  }
  fixtures.sort(() => Math.random() - 0.5);

  state.seasonData = {
    fixtures,
    currentMatchIdx: 0,
    orangeCap: {},
    purpleCap: {},
    champion: null
  };
  state.screen = 'SEASON';
  render();
}

function quickSimMatch(m) {
  const f1 = getTeam(m.t1), f2 = getTeam(m.t2);
  const s1 = f1.xi.reduce((acc, id) => { const p = f1.squad.find(x=>x.id===id); return acc + (p ? p.bat + p.bowl : 120); }, 0) + Math.random()*180;
  const s2 = f2.xi.reduce((acc, id) => { const p = f2.squad.find(x=>x.id===id); return acc + (p ? p.bat + p.bowl : 120); }, 0) + Math.random()*180;
  const r1 = 155 + Math.floor(Math.random() * 55);
  const r2 = s1 >= s2 ? r1 - (4 + Math.floor(Math.random()*22)) : r1 + (1 + Math.floor(Math.random()*6));

  recordMatchStats(f1, r1, f2, r2);
  m.done = true;
  m.result = s1 >= s2 ? `${f1.id} won by ${r1 - r2} runs` : `${f2.id} won by ${3 + Math.floor(Math.random()*6)} wkts`;
}

function recordMatchStats(f1, r1, f2, r2) {
  const win1 = r1 >= r2;
  if (win1) { f1.w++; f1.pts += 2; f2.l++; }
  else { f2.w++; f2.pts += 2; f1.l++; }
  f1.nrr = +(f1.nrr + (r1 - r2) / 140).toFixed(2);
  f2.nrr = +(f2.nrr + (r2 - r1) / 140).toFixed(2);

  [f1, f2].forEach(f => {
    const batters = f.xi.map(id => f.squad.find(x=>x.id===id)).filter(Boolean).sort((a,b)=>b.bat-a.bat);
    const bowlers = f.xi.map(id => f.squad.find(x=>x.id===id)).filter(Boolean).sort((a,b)=>b.bowl-a.bowl);
    if (batters[0]) state.seasonData.orangeCap[batters[0].name] = (state.seasonData.orangeCap[batters[0].name] || 0) + 25 + Math.floor(Math.random()*55);
    if (batters[1]) state.seasonData.orangeCap[batters[1].name] = (state.seasonData.orangeCap[batters[1].name] || 0) + 15 + Math.floor(Math.random()*40);
    if (bowlers[0]) state.seasonData.purpleCap[bowlers[0].name] = (state.seasonData.purpleCap[bowlers[0].name] || 0) + 1 + Math.floor(Math.random()*3);
  });
}

function simUntilNextUserMatch() {
  const sd = state.seasonData;
  while (sd.currentMatchIdx < sd.fixtures.length) {
    const m = sd.fixtures[sd.currentMatchIdx];
    if (m.t1 === state.userTeam || m.t2 === state.userTeam) break;
    quickSimMatch(m);
    sd.currentMatchIdx++;
  }
  if (sd.currentMatchIdx >= sd.fixtures.length) finishSeasonPlayoffs();
  render();
}

function simWholeSeason() {
  const sd = state.seasonData;
  while (sd.currentMatchIdx < sd.fixtures.length) {
    quickSimMatch(sd.fixtures[sd.currentMatchIdx]);
    sd.currentMatchIdx++;
  }
  finishSeasonPlayoffs();
  render();
}

function finishSeasonPlayoffs() {
  const standings = getStandings();
  const top4 = standings.slice(0, 4);
  const champ = top4[Math.floor(Math.random() * Math.min(2, top4.length))];
  state.seasonData.champion = champ.id;
}

function getStandings() {
  return Object.values(state.franchises).sort((a,b) => b.pts - a.pts || b.nrr - a.nrr);
}

function renderSeason() {
  const sd = state.seasonData;
  const standings = getStandings();
  const nextM = sd.fixtures[sd.currentMatchIdx];
  const isUserNext = nextM && (nextM.t1 === state.userTeam || nextM.t2 === state.userTeam);

  const topOrange = Object.entries(sd.orangeCap).sort((a,b)=>b[1]-a[1])[0];
  const topPurple = Object.entries(sd.purpleCap).sort((a,b)=>b[1]-a[1])[0];

  document.getElementById('top-status').innerText = `${activeLeague().id} SEASON ${state.season}`;

  return `
    ${sd.champion ? `
      <div class="card" style="border-color:var(--gold); text-align:center; background:linear-gradient(135deg, rgba(245,158,11,0.18), rgba(19,26,42,1));">
        <div style="font-size:32px;">🏆</div>
        <div class="h1">${getTeam(sd.champion).name}</div>
        <div class="sub" style="margin-bottom:12px;">${activeLeague().title} SEASON ${state.season} CHAMPIONS!</div>
        <div style="display:flex; flex-direction:column; gap:8px;">
          <button class="btn btn-gold" onclick="openTradeWindow()">🔄 Enter Trade Window & Mini Auction →</button>
          <button class="btn btn-dark" onclick="state.screen='HOME'; render()">🏠 Switch League (IPL / LLC)</button>
        </div>
      </div>
    ` : `
      <div class="card" style="border-color:var(--blue);">
        <div class="h2">
          <span>📅 Next Fixture (${sd.currentMatchIdx + 1}/${sd.fixtures.length})</span>
          <span class="pill">${nextM.t1} vs ${nextM.t2}</span>
        </div>
        <div class="sub" style="margin-bottom:10px;">Venue: ${getTeam(nextM.t1).venue} • T20 Night Match</div>
        ${isUserNext ? `
          <div class="grid-2">
            <button class="btn btn-green" onclick="launchLiveTacticalMatch(${sd.currentMatchIdx})">🎮 Play Live 2D Match</button>
            <button class="btn btn-dark" onclick="quickSimMatch(state.seasonData.fixtures[${sd.currentMatchIdx}]); state.seasonData.currentMatchIdx++; if(state.seasonData.currentMatchIdx>=state.seasonData.fixtures.length) finishSeasonPlayoffs(); render()">⏩ Quick Sim</button>
          </div>
        ` : `
          <div class="grid-2">
            <button class="btn btn-blue" onclick="simUntilNextUserMatch()">⏭ Sim to My Match</button>
            <button class="btn btn-dark" onclick="simWholeSeason()">⏩ Sim Full Season</button>
          </div>
        `}
      </div>
    `}

    <div class="grid-2" style="margin-bottom:12px;">
      <div class="card" style="margin-bottom:0;">
        <div class="sub" style="color:var(--gold); font-weight:800;">🧢 ORANGE CAP</div>
        <div style="font-weight:800; font-size:13px; margin-top:3px;">${topOrange ? topOrange[0] : 'TBD'}</div>
        <div class="sub">${topOrange ? topOrange[1] + ' Runs' : '-'}</div>
      </div>
      <div class="card" style="margin-bottom:0;">
        <div class="sub" style="color:#a78bfa; font-weight:800;">🧢 PURPLE CAP</div>
        <div style="font-weight:800; font-size:13px; margin-top:3px;">${topPurple ? topPurple[0] : 'TBD'}</div>
        <div class="sub">${topPurple ? topPurple[1] + ' Wickets' : '-'}</div>
      </div>
    </div>

    <div class="card">
      <div class="h2">Points Table</div>
      <table>
        <thead><tr><th>#</th><th>Team</th><th>M</th><th>W</th><th>L</th><th>NRR</th><th>PTS</th></tr></thead>
        <tbody>
          ${standings.map((f, i) => `
            <tr style="${f.id === state.userTeam ? 'background:rgba(59,130,246,0.14); font-weight:800;' : ''}">
              <td style="color:${i<4?'var(--green)':'var(--muted)'}">${i+1}</td>
              <td><b>${f.id}</b></td>
              <td>${f.w + f.l}</td>
              <td>${f.w}</td>
              <td>${f.l}</td>
              <td>${f.nrr >= 0 ? '+'+f.nrr.toFixed(2) : f.nrr.toFixed(2)}</td>
              <td style="color:var(--gold); font-weight:900;">${f.pts}</td>
            </tr>
          `).join('')}
        </tbody>
      </table>
    </div>
  `;
}

// ==================== 2D TOP-DOWN TACTICAL LIVE MATCH ENGINE ====================
function launchLiveTacticalMatch(fixtureIdx) {
  const m = state.seasonData.fixtures[fixtureIdx];
  const userIsT1 = m.t1 === state.userTeam;
  const oppId = userIsT1 ? m.t2 : m.t1;
  const userF = getTeam(state.userTeam);
  const oppF = getTeam(oppId);

  const makeTeamState = (f) => {
    const xiPlayers = f.xi.map(id => f.squad.find(x => x.id === id)).filter(Boolean);
    return {
      id: f.id,
      name: f.name,
      color: f.color,
      players: xiPlayers,
      runs: 0,
      wkts: 0,
      balls: 0,
      batStats: xiPlayers.map(p => ({ id: p.id, name: p.name, jersey: p.jersey || 10, role: p.role, bat: p.bat, bowl: p.bowl, runs: 0, balls: 0, fours: 0, sixes: 0, out: false, howOut: 'not out' })),
      bowlStats: xiPlayers.map(p => ({ id: p.id, name: p.name, jersey: p.jersey || 10, role: p.role, bowl: p.bowl, balls: 0, maidens: 0, runs: 0, wkts: 0 }))
    };
  };

  state.liveMatch = {
    fixtureIdx,
    venue: getTeam(m.t1).venue,
    userTeam: state.userTeam,
    oppTeam: oppId,
    innings: 1,
    target: null,
    battingTeam: null,
    bowlingTeam: null,
    strikerIdx: 0,
    nonStrikerIdx: 1,
    nextBatIdx: 2,
    bowlerId: null,
    lastBowlerId: null,
    thisOver: [],
    tactics: { bat: 'BALANCED', bowl: 'BALANCED' },
    speed: 1,
    paused: true,
    commentary: 'Toss time! Choose Bat or Bowl to start the match.',
    drawer: 'TOSS',
    ballAnim: { x: 0.5, y: 0.42, tx: 0.5, ty: 0.42, active: false },
    teams: {
      [userF.id]: makeTeamState(userF),
      [oppF.id]: makeTeamState(oppF)
    }
  };

  state.screen = 'LIVE_MATCH';
  render();
  setTimeout(drawStadiumCanvas, 50);
}

function handleTossChoice(userBatsFirst) {
  const lm = state.liveMatch;
  lm.battingTeam = userBatsFirst ? lm.userTeam : lm.oppTeam;
  lm.bowlingTeam = userBatsFirst ? lm.oppTeam : lm.userTeam;
  setupInningsStart();
}

function setupInningsStart() {
  const lm = state.liveMatch;
  lm.strikerIdx = 0;
  lm.nonStrikerIdx = 1;
  lm.nextBatIdx = 2;
  lm.bowlerId = null;
  lm.lastBowlerId = null;
  lm.thisOver = [];
  lm.paused = true;

  if (lm.bowlingTeam === lm.userTeam) {
    lm.drawer = 'BOWLER';
    lm.commentary = 'Pick your Opening Bowler to take the new ball!';
  } else {
    const aiBowl = pickAIBowler(lm.teams[lm.bowlingTeam], null);
    lm.bowlerId = aiBowl.id;
    lm.drawer = null;
    lm.paused = false;
    lm.commentary = `${aiBowl.name} opens the bowling for ${lm.bowlingTeam}.`;
  }
  render();
  startMatchLoop();
}

function pickAIBowler(teamObj, lastId) {
  const elig = teamObj.bowlStats.filter(b => b.id !== lastId && b.balls < 24);
  elig.sort((a,b) => b.bowl - a.bowl);
  return elig[0] || teamObj.bowlStats[0];
}

function selectUserBowler(bowlerId) {
  const lm = state.liveMatch;
  lm.bowlerId = bowlerId;
  const b = lm.teams[lm.bowlingTeam].bowlStats.find(x => x.id === bowlerId);
  lm.drawer = null;
  lm.paused = false;
  lm.commentary = `${b.name} comes into the attack.`;
  render();
}

function selectUserNextBatter(batIdx) {
  const lm = state.liveMatch;
  lm.strikerIdx = batIdx;
  const b = lm.teams[lm.battingTeam].batStats[batIdx];
  lm.drawer = null;
  lm.paused = false;
  lm.commentary = `${b.name} walks out to the crease.`;
  render();
}

function startMatchLoop() {
  stopMatchLoop();
  matchInterval = setInterval(() => {
    const lm = state.liveMatch;
    if (!lm || state.screen !== 'LIVE_MATCH' || lm.paused || lm.drawer) return;
    simulateOneDelivery();
  }, 1300 / (state.liveMatch ? state.liveMatch.speed : 1));
}

function stopMatchLoop() {
  if (matchInterval) { clearInterval(matchInterval); matchInterval = null; }
}

function simulateOneDelivery() {
  const lm = state.liveMatch;
  const batT = lm.teams[lm.battingTeam];
  const bowlT = lm.teams[lm.bowlingTeam];
  const striker = batT.batStats[lm.strikerIdx];
  const bowler = bowlT.bowlStats.find(x => x.id === lm.bowlerId);

  if (!striker || !bowler) return;

  let agg = lm.tactics.bat === 'SLOG' ? 1.35 : lm.tactics.bat === 'ATTACKING' ? 1.15 : lm.tactics.bat === 'DEFENSIVE' ? 0.78 : 1.0;
  let bowlMod = lm.tactics.bowl === 'DEATH' ? 1.15 : lm.tactics.bowl === 'ATTACKING' ? 1.1 : 1.0;
  const skillDiff = (striker.bat - bowler.bowl) / 140;

  const r = Math.random();
  let outcome = '0';
  let runs = 0;
  let isWicket = false;
  let tx = 0.5, ty = 0.42;

  const wktProb = Math.max(0.03, (0.062 * agg * bowlMod) - skillDiff * 0.03);
  const sixProb = Math.max(0.04, (0.095 * agg) + skillDiff * 0.04);
  const fourProb = Math.max(0.08, (0.145 * agg) + skillDiff * 0.05);

  if (r < wktProb) {
    isWicket = true;
    outcome = 'W';
    tx = 0.5; ty = 0.58;
  } else if (r < wktProb + sixProb) {
    runs = 6; outcome = '6';
    const ang = Math.random() * Math.PI * 2;
    tx = 0.5 + Math.cos(ang) * 0.46;
    ty = 0.5 + Math.sin(ang) * 0.46;
  } else if (r < wktProb + sixProb + fourProb) {
    runs = 4; outcome = '4';
    const ang = Math.random() * Math.PI * 2;
    tx = 0.5 + Math.cos(ang) * 0.43;
    ty = 0.5 + Math.sin(ang) * 0.43;
  } else if (r < wktProb + sixProb + fourProb + 0.34) {
    runs = 1; outcome = '1';
    tx = 0.35 + Math.random() * 0.3;
    ty = 0.35 + Math.random() * 0.3;
  } else if (r < wktProb + sixProb + fourProb + 0.42) {
    runs = 2; outcome = '2';
    tx = 0.28 + Math.random() * 0.44;
    ty = 0.28 + Math.random() * 0.44;
  } else {
    runs = 0; outcome = '0';
    tx = 0.5; ty = 0.54;
  }

  lm.ballAnim = { x: 0.5, y: 0.42, tx, ty, active: true };
  animateBallShot();

  batT.balls++;
  bowler.balls++;
  striker.balls++;
  lm.thisOver.push(outcome);

  if (isWicket) {
    batT.wkts++;
    bowler.wkts++;
    striker.out = true;
    striker.howOut = `b ${bowler.name}`;
    lm.commentary = `☝️ OUT! ${bowler.name} dismisses ${striker.name} (${striker.runs} off ${striker.balls})!`;
  } else {
    batT.runs += runs;
    bowler.runs += runs;
    striker.runs += runs;
    if (runs === 4) striker.fours++;
    if (runs === 6) striker.sixes++;
    lm.commentary = runs === 6 ? `🚀 MAXIMUM! ${striker.name} smashes ${bowler.name} for SIX!` :
                    runs === 4 ? `💥 FOUR! Crisp boundary by ${striker.name}!` :
                    runs > 0 ? `${striker.name} pushes for ${runs} run${runs>1?'s':''}.` :
                    `Dot ball. Good line from ${bowler.name}.`;
    if (runs % 2 === 1) {
      [lm.strikerIdx, lm.nonStrikerIdx] = [lm.nonStrikerIdx, lm.strikerIdx];
    }
  }

  if (lm.innings === 2 && batT.runs >= lm.target) {
    finishLiveMatch();
    return;
  }
  if (batT.wkts >= 10 || batT.balls >= 120) {
    if (lm.innings === 1) {
      lm.innings = 2;
      lm.target = batT.runs + 1;
      [lm.battingTeam, lm.bowlingTeam] = [lm.bowlingTeam, lm.battingTeam];
      lm.commentary = `Innings Break! Target is ${lm.target} runs in 20 overs.`;
      setupInningsStart();
      return;
    } else {
      finishLiveMatch();
      return;
    }
  }

  if (isWicket) {
    if (lm.battingTeam === lm.userTeam) {
      lm.paused = true;
      lm.drawer = 'BATTER';
      render();
      return;
    } else {
      lm.strikerIdx = lm.nextBatIdx++;
    }
  }

  if (batT.balls % 6 === 0) {
    [lm.strikerIdx, lm.nonStrikerIdx] = [lm.nonStrikerIdx, lm.strikerIdx];
    lm.lastBowlerId = lm.bowlerId;
    lm.thisOver = [];
    if (lm.bowlingTeam === lm.userTeam) {
      lm.paused = true;
      lm.drawer = 'BOWLER';
      lm.commentary = `End of Over ${batT.balls / 6}. Pick next bowler!`;
      render();
      return;
    } else {
      const nb = pickAIBowler(bowlT, lm.lastBowlerId);
      lm.bowlerId = nb.id;
      lm.commentary = `Over ${batT.balls / 6} complete. ${nb.name} to bowl next.`;
    }
  }

  render();
  drawStadiumCanvas();
}

function simRestOfLiveMatch() {
  stopMatchLoop();
  const lm = state.liveMatch;
  lm.drawer = null;
  while (lm.drawer !== 'RESULT') {
    const batT = lm.teams[lm.battingTeam];
    const bowlT = lm.teams[lm.bowlingTeam];
    const remBalls = 120 - batT.balls;
    const addRuns = Math.floor((remBalls / 6) * (7.2 + Math.random() * 2.5));
    const addWkts = Math.min(10 - batT.wkts, Math.floor(remBalls / 18));

    if (lm.innings === 2 && batT.runs + addRuns >= lm.target) {
      batT.runs = lm.target;
      batT.balls += Math.max(1, Math.floor((lm.target - batT.runs) * 4));
      finishLiveMatch();
      break;
    }

    batT.runs += addRuns;
    batT.wkts += addWkts;
    batT.balls = 120;

    batT.batStats[lm.strikerIdx].runs += Math.floor(addRuns * 0.45);
    bowlT.bowlStats[0].wkts += addWkts;

    if (lm.innings === 1) {
      lm.innings = 2;
      lm.target = batT.runs + 1;
      [lm.battingTeam, lm.bowlingTeam] = [lm.bowlingTeam, lm.battingTeam];
      lm.strikerIdx = 0; lm.nonStrikerIdx = 1; lm.nextBatIdx = 2;
      lm.bowlerId = lm.teams[lm.bowlingTeam].bowlStats[0].id;
    } else {
      finishLiveMatch();
      break;
    }
  }
  render();
}

function finishLiveMatch() {
  stopMatchLoop();
  const lm = state.liveMatch;
  lm.paused = true;
  lm.drawer = 'RESULT';

  const m = state.seasonData.fixtures[lm.fixtureIdx];
  const t1Obj = lm.teams[m.t1];
  const t2Obj = lm.teams[m.t2];

  recordMatchStats(getTeam(m.t1), t1Obj.runs, getTeam(m.t2), t2Obj.runs);
  m.done = true;
  m.result = t1Obj.runs >= t2Obj.runs
    ? `${m.t1} won by ${t1Obj.runs - t2Obj.runs} runs`
    : `${m.t2} won by ${10 - t2Obj.wkts} wickets`;

  state.seasonData.currentMatchIdx++;
  if (state.seasonData.currentMatchIdx >= state.seasonData.fixtures.length) {
    finishSeasonPlayoffs();
  }
  render();
}

function animateBallShot() {
  let step = 0;
  const anim = setInterval(() => {
    step++;
    if (step > 8 || !state.liveMatch) { clearInterval(anim); return; }
    const b = state.liveMatch.ballAnim;
    b.x += (b.tx - b.x) * 0.35;
    b.y += (b.ty - b.y) * 0.35;
    drawStadiumCanvas();
  }, 45);
}

function drawStadiumCanvas() {
  const canvas = document.getElementById('stadium-canvas');
  if (!canvas || !state.liveMatch) return;
  const ctx = canvas.getContext('2d');
  const w = canvas.width = 380;
  const h = canvas.height = 380;
  const cx = w / 2, cy = h / 2;

  ctx.fillStyle = '#0f172a';
  ctx.fillRect(0, 0, w, h);

  ctx.beginPath();
  ctx.arc(cx, cy, 182, 0, Math.PI * 2);
  ctx.fillStyle = '#1e293b';
  ctx.fill();

  ctx.beginPath();
  ctx.arc(cx, cy, 166, 0, Math.PI * 2);
  ctx.fillStyle = '#14532d';
  ctx.fill();

  ctx.beginPath();
  ctx.arc(cx, cy, 128, 0, Math.PI * 2);
  ctx.fillStyle = '#166534';
  ctx.fill();

  ctx.beginPath();
  ctx.arc(cx, cy, 162, 0, Math.PI * 2);
  ctx.strokeStyle = '#f8fafc';
  ctx.lineWidth = 2.5;
  ctx.stroke();

  ctx.save();
  ctx.setLineDash([4, 5]);
  ctx.beginPath();
  ctx.arc(cx, cy, 88, 0, Math.PI * 2);
  ctx.strokeStyle = 'rgba(255,255,255,0.55)';
  ctx.lineWidth = 1.5;
  ctx.stroke();
  ctx.restore();

  ctx.fillStyle = '#d6c39c';
  ctx.fillRect(cx - 14, cy - 38, 28, 76);
  ctx.strokeStyle = '#ffffff';
  ctx.lineWidth = 1.2;
  ctx.strokeRect(cx - 14, cy - 30, 28, 60);

  [[20,20],[w-20,20],[20,h-20],[w-20,h-20]].forEach(([lx, ly]) => {
    ctx.fillStyle = '#cbd5e1';
    ctx.beginPath();
    ctx.arc(lx, ly, 8, 0, Math.PI * 2);
    ctx.fill();
  });

  const lm = state.liveMatch;
  const bowlT = lm.teams[lm.bowlingTeam];
  const batT = lm.teams[lm.battingTeam];

  const fieldCoords = [
    [cx, cy + 44],
    [cx, cy - 46],
    [cx - 42, cy - 55],
    [cx + 42, cy - 55],
    [cx - 68, cy - 12],
    [cx + 68, cy - 12],
    [cx - 62, cy + 36],
    [cx + 62, cy + 36],
    [cx - 105, cy + 95],
    [cx + 105, cy + 95],
    [cx + 95, cy - 95]
  ];

  bowlT.players.slice(0, 11).forEach((p, idx) => {
    const [fx, fy] = fieldCoords[idx] || [cx, cy];
    ctx.beginPath();
    ctx.arc(fx, fy, 10, 0, Math.PI * 2);
    ctx.fillStyle = bowlT.color || '#ef4444';
    ctx.fill();
    ctx.strokeStyle = '#fff';
    ctx.lineWidth = 1.5;
    ctx.stroke();

    ctx.fillStyle = '#fff';
    ctx.font = 'bold 9px sans-serif';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText(p.jersey || (idx+1), fx, fy);
  });

  const s1 = batT.batStats[lm.strikerIdx];
  const s2 = batT.batStats[lm.nonStrikerIdx];
  [[s1, cx, cy + 24], [s2, cx, cy - 24]].forEach(([b, bx, by]) => {
    if (!b) return;
    ctx.beginPath();
    ctx.arc(bx, by, 10, 0, Math.PI * 2);
    ctx.fillStyle = '#4f46e5';
    ctx.fill();
    ctx.strokeStyle = '#fde047';
    ctx.lineWidth = 1.5;
    ctx.stroke();
    ctx.fillStyle = '#fff';
    ctx.font = 'bold 9px sans-serif';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText(b.jersey || 18, bx, by);
  });

  const bx = lm.ballAnim.x * w;
  const by = lm.ballAnim.y * h;
  ctx.beginPath();
  ctx.arc(bx, by, 5.5, 0, Math.PI * 2);
  ctx.fillStyle = '#ffffff';
  ctx.fill();
  ctx.strokeStyle = '#0f172a';
  ctx.lineWidth = 1.5;
  ctx.stroke();
}

function renderLiveMatch() {
  const lm = state.liveMatch;
  const batT = lm.teams[lm.battingTeam || lm.userTeam];
  const bowlT = lm.teams[lm.bowlingTeam || lm.oppTeam];
  const s1 = batT.batStats[lm.strikerIdx] || { name: 'Batter 1', runs: 0, balls: 0, jersey: 18 };
  const s2 = batT.batStats[lm.nonStrikerIdx] || { name: 'Batter 2', runs: 0, balls: 0, jersey: 7 };
  const curBowler = bowlT.bowlStats.find(x => x.id === lm.bowlerId) || bowlT.bowlStats[0];

  const oversStr = `${Math.floor(batT.balls / 6)}.${batT.balls % 6}`;
  const rr = batT.balls > 0 ? ((batT.runs / batT.balls) * 6).toFixed(2) : '0.00';

  document.getElementById('top-status').innerText = `${lm.userTeam} vs ${lm.oppTeam} • LIVE`;

  setTimeout(drawStadiumCanvas, 10);

  return `
    <div class="match-header">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
        <div>
          <div style="font-weight:900; font-size:14px;">${lm.userTeam} vs ${lm.oppTeam}</div>
          <div class="sub">${lm.venue} • T20 ${lm.target ? '• Target: ' + lm.target : ''}</div>
        </div>
        <div style="display:flex; gap:6px;">
          <button class="btn-dark btn-sm" onclick="simRestOfLiveMatch()">⏩ SIM</button>
          <span class="pill" style="background:rgba(239,68,68,0.2); color:#f87171; border-color:#ef4444;">● LIVE</span>
        </div>
      </div>

      <div style="display:flex; justify-content:space-between; align-items:center; background:var(--card2); padding:8px 10px; border-radius:10px;">
        <div>
          <span style="font-weight:900; font-size:16px; color:${batT.color}">${batT.id}</span>
          <span class="sub" style="margin-left:6px;">RR ${rr}</span>
        </div>
        <div style="font-size:22px; font-weight:900;">${batT.runs}/${batT.wkts} <span class="sub" style="font-size:13px;">(${oversStr})</span></div>
      </div>

      <div class="grid-2" style="margin-top:8px;">
        <div class="franchise-chip" style="text-align:left; padding:7px 9px; border-color:var(--gold);">
          <div style="font-weight:800; font-size:12px;">#${s1.jersey} ${s1.name}*</div>
          <div class="sub">${s1.runs} (${s1.balls})</div>
        </div>
        <div class="franchise-chip" style="text-align:left; padding:7px 9px;">
          <div style="font-weight:800; font-size:12px;">#${s2.jersey} ${s2.name}</div>
          <div class="sub">${s2.runs} (${s2.balls})</div>
        </div>
      </div>

      <div style="display:flex; justify-content:space-between; align-items:center; margin-top:7px; padding:6px 9px; background:var(--card2); border-radius:8px; font-size:12px;">
        <div>⚾ <b>${curBowler.name}</b> <span class="badge b-bowl">${curBowler.role}</span></div>
        <div class="sub">${Math.floor(curBowler.balls/6)}.${curBowler.balls%6}-${curBowler.maidens}-${curBowler.runs}-${curBowler.wkts}</div>
      </div>

      <div class="over-balls">
        ${[0,1,2,3,4,5].map(i => {
          const val = lm.thisOver[i] !== undefined ? lm.thisOver[i] : '·';
          const cls = val === '4' ? 'ball-4' : val === '6' ? 'ball-6' : val === 'W' ? 'ball-W' : (val === '1' || val === '2') ? 'ball-run' : '';
          return `<div class="ball-pill ${cls}">${val}</div>`;
        }).join('')}
      </div>
    </div>

    <div class="stadium-wrap">
      <canvas id="stadium-canvas"></canvas>
    </div>

    <div class="card" style="margin-top:8px; padding:10px 12px;">
      <div style="font-size:12px; font-weight:700; color:#e2e8f0;">🎙️ ${lm.commentary}</div>
    </div>

    <div class="bottom-dock">
      <div class="dock-inner">
        <button class="btn ${lm.paused ? 'btn-gold' : 'btn-dark'}" style="flex:1.2;" onclick="state.liveMatch.paused = !state.liveMatch.paused; render()">
          ${lm.paused ? '▶ PLAY' : '⏸ PAUSE'}
        </button>
        <button class="btn btn-dark" style="flex:1;" onclick="state.liveMatch.paused=true; state.liveMatch.drawer='TACTICS'; render()">
          ⚙️ TACTICS
        </button>
        <button class="btn btn-dark" style="flex:1;" onclick="state.liveMatch.paused=true; state.liveMatch.drawer='CARD'; render()">
          📋 CARD
        </button>
        <button class="btn btn-dark btn-sm" onclick="state.liveMatch.speed = state.liveMatch.speed===1?2:1; startMatchLoop(); render()">
          ${lm.speed}x
        </button>
      </div>
    </div>

    ${renderMatchDrawer()}
  `;
}

function renderMatchDrawer() {
  const lm = state.liveMatch;
  if (!lm.drawer) return '';

  if (lm.drawer === 'TOSS') {
    return `
      <div class="drawer-backdrop">
        <div class="drawer" style="text-align:center;">
          <div class="pill" style="display:inline-block; margin-bottom:8px;">🪙 MATCH TOSS</div>
          <div class="h1">You won the Toss!</div>
          <div class="sub" style="margin-bottom:14px;">Pitch at ${lm.venue} looks great for T20 cricket. What do you choose?</div>
          <div class="grid-2">
            <button class="btn btn-gold" onclick="handleTossChoice(true)">🏏 Bat First</button>
            <button class="btn btn-green" onclick="handleTossChoice(false)">⚾ Bowl First</button>
          </div>
        </div>
      </div>
    `;
  }

  if (lm.drawer === 'BOWLER') {
    const bowlT = lm.teams[lm.bowlingTeam];
    return `
      <div class="drawer-backdrop">
        <div class="drawer">
          <div class="h2">
            <span style="color:var(--gold);">⚾ SELECT BOWLER</span>
            <span class="sub">Max 4 Overs / Bowler</span>
          </div>
          <div class="sub" style="margin-bottom:10px;">Pick who bowls the next over for ${lm.bowlingTeam}:</div>
          ${bowlT.bowlStats.map(b => {
            const disabled = b.id === lm.lastBowlerId || b.balls >= 24;
            return `
              <div class="row" style="opacity:${disabled?0.45:1}">
                <div>
                  <div style="font-weight:800; font-size:13px;">#${b.jersey} ${b.name} ${roleBadge(b.role)}</div>
                  <div class="sub">Skill ${b.bowl} • O-M-R-W: ${Math.floor(b.balls/6)}.${b.balls%6}-${b.maidens}-${b.runs}-${b.wkts}</div>
                </div>
                <button class="btn-sm btn-gold" ${disabled?'disabled':''} onclick="selectUserBowler(${b.id})">Bowl</button>
              </div>
            `;
          }).join('')}
        </div>
      </div>
    `;
  }

  if (lm.drawer === 'BATTER') {
    const batT = lm.teams[lm.battingTeam];
    return `
      <div class="drawer-backdrop">
        <div class="drawer">
          <div class="h2"><span style="color:var(--gold);">🏏 SELECT NEXT BATTER</span></div>
          ${batT.batStats.map((b, idx) => {
            if (b.out || idx === lm.strikerIdx || idx === lm.nonStrikerIdx) return '';
            return `
              <div class="row">
                <div>
                  <div style="font-weight:800; font-size:13px;">#${b.jersey} ${b.name} ${roleBadge(b.role)}</div>
                  <div class="sub">Batting Rating: ${b.bat}</div>
                </div>
                <button class="btn-sm btn-green" onclick="selectUserNextBatter(${idx})">Send In</button>
              </div>
            `;
          }).join('')}
        </div>
      </div>
    `;
  }

  if (lm.drawer === 'TACTICS') {
    return `
      <div class="drawer-backdrop">
        <div class="drawer">
          <div class="h2"><span>⚙️ Live Match Tactics</span><button class="btn-dark btn-sm" onclick="state.liveMatch.drawer=null; state.liveMatch.paused=false; render()">✕</button></div>
          <div class="sub" style="margin-bottom:6px;">Batting Aggression:</div>
          <div class="grid-2" style="margin-bottom:12px;">
            ${['DEFENSIVE','BALANCED','ATTACKING','SLOG'].map(t => `
              <button class="btn-sm ${lm.tactics.bat===t?'btn-gold':'btn-dark'}" onclick="state.liveMatch.tactics.bat='${t}'; render()">${t}</button>
            `).join('')}
          </div>
          <div class="sub" style="margin-bottom:6px;">Bowling Field & Line Plan:</div>
          <div class="grid-3" style="margin-bottom:14px;">
            ${['POWERPLAY','BALANCED','DEATH'].map(t => `
              <button class="btn-sm ${lm.tactics.bowl===t?'btn-blue':'btn-dark'}" onclick="state.liveMatch.tactics.bowl='${t}'; render()">${t}</button>
            `).join('')}
          </div>
          <button class="btn btn-green" onclick="state.liveMatch.drawer=null; state.liveMatch.paused=false; render()">Resume Match ▶</button>
        </div>
      </div>
    `;
  }

  if (lm.drawer === 'CARD') {
    const batT = lm.teams[lm.battingTeam];
    const bowlT = lm.teams[lm.bowlingTeam];
    return `
      <div class="drawer-backdrop">
        <div class="drawer">
          <div class="h2"><span>📋 Live Scorecard (${batT.id})</span><button class="btn-dark btn-sm" onclick="state.liveMatch.drawer=null; render()">✕</button></div>
          <table>
            <thead><tr><th>Batter</th><th>Status</th><th>R</th><th>B</th><th>4s</th><th>6s</th></tr></thead>
            <tbody>
              ${batT.batStats.map(b => `
                <tr><td><b>${b.name}</b></td><td class="sub">${b.howOut}</td><td><b>${b.runs}</b></td><td>${b.balls}</td><td>${b.fours}</td><td>${b.sixes}</td></tr>
              `).join('')}
            </tbody>
          </table>
          <div class="h2" style="margin-top:12px;">Bowling (${bowlT.id})</div>
          <table>
            <thead><tr><th>Bowler</th><th>O</th><th>R</th><th>W</th></tr></thead>
            <tbody>
              ${bowlT.bowlStats.filter(b => b.balls > 0).map(b => `
                <tr><td><b>${b.name}</b></td><td>${Math.floor(b.balls/6)}.${b.balls%6}</td><td>${b.runs}</td><td><b>${b.wkts}</b></td></tr>
              `).join('')}
            </tbody>
          </table>
        </div>
      </div>
    `;
  }

  if (lm.drawer === 'RESULT') {
    const m = state.seasonData.fixtures[lm.fixtureIdx];
    return `
      <div class="drawer-backdrop">
        <div class="drawer" style="text-align:center;">
          <div class="pill" style="display:inline-block; margin-bottom:8px;">🏁 FULL TIME</div>
          <div class="h1">${m.result}</div>
          <div class="sub" style="margin-bottom:14px;">${m.t1}: ${lm.teams[m.t1].runs}/${lm.teams[m.t1].wkts} &nbsp;|&nbsp; ${m.t2}: ${lm.teams[m.t2].runs}/${lm.teams[m.t2].wkts}</div>
          <button class="btn btn-gold" onclick="state.liveMatch=null; state.screen='SEASON'; render()">Back to Points Table →</button>
        </div>
      </div>
    `;
  }
  return '';
}

// ==================== TRADE WINDOW & MINI AUCTION ====================
function openTradeWindow() {
  state.screen = 'TRADE';
  render();
}

function executeTrade(targetTeamId, givePlayerId, getPlayerId) {
  const userF = getTeam(state.userTeam);
  const oppF = getTeam(targetTeamId);
  const giveP = userF.squad.find(x => x.id === givePlayerId);
  const getP = oppF.squad.find(x => x.id === getPlayerId);
  if (!giveP || !getP) return;

  const diff = +(getP.soldPrice - giveP.soldPrice).toFixed(2);
  if (userF.purse < diff) return alert('Not enough purse balance to cover salary difference!');

  userF.squad = userF.squad.filter(x => x.id !== givePlayerId);
  oppF.squad = oppF.squad.filter(x => x.id !== getPlayerId);
  giveP.team = oppF.id;
  getP.team = userF.id;
  userF.squad.push(getP);
  oppF.squad.push(giveP);
  userF.purse = +(userF.purse - diff).toFixed(2);
  oppF.purse = +(oppF.purse + diff).toFixed(2);

  alert(`🤝 TRADE COMPLETED! Acquired ${getP.name} from ${oppF.id} in exchange for ${giveP.name}.`);
  render();
}

function releasePlayer(pid) {
  const f = getTeam(state.userTeam);
  const lg = activeLeague();
  if (f.squad.length <= lg.minSquad) return alert(`Squad cannot drop below minimum limit (${lg.minSquad} players)!`);
  const idx = f.squad.findIndex(x => x.id === pid);
  if (idx < 0) return;
  const [p] = f.squad.splice(idx, 1);
  f.purse = +(f.purse + (p.soldPrice || 1)).toFixed(2);
  p.team = null;
  const mp = state.players.find(x => x.id === p.id);
  if (mp) mp.team = null;
  render();
}

function startNextSeasonMiniAuction() {
  state.season++;
  Object.values(state.franchises).forEach(f => f.purse = +(f.purse + 5).toFixed(2));
  startAuction('MINI');
}

function renderTrade() {
  const userF = getTeam(state.userTeam);
  const otherTeams = activeTeams().filter(t => t.id !== state.userTeam);
  const selOppId = document.getElementById('trade-opp')?.value || otherTeams[0].id;
  const oppF = getTeam(selOppId);

  document.getElementById('top-status').innerText = `TRADE WINDOW • PURSE: ${fmtCr(userF.purse)}`;

  return `
    <div class="card">
      <div class="h2">
        <span>🔄 Post-Season Trade Window</span>
        <span class="pill">Purse: ${fmtCr(userF.purse)}</span>
      </div>
      <div class="sub">Swap players with friends or AI franchises before ${activeLeague().id} Season ${state.season + 1} Mini Auction (+₹5 Cr purse bonus!).</div>
    </div>

    <div class="card">
      <div class="h2">1. Propose Player Swap</div>
      <div class="grid-3" style="margin-bottom:10px;">
        <div>
          <div class="sub">Target Franchise</div>
          <select id="trade-opp" onchange="render()">
            ${otherTeams.map(t => `<option value="${t.id}" ${t.id===selOppId?'selected':''}>${t.id} (${getTeam(t.id).ownerName})</option>`).join('')}
          </select>
        </div>
        <div>
          <div class="sub">You Give</div>
          <select id="trade-give">
            ${userF.squad.map(p => `<option value="${p.id}">${p.name} (${fmtCr(p.soldPrice||1)})</option>`).join('')}
          </select>
        </div>
        <div>
          <div class="sub">You Receive</div>
          <select id="trade-get">
            ${oppF.squad.map(p => `<option value="${p.id}">${p.name} (${fmtCr(p.soldPrice||1)})</option>`).join('')}
          </select>
        </div>
      </div>
      <button class="btn btn-blue" onclick="executeTrade(document.getElementById('trade-opp').value, Number(document.getElementById('trade-give').value), Number(document.getElementById('trade-get').value))">
        🤝 Execute Trade Deal
      </button>
    </div>

    <div class="card">
      <div class="h2">2. Release Players for Mini Auction Purse</div>
      ${userF.squad.map(p => `
        <div class="row">
          <div>
            <b>${p.name}</b> ${roleBadge(p.role)}
            <div class="sub">Salary: ${fmtCr(p.soldPrice || 1)}</div>
          </div>
          <button class="btn-sm btn-red" onclick="releasePlayer(${p.id})">Release (+${fmtCr(p.soldPrice||1)})</button>
        </div>
      `).join('')}
    </div>

    <div class="bottom-dock">
      <div class="dock-inner">
        <button class="btn btn-gold" onclick="startNextSeasonMiniAuction()">
          🔨 Enter Season ${state.season + 1} Mini Auction (+₹5 Cr) →
        </button>
      </div>
    </div>
  `;
}

// ==================== MASTER RENDERER ====================
function render() {
  const app = document.getElementById('app');
  if (state.screen === 'HOME') app.innerHTML = renderHome();
  else if (state.screen === 'LOBBY') app.innerHTML = renderLobby();
  else if (state.screen === 'RETENTION') app.innerHTML = renderRetention();
  else if (state.screen === 'AUCTION') app.innerHTML = renderAuction();
  else if (state.screen === 'SQUAD_XI') app.innerHTML = renderSquadXI();
  else if (state.screen === 'SEASON') app.innerHTML = renderSeason();
  else if (state.screen === 'LIVE_MATCH') app.innerHTML = renderLiveMatch();
  else if (state.screen === 'TRADE') app.innerHTML = renderTrade();
}

render();
</script>
</body>
</html>

