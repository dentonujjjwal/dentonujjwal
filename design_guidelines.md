# Mobile Data Sharing System - Design Guidelines

## Architecture

### Authentication
- **Methods**: Phone + OTP (primary), Email/Password, Apple Sign-In (iOS), Google Sign-In (Android)
- **Login/Signup**: Include privacy policy, terms links, encryption explanation
- **Account Features**: Profile with avatar, verified phone badge, security settings, logout (with confirmation), delete account (Settings > Account > Delete with double confirmation)
- **Prototype**: Mock auth with local state

### Navigation
**Bottom Tabs (5)**:
1. **Home**: Dashboard with balance/quick actions
2. **Transfer**: Core action (centered, emphasized icon)
3. **Contacts**: Manage sharing contacts
4. **Emergency**: Emergency contacts & quick send
5. **Profile**: Account, settings, history

**Flows**: Linear onboarding (stack), primary features (tabs), forms (modals), critical actions (full-screen overlays)

## Screens

### 1. Onboarding (Stack)
Welcome → Phone Verify → Set Daily Limit → Add Contact → Complete
- Transparent header, skip button (top-right)
- Centered content with illustrations
- Primary CTA (bottom: insets.bottom + 32px)
- Progress indicator top
- **Safe Area**: Top: insets.top + 24px, Bottom: insets.bottom + 32px

### 2. Home (Tab)
- Transparent header: logo (center), bell icon (right)
- Pull-to-refresh scrollable content
- **Hero Card**: Balance with circular progress, gradient background (primary→secondary 135deg), daily limit
- **Quick Actions**: Send/Request Data buttons
- **Recent Transfers**: Last 5 items
- **Usage Chart**: Mini statistics
- **Floating Emergency Button**: Bottom-right (right: 16px, bottom: tabBarHeight + 16px), shadow: {0, 2, 0.10, 2}
- **Safe Area**: Top: headerHeight + 24px, Bottom: tabBarHeight + 24px

### 3. Transfer (Tab)
- Header: "Transfer Data", cancel (left)
- Scrollable form, sticky submit button
- **Fields**: Contact selector (searchable), amount input (MB) + presets (100/500/1000MB), balance indicator, note (optional, encrypted), encryption badge
- **Validation**: Min 10MB, real-time balance check, visual error feedback
- **Success**: Modal with confetti → transfer details
- **Safe Area**: Top/Bottom: 24px, Bottom + insets.bottom

### 4. Contacts (Tab)
- Header: "Contacts", add (right), search bar
- **Cards**: Avatar (initials fallback), name, phone, last transfer date
- **Swipe**: Edit/Delete actions
- **Sections**: "Recent", "All Contacts"
- **Empty State**: "No contacts yet" + CTA
- **Safe Area**: Top: headerHeight + 24px, Bottom: tabBarHeight + 24px

### 5. Emergency (Tab)
- Header: "Emergency", info (right)
- **Emergency Panel**: Large "Send Emergency Data" button, warning icon
- **Priority Sections**: 1 (Primary/auto-notify), 2 (Secondary), 3 (Tertiary)
- **Max**: 5 contacts total
- **Action**: Double-tap → full-screen countdown (3-2-1) → execute
- **Safe Area**: Top: 24px, Bottom: tabBarHeight + 24px

### 6. Profile (Tab)
- Transparent header: "Profile"
- **Profile Header**: Editable avatar, display name, verified phone
- **Settings**: Daily limit (slider + input), Security (encryption, 2FA toggle), Notifications, Theme (light/dark/auto)
- **Actions**: Transfer History, Privacy Policy, Terms, Log Out, Delete Account
- **Safe Area**: Top: headerHeight + 24px, Bottom: tabBarHeight + 24px

### 7. Transfer History (Modal)
- Header: "Transfer History", close (right)
- **Filters**: All/Sent/Received chips, date range
- **Cards**: Contact avatar, amount (MB), status badge (completed/pending/failed), timestamp, encryption indicator
- Pull-to-refresh, tap for details
- **Safe Area**: Top: 24px, Bottom: insets.bottom + 24px

## Design System

### Colors
**Primary**: #2563EB (blue), Dark: #1E40AF, Light: #60A5FA  
**Secondary**: #7C3AED (purple), Dark: #5B21B6, Light: #A78BFA  
**Semantic**: Success #10B981, Warning #F59E0B, Error #EF4444, Info #3B82F6  
**Light Mode**: BG #FFFFFF, Surface #F8FAFC, Border #E2E8F0, Text #0F172A/#64748B/#94A3B8  
**Dark Mode**: BG #0F172A, Surface #1E293B, Border #334155, Text #F8FAFC/#94A3B8/#64748B

### Typography (System: SF iOS / Roboto Android)
- H1: 32px Bold -0.5ls | H2: 24px Bold -0.3ls | H3: 20px Semibold -0.2ls
- Body Lg: 17px -0.1ls | Body: 15px | Body Sm: 13px
- Caption: 11px Medium 0.3ls | Button: 15px Semibold 0.5ls (uppercase primary)

### Spacing
xs: 4px, sm: 8px, md: 12px, lg: 16px, xl: 24px, xxl: 32px, xxxl: 48px

### Components

**Cards**:
- Border radius: 12px (standard), 16px (prominent)
- Balance: gradient background
- Contact/Log: surface color, 1px border
- Modal elevation: shadow {0, 4, 0.15, 8}

**Buttons** (48px min height):
- Primary: solid fill, white text, 12px radius | States: default, pressed (90% opacity), disabled (50%)
- Secondary: outlined, primary border/text, 12px radius
- Tertiary: text only, primary color
- FAB: circular, primary, white icon, shadow {0, 2, 0.10, 2}

**Icons** (Feather @expo/vector-icons):
- Size: 16px (inline), 20px (standard), 24px (tab bar)
- Emergency: AlertCircle/Triangle | Transfer: Send | Contact: Users | Profile: User | Home: Home | Add: Plus | Success: CheckCircle | Error: XCircle

**Inputs** (48px height):
- Border: 1px, 8px radius
- Focus: 2px primary border
- Error: 1px error border + text below
- Placeholder: text tertiary

**Interactions**:
- Touch target: 44x44px (iOS), 48x48px (Android)
- Press opacity: 0.7
- Haptics: light (success), notification error (errors)
- Transitions: 300ms slide
- Modals: slide up + backdrop fade
- List stagger: 50ms on mount
- Balance ring: animated progress
- Emergency countdown: bold scale animation
- Success: modal + confetti
- Swipe: left (iOS edit/delete), long-press (Android)

### Accessibility
- Contrast: WCAG AA (4.5:1 text, 3:1 UI)
- Dynamic Type support
- Screen reader labels on all interactive elements
- Semantic roles/aria-labels
- Focus indicators for keyboard nav
- Descriptive error messages

### Assets
1. **App Icon**: Circular data transfer symbol, primary blue
2. **Balance Ring**: Custom SVG animated progress
3. **Empty States**: No contacts (people connecting), no transfers (exchange), no emergency (shield+person)
4. **Avatars**: 8 preset geometric patterns (modern, abstract) using primary/secondary/complementary colors
5. **Onboarding**: 3 illustrations (security/encryption, contact/sharing, emergency feature)