# AIspace Mobile App — Interface Design

## Design Philosophy

**Retro 8-bit Pixel Art Terminal Aesthetic**

The entire visual identity is inspired by classic arcade and early computing terminals. Every element uses hard pixel shadows, zero border-radius (clip-path only), Press Start 2P font, and a dark space terminal color palette. The purple pixel ghost mascot serves as the app's personality and appears meaningfully on every screen.

---

## Screen List

1. **Splash Screen** — App launch with animated ghost mascot
2. **Login Screen** — Email/password authentication
3. **SignUp Screen** — New user registration
4. **Dashboard Screen** — Home screen with user greeting and quick stats
5. **Projects List Screen** — Browse all user projects with filtering
6. **New Project Screen** — Modal to create a new project
7. **Project Detail Screen** — View project metadata and manage skills
8. **Chat Screen** — Core AI chat interface for project planning
9. **Profile Screen** — User settings, AI engine config, API keys
10. **Skill Library Sheet** — Bottom sheet to toggle AI behavior modules

---

## Primary Content and Functionality

### Splash Screen
- **Content**: Centered large ghost mascot (size=96), app title "AISPACE" in Press Start 2P
- **Functionality**: Auto-navigate to Login or Dashboard based on auth state
- **Animation**: Ghost floats up/down using `react-native-reanimated` with `steps()` easing

### Login Screen
- **Content**: 
  - Ghost mascot (size=64) above form
  - Email input field
  - Password input field
  - "LOGIN" button
  - "NO ACCOUNT? SIGN UP" link
- **Functionality**: Email/password Firebase Auth, error handling, navigation to Dashboard on success

### SignUp Screen
- **Content**:
  - Ghost mascot (size=64)
  - Display name input
  - Email input
  - Password input (with strength indicator)
  - "CREATE ACCOUNT" button
  - "ALREADY HAVE ACCOUNT? LOGIN" link
- **Functionality**: Create Firebase Auth user, save to Firestore users collection, seed skills on first signup

### Dashboard Screen
- **Content**:
  - Header: "WELCOME, [NAME]" in cyan
  - Ghost mascot (size=80) centered with purple glow
  - Quick stats: "N PROJECTS" | "N MESSAGES" | "N SKILLS"
  - "► START NEW PROJECT" button
  - "► VIEW ALL PROJECTS" button
  - Recent projects list (3 items)
- **Functionality**: Show user greeting, display quick navigation, load recent projects

### Projects List Screen
- **Content**:
  - Header: "MY PROJECTS" + "[N] ACTIVE" in cyan
  - Horizontal filter chips: [ALL] [CODING] [DESIGN] [RESEARCH] [PRODUCTIVITY] [MARKETING] [EDUCATION] [OTHER]
  - Vertical list of project cards (type-colored with hard shadow)
  - Each card: type badge, title, description (2 lines), active skill dots, arrow
  - Swipe-left delete action (red ✕)
  - FAB (floating action button) bottom-right: pixel ++ button
  - Pull-to-refresh
  - Empty state: Ghost (size=80) + "NO PROJECTS FOUND"
- **Functionality**: Filter projects by type, create new project, delete project, navigate to detail/chat

### New Project Screen
- **Content**:
  - Modal header: "■ NEW PROJECT ■" + close button
  - Project title input
  - Project type selector (horizontal scroll of type chips)
  - Description input (multiline, 5 lines min)
  - Character counter: "░░░ 0 / 500 ░░░"
  - "► CREATE & LAUNCH AI CHAT" button
  - Bottom decoration: row of pixel blocks
- **Functionality**: Validate inputs, save to Firestore projects collection, navigate to ChatScreen

### Project Detail Screen
- **Content**:
  - Header: back arrow | "PROJECT DETAIL" | edit icon
  - Type-colored pixel card with project info
  - Type badge + date
  - Title (12px white)
  - Description (8px muted)
  - Divider row
  - Stats: CREATED | MESSAGES | SKILLS (all cyan)
  - Active skills section with skill chips
  - Ghost mascot (size=48) floats in top-right corner
  - "► OPEN AI CHAT" button (primary)
  - "□ MANAGE SKILLS" button (secondary)
  - "✕ DELETE PROJECT" link (red)
- **Functionality**: Display project details, manage skills, navigate to chat or skill library

### Chat Screen (Core Feature)
- **Content**:
  - Header: back arrow | project title (truncated) | ghost icon + "AISPACE" | settings icon
  - AI status pill: "● GEMMA2 LOCAL" (green) OR "● GEMINI CLOUD" (cyan)
  - Chat area using react-native-gifted-chat
    - AI bubble: ghost avatar (size=40), name "◄ AISPACE", dark bg, cyan border, hard shadow
    - User bubble: "YOU ►" label, purple bg, hard shadow
    - Typing indicator: ghost (size=32) + blinking blocks + "AISPACE IS THINKING..."
  - Input bar: skill count badge | text input | send button
  - Markdown rendering for AI responses
- **Functionality**: Send/receive messages, auto-send first message on load, stream AI responses, render markdown

### Profile Screen
- **Content**:
  - Header: "■ PROFILE ■"
  - Avatar: Ghost (size=80) with purple glow
  - Display name (10px white)
  - Email (7px muted)
  - "░ AI ENGINE ░" card:
    - Ollama server URL input
    - AI model input (default: gemma2)
    - "► TEST CONNECTION" button
    - Status: "● ONLINE / GEMMA2 READY" or "✕ OFFLINE"
  - "░ CLOUD FALLBACK ░" card:
    - Gemini API key input (password type, stored in expo-secure-store)
  - "░ APP SETTINGS ░" card:
    - "► CLEAR ALL CHATS" button (danger)
  - "✕ LOGOUT" button (full-width danger)
- **Functionality**: Edit Ollama URL and model, test connection, store Gemini API key, clear chats, logout

### Skill Library Sheet
- **Content**:
  - Bottom sheet (70% screen height)
  - Drag handle: ■ ■ ■
  - Header: Ghost (size=32) + "░░ SKILL LIBRARY ░░" | "[N] SKILLS ACTIVE" in cyan
  - Search input: "► SEARCH SKILLS..."
  - Category tabs (horizontal scroll): [ALL] [PLANNING] [DEVELOPMENT] [DESIGN] [RESEARCH] [WRITING]
  - 2-column skill card grid
    - Active card: green border, green shadow, "ACTIVE" badge
    - Inactive card: gray border, gray shadow
    - Each card: icon + skill name (7px) + description (6px, 2 lines) + ON/OFF toggle
- **Functionality**: Search skills, filter by category, toggle skill active state, update Firestore activeSkills array

---

## Key User Flows

### Flow 1: New User Onboarding
1. User launches app → Splash Screen
2. Splash detects no auth → Login Screen
3. User taps "NO ACCOUNT? SIGN UP" → SignUp Screen
4. User fills form, taps "CREATE ACCOUNT"
5. App creates Firebase Auth user, saves to Firestore, seeds DEFAULT_SKILLS
6. Auto-navigate to Dashboard

### Flow 2: Create Project & Chat
1. User on Dashboard taps "► START NEW PROJECT"
2. NewProjectScreen modal slides up
3. User fills title, selects type, writes description
4. User taps "► CREATE & LAUNCH AI CHAT"
5. Project saved to Firestore, navigate to ChatScreen
6. ChatScreen loads, auto-sends first AI message (project analysis)
7. User can now chat with AI about their project

### Flow 3: Manage Skills
1. User on ChatScreen taps skill badge or navigates to ProjectDetail
2. User taps "□ MANAGE SKILLS"
3. SkillLibrarySheet slides up
4. User searches/filters skills, toggles ON/OFF
5. Each toggle updates Firestore activeSkills array
6. AI system prompt is rebuilt with active skills on next message

### Flow 4: Configure AI Engine
1. User on Dashboard taps profile icon
2. Navigate to ProfileScreen
3. User enters Ollama server URL (default: http://localhost:11434)
4. User enters preferred model name (default: gemma2)
5. User taps "► TEST CONNECTION"
6. App attempts Ollama connection, shows status
7. If offline, user can add Gemini API key as fallback
8. Settings saved to Firestore users collection

---

## Color Choices

### Primary Palette (from spec)
- **Background**: `#0A0A0F` (deep space black)
- **Surface**: `#13131A` (elevated dark)
- **Surface Elevated**: `#1C1C2E` (card/modal)
- **Border**: `#2A2A4A` (subtle dividers)
- **Primary**: `#6C63FF` (main accent purple)
- **Primary Bright**: `#8B83FF` (highlights)
- **Primary Dark**: `#4A42CC` (shadows)
- **Accent Cyan**: `#00F5FF` (labels, status)
- **Accent Green**: `#00FF88` (active states)
- **Accent Yellow**: `#FFE500` (warnings)
- **Accent Red**: `#FF3B3B` (errors, delete)
- **Accent Pink**: `#FF6AC1` (secondary accent)
- **Text Primary**: `#E8E8FF` (main text)
- **Text Secondary**: `#7777AA` (muted text)
- **Text Muted**: `#44446A` (very muted)
- **Text Accent**: `#00F5FF` (cyan text)

### Project Type Colors
- **Coding**: bg=`#3B82F6`, shadow=`#1D4ED8`
- **Design**: bg=`#FF6AC1`, shadow=`#BE185D`
- **Research**: bg=`#A78BFA`, shadow=`#7C3AED`
- **Productivity**: bg=`#00FF88`, shadow=`#059669`
- **Marketing**: bg=`#FF9500`, shadow=`#C2410C`
- **Education**: bg=`#10B981`, shadow=`#065F46`
- **Other**: bg=`#6C63FF`, shadow=`#4A42CC`

### Ghost Mascot
- **Primary Purple**: `#8B5FA2` (main body)
- **Dark Purple**: `#442859` (outlines)
- **Light Purple**: `#8D62A0` (highlights)

---

## Typography

- **Font**: Press Start 2P (loaded via `@expo-google-fonts/press-start-2p`)
- **All text**: UPPERCASE (enforced in code)
- **Sizes**:
  - Hero/Title: 12px
  - Header/Label: 9px
  - Body/Input: 8px
  - Small/Muted: 7px
  - Tiny: 6px

---

## Visual Elements

### Hard Pixel Shadows
- All shadows use `shadowRadius: 0` (no blur)
- Shadow offset: typically `shadowOffset: { width: 2, height: 2 }`
- On Android: use `borderRightWidth` + `borderBottomWidth` instead of `elevation`

### Zero Border-Radius
- No `borderRadius` property anywhere
- Use `View` overlays with `overflow: 'hidden'` for corner cuts if needed
- Prefer hard rectangular corners

### Ghost Mascot Sizing
- **Tiny**: 24px (badges, list items)
- **Small**: 40px (chat avatars, card corners)
- **Medium**: 64px (form screens)
- **Large**: 80-96px (dashboard hero, empty states)
- **Giant**: 120px (splash screen)

### Animations
- All animations use `steps()` easing (never `linear`, `ease`, `cubic-bezier`)
- Duration: 80-300ms for interactions, up to 800ms for floats
- Ghost float: `-10px` vertical movement over 800ms with 4 steps
- Blinking cursor: 500ms cycle with 1 step
- Press feedback: scale to 0.97 over 80ms

---

## Interaction Patterns

### Buttons
- Primary: Full-width, purple bg, hard shadow, scale 0.97 on press
- Secondary: Outline style, cyan border, scale 0.95 on press
- Danger: Red bg/text, hard shadow, scale 0.97 on press

### Cards
- Type-colored bg, hard shadow (color-based), cyan border on hover/focus
- Swipe-left to reveal delete action (red)

### Inputs
- Dark bg, cyan border, hard shadow
- Placeholder: muted text
- Focus: cyan glow effect (via border color change)
- Keyboard avoidance: `KeyboardAvoidingView` on all forms

### Lists
- Use `FlatList` for performance
- Pull-to-refresh on main lists
- Skeleton loaders while fetching

---

## Responsive Design

- **Portrait orientation only** (9:16 aspect ratio)
- **One-handed usage**: All interactive elements within thumb reach
- **Safe area**: Use `ScreenContainer` to handle notches and home indicators
- **Tab bar**: Always visible at bottom, 56px height + safe area inset

---

## Accessibility

- All text elements have sufficient contrast (cyan on dark, white on dark)
- Buttons have minimum 44x44pt touch target
- Ghost mascot serves as visual anchor on every screen
- Error messages display in red with clear language
- Loading states show spinner + "LOADING..." text

---

## Empty States

- Ghost mascot (size=80-120)
- Centered message: "NO PROJECTS FOUND" or "NO MESSAGES YET"
- Optional action button: "► CREATE PROJECT" or similar
- Muted text explaining what to do next
