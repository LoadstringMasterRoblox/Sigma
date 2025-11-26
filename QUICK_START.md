# Quick Start - Get Your IPA in 10 Minutes! 🚀

## Step 1: Extract the Zip
Extract `PuzzleGame.zip` to a folder on your computer.

## Step 2: Push to GitHub

Open Command Prompt or Terminal in the PuzzleGame folder and run:

```bash
# Initialize git repository
git init

# Add all files
git add .

# Make first commit
git commit -m "Initial commit - Puzzle Game"

# Create main branch
git branch -M main

# Add your GitHub repository (CREATE IT FIRST ON GITHUB!)
git remote add origin https://github.com/YOUR_USERNAME/PuzzleGame.git

# Push to GitHub
git push -u origin main
```

**Or if you want to add codemagic.yaml separately:**

```bash
git add codemagic.yaml
git commit -m 'Add first workflow'
git push
```

## Step 3: Set Up Codemagic

1. Go to https://codemagic.io
2. Click "Sign up for free"
3. Sign in with your GitHub account
4. Click "Add application"
5. Select "GitHub" 
6. Choose your "PuzzleGame" repository
7. Click "Finish: Add application"

## Step 4: Start Your First Build

1. Codemagic will detect the `codemagic.yaml` file automatically
2. Click "Start new build"
3. Select "main" branch
4. Click "Start new build"
5. Wait 5-10 minutes ⏱️

## Step 5: Download Your IPA

1. Once build completes (green checkmark ✅)
2. Click on the build
3. Scroll down to "Artifacts"
4. Download `PuzzleGame.ipa`
5. Done! 🎉

## Step 6: Install on Your iPhone

### Option A: AltStore (Free, Easy)
1. Download AltStore from https://altstore.io
2. Install AltServer on your PC
3. Connect iPhone via USB
4. Open AltStore on iPhone
5. Tap "+" and select your IPA
6. Done!

### Option B: Sideloadly (Free/Paid)
1. Download from https://sideloadly.io
2. Connect iPhone via USB
3. Drag IPA into Sideloadly
4. Enter Apple ID
5. Click Start
6. Done!

### Option C: TestFlight (Requires $99 Apple Developer)
1. Set up App Store Connect in Codemagic
2. Enable TestFlight in codemagic.yaml
3. Build automatically uploads
4. Install via TestFlight app

---

## Troubleshooting

### "Repository not found" on git push
**Fix:** Create the repository on GitHub first at https://github.com/new

### "Permission denied" on git push
**Fix:** Set up SSH keys or use HTTPS with personal access token

### Can't see codemagic.yaml on GitHub
**Fix:** Make sure you're in the right folder when running git commands

### Codemagic doesn't detect the YAML
**Fix:** Make sure `codemagic.yaml` is in the root folder (not in a subfolder)

### Build fails with code signing error
**Fix:** See CODEMAGIC_SETUP.md for unsigned build configuration

---

## That's It!

You now have a working iOS puzzle game IPA built without owning a Mac! 🎮

**Need more details?** Check out `CODEMAGIC_SETUP.md` for the full guide.

**Have fun!** 🎉
