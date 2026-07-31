PASSAGE CONSOLE - local auto-populating version
================================================

Two files, kept in the SAME folder:
  boating-server.py       the little local server + data proxy
  boating-dashboard.html  the dashboard itself

WHY THIS VERSION
Opened on its own, the dashboard tries to pull the DFO tide feed and the
NDBC buoy straight from your browser, and most browsers block that (a CORS
security rule). This version runs a tiny server on your own machine that
fetches those feeds for you, so the tide and buoy panels fill in on their own.


RUN IT
  1. Keep both files in the same folder.
  2. Open a terminal in that folder.
  3. Run:
        python3 boating-server.py
     (Windows, if that fails, try:  py boating-server.py )
  4. It opens http://localhost:8787 automatically. If not, open that yourself.
  5. Stop it with Ctrl+C when you're done.

That's it. Tide + buoy populate live. No accounts, no keys.


THE AI "SKIPPER'S READ" (optional)
The hosted/artifact version gets this for free. Running locally, it needs your
own Anthropic API key. Everything else works without it, and the banner verdict
is still calculated from the live wind/wave/tide numbers.

Getting a key (about 5 minutes):
  1. Go to console.anthropic.com and sign up (or sign in).
     This is the developer console. It is a SEPARATE product from the Claude
     app you already use - a Claude Pro/Max subscription does NOT include API
     access, and this has its own billing.
  2. Add a payment method under Billing and load credits. There is a $5 minimum.
     A brand-new key will error until credits are on the account.
  3. Go to API Keys, click Create Key, name it, and copy it immediately
     (it is shown only once). It looks like  sk-ant-...

Turn it on, before step 3 of "RUN IT" above:
  Mac/Linux:
        export ANTHROPIC_API_KEY="sk-ant-...paste-your-key..."
  Windows (Command Prompt):
        set ANTHROPIC_API_KEY=sk-ant-...paste-your-key...
Then start the server as normal. The startup line will say the AI read is ON.

Cost: tiny. Each skipper's read is a small request, roughly a fifth of a cent
on the default model (Haiku 4.5). Your $5 of credit covers thousands of them.
You only pay for what you use; leave it idle and it costs nothing.

Model: the default (claude-haiku-4-5-20251001) is set for you, so a key alone is
enough. To use a different one, also set ANTHROPIC_MODEL. If a read ever comes
back with a model error, that is the setting to change.
  Models + current pricing: https://docs.claude.com/en/docs/about-claude/models
  Your usage + billing:      https://console.anthropic.com


GOOD TO KNOW / VERIFY BEFORE YOU GO
- This is decision-support, not an official product. Always check the official
  Environment Canada Howe Sound / Strait of Georgia marine forecast and any
  wind warnings before departing, and use your own judgement.
- Tides are DFO astronomical PREDICTIONS for Point Atkinson. Real levels shift
  with wind and barometric pressure.
- There is no tidal-current station on the crossing itself. The flood/ebb shown
  is derived from the Point Atkinson tide trend, so treat it as a direction
  indicator, not a measured current. The real hazard on this passage is wind,
  and wind against the tidal stream.
- Buoy 46146 (Halibut Bank) is ECCC-owned but distributed through the US NDBC
  service. It sits mid-Strait and typically reads rougher than the sheltered
  water near Bowen - use it as an offshore reference, not the route exactly.
- The Ragged/Pasley marker is approximate.
- DFO is migrating the tide API to a new host; the server already tries the new
  one automatically if the old address stops answering.
