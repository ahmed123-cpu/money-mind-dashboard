# Multi-Language Support (English & Arabic) Setup

## Overview
MoneyMind now supports English and Arabic languages with automatic RTL (Right-to-Left) support for Arabic. The implementation uses `next-intl` for seamless multi-language routing and message management.

## Architecture

### URL Routing
- All routes are now prefixed with locale codes: `/en/*` and `/ar/*`
- The middleware automatically redirects to the user's preferred locale
- Language preference is stored in localStorage and URL path

### File Structure
```
├── messages/
│   ├── en.json          # English translations
│   └── ar.json          # Arabic translations
├── i18n/
│   └── request.ts       # i18n configuration
├── middleware.ts        # Locale routing middleware
├── app/
│   ├── layout.tsx       # Root layout (simple wrapper)
│   └── [locale]/
│       ├── layout.tsx   # Locale-specific layout with RTL support
│       ├── page.tsx     # Landing page
│       ├── auth/
│       │   ├── login/page.tsx
│       │   └── signup/page.tsx
│       └── dashboard/
│           ├── page.tsx
│           ├── expenses/page.tsx
│           ├── goals/page.tsx
│           ├── insights/page.tsx
│           └── settings/page.tsx
└── components/
    ├── language-switcher.tsx  # Language toggle component
    └── sidebar.tsx            # Updated with language switcher
```

## Key Components

### 1. Language Switcher (`components/language-switcher.tsx`)
- Located in the sidebar next to the theme toggle
- Allows users to switch between English and Arabic
- Automatically updates all UI text and applies RTL layout for Arabic

### 2. Locale Layout (`app/[locale]/layout.tsx`)
- Sets `dir="rtl"` attribute on HTML element for Arabic
- All client providers wrapped for each locale
- Automatic RTL/LTR layout switching

### 3. Middleware (`middleware.ts`)
- Handles locale detection and routing
- Supports browser language preferences
- Maintains locale in URL path

## Translation Keys Structure

Translations are organized by feature:
- `nav` - Navigation menu items
- `auth` - Login and signup page text
- `dashboard` - Dashboard page text
- `expenses` - Expenses page text
- `goals` - Goals page text
- `insights` - Insights page text
- `settings` - Settings page text
- `menu` - Menu and dropdown items
- `common` - Common UI elements

## Usage in Components

### Server Components
```tsx
import { useTranslations } from 'next-intl'

export default function MyComponent() {
  const t = useTranslations('featureName')
  return <h1>{t('keyName')}</h1>
}
```

### Client Components
Add `'use client'` at the top and use the same approach:
```tsx
'use client'
import { useTranslations } from 'next-intl'

export default function MyComponent() {
  const t = useTranslations('featureName')
  return <h1>{t('keyName')}</h1>
}
```

## RTL Support

### Automatic
- The HTML `dir` attribute is automatically set based on locale
- Flexbox and grid layouts naturally reverse in RTL mode
- Text alignment automatically mirrors

### Manual RTL Adjustments (if needed)
For components requiring special RTL handling, use the locale context:
```tsx
import { useLocale } from 'next-intl'

export default function Component() {
  const locale = useLocale()
  const isRTL = locale === 'ar'
  
  return <div style={{ marginLeft: isRTL ? 0 : 16 }}>
}
```

## Adding New Pages

1. Create page in `/app/[locale]/yourpage/page.tsx`
2. Add `'use client'` if using context/hooks
3. Add translations to `messages/en.json` and `messages/ar.json`
4. Import and use `useTranslations()` hook

## Adding New Translation Keys

1. Add keys to both `messages/en.json` and `messages/ar.json`
2. Keep the same key structure in both files
3. Import `useTranslations()` in your component
4. Use `t('namespace.key')` to access translations

## Supported Locales
- `en` - English (default)
- `ar` - Arabic

## Testing Different Locales

- English: Navigate to `http://localhost:3000/en`
- Arabic: Navigate to `http://localhost:3000/ar`
- Use the language switcher in the sidebar to toggle between languages

## Notes

- All text is translatable and extracted into JSON files
- RTL layout is automatically applied for Arabic
- User preference is preserved in localStorage and URL path
- Theme (light/dark) works independently of language selection
