# AIspace — Project TODO

## Infrastructure & Setup
- [x] Update theme.config.js with AIspace color palette
- [x] Create src/constants/theme.ts with COLORS object
- [x] Create src/constants/projectTypes.ts with project type definitions
- [x] Create src/constants/skills.ts with DEFAULT_SKILLS array
- [x] Create src/types/index.ts with all TypeScript interfaces
- [x] Create firebase.config.ts placeholder with comments
- [x] Create src/store/authStore.ts (Zustand)
- [x] Create src/store/projectStore.ts (Zustand)
- [x] Create src/store/settingsStore.ts (Zustand)

## UI Components
- [x] Create src/components/GhostMascot.tsx with pixel art SVG
- [x] Create src/components/PixelButton.tsx with hard shadows
- [x] Create src/components/PixelCard.tsx with corner cuts
- [x] Create src/components/PixelInput.tsx with styling
- [x] Create src/components/PixelBadge.tsx
- [x] Create src/components/PixelToggle.tsx
- [x] Create src/components/ProjectCard.tsx
- [x] Create src/components/SkillCard.tsx
- [x] Create src/components/SkillLibrarySheet.tsx with bottom sheet

## Services & Hooks
- [x] Create src/services/auth.service.ts (Firebase Auth)
- [x] Create src/services/projects.service.ts (Firestore)
- [x] Create src/services/messages.service.ts (Firestore)
- [x] Create src/services/skills.service.ts (Firestore)
- [x] Create src/services/gemini.service.ts (Gemini API)
- [x] Create src/services/ai.service.ts (Ollama + Gemini fallback)
- [x] Create src/hooks/useAuth.ts
- [x] Create src/hooks/useProjects.ts
- [x] Create src/hooks/useMessages.ts
- [x] Create src/hooks/useSkills.ts
- [x] Create src/utils/buildSystemPrompt.ts
- [x] Create src/utils/formatDate.ts

## Navigation
- [x] Create src/navigation/RootNavigator.tsx
- [x] Create src/App.tsx entry point with gesture handler and bottom sheet provider
- [x] Update app/(tabs)/index.tsx to use App.tsx

## Screens — Authentication
- [x] Create src/screens/SplashScreen.tsx with ghost animation
- [x] Create src/screens/LoginScreen.tsx with email/password form
- [x] Create src/screens/SignUpScreen.tsx with registration form

## Screens — Main App
- [x] Create src/screens/DashboardScreen.tsx with quick stats
- [x] Create src/screens/ProjectsListScreen.tsx with filtering and FAB
- [x] Create src/screens/NewProjectScreen.tsx as modal
- [x] Create src/screens/ProjectDetailScreen.tsx
- [x] Create src/screens/ChatScreen.tsx with custom message UI
- [x] Create src/screens/ProfileScreen.tsx with settings

## Integration & Polish
- [x] Wire up Firebase Auth to auth screens
- [x] Wire up Firestore projects collection
- [x] Wire up Firestore messages collection
- [x] Wire up Firestore skills collection
- [x] Implement AI message sending (Ollama + Gemini fallback)
- [x] Implement first message auto-send on ChatScreen load
- [x] Implement skill toggling and system prompt injection
- [x] Implement pull-to-refresh on ProjectsList
- [ ] Test all user flows end-to-end
- [x] Generate app logo and update branding
- [ ] Create checkpoint before delivery

## Known Constraints
- Firebase credentials must be filled in by user in firebase.config.ts
- Gemini API key stored in expo-secure-store (optional, but recommended)
- Ollama local server URL configurable in Profile screen
- All text must be UPPERCASE
- All fonts must be Press Start 2P
- All shadows must be hard pixel shadows (shadowRadius: 0)
- All border-radius must be zero (use clip-path for corners)
- Ghost mascot must appear on every screen
