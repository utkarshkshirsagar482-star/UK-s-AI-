# Design Guidelines: Web-Based MCP Host Application

## Design Approach

**Selected Approach**: Design System Approach (Developer-Focused)

**Justification**: This is a utility-focused developer productivity tool requiring efficiency, clarity, and functional excellence. The application is information-dense with complex components (API management, chat interface, JSON editing) where performance and usability are paramount.

**Primary References**: Drawing from Linear's clean developer-focused UI, GitHub's dashboard patterns, and VS Code's information hierarchy. These exemplify how to create functional interfaces that developers trust and enjoy using.

**Key Design Principles**:
1. **Clarity First**: Every element serves a clear purpose - no decorative clutter
2. **Scannable Hierarchy**: Developers need to quickly locate and access tools
3. **Progressive Disclosure**: Advanced features accessible but not overwhelming
4. **Responsive Precision**: Works seamlessly from laptop to ultrawide monitors

---

## Core Design Elements

### A. Typography System

**Font Families**:
- **Primary (Interface)**: Inter or System UI stack for clean readability
- **Monospace (Code/JSON)**: 'Fira Code', 'JetBrains Mono', or monospace for JSON editor and API keys

**Type Scale**:
- **Page Titles**: text-2xl font-semibold (24px)
- **Section Headers**: text-lg font-semibold (18px)
- **Body Text**: text-base (16px) - regular weight
- **Labels/Captions**: text-sm (14px) - medium weight
- **Code/JSON**: text-sm monospace

**Hierarchy Guidelines**:
- Use font-weight variations (medium vs semibold) for hierarchy within same size
- Maintain 1.5 line-height for body text, 1.2 for headings
- Code blocks use 1.6 line-height for better readability

---

### B. Layout System

**Spacing Primitives**: Using Tailwind units of **2, 4, 6, and 8** for consistency
- **Micro spacing** (within components): p-2, gap-2
- **Component spacing** (between elements): p-4, gap-4, mb-4
- **Section spacing** (major divisions): p-6, mb-6
- **Page margins**: p-8, container spacing

**Grid Structure**:
- **Application Shell**: Two-column layout with fixed sidebar (280px) and fluid main content
- **Main Content**: Single column with max-w-7xl container
- **Chat Interface**: Flexible height with fixed input at bottom
- **Responsive Breakpoints**: Collapse sidebar to hamburger menu on tablet/mobile

**Container Strategy**:
```
Desktop: Sidebar (280px fixed) + Main (fluid with max-w-7xl)
Tablet: Overlay sidebar + Main (full width with px-6)
Mobile: Overlay sidebar + Main (full width with px-4)
```

---

### C. Component Library

### Navigation & Shell Components

**Sidebar Navigation** (280px fixed width):
- Logo/branding at top (h-16)
- Navigation items with icons and labels
- Active state indicator (border accent on left)
- API key status indicator at bottom
- Spacing: py-2 for nav items, px-4 container padding

**Top Bar** (if used):
- Height: h-14
- Contains: Breadcrumb/title on left, actions on right
- Padding: px-8

### Core Functional Components

**API Key Management Panel**:
- Card-based layout with border
- Input field with "Add API Key" button inline
- List of saved keys with:
  - Masked display (e.g., "sk-...xyz123")
  - Label/name field
  - "Test Connection" button
  - Delete action (icon button)
- Spacing: p-6 for card padding, gap-4 between list items

**Chat Window**:
- **Message Container**: Flex column with gap-4 between messages
- **User Messages**: Aligned right, max-w-2xl, rounded-2xl, px-4 py-3
- **AI Responses**: Aligned left, max-w-3xl, rounded-2xl, px-4 py-3
- **Input Area**: Fixed at bottom with:
  - Multiline textarea (min-h-20, max-h-40)
  - Send button (icon button, positioned absolute right)
  - Container padding: p-4
- **Scroll Behavior**: Auto-scroll to bottom on new messages

**MCP Server Configuration**:
- **JSON Editor Area**:
  - Full-width code editor with syntax highlighting
  - Monospace font (text-sm)
  - Line numbers on left (w-12)
  - Min height: min-h-96
  - Border with rounded corners (rounded-lg)
- **Upload Section**:
  - Drag-and-drop zone (border-2 border-dashed)
  - Height: h-32
  - "Browse files" button centered
  - File name display when loaded
- **Action Bar**:
  - Save, Validate, Reset buttons
  - Right-aligned
  - Gap-2 between buttons

### Form Elements

**Input Fields**:
- Height: h-10
- Padding: px-3
- Border radius: rounded-md
- Focus state: ring-2 offset treatment
- Labels: text-sm font-medium, mb-2

**Buttons**:
- **Primary**: h-10, px-6, rounded-md, font-medium
- **Secondary**: Same sizing, different treatment
- **Icon Buttons**: w-10 h-10, rounded-md, centered icon
- **Disabled State**: Reduced opacity (opacity-50)

**Dropdowns/Selects**:
- Height: h-10
- Full width by default
- Chevron icon on right
- Padding: pl-3 pr-10

### Data Display Components

**Connection Status Indicator**:
- Small badge component (h-6, px-2, rounded-full)
- Includes dot indicator and status text
- Positioned in API key list items

**Server List**:
- Card-based items with:
  - Server name (text-base font-medium)
  - Status badge
  - Connection details (text-sm)
  - Action buttons (icon buttons)
- Gap-3 between list items

**Code Block** (for displaying JSON/responses):
- Pre-formatted text with monospace font
- Overflow-x auto for horizontal scrolling
- Padding: p-4
- Border radius: rounded-lg
- Max height with scrolling for long content

---

### D. Layout Compositions

**Main Application Layout**:
```
├── Sidebar (280px fixed, full height)
│   ├── Logo/Brand (h-16, px-4)
│   ├── Navigation Items (py-2, px-4 each)
│   └── API Status Footer (px-4, pb-6)
│
└── Main Content Area (flex-1)
    ├── Tab Navigation (h-12, border-bottom)
    │   └── Tabs: Chat | MCP Servers | API Keys | Settings
    │
    └── Content Panel (p-8)
        └── Tab-specific content
```

**Chat Tab Layout**:
```
├── Header (mb-6)
│   └── Model selector dropdown + Settings icon
│
├── Messages Container (flex-1, overflow-auto)
│   └── Message list with gap-4
│
└── Input Area (fixed bottom, p-4)
    └── Textarea + Send button
```

**MCP Servers Tab**:
```
├── Header Row (flex justify-between, mb-6)
│   ├── "MCP Servers" title
│   └── "Add Server" button
│
├── Two Column Layout (grid grid-cols-2 gap-6)
│   ├── Server List (left column)
│   │   └── Server cards with status
│   │
│   └── Configuration Panel (right column)
│       ├── JSON Editor
│       ├── Upload Area
│       └── Action Buttons
```

**API Keys Tab**:
```
├── Add Key Section (mb-8)
│   └── Input + Add button inline
│
└── Keys List
    └── Card for each key (p-4, gap-4)
        ├── Masked key display
        ├── Label field
        └── Actions (Test, Delete)
```

---

### E. Interaction Patterns

**Animations**: Minimal, functional only
- Sidebar toggle: 200ms ease transition
- Tab switching: Fade transition (150ms)
- Button hover states: No animation, instant state change
- Message appearance: Subtle fade-in (100ms)

**Micro-interactions**:
- Input focus: Ring appears instantly
- Button clicks: Slight opacity shift (no animation)
- Dropdown open: Instant appearance with slight offset
- Toast notifications: Slide in from top-right

---

## Accessibility Standards

- **Focus Management**: Visible focus rings on all interactive elements (ring-2)
- **Keyboard Navigation**: Tab order follows logical flow, Escape closes modals
- **Form Labels**: All inputs have associated labels (even if visually hidden)
- **ARIA Attributes**: Proper roles for chat messages, status indicators, and dynamic content
- **Color Independence**: Never rely solely on color for status (use icons + text)
- **Text Contrast**: Maintain WCAG AA standards for all text
- **Screen Reader**: Announce chat messages, connection status changes

---

## Critical Implementation Notes

1. **No Hero Sections**: This is a functional application, not a marketing site
2. **Fixed Layouts**: Sidebar and input areas remain fixed during scroll
3. **Monospace Consistency**: All code/JSON must use same monospace font
4. **Real-time Updates**: Design accommodates live status updates without layout shift
5. **Error States**: Clear error messaging inline with forms and actions
6. **Empty States**: Thoughtful designs for empty chat, no servers, no API keys
7. **Loading States**: Skeleton screens for async operations, spinners for actions

This design prioritizes developer efficiency while maintaining a modern, professional aesthetic suitable for a production development tool.