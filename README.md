# PLM Part Namer — Azure Static Web App

A rules-based part naming tool. No API key required — all logic runs in the browser.

## Files
- `index.html` — the entire app (HTML + CSS + JS in one file)
- `staticwebapp.config.json` — Azure routing config
- `README.md` — this file

---

## Deploy to Azure Static Web Apps

### Option A: Deploy via Azure Portal (easiest, no CLI needed)

1. Go to https://portal.azure.com
2. Search for **Static Web Apps** → click **Create**
3. Fill in:
   - Subscription & Resource Group (create new if needed)
   - Name: `plm-part-namer` (or whatever you like)
   - Plan type: **Free**
   - Region: pick closest to your team
   - Source: **GitHub** (recommended) or **Azure DevOps**
4. Connect your GitHub account and select your repo/branch
5. Build details:
   - App location: `/`
   - API location: *(leave blank)*
   - Output location: `/`
6. Click **Review + Create** → **Create**
7. Azure will set up a GitHub Action that auto-deploys on every push

Your app will be live at a URL like:
`https://purple-flower-abc123.azurestaticapps.net`

You can add a custom domain under **Settings → Custom domains**.

---

### Option B: Deploy via Azure CLI

```bash
# Install Azure CLI if needed: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli
az login

az staticwebapp create \
  --name plm-part-namer \
  --resource-group your-resource-group \
  --source https://github.com/yourorg/yourrepo \
  --location "East US 2" \
  --branch main \
  --app-location "/" \
  --output-location "/" \
  --login-with-github
```

---

## Updating the app

Once deployed via GitHub:
1. Edit `index.html` locally
2. `git commit -m "update naming rules"` 
3. `git push`
4. Azure auto-deploys within ~1-2 minutes — everyone gets the update instantly

---

## Connecting to your organization

- Share the Azure Static Web App URL with your team
- Bookmark it in your PLM system, Confluence, SharePoint, or Teams
- No install required — works in any browser

---

## Customizing naming rules

All logic is in the `<script>` tag at the bottom of `index.html`:

- **Add new component types**: add an entry to the `COMPONENT_TYPES` array
- **Add known brands**: add to the `BRANDS` array  
- **Add known locations/subsystems**: add to the `LOCATION_MAP` object
- **Add fastener head types**: edit the `parseFastener()` function
- **Add new unit patterns**: add to `UNIT_PATTERNS`
