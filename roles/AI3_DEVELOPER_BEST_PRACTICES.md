# AI3 Developer Best Practices - Code Quality Standards

**Purpose:** Production-ready coding standards for ATLAS implementations
**Audience:** AI3 (Implementer role)
**Tech Stack:** Next.js 14+, React 18+, TypeScript, Tailwind CSS
**Status:** v1.0

---

## Overview

This guide defines **code quality standards** for all implementations.

**Target:** Customer websites and internal tools that are:
- Fast (<2s mobile load)
- Accessible (WCAG AA compliant)
- Maintainable (clear, documented)
- Secure (no vulnerabilities)
- Tested (high confidence)

**Philosophy:** Quality over speed. Better to take 2x time and ship excellent code than rush and create tech debt.

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [TypeScript Standards](#typescript-standards)
3. [React Component Patterns](#react-component-patterns)
4. [Styling with Tailwind](#styling-with-tailwind)
5. [Performance Optimization](#performance-optimization)
6. [Accessibility (WCAG AA)](#accessibility-wcag-aa)
7. [SEO Best Practices](#seo-best-practices)
8. [Forms & Validation](#forms--validation)
9. [Error Handling](#error-handling)
10. [Testing Strategy](#testing-strategy)
11. [Security Guidelines](#security-guidelines)
12. [Code Documentation](#code-documentation)
13. [Common Patterns](#common-patterns)
14. [Anti-Patterns to Avoid](#anti-patterns-to-avoid)

---

## Project Structure

### **Next.js App Router Structure**

```
customers/customer-name/
├── app/
│   ├── layout.tsx                 # Root layout
│   ├── page.tsx                   # Home page
│   ├── about/
│   │   └── page.tsx               # About page
│   ├── services/
│   │   └── page.tsx               # Services page
│   ├── contact/
│   │   └── page.tsx               # Contact page
│   ├── api/                       # API routes (if needed)
│   │   └── contact/
│   │       └── route.ts
│   ├── globals.css                # Global styles
│   └── not-found.tsx              # 404 page
│
├── components/
│   ├── ui/                        # Reusable UI components
│   │   ├── Button.tsx
│   │   ├── Card.tsx
│   │   └── Input.tsx
│   ├── layout/                    # Layout components
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   └── Navigation.tsx
│   ├── sections/                  # Page sections
│   │   ├── Hero.tsx
│   │   ├── Services.tsx
│   │   ├── About.tsx
│   │   └── Contact.tsx
│   └── forms/                     # Form components
│       └── ContactForm.tsx
│
├── lib/
│   ├── utils.ts                   # Utility functions
│   ├── validations.ts             # Form validations
│   └── constants.ts               # App constants
│
├── public/
│   ├── images/
│   │   ├── logo.svg
│   │   └── hero.jpg
│   ├── fonts/                     # Custom fonts (if needed)
│   └── favicon.ico
│
├── types/
│   └── index.ts                   # TypeScript types
│
├── __tests__/                     # Tests
│   ├── components/
│   └── lib/
│
├── .env.local                     # Environment variables (gitignored)
├── .env.example                   # Example env vars (committed)
├── next.config.js                 # Next.js config
├── tailwind.config.ts             # Tailwind config
├── tsconfig.json                  # TypeScript config
├── package.json
└── README.md
```

---

## TypeScript Standards

### **1. Always Use Strict Mode**

```typescript
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  }
}
```

### **2. Define Types Explicitly**

**❌ Bad:**
```typescript
function calculateFee(amount, rate) {
  return amount * rate;
}
```

**✅ Good:**
```typescript
function calculateFee(amount: number, rate: number): number {
  return amount * rate;
}
```

### **3. Use Type Aliases and Interfaces**

```typescript
// types/index.ts

// For object shapes
export interface Customer {
  id: string;
  name: string;
  email: string;
  phone?: string; // Optional
}

// For complex types
export type ServiceCategory = 'massage' | 'physical-therapy' | 'wellness';

// For component props
export interface ButtonProps {
  children: React.ReactNode;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
}
```

### **4. Avoid `any`**

**❌ Bad:**
```typescript
const data: any = fetchData();
```

**✅ Good:**
```typescript
interface ApiResponse {
  data: Customer[];
  total: number;
}

const response: ApiResponse = await fetchData();
```

**✅ When truly unknown:**
```typescript
const data: unknown = fetchData();

// Type guard before using
if (isCustomer(data)) {
  console.log(data.name);
}
```

### **5. Use `const` by Default**

```typescript
// ✅ Good
const MAX_RETRIES = 3;
const apiUrl = process.env.NEXT_PUBLIC_API_URL;

// ⚠️ Use `let` only if value will change
let retryCount = 0;

// ❌ Never use `var`
```

---

## React Component Patterns

### **1. Use Functional Components**

```typescript
// ✅ Good - Functional component
interface HeroProps {
  title: string;
  subtitle: string;
  ctaText: string;
  ctaUrl: string;
}

export function Hero({ title, subtitle, ctaText, ctaUrl }: HeroProps) {
  return (
    <section className="hero">
      <h1>{title}</h1>
      <p>{subtitle}</p>
      <a href={ctaUrl}>{ctaText}</a>
    </section>
  );
}

// ❌ Avoid class components (legacy)
```

### **2. Component File Structure**

```typescript
// components/sections/Hero.tsx

// 1. Imports (organized)
import { Button } from '@/components/ui/Button';
import { cn } from '@/lib/utils';
import Image from 'next/image';

// 2. Types/Interfaces
interface HeroProps {
  title: string;
  subtitle: string;
  imageSrc: string;
  imageAlt: string;
}

// 3. Component
export function Hero({ title, subtitle, imageSrc, imageAlt }: HeroProps) {
  return (
    <section className="relative min-h-screen">
      <Image
        src={imageSrc}
        alt={imageAlt}
        fill
        className="object-cover"
        priority
      />
      <div className="relative z-10 container mx-auto px-4">
        <h1 className="text-5xl font-bold text-white">{title}</h1>
        <p className="text-xl text-white/90 mt-4">{subtitle}</p>
        <Button className="mt-8">Book Now</Button>
      </div>
    </section>
  );
}

// 4. Helpers (if needed)
function calculateHeight(isMobile: boolean): string {
  return isMobile ? '400px' : '600px';
}
```

### **3. Props Destructuring**

```typescript
// ✅ Good - Destructure in parameter
export function Card({ title, description, imageUrl }: CardProps) {
  return <div>...</div>;
}

// ❌ Bad - Don't use props object
export function Card(props: CardProps) {
  return <div>{props.title}</div>;
}
```

### **4. Default Props**

```typescript
// ✅ Good - Use default parameters
interface ButtonProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
}

export function Button({
  children,
  variant = 'primary'
}: ButtonProps) {
  return <button className={styles[variant]}>{children}</button>;
}
```

### **5. Conditional Rendering**

```typescript
// ✅ Good - Early return for complex conditions
export function UserProfile({ user }: { user: User | null }) {
  if (!user) {
    return <div>Please log in</div>;
  }

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}

// ✅ Good - && for simple conditions
export function Notification({ message }: { message?: string }) {
  return (
    <div>
      {message && <p className="notification">{message}</p>}
    </div>
  );
}

// ❌ Bad - Ternary for complex JSX
return user ? (
  <div>...</div>
) : otherUser ? (
  <div>...</div>
) : (
  <div>...</div>
);
```

### **6. State Management**

```typescript
// ✅ Good - useState for component state
export function ContactForm() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [isSubmitting, setIsSubmitting] = useState(false);

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setIsSubmitting(true);
    // Submit logic
    setIsSubmitting(false);
  };

  return <form onSubmit={handleSubmit}>...</form>;
}

// ✅ Good - useReducer for complex state
type State = {
  status: 'idle' | 'submitting' | 'success' | 'error';
  message: string;
};

type Action =
  | { type: 'submit' }
  | { type: 'success'; message: string }
  | { type: 'error'; message: string };

function reducer(state: State, action: Action): State {
  switch (action.type) {
    case 'submit':
      return { ...state, status: 'submitting', message: '' };
    case 'success':
      return { status: 'success', message: action.message };
    case 'error':
      return { status: 'error', message: action.message };
    default:
      return state;
  }
}

export function Form() {
  const [state, dispatch] = useReducer(reducer, {
    status: 'idle',
    message: ''
  });
  // Use state and dispatch
}
```

### **7. Effects and Side Effects**

```typescript
// ✅ Good - useEffect for side effects
export function DataFetcher({ id }: { id: string }) {
  const [data, setData] = useState<Data | null>(null);

  useEffect(() => {
    let isCancelled = false;

    async function fetchData() {
      const result = await fetch(`/api/data/${id}`);
      const json = await result.json();

      if (!isCancelled) {
        setData(json);
      }
    }

    fetchData();

    // Cleanup
    return () => {
      isCancelled = true;
    };
  }, [id]); // Dependency array

  return <div>{data?.name}</div>;
}
```

### **8. Custom Hooks**

```typescript
// lib/hooks/useLocalStorage.ts

export function useLocalStorage<T>(
  key: string,
  initialValue: T
): [T, (value: T) => void] {
  const [storedValue, setStoredValue] = useState<T>(() => {
    if (typeof window === 'undefined') {
      return initialValue;
    }
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });

  const setValue = (value: T) => {
    try {
      setStoredValue(value);
      if (typeof window !== 'undefined') {
        window.localStorage.setItem(key, JSON.stringify(value));
      }
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue];
}

// Usage
function MyComponent() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  return <div>Current theme: {theme}</div>;
}
```

---

## Styling with Tailwind

### **1. Use Tailwind Utility Classes**

```tsx
// ✅ Good - Utility-first
<div className="flex items-center justify-between p-4 bg-white rounded-lg shadow-md">
  <h2 className="text-2xl font-bold text-gray-900">Title</h2>
  <button className="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">
    Click me
  </button>
</div>

// ❌ Bad - Inline styles
<div style={{ display: 'flex', padding: '16px' }}>
  <h2 style={{ fontSize: '24px', fontWeight: 'bold' }}>Title</h2>
</div>
```

### **2. Use `cn()` Helper for Conditional Classes**

```typescript
// lib/utils.ts
import { clsx, type ClassValue } from 'clsx';
import { twMerge } from 'tailwind-merge';

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}

// Usage in component
import { cn } from '@/lib/utils';

interface ButtonProps {
  variant?: 'primary' | 'secondary';
  size?: 'sm' | 'md' | 'lg';
  children: React.ReactNode;
}

export function Button({ variant = 'primary', size = 'md', children }: ButtonProps) {
  return (
    <button
      className={cn(
        // Base styles
        'rounded font-medium transition-colors',
        // Variant styles
        variant === 'primary' && 'bg-blue-600 text-white hover:bg-blue-700',
        variant === 'secondary' && 'bg-gray-200 text-gray-900 hover:bg-gray-300',
        // Size styles
        size === 'sm' && 'px-3 py-1.5 text-sm',
        size === 'md' && 'px-4 py-2 text-base',
        size === 'lg' && 'px-6 py-3 text-lg'
      )}
    >
      {children}
    </button>
  );
}
```

### **3. Extract Repeated Patterns to Components**

```tsx
// ❌ Bad - Repeated classes
<div>
  <div className="p-6 bg-white rounded-lg shadow-md">...</div>
  <div className="p-6 bg-white rounded-lg shadow-md">...</div>
  <div className="p-6 bg-white rounded-lg shadow-md">...</div>
</div>

// ✅ Good - Reusable Card component
export function Card({ children }: { children: React.ReactNode }) {
  return (
    <div className="p-6 bg-white rounded-lg shadow-md">
      {children}
    </div>
  );
}

// Usage
<div>
  <Card>Content 1</Card>
  <Card>Content 2</Card>
  <Card>Content 3</Card>
</div>
```

### **4. Responsive Design**

```tsx
// ✅ Mobile-first approach
<div className="
  flex flex-col           // Mobile: stack vertically
  md:flex-row             // Tablet+: horizontal
  gap-4                   // Always 4 units gap
  p-4                     // Mobile: 4 units padding
  md:p-6                  // Tablet+: 6 units
  lg:p-8                  // Desktop: 8 units
">
  <div className="w-full md:w-1/2">Content 1</div>
  <div className="w-full md:w-1/2">Content 2</div>
</div>
```

### **5. Dark Mode Support (Optional)**

```tsx
// tailwind.config.ts
export default {
  darkMode: 'class', // or 'media'
  // ...
}

// Component
<div className="bg-white dark:bg-gray-900 text-gray-900 dark:text-white">
  Content that adapts to dark mode
</div>
```

---

## Performance Optimization

### **1. Image Optimization**

```tsx
// ✅ Good - Use Next.js Image component
import Image from 'next/image';

export function Hero() {
  return (
    <div className="relative h-screen">
      <Image
        src="/images/hero.jpg"
        alt="Hero image"
        fill
        className="object-cover"
        priority  // Load immediately (above fold)
        sizes="100vw"
        quality={85}
      />
    </div>
  );
}

// For images below the fold
<Image
  src="/images/service.jpg"
  alt="Service image"
  width={600}
  height={400}
  loading="lazy"  // Lazy load
  sizes="(max-width: 768px) 100vw, 50vw"
/>

// ❌ Bad - Regular img tag (no optimization)
<img src="/images/hero.jpg" alt="Hero" />
```

### **2. Font Optimization**

```tsx
// app/layout.tsx
import { Inter } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={inter.variable}>
      <body>{children}</body>
    </html>
  );
}

// tailwind.config.ts
export default {
  theme: {
    extend: {
      fontFamily: {
        sans: ['var(--font-inter)', 'sans-serif'],
      },
    },
  },
}
```

### **3. Code Splitting and Dynamic Imports**

```tsx
// ✅ Good - Lazy load heavy components
import dynamic from 'next/dynamic';

const BookingWidget = dynamic(() => import('@/components/BookingWidget'), {
  loading: () => <div>Loading booking widget...</div>,
  ssr: false, // Don't render on server if not needed
});

export function Services() {
  return (
    <div>
      <h2>Our Services</h2>
      <BookingWidget />
    </div>
  );
}
```

### **4. Memoization**

```tsx
import { memo, useMemo, useCallback } from 'react';

// Memoize expensive components
export const ServiceCard = memo(function ServiceCard({
  service
}: {
  service: Service
}) {
  return (
    <div className="card">
      <h3>{service.name}</h3>
      <p>{service.description}</p>
    </div>
  );
});

// Memoize expensive calculations
export function PricingTable({ services }: { services: Service[] }) {
  const totalPrice = useMemo(() => {
    return services.reduce((sum, service) => sum + service.price, 0);
  }, [services]);

  return <div>Total: ${totalPrice}</div>;
}

// Memoize callbacks
export function Form() {
  const [value, setValue] = useState('');

  const handleChange = useCallback((e: React.ChangeEvent<HTMLInputElement>) => {
    setValue(e.target.value);
  }, []);

  return <input value={value} onChange={handleChange} />;
}
```

### **5. Reduce Bundle Size**

```tsx
// ✅ Good - Import only what you need
import { useState } from 'react';

// ❌ Bad - Import everything
import * as React from 'react';

// ✅ Good - Tree-shakeable imports
import { Button } from '@/components/ui/Button';

// ❌ Bad - Barrel imports (can hurt tree-shaking)
import { Button, Card, Input } from '@/components/ui';
```

---

## Accessibility (WCAG AA)

### **1. Semantic HTML**

```tsx
// ✅ Good - Semantic structure
<header>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <h1>Page Title</h1>
    <p>Content</p>
  </article>
</main>

<footer>
  <p>&copy; 2025 Company Name</p>
</footer>

// ❌ Bad - Divs for everything
<div>
  <div>
    <div><a href="/">Home</a></div>
  </div>
</div>
```

### **2. ARIA Labels**

```tsx
// ✅ Good - Descriptive labels
<button
  aria-label="Close menu"
  onClick={closeMenu}
>
  <CloseIcon />
</button>

<nav aria-label="Main navigation">
  <ul>...</ul>
</nav>

<section aria-labelledby="services-heading">
  <h2 id="services-heading">Our Services</h2>
  <div>...</div>
</section>
```

### **3. Form Accessibility**

```tsx
// ✅ Good - Proper labels and error handling
export function ContactForm() {
  const [errors, setErrors] = useState<Record<string, string>>({});

  return (
    <form onSubmit={handleSubmit} noValidate>
      <div>
        <label htmlFor="name" className="block mb-2">
          Name *
        </label>
        <input
          type="text"
          id="name"
          name="name"
          required
          aria-required="true"
          aria-invalid={!!errors.name}
          aria-describedby={errors.name ? 'name-error' : undefined}
          className="w-full border rounded px-3 py-2"
        />
        {errors.name && (
          <p id="name-error" className="text-red-600 text-sm mt-1" role="alert">
            {errors.name}
          </p>
        )}
      </div>

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Submitting...' : 'Submit'}
      </button>
    </form>
  );
}
```

### **4. Keyboard Navigation**

```tsx
// ✅ Good - Keyboard accessible
export function Modal({ isOpen, onClose, children }: ModalProps) {
  useEffect(() => {
    const handleEscape = (e: KeyboardEvent) => {
      if (e.key === 'Escape') {
        onClose();
      }
    };

    if (isOpen) {
      document.addEventListener('keydown', handleEscape);
      return () => document.removeEventListener('keydown', handleEscape);
    }
  }, [isOpen, onClose]);

  if (!isOpen) return null;

  return (
    <div
      role="dialog"
      aria-modal="true"
      aria-labelledby="modal-title"
    >
      <button
        onClick={onClose}
        aria-label="Close modal"
        className="absolute top-4 right-4"
      >
        ×
      </button>
      <h2 id="modal-title">Modal Title</h2>
      {children}
    </div>
  );
}
```

### **5. Color Contrast**

```tsx
// ✅ Good - WCAG AA contrast ratios
// Text: 4.5:1 for normal text, 3:1 for large text
// Use tools: https://webaim.org/resources/contrastchecker/

<div className="bg-gray-900 text-white">  // High contrast ✅
  Content
</div>

<button className="bg-blue-600 text-white">  // High contrast ✅
  Click me
</button>

// ❌ Bad - Low contrast
<div className="bg-gray-300 text-gray-400">  // Too similar ❌
  Hard to read
</div>
```

### **6. Alt Text for Images**

```tsx
// ✅ Good - Descriptive alt text
<Image
  src="/images/massage-therapy.jpg"
  alt="Licensed massage therapist performing deep tissue massage"
  width={600}
  height={400}
/>

// ✅ Good - Empty alt for decorative images
<Image
  src="/images/decorative-pattern.svg"
  alt=""
  width={100}
  height={100}
/>

// ❌ Bad - Missing or poor alt text
<img src="/image.jpg" alt="image" />  // Not descriptive
<img src="/photo.jpg" />  // Missing alt
```

---

## SEO Best Practices

### **1. Metadata**

```tsx
// app/layout.tsx (site-wide)
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: {
    default: 'Business Name - Tagline',
    template: '%s | Business Name',
  },
  description: 'Compelling 150-160 character description for search results',
  keywords: ['keyword1', 'keyword2', 'keyword3'],
  authors: [{ name: 'Business Name' }],
  openGraph: {
    title: 'Business Name',
    description: 'Description for social sharing',
    url: 'https://example.com',
    siteName: 'Business Name',
    images: [
      {
        url: 'https://example.com/og-image.jpg',
        width: 1200,
        height: 630,
      },
    ],
    locale: 'en_US',
    type: 'website',
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Business Name',
    description: 'Description for Twitter',
    images: ['https://example.com/twitter-image.jpg'],
  },
  robots: {
    index: true,
    follow: true,
  },
};

// app/about/page.tsx (page-specific)
export const metadata: Metadata = {
  title: 'About Us',
  description: 'Learn about our team and mission',
};
```

### **2. Structured Data (JSON-LD)**

```tsx
// app/page.tsx
export default function HomePage() {
  const jsonLd = {
    '@context': 'https://schema.org',
    '@type': 'LocalBusiness',
    name: 'Business Name',
    image: 'https://example.com/logo.jpg',
    '@id': 'https://example.com',
    url: 'https://example.com',
    telephone: '+1-555-555-5555',
    priceRange: '$$',
    address: {
      '@type': 'PostalAddress',
      streetAddress: '123 Main St',
      addressLocality: 'City',
      addressRegion: 'State',
      postalCode: '12345',
      addressCountry: 'US',
    },
    geo: {
      '@type': 'GeoCoordinates',
      latitude: 40.7128,
      longitude: -74.0060,
    },
    openingHoursSpecification: {
      '@type': 'OpeningHoursSpecification',
      dayOfWeek: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'],
      opens: '09:00',
      closes: '17:00',
    },
  };

  return (
    <>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      <main>
        <h1>Welcome to Business Name</h1>
        {/* ... */}
      </main>
    </>
  );
}
```

### **3. Sitemap and robots.txt**

```typescript
// app/sitemap.ts
import { MetadataRoute } from 'next';

export default function sitemap(): MetadataRoute.Sitemap {
  return [
    {
      url: 'https://example.com',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 1,
    },
    {
      url: 'https://example.com/about',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 0.8,
    },
    {
      url: 'https://example.com/services',
      lastModified: new Date(),
      changeFrequency: 'weekly',
      priority: 0.9,
    },
    {
      url: 'https://example.com/contact',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 0.7,
    },
  ];
}

// app/robots.ts
import { MetadataRoute } from 'next';

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
      disallow: '/private/',
    },
    sitemap: 'https://example.com/sitemap.xml',
  };
}
```

### **4. Semantic HTML for SEO**

```tsx
// ✅ Good - Clear hierarchy
<main>
  <article>
    <header>
      <h1>Main Page Heading</h1>
      <p>Published on <time dateTime="2025-01-15">January 15, 2025</time></p>
    </header>

    <section>
      <h2>Section Heading</h2>
      <p>Content...</p>

      <h3>Subsection</h3>
      <p>More content...</p>
    </section>
  </article>
</main>

// ❌ Bad - Multiple H1s, poor hierarchy
<div>
  <h1>Title 1</h1>
  <h1>Title 2</h1>  // Don't do this
  <h3>Section</h3>  // Skipped H2
</div>
```

---

## Forms & Validation

### **1. Client-Side Validation**

```typescript
// lib/validations.ts
import { z } from 'zod';

export const contactFormSchema = z.object({
  name: z.string().min(2, 'Name must be at least 2 characters'),
  email: z.string().email('Invalid email address'),
  phone: z.string().regex(/^\d{10}$/, 'Phone must be 10 digits').optional(),
  message: z.string().min(10, 'Message must be at least 10 characters'),
});

export type ContactFormData = z.infer<typeof contactFormSchema>;
```

```tsx
// components/forms/ContactForm.tsx
'use client';

import { useState } from 'react';
import { contactFormSchema, type ContactFormData } from '@/lib/validations';

export function ContactForm() {
  const [formData, setFormData] = useState<ContactFormData>({
    name: '',
    email: '',
    phone: '',
    message: '',
  });
  const [errors, setErrors] = useState<Partial<Record<keyof ContactFormData, string>>>({});
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [submitStatus, setSubmitStatus] = useState<'idle' | 'success' | 'error'>('idle');

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setErrors({});
    setIsSubmitting(true);

    // Validate
    const result = contactFormSchema.safeParse(formData);

    if (!result.success) {
      const fieldErrors: Partial<Record<keyof ContactFormData, string>> = {};
      result.error.issues.forEach((issue) => {
        if (issue.path[0]) {
          fieldErrors[issue.path[0] as keyof ContactFormData] = issue.message;
        }
      });
      setErrors(fieldErrors);
      setIsSubmitting(false);
      return;
    }

    // Submit
    try {
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(result.data),
      });

      if (!response.ok) throw new Error('Submission failed');

      setSubmitStatus('success');
      setFormData({ name: '', email: '', phone: '', message: '' });
    } catch (error) {
      setSubmitStatus('error');
    } finally {
      setIsSubmitting(false);
    }
  };

  const handleChange = (
    e: React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement>
  ) => {
    const { name, value } = e.target;
    setFormData((prev) => ({ ...prev, [name]: value }));
    // Clear error for this field
    if (errors[name as keyof ContactFormData]) {
      setErrors((prev) => ({ ...prev, [name]: undefined }));
    }
  };

  return (
    <form onSubmit={handleSubmit} className="space-y-4">
      {/* Name field */}
      <div>
        <label htmlFor="name" className="block text-sm font-medium mb-1">
          Name *
        </label>
        <input
          type="text"
          id="name"
          name="name"
          value={formData.name}
          onChange={handleChange}
          required
          aria-required="true"
          aria-invalid={!!errors.name}
          aria-describedby={errors.name ? 'name-error' : undefined}
          className="w-full border border-gray-300 rounded px-3 py-2 focus:ring-2 focus:ring-blue-500"
        />
        {errors.name && (
          <p id="name-error" className="text-red-600 text-sm mt-1" role="alert">
            {errors.name}
          </p>
        )}
      </div>

      {/* Email field */}
      <div>
        <label htmlFor="email" className="block text-sm font-medium mb-1">
          Email *
        </label>
        <input
          type="email"
          id="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
          required
          aria-required="true"
          aria-invalid={!!errors.email}
          aria-describedby={errors.email ? 'email-error' : undefined}
          className="w-full border border-gray-300 rounded px-3 py-2"
        />
        {errors.email && (
          <p id="email-error" className="text-red-600 text-sm mt-1" role="alert">
            {errors.email}
          </p>
        )}
      </div>

      {/* Message field */}
      <div>
        <label htmlFor="message" className="block text-sm font-medium mb-1">
          Message *
        </label>
        <textarea
          id="message"
          name="message"
          value={formData.message}
          onChange={handleChange}
          required
          rows={5}
          aria-required="true"
          aria-invalid={!!errors.message}
          aria-describedby={errors.message ? 'message-error' : undefined}
          className="w-full border border-gray-300 rounded px-3 py-2"
        />
        {errors.message && (
          <p id="message-error" className="text-red-600 text-sm mt-1" role="alert">
            {errors.message}
          </p>
        )}
      </div>

      {/* Submit button */}
      <button
        type="submit"
        disabled={isSubmitting}
        className="w-full bg-blue-600 text-white py-3 rounded font-medium hover:bg-blue-700 disabled:opacity-50"
      >
        {isSubmitting ? 'Submitting...' : 'Send Message'}
      </button>

      {/* Success/error messages */}
      {submitStatus === 'success' && (
        <p className="text-green-600 text-center" role="status">
          Thank you! We'll be in touch soon.
        </p>
      )}
      {submitStatus === 'error' && (
        <p className="text-red-600 text-center" role="alert">
          Something went wrong. Please try again.
        </p>
      )}
    </form>
  );
}
```

### **2. Server-Side Validation (API Route)**

```typescript
// app/api/contact/route.ts
import { NextResponse } from 'next/server';
import { contactFormSchema } from '@/lib/validations';

export async function POST(request: Request) {
  try {
    const body = await request.json();

    // Validate input
    const result = contactFormSchema.safeParse(body);

    if (!result.success) {
      return NextResponse.json(
        { error: 'Validation failed', issues: result.error.issues },
        { status: 400 }
      );
    }

    // Process submission (send email, save to DB, etc.)
    // Example: Send email via service
    // await sendEmail({
    //   to: 'info@example.com',
    //   subject: `Contact form from ${result.data.name}`,
    //   body: result.data.message,
    // });

    return NextResponse.json({ success: true }, { status: 200 });
  } catch (error) {
    console.error('Contact form error:', error);
    return NextResponse.json(
      { error: 'Internal server error' },
      { status: 500 }
    );
  }
}
```

---

## Error Handling

### **1. Error Boundaries**

```tsx
// components/ErrorBoundary.tsx
'use client';

import { Component, type ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode;
}

interface State {
  hasError: boolean;
  error?: Error;
}

export class ErrorBoundary extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    console.error('Error boundary caught:', error, errorInfo);
    // Log to error tracking service (e.g., Sentry)
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || (
        <div className="min-h-screen flex items-center justify-center">
          <div className="text-center">
            <h2 className="text-2xl font-bold mb-2">Something went wrong</h2>
            <p className="text-gray-600 mb-4">We're sorry for the inconvenience.</p>
            <button
              onClick={() => this.setState({ hasError: false })}
              className="px-4 py-2 bg-blue-600 text-white rounded"
            >
              Try again
            </button>
          </div>
        </div>
      );
    }

    return this.props.children;
  }
}

// Usage in layout
<ErrorBoundary>
  {children}
</ErrorBoundary>
```

### **2. API Error Handling**

```typescript
// lib/api.ts
export class ApiError extends Error {
  constructor(public status: number, message: string) {
    super(message);
    this.name = 'ApiError';
  }
}

export async function fetchApi<T>(
  url: string,
  options?: RequestInit
): Promise<T> {
  try {
    const response = await fetch(url, options);

    if (!response.ok) {
      throw new ApiError(response.status, `API error: ${response.statusText}`);
    }

    return response.json();
  } catch (error) {
    if (error instanceof ApiError) {
      throw error;
    }
    throw new ApiError(500, 'Network error');
  }
}

// Usage
try {
  const data = await fetchApi<User>('/api/user');
  // Use data
} catch (error) {
  if (error instanceof ApiError) {
    if (error.status === 404) {
      // Handle not found
    } else if (error.status >= 500) {
      // Handle server error
    }
  }
}
```

---

## Testing Strategy

### **1. Unit Tests**

```typescript
// __tests__/lib/utils.test.ts
import { describe, it, expect } from '@jest/globals';
import { cn } from '@/lib/utils';

describe('cn utility', () => {
  it('merges class names', () => {
    expect(cn('class1', 'class2')).toBe('class1 class2');
  });

  it('handles conditional classes', () => {
    expect(cn('base', true && 'truthy', false && 'falsy')).toBe('base truthy');
  });

  it('merges Tailwind classes correctly', () => {
    expect(cn('p-4', 'p-8')).toBe('p-8'); // p-8 overrides p-4
  });
});
```

### **2. Component Tests**

```tsx
// __tests__/components/Button.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from '@/components/ui/Button';

describe('Button', () => {
  it('renders children', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const handleClick = jest.fn();
    render(<Button onClick={handleClick}>Click</Button>);
    fireEvent.click(screen.getByText('Click'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('applies variant styles', () => {
    render(<Button variant="secondary">Button</Button>);
    const button = screen.getByRole('button');
    expect(button).toHaveClass('bg-gray-200');
  });

  it('disables button when disabled prop is true', () => {
    render(<Button disabled>Disabled</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });
});
```

### **3. Integration Tests (Optional)**

```typescript
// __tests__/integration/contact-form.test.tsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import { ContactForm } from '@/components/forms/ContactForm';

describe('ContactForm integration', () => {
  it('submits form with valid data', async () => {
    render(<ContactForm />);

    fireEvent.change(screen.getByLabelText(/name/i), {
      target: { value: 'John Doe' },
    });
    fireEvent.change(screen.getByLabelText(/email/i), {
      target: { value: 'john@example.com' },
    });
    fireEvent.change(screen.getByLabelText(/message/i), {
      target: { value: 'This is a test message.' },
    });

    fireEvent.click(screen.getByText('Send Message'));

    await waitFor(() => {
      expect(screen.getByText(/thank you/i)).toBeInTheDocument();
    });
  });

  it('shows validation errors for invalid data', async () => {
    render(<ContactForm />);

    fireEvent.click(screen.getByText('Send Message'));

    await waitFor(() => {
      expect(screen.getByText(/name must be at least 2 characters/i)).toBeInTheDocument();
    });
  });
});
```

---

## Security Guidelines

### **1. Environment Variables**

```bash
# .env.local (gitignored)
DATABASE_URL="postgresql://..."
NEXT_PUBLIC_API_URL="https://api.example.com"
RESEND_API_KEY="re_..."

# .env.example (committed)
DATABASE_URL="postgresql://user:password@localhost:5432/db"
NEXT_PUBLIC_API_URL="https://api.example.com"
RESEND_API_KEY="your_api_key_here"
```

```typescript
// ✅ Good - Server-side only
// app/api/route.ts
const apiKey = process.env.RESEND_API_KEY; // Available server-side

// ✅ Good - Client-side (public)
// components/Map.tsx
const mapKey = process.env.NEXT_PUBLIC_MAPS_KEY; // Prefixed with NEXT_PUBLIC_

// ❌ Bad - Never commit secrets
const apiKey = "re_abc123"; // Don't hardcode
```

### **2. Input Sanitization**

```typescript
// ✅ Good - Validate and sanitize
import DOMPurify from 'isomorphic-dompurify';

function sanitizeHtml(dirty: string): string {
  return DOMPurify.sanitize(dirty);
}

// Usage
const cleanHtml = sanitizeHtml(userInput);
```

### **3. API Rate Limiting (Optional)**

```typescript
// lib/rate-limit.ts
import { LRUCache } from 'lru-cache';

type RateLimitOptions = {
  interval: number;
  uniqueTokenPerInterval: number;
};

export function rateLimit(options: RateLimitOptions) {
  const tokenCache = new LRUCache({
    max: options.uniqueTokenPerInterval || 500,
    ttl: options.interval || 60000,
  });

  return {
    check: (limit: number, token: string) =>
      new Promise<void>((resolve, reject) => {
        const tokenCount = (tokenCache.get(token) as number[]) || [0];
        if (tokenCount[0] === 0) {
          tokenCache.set(token, tokenCount);
        }
        tokenCount[0] += 1;

        const currentUsage = tokenCount[0];
        const isRateLimited = currentUsage >= limit;

        return isRateLimited ? reject() : resolve();
      }),
  };
}

// Usage in API route
const limiter = rateLimit({
  interval: 60 * 1000, // 1 minute
  uniqueTokenPerInterval: 500,
});

export async function POST(request: Request) {
  const ip = request.headers.get('x-forwarded-for') || 'anonymous';

  try {
    await limiter.check(10, ip); // 10 requests per minute
  } catch {
    return new Response('Rate limit exceeded', { status: 429 });
  }

  // Process request
}
```

### **4. Content Security Policy**

```typescript
// next.config.js
const ContentSecurityPolicy = `
  default-src 'self';
  script-src 'self' 'unsafe-eval' 'unsafe-inline';
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  font-src 'self' data:;
  connect-src 'self' https://api.example.com;
  frame-src 'self' https://calendly.com;
`;

module.exports = {
  async headers() {
    return [
      {
        source: '/:path*',
        headers: [
          {
            key: 'Content-Security-Policy',
            value: ContentSecurityPolicy.replace(/\s{2,}/g, ' ').trim(),
          },
          {
            key: 'X-Frame-Options',
            value: 'SAMEORIGIN',
          },
          {
            key: 'X-Content-Type-Options',
            value: 'nosniff',
          },
          {
            key: 'Referrer-Policy',
            value: 'strict-origin-when-cross-origin',
          },
        ],
      },
    ];
  },
};
```

---

## Code Documentation

### **1. Component Documentation**

```tsx
/**
 * Button component with multiple variants and sizes.
 *
 * @example
 * ```tsx
 * <Button variant="primary" size="lg" onClick={handleClick}>
 *   Click me
 * </Button>
 * ```
 */
export interface ButtonProps {
  /** Button content */
  children: React.ReactNode;
  /** Visual style variant */
  variant?: 'primary' | 'secondary' | 'outline';
  /** Size variant */
  size?: 'sm' | 'md' | 'lg';
  /** Click handler */
  onClick?: () => void;
  /** Disabled state */
  disabled?: boolean;
  /** Additional CSS classes */
  className?: string;
}

export function Button({
  children,
  variant = 'primary',
  size = 'md',
  onClick,
  disabled = false,
  className,
}: ButtonProps) {
  // Implementation
}
```

### **2. Function Documentation**

```typescript
/**
 * Calculates the total price including tax and fees.
 *
 * @param basePrice - The base price before tax
 * @param taxRate - Tax rate as decimal (e.g., 0.08 for 8%)
 * @param fees - Optional additional fees
 * @returns Total price rounded to 2 decimal places
 *
 * @example
 * ```ts
 * const total = calculateTotal(100, 0.08, 5);
 * // Returns: 113.00
 * ```
 */
export function calculateTotal(
  basePrice: number,
  taxRate: number,
  fees: number = 0
): number {
  const subtotal = basePrice + fees;
  const tax = subtotal * taxRate;
  const total = subtotal + tax;
  return Math.round(total * 100) / 100;
}
```

### **3. README for Each Project**

```markdown
# Customer Name - Website

## Overview
Modern, fast website for [Customer Name] built with Next.js 14.

## Tech Stack
- Next.js 14 (App Router)
- React 18
- TypeScript
- Tailwind CSS
- Vercel (hosting)

## Getting Started

\`\`\`bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build

# Run production build
npm start
\`\`\`

## Project Structure
See `/docs/ARCHITECTURE.md` for detailed structure.

## Environment Variables
Copy `.env.example` to `.env.local` and fill in values.

## Deployment
Deployed automatically via Vercel when pushing to `main` branch.

## Performance Targets
- Mobile load time: <2s
- Lighthouse score: 90+
- WCAG AA compliant

## Contact
Built by your company - [contact info]
```

---

## Common Patterns

### **1. Loading States**

```tsx
export function ServicesList() {
  const [services, setServices] = useState<Service[]>([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    async function loadServices() {
      try {
        const data = await fetch('/api/services').then(r => r.json());
        setServices(data);
      } catch (err) {
        setError('Failed to load services');
      } finally {
        setIsLoading(false);
      }
    }
    loadServices();
  }, []);

  if (isLoading) {
    return (
      <div className="flex justify-center p-8">
        <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-600" />
      </div>
    );
  }

  if (error) {
    return (
      <div className="text-red-600 p-4 bg-red-50 rounded">
        {error}
      </div>
    );
  }

  return (
    <div className="grid gap-4">
      {services.map((service) => (
        <ServiceCard key={service.id} service={service} />
      ))}
    </div>
  );
}
```

### **2. Responsive Navigation**

```tsx
'use client';

import { useState } from 'react';
import Link from 'next/link';

export function Navigation() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <nav className="bg-white shadow">
      <div className="container mx-auto px-4">
        <div className="flex justify-between items-center h-16">
          {/* Logo */}
          <Link href="/" className="text-xl font-bold">
            Logo
          </Link>

          {/* Desktop Navigation */}
          <div className="hidden md:flex space-x-8">
            <Link href="/" className="hover:text-blue-600">Home</Link>
            <Link href="/about" className="hover:text-blue-600">About</Link>
            <Link href="/services" className="hover:text-blue-600">Services</Link>
            <Link href="/contact" className="hover:text-blue-600">Contact</Link>
          </div>

          {/* Mobile Menu Button */}
          <button
            onClick={() => setIsOpen(!isOpen)}
            className="md:hidden"
            aria-label="Toggle menu"
            aria-expanded={isOpen}
          >
            {isOpen ? '✕' : '☰'}
          </button>
        </div>

        {/* Mobile Navigation */}
        {isOpen && (
          <div className="md:hidden pb-4">
            <Link href="/" className="block py-2 hover:text-blue-600">Home</Link>
            <Link href="/about" className="block py-2 hover:text-blue-600">About</Link>
            <Link href="/services" className="block py-2 hover:text-blue-600">Services</Link>
            <Link href="/contact" className="block py-2 hover:text-blue-600">Contact</Link>
          </div>
        )}
      </div>
    </nav>
  );
}
```

### **3. Calendly Integration**

```tsx
'use client';

import { useEffect } from 'react';

declare global {
  interface Window {
    Calendly?: {
      initInlineWidget: (options: {
        url: string;
        parentElement: HTMLElement;
        prefill?: Record<string, string>;
        utm?: Record<string, string>;
      }) => void;
    };
  }
}

export function BookingWidget() {
  useEffect(() => {
    const script = document.createElement('script');
    script.src = 'https://assets.calendly.com/assets/external/widget.js';
    script.async = true;
    document.body.appendChild(script);

    return () => {
      document.body.removeChild(script);
    };
  }, []);

  return (
    <div
      className="calendly-inline-widget"
      data-url="https://calendly.com/your-link"
      style={{ minWidth: '320px', height: '630px' }}
    />
  );
}
```

---

## Anti-Patterns to Avoid

### **❌ 1. Prop Drilling**

```tsx
// Bad - Passing props through many levels
<GrandParent data={data}>
  <Parent data={data}>
    <Child data={data} />
  </Parent>
</GrandParent>

// Good - Use context for deeply nested props
const DataContext = createContext<Data | null>(null);

<DataContext.Provider value={data}>
  <GrandParent>
    <Parent>
      <Child />  // Uses useContext(DataContext)
    </Parent>
  </GrandParent>
</DataContext.Provider>
```

### **❌ 2. Mutating State Directly**

```tsx
// Bad
const [items, setItems] = useState([1, 2, 3]);
items.push(4);  // ❌ Mutating state
setItems(items);

// Good
const [items, setItems] = useState([1, 2, 3]);
setItems([...items, 4]);  // ✅ New array
```

### **❌ 3. Not Handling Loading/Error States**

```tsx
// Bad - No loading or error handling
const [data, setData] = useState();
useEffect(() => {
  fetch('/api/data').then(r => r.json()).then(setData);
}, []);
return <div>{data.name}</div>;  // What if data is undefined?

// Good - Handle all states
const [data, setData] = useState<Data | null>(null);
const [isLoading, setIsLoading] = useState(true);
const [error, setError] = useState<string | null>(null);

if (isLoading) return <div>Loading...</div>;
if (error) return <div>Error: {error}</div>;
if (!data) return <div>No data</div>;
return <div>{data.name}</div>;
```

### **❌ 4. Unnecessary useEffect**

```tsx
// Bad - useEffect for simple calculation
const [count, setCount] = useState(0);
const [doubled, setDoubled] = useState(0);

useEffect(() => {
  setDoubled(count * 2);
}, [count]);

// Good - Just calculate it
const [count, setCount] = useState(0);
const doubled = count * 2;
```

### **❌ 5. Key Prop with Index**

```tsx
// Bad - Using index as key
{items.map((item, index) => (
  <div key={index}>{item}</div>
))}

// Good - Use stable unique ID
{items.map((item) => (
  <div key={item.id}>{item.name}</div>
))}
```

---

## Performance Checklist

Before declaring implementation complete:

**✓ Images**
- [ ] All images use Next.js `<Image>` component
- [ ] Above-fold images have `priority` prop
- [ ] Images have appropriate `sizes` attribute
- [ ] Images are optimized (WebP, correct dimensions)

**✓ Loading Performance**
- [ ] Mobile load time <2s (tested with PageSpeed Insights)
- [ ] Lighthouse performance score 90+
- [ ] No render-blocking resources
- [ ] Fonts optimized (next/font)

**✓ Code Splitting**
- [ ] Heavy components lazy loaded with `dynamic()`
- [ ] Third-party scripts loaded asynchronously
- [ ] No unnecessary imports

**✓ Accessibility**
- [ ] WCAG AA compliant (tested with WAVE or axe)
- [ ] All images have alt text
- [ ] Forms have proper labels and error handling
- [ ] Keyboard navigation works
- [ ] Color contrast meets standards

**✓ SEO**
- [ ] Page titles unique and descriptive
- [ ] Meta descriptions present (150-160 chars)
- [ ] Structured data (JSON-LD) implemented
- [ ] Sitemap.xml generated
- [ ] robots.txt configured
- [ ] Open Graph tags present

**✓ Testing**
- [ ] Build succeeds: `npm run build`
- [ ] All tests pass: `npm test`
- [ ] No console errors in browser
- [ ] Forms submit successfully
- [ ] Links work
- [ ] Mobile responsive

---

## Related Documentation

- `AI3_IMPLEMENTER_GUIDE.md` - Implementation workflow
- `GIT_WORKFLOW.md` - Git procedures
- Next.js docs: https://nextjs.org/docs
- React docs: https://react.dev
- Tailwind docs: https://tailwindcss.com

---

## Remember

**Quality is not negotiable.**

- Fast load times = better UX = better conversions
- Accessibility = inclusivity = larger audience
- Clean code = maintainable = sustainable business
- Testing = confidence = reliable product

**Build sites you're proud to show. Every customer site is a portfolio piece.** ✨
