# Codemagic.io Setup Guide 🚀

## What is Codemagic?

Codemagic is a CI/CD platform specifically designed for mobile apps. It provides free builds for iOS apps without needing a Mac!

## Free Tier Benefits:
- ✅ 500 build minutes/month (FREE)
- ✅ macOS build machines included
- ✅ Automatic code signing
- ✅ Direct TestFlight/App Store publishing
- ✅ No credit card required for free tier

---

## Setup Instructions

### Step 1: Create Codemagic Account

1. Go to https://codemagic.io
2. Click "Sign up for free"
3. Sign up with GitHub, GitLab, or Bitbucket

### Step 2: Upload Your Code to GitHub

```bash
cd PuzzleGame
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/PuzzleGame.git
git push -u origin main
```

### Step 3: Connect Repository to Codemagic

1. In Codemagic dashboard, click "Add application"
2. Select your Git provider (GitHub)
3. Authorize Codemagic to access your repositories
4. Select "PuzzleGame" repository
5. Click "Finish: Add application"

### Step 4: Configure the Build

1. Click on your app in Codemagic
2. Go to "Start your first build"
3. Select "codemagic.yaml" configuration
4. Codemagic will automatically detect the `codemagic.yaml` file in your repo

### Step 5: Set Up Code Signing (Optional for TestFlight/App Store)

#### For Development/Testing (No Apple Account Needed):
- Skip code signing setup
- The build will create an unsigned IPA
- Use AltStore or Sideloadly to install

#### For App Store/TestFlight (Requires Apple Developer Account - $99/year):

1. **In Codemagic Dashboard:**
   - Go to Teams > Your Team > Integrations
   - Click "App Store Connect"
   - Follow the wizard to connect your Apple Developer account

2. **Get Your App Store Connect API Key:**
   - Go to https://appstoreconnect.apple.com
   - Users and Access > Keys
   - Create a new key with "Developer" access
   - Download the .p8 key file
   - Note the Key ID and Issuer ID

3. **Add to Codemagic:**
   - Paste Issuer ID
   - Paste Key ID
   - Upload the .p8 file

### Step 6: Update codemagic.yaml

Edit `codemagic.yaml` and change:

```yaml
environment:
  vars:
    BUNDLE_ID: "com.yourname.puzzlegame"  # Change to your bundle ID
    
publishing:
  email:
    recipients:
      - your-email@example.com  # Change to your email
```

### Step 7: Start Build

1. Click "Start new build"
2. Select branch (main/master)
3. Click "Start new build"
4. Wait 5-10 minutes for the build to complete

### Step 8: Download Your IPA

Once the build completes:

1. Click on the completed build
2. Scroll to "Artifacts" section
3. Download the `.ipa` file
4. Install using AltStore, Sideloadly, or TestFlight

---

## Configuration Options

### Build Without Code Signing (For Testing)

If you don't have an Apple Developer account, modify `codemagic.yaml`:

```yaml
workflows:
  ios-workflow:
    name: iOS Puzzle Game Build (Unsigned)
    environment:
      ios_signing:
        distribution_type: development
        bundle_identifier: com.yourname.puzzlegame
      vars:
        XCODE_WORKSPACE: "PuzzleGame.xcodeproj"
        XCODE_SCHEME: "PuzzleGame"
    scripts:
      - name: Build unsigned app
        script: |
          xcodebuild -project "$XCODE_WORKSPACE" \
            -scheme "$XCODE_SCHEME" \
            -sdk iphoneos \
            -configuration Release \
            CODE_SIGNING_ALLOWED=NO \
            CODE_SIGN_IDENTITY="" \
            CODE_SIGNING_REQUIRED=NO \
            clean build
      - name: Create IPA
        script: |
          mkdir -p Payload
          cp -r build/Release-iphoneos/PuzzleGame.app Payload/
          zip -r PuzzleGame.ipa Payload
    artifacts:
      - PuzzleGame.ipa
```

### Change Bundle Identifier

In `codemagic.yaml`, update:
```yaml
BUNDLE_ID: "com.yourcompany.yourapp"
```

Also update in `PuzzleGame.xcodeproj/project.pbxproj`:
```
PRODUCT_BUNDLE_IDENTIFIER = com.yourcompany.yourapp;
```

### Enable Automatic Publishing to TestFlight

```yaml
publishing:
  app_store_connect:
    auth: integration
    submit_to_testflight: true
    beta_groups:
      - Internal Testers
```

---

## Triggering Builds

### Automatic Triggers (Push/PR)

Add to `codemagic.yaml`:

```yaml
workflows:
  ios-workflow:
    triggering:
      events:
        - push
        - pull_request
      branch_patterns:
        - pattern: 'main'
          include: true
          source: true
```

### Manual Trigger

Just click "Start new build" in the Codemagic dashboard

---

## Troubleshooting

### Build Fails - "No provisioning profile found"
**Solution:** Either:
1. Set up code signing properly in Codemagic
2. Use the unsigned build configuration above

### Build Fails - "Xcode project not found"
**Solution:** Make sure `codemagic.yaml` is in the root of your repository

### Can't Install IPA on iPhone
**Solution:** 
- Unsigned IPAs need AltStore or Sideloadly
- Or use Apple Developer account + TestFlight

### Build Takes Too Long
**Solution:** 
- Free tier has 500 minutes/month
- Each build takes ~5-10 minutes
- Upgrade to paid plan if needed

---

## Comparing Build Services

| Feature | Codemagic | GitHub Actions | Xcode Cloud |
|---------|-----------|----------------|-------------|
| Free builds | 500 min/month | 2000 min/month | 25 hrs/month |
| macOS included | ✅ Yes | ✅ Yes | ✅ Yes |
| Easy iOS setup | ✅ Very easy | ⚠️ Medium | ✅ Very easy |
| Code signing | ✅ Built-in | ❌ Manual | ✅ Built-in |
| Best for | iOS/Flutter | Any platform | iOS only |

---

## Next Steps

1. ✅ Upload code to GitHub
2. ✅ Create Codemagic account
3. ✅ Connect repository
4. ✅ Start build
5. ✅ Download IPA
6. ✅ Install with AltStore or TestFlight

**Need help?** Check out:
- Codemagic docs: https://docs.codemagic.io
- Codemagic Slack: https://codemagic.io/slack
- Video tutorial: Search "Codemagic iOS tutorial" on YouTube

---

Good luck building your puzzle game! 🎮🎉
