# YT Apps Hub

Minimal APK distribution page for YouTube and YouTube Music.

Built with:
- HTML
- TailwindCSS
- Google Apps Script Web App API

---

## Features

- Clean responsive UI
- Dark mode support
- Dynamic APK updates
- Google Drive powered
- No backend hosting required
- Works with GitHub Pages
- Mobile optimized

---

# Setup

## 1. Create Google Apps Script

Create a new Apps Script project and add this in `Code.gs`:

```javascript
function doGet(e) {

  var youtubeFile = DriveApp.getFileById('YOUTUBE_FILE_ID');
  var musicFile = DriveApp.getFileById('MUSIC_FILE_ID');

  var data = {
    youtube: {
      name: youtubeFile.getName(),
      updated: youtubeFile.getLastUpdated().toLocaleString(),
      url: 'https://drive.google.com/uc?export=download&id=YOUTUBE_FILE_ID'
    },

    music: {
      name: musicFile.getName(),
      updated: musicFile.getLastUpdated().toLocaleString(),
      url: 'https://drive.google.com/uc?export=download&id=MUSIC_FILE_ID'
    }
  };

  return ContentService
    .createTextOutput(JSON.stringify(data))
    .setMimeType(ContentService.MimeType.JSON);
}
```

Replace:
- `YOUTUBE_FILE_ID`
- `MUSIC_FILE_ID`

with your Google Drive file IDs.

---

## 2. Deploy Apps Script

Deploy as:

- **Type:** Web App
- **Execute as:** Me
- **Who has access:** Anyone

Copy the generated Web App URL.

---

## 3. Replace API URL

Inside `index.html`:

```javascript
const API_URL = "YOUR_GOOGLE_SCRIPT_WEB_APP_URL";
```

Replace with your deployed Apps Script URL.

---

## 4. Upload to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin YOUR_REPO_URL
git push -u origin main
```

---

## 5. Enable GitHub Pages

Go to:

```text
Repository → Settings → Pages
```

Set:
- Source → Deploy from branch
- Branch → main
- Folder → /root

Save.

Site URL:

```text
https://yourusername.github.io/repository-name
```

---

# File Structure

```text
.
├── index.html
├── README.md
└── Code.gs
```

---

# Notes

If data does not load:

- Redeploy Apps Script after changes
- Ensure access is set to "Anyone"
- Check browser console for errors
- Verify Drive file permissions

---

# License

MIT
