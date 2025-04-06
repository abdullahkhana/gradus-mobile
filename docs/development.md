# Gradus App: In-Depth Development Plan

## Guiding Principles:
*   Iterative Development
*   Component-Based (Well-Designed)
*   Clear State Management (Zustand)
*   Backend Logic (Supabase)
*   **Design Excellence (Using Provided Custom Theme)**
*   Content is King (and Hard)

---

## Phase 0: Project Setup & Foundation (Estimated Duration: 1 Week)

### Step 0.1: Version Control Setup (DONE)
*   Create Git repo, establish branching strategy.
    *   *(AI Note: Provide instructions/reminders).*

### Step 0.2: Expo Project Initialization  (DONE)
*   `npx create-expo-app@latest gradus-app --template blank-ts`
*   `cd gradus-app`
*   `npx expo install expo-router ...`
*   Configure `app.json`.
    *   *(AI Note: Provide modifications).*

### Step 0.3: Core Dependency Installation
*   `npm install @supabase/supabase-js`
*   `npm install zustand`
*   **Install UI Library: Tamagui**
    *   *(AI Note: Confirm user wants Tamagui. Guide through Tamagui Expo setup instructions from its documentation. We will integrate the custom theme in Step 1.6).*
*   Install Utility Libraries: `npm install date-fns lodash zod`

### Step 0.4: Environment Setup
*   Create `.env`, add to `.gitignore`. Define Supabase vars.
    *   *(AI Note: Provide content/structure).*
*   Mention EAS Secrets.

### Step 0.5: Code Quality Tools
*   Install ESLint, Prettier, configs.
    *   *(AI Note: Suggest packages/configs).*
*   Configure pre-commit hooks (Husky, lint-staged).
    *   *(AI Note: Provide setup commands).*

### Step 0.6: Basic Project Structure Setup
*   Create folders: `app/`, `assets/` (fonts/, images/), `components/` (common/, layout/, auth/, papers/, scan/, feedback/, resources/), `constants/`, `contexts/`, `hooks/`, `services/` (api/, supabase/, ai/, ocr/, analysis/), `store/`, `types/`, `utils/`.
    *   *(AI Note: Provide `mkdir` commands).*

### Step 0.7: Supabase Project Setup
*   Create project, enable Auth, Storage, buckets, policies.
    *   *(AI Note: Instruct on Supabase dashboard actions. Remind about URL/Key).*

---

## Phase 1: Authentication & Core Navigation (Estimated Duration: 1-2 Weeks)

### Step 1.1: Root Layout & Auth State Management
*   Implement `app/_layout.tsx`. Initialize Supabase client (`services/supabase/client.ts`). Basic layout structure.
    *   *(AI Note: Provide `client.ts`. Provide initial `_layout.tsx` structure. Theme provider setup will be detailed in Step 1.6).*

### Step 1.2: Zustand User Store Setup
*   Create `store/userStore.ts`. Define state and actions.
    *   *(AI Note: Provide clean store structure).*

### Step 1.3: Authentication Service Logic
*   Implement `services/supabase/auth.ts` wrapping Supabase methods, interacting with `userStore`.
    *   *(AI Note: Provide functions with error handling).*

### Step 1.4: Authentication Screens UI & Logic
*   Create `app/(auth)/_layout.tsx` (Stack). Create screens (`sign-in.tsx`, `sign-up.tsx`).
*   **Design Focus (Using Tamagui Basics initially):** Implement initial UI using basic Tamagui components. Create reusable components (`InputFields.tsx`, `Button.tsx`, `AuthForm.tsx`). Use Zod. Connect UI to `userStore`. Handle navigation, basic loading/error states.
    *   *(AI Note: Provide code. Styling will be refined post-theme integration in Step 1.6. Focus on structure and logic here).*

### Step 1.5: Basic Tab Navigation Setup
*   Implement `app/(tabs)/_layout.tsx` (Tabs). Define tabs.
*   **Design Focus:** Configure basic tab icons (`TabBarIcon.tsx`) and labels.
*   Create placeholder screens.
    *   *(AI Note: Provide structure for layout and `TabBarIcon`. Styling using custom theme will come later).*

### Step 1.6: Integrate Custom Theme & Fonts
*   **1.6.1: Create `themes.ts`:** Create a file named `themes.ts` (e.g., at the project root or a `config/` directory).
    *   *(AI Note: Instruct the user to paste their provided custom theme definition content into this file. Wait for confirmation).*
*   **1.6.2: Update `tamagui.config.ts`:** Modify the existing `tamagui.config.ts` file.
    *   *(AI Note: Instruct the user to import `themes` from their new `./themes` file and spread it into the `createTamagui` config object, matching the structure they provided: `import { themes } from './themes'; ... createTamagui({ themes, ...defaultConfig })`. Provide the exact code modification snippet. Wait for confirmation).*
*   **1.6.3: Configure Theme Provider:** In `app/_layout.tsx`, ensure the `TamaguiProvider` component wraps the application content and is configured correctly using the `config` imported from `tamagui.config.ts`. Set a default theme (e.g., `defaultTheme="light"` or `defaultTheme="dark"`).
    *   *(AI Note: Provide the updated `app/_layout.tsx` code showing the `TamaguiProvider` wrapping the `Slot` or `Stack`, configured with the imported `config` and a default theme. Remind the user that all subsequent UI components will now use this theme).*
*   **1.6.4: Load Custom Fonts:** Implement font loading using `expo-font` (e.g., in `app/_layout.tsx` using `useFonts`). Ensure font keys match those potentially used in `tamagui.config.ts` if customized there.
    *   *(AI Note: Provide the standard `useFonts` hook implementation).*

---

## Phase 2 onwards:

*   *(AI Note: For all subsequent steps involving UI (Screens, Components), **strictly base all styling suggestions (colors, backgrounds, borders, shadows, status indicators) on the tokens and palettes defined in the user's `themes.ts` file** integrated in Step 1.6. Use Tamagui theme tokens like `$color.accent9`, `$background`, `$color.red9`, etc., extensively in code examples.)*



## Phase 2: Content Pipeline & Static Paper Display (Estimated Duration: 2-3 Weeks)

### Step 2.1: Finalize Supabase Database Schema
*   Create tables, relationships, RLS policies in Supabase dashboard.
    *   *(AI Note: Instruct user. Provide example SQL/RLS policies focusing on security).*
*   Generate TypeScript types: `npx supabase gen types typescript ... > src/types/supabase.ts`.
    *   *(AI Note: Remind user to run this).*

### Step 2.2: CRITICAL EXTERNAL TASK: Content Preprocessing Tool
*   *(AI Note: Acknowledge this external task).*

### Step 2.3: Populate Initial Content
*   *(AI Note: Remind user this is a prerequisite done via the tool/manually).*

### Step 2.4: API Service for Papers
*   Implement functions in `services/api/papers.ts` (fetch subjects, papers, questions, marking scheme points).
    *   *(AI Note: Provide clean query functions using Supabase client and generated types, include error handling).*

### Step 2.5: Paper Selection UI & Logic
*   Implement `app/(tabs)/papers/index.tsx`.
*   **Design Focus:** Create intuitive components like `SubjectSelector.tsx` (Dropdown/Tabs) and `PaperList.tsx` (Cleanly styled list items). Fetch and display data clearly. Implement filtering UI smoothly. Use loading indicators.
*   Navigate to `papers/[paperId]` on selection.
    *   *(AI Note: Suggest layout, provide component structures emphasizing clarity and usability. Show data fetching with loading states).*

### Step 2.6: View Paper Screen (Question List)
*   Implement `app/(tabs)/papers/[paperId].tsx`.
*   **Design Focus:** Fetch questions for `paperId`. Display the list clearly (e.g., Card per question, Accordion). Ensure easy navigation to each question's solve screen. Handle loading state.
    *   *(AI Note: Suggest layout for question list, provide code using UI library components).*

### Step 2.7: Basic Question Display Component
*   Develop `components/papers/QuestionDisplay.tsx`. Input: `question` object.
*   **Design Focus:** Render question text, marks clearly. Fetch and display diagram image from Supabase Storage using `expo-image` with good loading/error state handling (placeholders/shimmers). Ensure readability and appropriate spacing.
    *   *(AI Note: Provide component code focusing on visual presentation and robust image handling).*

---

## Phase 3: OCR Scanning & Standalone Feedback (Estimated Duration: 2-3 Weeks)

### Step 3.1: Scan Tab UI & Camera Integration
*   Implement UI for `app/(tabs)/scan.tsx`.
*   **Design Focus:** Integrate `expo-camera` (`components/scan/CameraView.tsx`) with clear instructions/UI overlays. Handle permissions gracefully (`hooks/useCameraPermission.ts`). Design intuitive capture button and gallery access button.
    *   *(AI Note: Provide permission hook, `CameraView` structure with user-friendly overlays/controls).*

### Step 3.2: Image Processing & Cropping
*   **Design Focus:** Implement user-friendly preview and cropping (`components/scan/ImageCropper.tsx` using `expo-image-manipulator`). Provide clear visual guides for cropping. Optimize image (`utils/imageProcessor.ts`).
    *   *(AI Note: Suggest library/structure for cropping UI, focusing on ease of use).*

### Step 3.3: OCR Service Implementation
*   Set up Google Cloud Vision API key securely. *(AI Note: Remind user)*.
*   Implement `services/ocr/googleVision.ts` (image -> base64 -> API -> text).
    *   *(AI Note: Provide service function structure).*

### Step 3.4: OCR Result Display & Handling
*   **Design Focus:** Display extracted text clearly (`components/scan/OcrResultDisplay.tsx`) in an editable format. Provide obvious "Edit" and "Submit" actions. Handle loading state during OCR.
*   (Optional) Design UI for linking scan to question (modal search/suggestions).

### Step 3.5: AI Service & Initial Evaluation Prompt
*   Set up Gemini API key securely. *(AI Note: Remind user)*.
*   Implement core Gemini call (`services/ai/gemini.ts`).
*   Define Prompt V1 (`services/ai/promptEngineering.ts`).
    *   *(AI Note: Provide service function and example prompt).*

### Step 3.6: Backend Evaluation Logic (Edge Function Recommended)
*   Create Supabase Edge Function (`evaluate-answer`). Input: text, `question_id`. Fetches marking scheme, calls AI per point, aggregates, saves results (`evaluation_results`, `user_answers`).
    *   *(AI Note: Guide on Edge Function setup. Recommend this approach. Provide structure).*

### Step 3.7: Feedback Display Implementation
*   **Design Focus:** Create visually clear feedback components (`components/feedback/FeedbackSummary.tsx`, `MarkingSchemePointFeedback.tsx`). Use colors (subtly, e.g., green for correct, red/amber for incorrect points), icons, and clear text hierarchy. Display in a modal (`app/modal.tsx`) or dedicated route. Use `feedbackStore` (Zustand).
    *   *(AI Note: Provide component structures emphasizing clarity and actionable insights for the user. Explain modal setup).*

---

*(Phases 4-7 follow the same pattern: AI provides step-by-step guidance, code snippets, and commands, always considering and suggesting good UI/UX design practices, consistency, and clarity, leveraging the chosen UI library and theme.)*

---

## Phase 4: "Solve on App" Feature & Integrated Feedback (...)

*   **Design Focus:** Ensure Solve screen (`papers/solve/[questionId].tsx`) is clean, `QuestionDisplay` is prominent, `AnswerInput` (`TextInput` initially) is easy to use. Integrate feedback display seamlessly post-submission.

---

## Phase 5: Analysis, Resources & Recommendations (...)

*   **Design Focus:** Display weak topics (`WeakTopicIndicator.tsx`) and recommendations clearly on Home screen. Design Resource Hub (`resources/...`) for easy browsing (`TopicBrowser.tsx`, `ResourceCard.tsx`) with clear resource types.

---

## Phase 6: Polishing, Testing & Beta Release (...)

*   **Design Focus:** Implement smooth loading states (skeletons), transitions (`react-native-reanimated`). Refine overall visual consistency and branding. Optimize performance. Conduct accessibility audit.

---

## Phase 7: Launch & Post-Launch Iteration (...)

*   *(AI Note: Focus shifts to build/submission commands, monitoring reminders, and iterating based on feedback).*

---

**Let's begin! Please provide the guidance and commands for Phase 0, Step 0.1.**