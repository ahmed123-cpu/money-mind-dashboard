# Dark Mode & Profile Customization Features

## Features Added

### 1. Dark Mode Support
- **ThemeProvider Integration**: Next-themes provider wraps the entire app
- **Theme Toggle Component**: Sun/Moon icon button in the sidebar for instant dark/light switching
- **Color System**: Professional fintech color palette with proper dark mode colors
  - Light mode: Blue primary with green accent
  - Dark mode: Lighter blue primary with lighter green accent
- **System Detection**: Automatically detects user's system preference on first visit
- **Persistence**: Theme preference is stored in localStorage

### 2. Profile Customization

#### Profile Picture Upload
- **Image Upload**: Users can upload custom profile pictures
- **Preview**: Real-time preview of selected image
- **Storage**: Images are stored as base64 in localStorage
- **Avatar Fallback**: Displays user's initials if no image is uploaded

#### Profile Information Form
- **Full Name**: Edit your display name
- **Email**: Update email address (validation included)
- **Phone Number**: Optional contact number
- **Location**: Optional city and country information
- **Bio**: Optional personal bio (up to 500 characters)

### 3. Settings Page
- **New Route**: `/dashboard/settings` accessible from sidebar
- **Organized Layout**: Separate sections for picture and information
- **Form Validation**: React Hook Form + Zod validation
- **Error Handling**: Clear error messages for invalid inputs
- **Success Feedback**: "Saving..." state during submission

### 4. Updated Components

#### Sidebar
- **Settings Link**: New navigation item pointing to settings page
- **Theme Toggle**: Button to switch between light/dark modes
- **Layout**: Flexbox arrangement for theme toggle and menu button

#### Authentication Context
- **updateUser Method**: New function to update user profile data
- **Data Persistence**: Profile changes stored in localStorage
- **Type Safety**: Full TypeScript support

#### User Type
Extended with new optional fields:
- `bio?: string`
- `phone?: string`
- `location?: string`

## Technical Implementation

### Dependencies Used
- `next-themes`: Dark mode management
- `react-hook-form`: Form state management
- `zod`: Schema validation
- `lucide-react`: Icons (Sun, Moon)

### Storage Strategy
- All profile data stored in localStorage under `moneymind_user`
- Base64 encoded profile images stored inline
- Ready for Firebase/Backend integration

## User Flow

### Setting Up Dark Mode
1. Click sun/moon icon in sidebar
2. Theme switches instantly with smooth transition
3. Preference persists across sessions

### Customizing Profile
1. Click "Settings" in sidebar navigation
2. Upload profile picture (optional)
3. Fill in personal information
4. Click "Save Changes"
5. Profile updates instantly with localStorage persistence

## Future Enhancements
- Backend API integration for persistent profile storage
- Profile picture compression and optimization
- Advanced image cropping tool
- Privacy settings
- Theme customization options
