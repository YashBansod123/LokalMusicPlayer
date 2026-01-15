# 🎵 Lokal Music Player

A beautiful, feature-rich music streaming app built with React Native and Expo, using the JioSaavn API.

## ✨ Features

- 🔍 **Search Functionality** - Search for songs with real-time results and pagination
- 🎵 **Background Playback** - Music continues playing when app is minimized or screen is off
- 📱 **Mini Player** - Persistent bottom player bar synced across all screens
- 🎛️ **Full Player Controls** - Complete playback controls with seek bar
- 📝 **Queue Management** - Add, remove, and reorder songs in the queue
- 🔀 **Shuffle Mode** - Randomize playback order
- 🔁 **Repeat Modes** - Repeat off, repeat all, or repeat one
- 💾 **Persistent Storage** - Queue and playback state saved locally using MMKV
- 🎨 **Beautiful UI** - Gradient design inspired by modern music players
- ⚡ **Performance** - Optimized with proper state management using Zustand


## 🛠️ Tech Stack

- **React Native** with **Expo** (SDK 54)
- **TypeScript** for type safety
- **React Navigation v6** for navigation
- **Zustand** for state management
- **MMKV** for local storage
- **Expo AV** for audio playback
- **JioSaavn API** for music data

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- Node.js (v18 or higher)
- npm or yarn
- Expo CLI: `npm install -g expo-cli`
- Android Studio (for Android) or Xcode (for iOS)
- Expo Go app on your phone (for testing)

## 🚀 Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/PratibhaSikheriya/LokalMusicPlayer.git
cd lokal-music-player
```

### 2. Install dependencies

```bash
npm install
```

### 3. Start the development server

```bash
npx expo start
```

### 4. Run on device/emulator

- **Android**: Press `a` in the terminal or scan QR code with Expo Go
- **iOS**: Press `i` in the terminal or scan QR code with Expo Go
- **Web**: Press `w` in the terminal

## 📁 Project Structure

```
lokal-music-player/
├── .expo
├── assets
├── node_modules
├── src/
│   ├── api/
│   │   └── saavn.ts              # API service for JioSaavn
│   ├── components/
│   │   ├── MiniPlayer.tsx        # Bottom mini player component
│   │   ├── SearchBar.tsx         # Search input component
│   │   └── SongCard.tsx          # Song list item component
│   ├── constants/
│   │   └── colors.ts             # App color scheme
│   ├── navigation/
│   │   └── AppNavigator.tsx      # Navigation configuration
│   │   └── TabNavigator.tsx      # For Tab Switching
│   ├── screens/
│   │   ├── HomeScreen.tsx        # Main screen with search & songs
│   │   ├── PlayerScreen.tsx      # Full player screen
│   │   └── QueueScreen.tsx       # Queue management screen
│   │   └── FavoriteesScreen.tsx
│   │   └── PlaylistsScreen.tsx
│   │   └── SearchScreen.tsx
│   │   └── SettingScreen.tsx
│   ├── store/
│   │   ├── musicStore.ts         # Music state management
│   │   ├── playerStore.ts        # Player state management
│   │   └── queueStore.ts         # Queue state management
│   │   └── themeStore.ts
│   ├── services/
│   │   └── audioService.ts       # Audio playback service
│   ├── types/
│   │   └── index.ts              # TypeScript type definitions
│   │   └── expo.d.ts
│   │   └── declaration.d.ts
│   └── utils/
│       ├── formatTime.ts         # Time formatting utilities
│       └── storage.ts            # MMKV storage utilities
├── App.tsx                        # Main app entry point
├── app.json                       # Expo configuration
├── .gitignore
├── index.ts
├── babel.config.js
├── package-lock.js
├── package.json                   # Dependencies
└── tsconfig.json                  # TypeScript configuration
└── README.md
```

## 🏗️ Architecture

### State Management

The app uses **Zustand** for state management with three separate stores:

1. **playerStore** - Manages current song, playback state, position, duration
2. **queueStore** - Manages song queue, current index, shuffle/repeat modes
3. **musicStore** - Manages search results, favorites, recently played

### Audio Service

The `audioService` is a singleton that handles all audio operations:
- Loading and playing songs
- Play/pause/seek controls
- Next/previous track navigation
- Background playback configuration
- Status updates and callbacks

### Persistent Storage

Uses **MMKV** for fast, synchronous storage:
- Queue persistence across app restarts
- Current playback position
- User preferences

### Navigation Flow

```
Home Screen (Search & Browse)
    ↓ (Tap song)
Mini Player (Bottom bar - always visible)
    ↓ (Tap mini player)
Full Player Screen (Complete controls)
    ↓ (Open queue)
Queue Screen (Manage playlist)
```

## 🎯 Key Features Implementation

### Background Playback

Configured in `audioService.ts` with:
```typescript
await Audio.setAudioModeAsync({
  staysActiveInBackground: true,
  playsInSilentModeIOS: true,
  shouldDuckAndroid: true,
});
```

### Queue Synchronization

Queue state is synced between:
- Mini player
- Full player
- Queue screen
- Persistent storage (MMKV)

All changes propagate instantly through Zustand store.

### Shuffle Algorithm

Uses Fisher-Yates shuffle while keeping current song at position 0:
```typescript
const currentSong = queue[currentIndex];
const otherSongs = queue.filter((_, i) => i !== currentIndex);
// Shuffle otherSongs...
const shuffledQueue = [currentSong, ...otherSongs];
```

## 🔧 Configuration

### API Configuration

The JioSaavn API base URL is configured in `src/api/saavn.ts`:
```typescript
const BASE_URL = 'https://saavn.sumit.co';
```

No API key required!


## 🚀 Performance Optimizations

1. **Image Caching** - Uses React Native's built-in image caching
2. **List Optimization** - FlatList with proper key extraction and item layout
3. **State Updates** - Zustand provides minimal re-renders
4. **MMKV Storage** - Faster than AsyncStorage for persistence

## 🔮 Future Enhancements

- [ ] Download songs for offline playback
- [ ] Create and manage playlists
- [ ] Lyrics display
- [ ] Sleep timer
- [ ] Equalizer
- [ ] Social sharing
- [ ] Artist pages
- [ ] Album views
- [ ] Search history
- [ ] Dark/Light theme toggle


Built by Pratibha Sikheriya ❤️ 
