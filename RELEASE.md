# How to Create a Release

## 1. Build die App
```bash
cd c:/temp/cv-manager-go
wails build -clean
```

## 2. Kopiere die EXE
```bash
cp build/bin/cv-manager-pro.exe /c/temp/github-releases/cv-manager-pro-v1.1.3.exe
```

## 3. Update version.json
- Ändere `latest_version`
- Ändere `download_url`
- Ändere `release_notes`

## 4. Erstelle GitHub Release
```bash
gh release create v1.1.3 \
  --repo nash87/cv-manager-pro-releases \
  --title "v1.1.3 - Window Controls & Obsidian UI" \
  --notes "$(cat RELEASE_NOTES.md)" \
  /c/temp/github-releases/cv-manager-pro-v1.1.3.exe
```

## 5. Pushe version.json
```bash
git add version.json README.md
git commit -m "Release v1.1.3"
git push
```
