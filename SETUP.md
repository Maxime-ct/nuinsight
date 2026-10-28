# NU Insight: upload to Vercel

Four files go in the **root** of your GitHub repo (replace the old ones):

- `index.html`: the public site (new design)
- `studio.html`: your private posting page
- `feed.json`: the content. Studio writes it, the site reads it
- `SETUP.md`: this guide (optional)

Photos uploaded through Studio are saved by Studio into a `photos/` folder in the same repo. You don't create it.

## 1. Replace the files in GitHub
Open your repo on github.com → **Add file → Upload files** → drag in the new `index.html`, `studio.html` and `feed.json` → **Commit changes**. GitHub replaces files with the same name.

## 2. Make sure Vercel deploys from that repo
Studio publishes by committing to GitHub, so Vercel has to redeploy whenever the repo changes.

1. In Vercel open your project → **Settings → Git**.
2. If it shows your GitHub repo, you're done. Every commit now redeploys.
3. If it says "No connected Git repository" (the project was made by drag-and-drop or the CLI), create a new project instead: **Add New → Project → Import** your repo. Set **Framework Preset: Other**, leave Build Command and Output Directory empty, and click **Deploy**. Then move your domain to the new project if you use one.

## 3. Create a token (once)
1. github.com/settings/tokens → **Fine-grained tokens → Generate new token**.
2. **Repository access → Only select repositories** → pick your repo.
3. **Repository permissions → Contents: Read and write**.
4. Generate, then copy the token (`github_pat_…`). GitHub shows it only once.

## 4. Connect Studio
1. Open `https://your-site.vercel.app/studio.html`.
2. Click **Connect** and enter your GitHub username, repo name, branch (`main`) and the token.
3. Click **Save and load**. The top bar should say "Connected".

The token is saved only in the browser you typed it into. It is never written into the site. Studio is a normal page that anyone could open, but without the token it can't publish anything.

## 5. Posting
1. **Albums → + New album**, then enter the event name and date.
2. **Add photos**. Photos are shrunk to 1600px automatically, and the date taken is read from each file.
3. Add captions if you like, and press **Cover** on the photo you want as the album cover.
4. Press **Publish**. Vercel redeploys in under a minute, and open pages pick up the change within about 20 seconds after that.

## Things to know
- **Sample content:** the six albums and the poll are put back exactly as in your page. The first album ("2026 NU Vision Career Fair Week") has no pictures yet because its photos were stored on the platform the page was built on, so add them again in Studio. The other five albums are the template's samples with grey placeholder pictures. In Studio, delete each one with **Delete album** once your real albums are in.
- **Poll:** the question and starting counts are edited in Studio. Visitors' own votes and likes are saved in their own browser only, so they aren't totalled across everyone. Counting across visitors needs a server.
- **Removing photos:** Remove and Delete album take things off the site, but the image files stay in the repo. That is harmless.
- **Clips (videos):** the Clips page is supported by the site, but Studio doesn't upload videos. To add one, put the file in a `clips/` folder in the repo and add an entry like `{"file":"night.mp4","title":"Music night","date":"2026-10-20"}` to `"clips"` in `feed.json`.
- **Backup:** `feed.json` is your whole content list. GitHub keeps its history, so you can restore an older version from there.
