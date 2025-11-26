# Puzzle Master - iOS Puzzle Game 🧩

A sliding tile puzzle game for iOS with 20 levels of increasing difficulty!

## Features ✨

- **20 Challenging Levels** - Start with 3x3 grids and progress to 6x6
- **Progressive Difficulty** - Each level gets harder with more tiles and shuffles
- **Level Unlocking System** - Beat levels to unlock the next challenge
- **Move Counter** - Track your efficiency
- **Timer** - Race against the clock
- **Save Progress** - Your unlocked levels are saved automatically
- **Beautiful UI** - Gradient backgrounds and smooth animations

## Game Rules 🎮

1. Tap tiles adjacent to the empty space to slide them
2. Arrange all tiles in numerical order (1, 2, 3... with empty space last)
3. Complete levels to unlock new ones
4. Try to solve each puzzle in the fewest moves!

## Building the App 🛠️

### Option 1: GitHub Actions (Recommended - No Mac Required!)

This is the easiest way to build your IPA without owning a Mac:

1. **Create a GitHub account** (free) at https://github.com

2. **Create a new repository:**
   - Click "New repository"
   - Name it "PuzzleGame" or whatever you want
   - Make it Public or Private
   - Don't initialize with README

3. **Upload this project:**
   ```bash
   cd PuzzleGame
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/PuzzleGame.git
   git push -u origin main
   ```

4. **Watch the build:**
   - Go to your repository on GitHub
   - Click "Actions" tab
   - The build will start automatically
   - Wait ~5-10 minutes for it to complete

5. **Download your IPA:**
   - Click on the completed workflow run
   - Scroll down to "Artifacts"
   - Download "PuzzleGame-IPA"
   - Unzip to get your IPA file

### Option 2: Using a Mac

If you have access to a Mac:

1. Install Xcode from the App Store
2. Open `PuzzleGame.xcodeproj`
3. Select your device or simulator
4. Click the Play button to build and run

### Option 3: Cloud Mac Services

Use a cloud Mac service (requires payment):
- MacStadium
- MacinCloud
- AWS Mac instances

## Installing the IPA on Your iPhone 📱

**Important:** Unsigned IPAs cannot be installed directly on iPhones. You need one of these methods:

### Method 1: AltStore (Free, Recommended)

1. Download AltStore from https://altstore.io
2. Install AltServer on your Windows PC
3. Connect iPhone via USB
4. Use AltStore to sideload the IPA
5. Trust the certificate in Settings > General > Device Management

**Note:** Apps expire after 7 days and need to be re-signed (free account) or 1 year (paid developer account)

### Method 2: Apple Developer Account ($99/year)

1. Sign up at https://developer.apple.com
2. Create a certificate and provisioning profile
3. Add these as GitHub Secrets:
   - `P12_CERTIFICATE`: Your .p12 certificate (base64 encoded)
   - `P12_PASSWORD`: Your certificate password
   - `PROVISIONING_PROFILE`: Your .mobileprovision file (base64 encoded)
4. Update `PRODUCT_BUNDLE_IDENTIFIER` in project.pbxproj
5. Push to GitHub - the workflow will create a signed IPA

### Method 3: Sideloadly (Free/Paid)

1. Download Sideloadly from https://sideloadly.io
2. Connect your iPhone
3. Drag the IPA to Sideloadly
4. Sign with your Apple ID
5. Install on device

### Method 4: TestFlight (Requires Developer Account)

1. Upload to App Store Connect
2. Invite yourself as a tester
3. Install via TestFlight app

## Project Structure 📁

```
PuzzleGame/
├── PuzzleGame/
│   ├── PuzzleGameApp.swift    # App entry point
│   ├── ContentView.swift      # Level selection screen
│   ├── GameView.swift         # Main game screen
│   ├── GameManager.swift      # Progress tracking
│   └── Info.plist            # App configuration
├── PuzzleGame.xcodeproj/      # Xcode project
│   └── project.pbxproj
└── .github/
    └── workflows/
        └── build.yml          # GitHub Actions workflow
```

## Customization 🎨

### Change Bundle Identifier
Edit `project.pbxproj` and replace:
```
PRODUCT_BUNDLE_IDENTIFIER = com.yourname.puzzlegame;
```

### Change App Name
Edit `Info.plist`:
```xml
<key>CFBundleDisplayName</key>
<string>Your App Name</string>
```

### Adjust Difficulty
Edit `GameView.swift`:
- Line ~125: Change grid size progression
- Line ~133: Change number of shuffles per level

### Add More Levels
Edit `ContentView.swift`:
- Line ~31: Change `ForEach(1...20` to your desired number

## Troubleshooting 🔧

### Build fails on GitHub Actions
- Make sure the workflow file is in `.github/workflows/`
- Check the Actions tab for error messages
- Ensure all Swift files are properly formatted

### Can't install IPA on iPhone
- Unsigned IPAs need AltStore, Sideloadly, or a developer certificate
- Make sure your iPhone trusts your PC (iTunes installed on Windows)
- Check that USB Debugging is enabled

### App crashes on launch
- Make sure you're using iOS 15.0 or later
- Check device compatibility (iPhone/iPad)

## Features Coming Soon 🚀

- Sound effects
- Achievements system
- Leaderboards
- Hints system
- Custom themes
- Daily challenges

## Support 💬

Having issues? Check these resources:
- [AltStore Documentation](https://faq.altstore.io)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [Apple Developer Portal](https://developer.apple.com)

## License 📄

Free to use and modify for personal projects!

---

**Enjoy solving puzzles! 🎉**
