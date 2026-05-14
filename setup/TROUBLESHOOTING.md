# Troubleshooting

Common issues and solutions when using Claude with Netora.

## Connection Issues

### "Unauthorized" or "Bearer token required"

**Cause:** Invalid or expired API key.

**Fix:**
1. Check that your API key is correct in Claude.ai Settings > Integrations
2. Make sure there are no extra spaces before/after the key
3. Verify the key hasn't expired in Netora Settings > API Keys
4. Try creating a new API key and updating the integration

### "No tools available" or Claude doesn't call any tools

**Cause:** MCP integration not properly connected.

**Fix:**
1. Go to Claude.ai Settings > Integrations
2. Verify the server URL is exactly: `https://api-production-fa50.up.railway.app/api/ai/tools/mcp/`
3. Check that the integration shows a green status indicator
4. Try removing and re-adding the integration
5. Make sure you're chatting inside a **Project** that has the system prompt configured

### "Method not found" error

**Cause:** Claude is sending a request the server doesn't support.

**Fix:** This is usually transient. Try your request again. If it persists, check that you're using the latest system prompt from this repository.

## Tool Execution Issues

### "Tool not found: xyz"

**Cause:** Claude is trying to call a tool name that doesn't exist in the registry.

**Fix:**
1. Upload the latest `knowledge/01-tool-catalog.md` to your project
2. Use the exact tool names from the catalog
3. If using a skill prompt, make sure you copied the entire prompt

### "Well has no DCA parameters"

**Cause:** The well doesn't have `dca_qi` and `dca_di` set, which are required for forecasting and economics.

**Fix:**
```
Update well TJ-001 with dca_qi=500, dca_di=0.05, dca_b=0.5
```
Or have Claude set them:
```
Set DCA parameters for all wells in "North Field": qi=500 bopd, di=5%/month, b=0.5
```

### "Well has no CAPEX"

**Cause:** `capex_usd` is not set on the well. Required for economics calculations.

**Fix:**
```
Set capex_usd to 5000000 for well TJ-001
```

### "No assumption found"

**Cause:** The project doesn't have an economic assumption set.

**Fix:**
```
Create a base case assumption for my project with oil price $70/bbl,
royalty 20%, income tax 34%, discount rate 10%.
```

### Monte Carlo returns "insufficient data"

**Cause:** Monte Carlo requires range definitions (low/base/high) for uncertain variables.

**Fix:** Specify ranges explicitly:
```
Run Monte Carlo for well TJ-001 with:
- qi: 300-500-700 bopd
- oil price: $55-70-90/bbl
- capex: $4M-5M-7M
- 1000 simulations
```

## Performance Issues

### Slow responses (>30 seconds)

**Possible causes:**
1. **Large dataset** — Field economics for 50+ wells takes longer. Be patient.
2. **Multiple sequential tool calls** — Complex workflows chain many tools. This is normal.
3. **Server load** — Try again in a few minutes.

**Tips:**
- Start with single-well analysis before running field-level
- Use `get_project_full_data` instead of listing fields + wells separately
- For large projects, specify the field name to narrow the scope

### Claude stops mid-analysis

**Cause:** Claude hit its output limit for a single message.

**Fix:** Ask Claude to continue:
```
Continue the analysis from where you stopped.
```
Or break the request into smaller parts:
```
First, just run the economics for Field A.
```

## Data Issues

### Numbers look wrong

**Checklist:**
1. Verify well DCA parameters (qi in bopd, di as fraction/month — not percent)
2. Check that `di` is monthly: 0.05 = 5%/month, NOT 0.05%/month
3. Verify CAPEX is in USD (not thousands)
4. Check assumption royalty/tax rates are in percent (20 = 20%, not 0.20)

### Fiscal comparison shows unexpected values

**Check:**
1. Country codes must be uppercase: `USA`, `VEN`, `COL`, `ARG`, `BRA`, `PER`, `ECU`, `BOL`
2. Venezuela IHI rate applies AFTER royalty deduction
3. Government equity share is a fraction (0.51 = 51% PDVSA)

### Production records not showing

**Fix:**
1. Verify the well has production data: `List production records for well X`
2. Check date format is `YYYY-MM-DD`
3. Records may not exist yet — add them first

## Still Having Issues?

1. **Check the system prompt** — Make sure you're using the latest version from this repo
2. **Re-upload knowledge files** — Delete and re-upload all 6 files from `knowledge/`
3. **Test with a simple command** — Try `List all my projects` to verify basic connectivity
4. **Check the API directly** — Visit `https://api-production-fa50.up.railway.app/api/ai/tools/mcp/` in a browser to verify the server is up
