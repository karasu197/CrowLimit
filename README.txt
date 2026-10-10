VANGUARD (BobLimt) - User Guide
===============================

A Destiny 2 packet limiter with a live overlay, clear tracker, leaderboards,
loadout swaps, and limiter sessions. This guide covers setup, the ports, the UI
and its customization, an FAQ, and a changelog at the bottom.


INSTALL & LAUNCH
----------------
1. Extract the WHOLE folder before running. Do not launch from inside the zip.
2. Keep these files together in one folder:
     BobLimt.exe, BobLimt.cfg, WinDivert.dll, WinDivert64.sys,
     qbtxr54.xaml, MapleMono-Bold.ttf, README.txt
3. Start Destiny 2 first, then run BobLimt.exe and accept the admin prompt
   (WinDivert needs administrator rights to capture packets).
4. Settings save to BobLimt.cfg; startup diagnostics go to BobLimt.launch.log.

Automatic updates
- On every launch BobLimt checks the public update channel. If a newer version
  exists it downloads the full package, closes, updates the folder, and restarts.
- Your BobLimt.cfg, background.png, custom icons, and Ahk folder are preserved
  across updates.


THE PORTS (what each one does)
------------------------------
- 3074  - Destiny gameplay / game-world traffic (PvE). Sub-toggles:
            DL       block inbound (download)
            UL       block outbound (upload)
            DL Slow  delay inbound ~1s instead of fully blocking
            UL Slow  delay outbound ~1s instead of fully blocking
- 27k   - Alternate player traffic group (PvP). DL and UL.
- 30k   - Instance traffic. Includes:
            30k                full instance block
            30k Slow           delayed instance traffic
            Load Manipulation  hold/release instance loads
- 7500  - API / "good 7500" block.
- Reconnect - One-shot pulse that forces a fresh instance connection.
- Reinject  - One-shot pulse that immediately releases (reinjects) all buffered
              3074 packets you are holding, instead of waiting for the buffer to
              flush on its own. It is a pulse, not a toggle - it flashes once.

Each port can be bound to a key in Keybinds and most show a badge on the overlay
with a live "seconds active" tick timer while engaged.


MAIN WINDOW
-----------
- Top-right shows the engine status: "WinDivert live", "WinDivert Inactive", or
  "Backend off".
- Directly under the status is the master TICKING SWITCH (tiny slider):
    ON  = "WinDivert live", ports can be ticked normally.
    OFF = "WinDivert Inactive", all ports are forced off and port hotkeys are
          ignored. Everything else (overlay, sessions, leaderboards, timers)
          keeps working - you just can't toggle ports until you switch it back on.
- Function buttons: Settings, Overlay (on/off), Preferences, Keybinds, Swaps, AHK.
- BLOCKED TRAFFIC panel shows live bytes blocked per port.
- WEEKLY / ALL-TIME panels are the community leaderboards (top 100, scrollable).
  Click the WEEKLY title to cycle 3074 / 27K / 30K / 7500.
- Anti-cheat audit records limiter opens, first-seen IP per Bungie ID, last
  opened time in Eastern time, and pass/block packet metadata for review.
- CLEARS panel is the Bungie clear heatmap (one month at a time).
- The "_" button minimizes to the system tray; the power button exits.
- The small "?" in the bottom-right opens the community Discord.


OVERLAY & ITS CUSTOMIZATION
---------------------------
- The overlay only shows while Destiny 2 is the foreground window.
- Open Settings > overlay editor (Confined region / Edit) to drag, resize, hide,
  and show each block. Draggable blocks:
    Timer, Clears, Active Modules, Net Monitor, Input Timer.
- Each block has an "H" button (hide/show) and a corner grip (resize).
- The accent color (Settings) drives overlay text, badge outlines, and icons.
- Transparent backgrounds, badge upload/download arrows, and the per-module
  "seconds active" tick timer can all be toggled in Settings.
- Module badge size and the icon-vs-port-label mode are adjustable in Settings.
- Custom badge icons can be imported from PNG/JPG/JPEG/JPRG/BMP/GIF. Imports are
  normalized into icons/<module>.png, icons/<module>.bmp, and a traced SVG sidecar.
- Settings > Tick sound lets you import a MP3 that plays whenever a limiter port
  is ticked on. Reset removes sounds/tick.mp3.

First-input timer (overlay widget)
- A second overlay timer with its own keybinds (Keybinds > TIMERS):
    Arm Timer      arms it; your next keypress/click starts it counting.
    Pause / Resume freezes or resumes the running clock.
    Reset Timer    stops and zeroes it.
- It is fully customizable like the other overlay blocks (move/resize/hide/accent).


KEYBINDS
--------
- Click a bind row, press the combo, release. Modifier combos (Ctrl+Shift+key,
  side mouse buttons, etc.) are supported. Press Esc while capturing to clear it.
- Sections: the port binds (3074 DL/UL/UL Slow/DL Slow, 27k DL/UL, 7500, 30k,
  30k Slow, Load Manipulation, Reconnect, Reinject, Game Pause), FREQUENTLY USED
  (Good 7500), HOST HOTKEYS (session pulses), and TIMERS (first-input timer).
- "Limit keybinds to Destiny focus" (Preferences) can suppress binds while alt-tabbed.


SWAPS (loadout swapping)
------------------------
- Five independent profiles across the top. Each has its own swap bind, duration,
  delay, inventory bind, open-loadouts bind, port choice, selected loadouts, and
  ending loadout.
- IMPORTANT: profiles do NOT share loadout pixel coordinates. Each profile stores
  its own slot coordinates - if you set up profile 1, profile 2 still needs its
  own pixels captured.
- Per-slot: the active checkbox decides if the slot is used; Edit captures that
  slot's screen coordinates (hover the Destiny slot and press F2).
- "Start Editing" captures all slots in order: click Start Editing, press
  Shift+0, then click loadout slots 1 through 20.
- QuickSwap binds (separate view) fire a single numbered loadout each.


LIMITER SESSIONS
----------------
- Host a session to share a code, or Join one with a code (type it or paste with Ctrl+V).
- Roles: Host, Admin, Member, and a restricted role. Hosts/admins can change any
  player's role by clicking their role tag (M / A / I).
- A controller (host or admin) clicks a player to select them, then pulses a port
  button to send that port to the players THEY selected. Selections are private
  to each controller - your picks are not shared with other hosts/admins.
- Members can toggle "Allow toggles" to opt in or out of receiving pulses.
- The Reconnect session button is a pulse: clicking it flashes briefly and
  returns to rest (the port buttons latch on/off, Reconnect does not).


BUNGIE CLEAR TRACKER
--------------------
- Enter your Bungie ID as Name#1234 in Settings to connect.
- Clears are counted per daily reset window. Raid/dungeon counts and a calendar
  heatmap show in the overlay and main window.
- Uses public Bungie data only - no OAuth login or client secret required.


AHK MANAGER
-----------
- BobLimt uses an "Ahk" folder beside the exe. Put .ahk scripts there.
- Refresh reloads the list, Open Folder opens it in Explorer, and the toggles
  start/stop individual scripts.


FAQ
---
Q: Why is my macro / swap not clicking the right spots?
A: Set your pixels (loadout slot coordinates) as needed, or all at once with
   "Start Editing". A swap can't click a slot whose coordinates were never captured.

Q: Why aren't my 2nd profile's swaps working?
A: Profiles do not inherit pixels from other profiles. Each profile needs its own
   loadout coordinates captured - set up the pixels on profile 2 separately.

Q: The overlay isn't showing.
A: It only appears while Destiny 2 is focused. Make sure Overlay is ON in the main
   window, and that you aren't alt-tabbed to another app.

Q: I'm pressing my port keybind but nothing happens.
A: Check the master ticking switch (top-right, under the status text). If it says
   "WinDivert Inactive", port hotkeys are disabled - switch it back to "WinDivert
   live". Also check that the bind isn't suppressed while Destiny is unfocused.

Q: A widget won't move / I can't find a block.
A: Open the overlay editor (Settings) to drag, resize, hide, and show each block.
   Hidden blocks are turned back on with their "H" button there.

Q: My keybind won't capture / a function key won't bind.
A: Click the bind row first, then press the combo and release. F10/Alt-style keys
   are supported. Press Esc while capturing to clear the bind.

Q: Leaderboards are empty or say to enable submission.
A: Turn on "Submit to leaderboard" in Preferences and set a valid Bungie ID.

Q: A session pulse from the host didn't affect me.
A: You must be selected by that controller AND (as a Member) have "Allow toggles"
   on. If your own ticking switch is set to Inactive, incoming pulses are ignored.

Q: WinDivert / driver errors on launch.
A: Run as administrator, keep WinDivert.dll and WinDivert64.sys beside the exe,
   and launch from the extracted folder (not from inside the zip).


CHANGELOG (recent updates)
--------------------------
v2.0.18
- Added a server-side Bungie ID blacklist. Blocked accounts reuse the existing
  login-locked screen and cannot submit leaderboard/audit/config/session RPCs.
- Added database guards that force stored Bungie IDs to lowercase-normalized
  keys and wipe mixed-case duplicate account rows so affected users can sign up
  again cleanly.

v2.0.17
- Added a manual Import button beside Help for cloud settings. Import is only
  available after the Bungie ID is verified on the registered PC, then rewrites
  BobLimt.cfg from the saved database blob and refreshes live settings.
- Changed cloud settings so startup no longer auto-imports and normal local
  saves no longer overwrite the cloud blob; the latest config uploads on close.
- Stopped packet audit storage from logging passed packets. New builds only
  submit blocked packet audit rows, preventing the packet audit table from
  growing into multi-GB database usage.

v2.0.16
- Added all-window box opacity, expanded background image import formats,
  Layover/Resize background fit, and performance optimizations for resized
  background drawing and hidden overlay repainting.

v2.0.14
- Made limiter sessions server-authoritative. Session codes are now used only to
  join; pulses and role changes require Supabase RPC approval for the locked
  Bungie ID/hardware hash, and Realtime broadcasts are only wake-up hints.

v2.0.13
- Fixed remote config restore after deleting BobLimt.cfg: saving a Bungie ID from
  a fresh local config now pulls the saved server config before uploading, so
  overlay/preferences/swap settings are not overwritten by defaults.

v2.0.12
- Added a compatibility retry for older Supabase audit RPC signatures so the
  limiter can still open while the hardware-lock SQL migration is being rolled
  out.

v2.0.11
- Preserved custom background.png and the custom icons folder across package
  auto-updates.

v2.0.10
- Added a Settings background image customizer beside the custom icon controls.
  The selected PNG/JPEG/BMP/GIF/TIFF/ICO image is normalized into
  background.png and painted behind all normal BobLimt window shells. Settings
  lets you keep the native-size layover or resize it to the current window. WebP
  works when Windows has a WebP WIC codec installed.

v2.0.9
- Added hardware-locked remote config sync. BobLimt now stores a compact
  protobuf-style base64 config blob in Supabase, keyed by Bungie ID and guarded
  by the locked hardware hash.
- Startup pulls the server config before the packet manager is built; later
  local config saves queue a background upload after the login check passes.
- The synced blob covers operational settings, UI preferences, keybinds, swap
  profiles, and quick swaps. Live session state and blocked byte counters stay
  out of the blob because those are volatile or already server-authoritative.

v2.0.8
- Hardened limiter sessions against public Realtime abuse: hosted sessions no
  longer advertise into a shared active-session lobby, new sessions use long
  cryptographically-random codes, old short session codes are rejected/cleared,
  and roster/control broadcasts require the new session auth marker.
- Active-session diagnostics no longer lists live session codes, because that
  made every hosted limiter session discoverable to anyone with the public anon
  key.

v2.0.7
- Hardened leaderboard writes against direct RPC abuse: submissions now require
  the locked hardware hash, old unauthenticated write signatures are removed,
  public lifetime seeding is disabled, and server-side caps/rate limits reject
  large scripted jumps.
- Update packages now require an official binary-repo URL plus a SHA-256 hash in
  latest.json before the updater will apply them.
- Build scripts no longer depend on vswhere.exe.

v2.0.6
- Added motherboard-hardware-lock login checks. First login claims the machine;
  clearing the lock server-side lets the next login claim a new machine.
- Added Ship Skip: Preferences > Quality of Life toggle plus a Skip swap profile
  that auto-runs from inbound 1100 dialogue-start packets without ticking ports.
- Fixed failed login checks getting stuck on "Checking this PC"; SQL/RPC issues
  now show a login-check error instead.
- The limiter can always be minimized or closed while a login check is blocking
  limiter actions.

v2.0.5
- Blocked Traffic now syncs from server-side per-port totals on startup.
- Weekly leaderboards now use resettable server-side per-port weekly counters.
- Added IP-lock enforcement: a Bungie ID locked to another IP keeps the limiter
  off and only leaves Help clickable until the lock is reset server-side.
- Fixed overlay recovery after long alt-tabs so it cannot stay hidden forever.

v2.0.4
- Fixed custom imported badge icons rendering as a solid dark/tinted block.
- Custom icon imports now normalize images, preserve color, infer simple
  transparent backgrounds for flat JPG-style icons, and emit PNG/BMP/SVG files.
- Added a Settings MP3 picker for a custom tick-on sound.
- Added server-side audit hooks for first login IP, last-opened Eastern time,
  and batched pass/block packet metadata across limiter ports.

v1.0.51
- New Reinject port: a one-shot pulse (own keybind) that immediately reinjects
  all buffered 3074 packets you are holding. Flashes once; not a toggle.
- New master ticking switch in the main window (under the status text). Turning
  it off shows "WinDivert Inactive", forces all ports off, and disables port
  hotkeys while leaving the overlay, sessions, leaderboards, and timers working.
- Added a 3074 DL Slow keybind (delay inbound), completing the 3074 slow pair.
- Session Reconnect button now flashes briefly instead of latching on/off.
- Added a "?" help button (bottom-right of the main window) that opens the Discord.

v1.0.50
- Fixed the occasional black flash when ticking / unticking modules (the overlay
  now updates position, size, and pixels in one atomic step).
- Slightly larger, easier-to-read in-module tick timers.

v1.0.49
- Limiter session card reworded to be neutral (Host / Join Session); removed text
  describing a host taking control of your limiter.

v1.0.46
- New overlay "first input" timer with Arm / Pause-Resume / Reset keybinds.
- Community leaderboards now list the top 100 (was 25), scrollable.
- Limiter sessions: each host/admin's control selection is private to them; a
  pulse only affects the players that controller selected.

v1.0.45
- Clears heatmap recolored into discrete bands (green / yellow / orange / red).
- Limiter sessions: a restricted player can no longer leave the session themselves.

Earlier releases added the community leaderboards, limiter sessions with roles,
the fireteam / current-activity card, loadout swap profiles + QuickSwap,
customizable overlay badge icons, and the Bungie clear tracker + heatmap.
