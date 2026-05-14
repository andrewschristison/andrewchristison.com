---
name: shadcn-ui
description: 'Shadcn/ui component patterns for this project. Use when building UI components, forms, tables, dialogs, or navigation. Covers component composition, Tailwind customisation, theming, and accessibility patterns specific to a B2B admin panel.'
license: MIT
metadata:
  author: dojo-admin
  version: "1.0.0"
---

# Shadcn/ui — Dojo Admin

Patterns for using shadcn/ui in a B2B admin panel context. Shadcn components are owned by the project — they live in `components/ui/` and can be modified freely.

## Core Principle

**Compose, don't customise the primitive.** Build feature components by composing shadcn primitives. If a primitive doesn't do what you need, build above it — don't reach into it.

## Scoring

**Goal: 10/10.** When reviewing UI component code, rate it 0-10. A 10/10 means all interactive elements are accessible, variants are used from the component API (not ad-hoc classnames), and no `style={{}}` props appear where Tailwind classes suffice.

---

## 1. Setup

```bash
# Initialise shadcn in an existing Next.js project
npx shadcn-ui@latest init

# Add specific components
npx shadcn-ui@latest add button card table badge form input select dialog toast
```

**`components.json` for this project:**

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "default",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "app/globals.css",
    "baseColor": "slate",
    "cssVariables": true
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils"
  }
}
```

---

## 2. Component Composition Patterns

### Data Tables

For student lists, payment history, attendance — use `Table` + `TableHeader` + `TableBody`:

```tsx
import {
  Table, TableBody, TableCell, TableHead, TableHeader, TableRow
} from '@/components/ui/table'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'

type Student = { id: string; name: string; beltLevel: string; active: boolean }

export function StudentTable({ students }: { students: Student[] }) {
  return (
    <Table>
      <TableHeader>
        <TableRow>
          <TableHead>Name</TableHead>
          <TableHead>Belt</TableHead>
          <TableHead>Status</TableHead>
          <TableHead className="text-right">Actions</TableHead>
        </TableRow>
      </TableHeader>
      <TableBody>
        {students.map((student) => (
          <TableRow key={student.id}>
            <TableCell className="font-medium">{student.name}</TableCell>
            <TableCell>
              <BeltBadge level={student.beltLevel} />
            </TableCell>
            <TableCell>
              <Badge variant={student.active ? 'default' : 'secondary'}>
                {student.active ? 'Active' : 'Inactive'}
              </Badge>
            </TableCell>
            <TableCell className="text-right">
              <Button variant="ghost" size="sm" asChild>
                <a href={`/students/${student.id}`}>View</a>
              </Button>
            </TableCell>
          </TableRow>
        ))}
      </TableBody>
    </Table>
  )
}
```

### Forms

Use `Form` (react-hook-form + zod) for all data entry:

```tsx
'use client'
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { z } from 'zod'
import { Form, FormControl, FormField, FormItem, FormLabel, FormMessage } from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { Button } from '@/components/ui/button'
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select'

const schema = z.object({
  fullName: z.string().min(2, 'Name must be at least 2 characters'),
  email: z.string().email('Enter a valid email'),
  beltLevel: z.enum(['white', 'yellow', 'orange', 'green', 'blue', 'brown', 'black']),
})

type FormValues = z.infer<typeof schema>

export function StudentForm({ onSubmit }: { onSubmit: (values: FormValues) => Promise<void> }) {
  const form = useForm<FormValues>({
    resolver: zodResolver(schema),
    defaultValues: { fullName: '', email: '', beltLevel: 'white' },
  })

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField
          control={form.control}
          name="fullName"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Full Name</FormLabel>
              <FormControl>
                <Input placeholder="Sensei Tanaka" {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />

        <FormField
          control={form.control}
          name="beltLevel"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Belt Level</FormLabel>
              <Select onValueChange={field.onChange} defaultValue={field.value}>
                <FormControl>
                  <SelectTrigger>
                    <SelectValue placeholder="Select belt" />
                  </SelectTrigger>
                </FormControl>
                <SelectContent>
                  {['white','yellow','orange','green','blue','brown','black'].map((belt) => (
                    <SelectItem key={belt} value={belt} className="capitalize">
                      {belt}
                    </SelectItem>
                  ))}
                </SelectContent>
              </Select>
              <FormMessage />
            </FormItem>
          )}
        />

        <Button type="submit" disabled={form.formState.isSubmitting}>
          {form.formState.isSubmitting ? 'Saving...' : 'Save Student'}
        </Button>
      </form>
    </Form>
  )
}
```

### Stat Cards (Dashboard)

```tsx
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'

export function StatCard({
  title,
  value,
  description,
  icon: Icon,
}: {
  title: string
  value: string | number
  description: string
  icon: React.ComponentType<{ className?: string }>
}) {
  return (
    <Card>
      <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
        <CardTitle className="text-sm font-medium">{title}</CardTitle>
        <Icon className="h-4 w-4 text-muted-foreground" />
      </CardHeader>
      <CardContent>
        <div className="text-2xl font-bold">{value}</div>
        <p className="text-xs text-muted-foreground">{description}</p>
      </CardContent>
    </Card>
  )
}
```

---

## 3. Theming

This project uses CSS variables for theming. Define in `app/globals.css`:

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 221.2 83.2% 53.3%;     /* Brand blue */
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 221.2 83.2% 53.3%;
    --radius: 0.5rem;
  }
}
```

---

## 4. Accessibility Rules

- All interactive elements must be keyboard accessible
- Use `asChild` with `Button` to render anchors without wrapping elements
- Never remove focus rings (`outline-none` without a replacement is forbidden)
- Use `aria-label` on icon-only buttons
- Dialogs must trap focus via `DialogContent` (built-in to shadcn)
- Use `FormMessage` to announce validation errors to screen readers

---

## 5. Common Anti-Patterns

| Don't | Do instead |
|-------|-----------|
| `<button className="bg-blue-500 px-4 py-2 ...">` | `<Button variant="default">` |
| `style={{ color: 'red' }}` | `className="text-destructive"` |
| Custom spinner component | `<Loader2 className="animate-spin" />` from lucide-react |
| `onClick` on a `<div>` | `<Button variant="ghost">` |
| Importing from `@radix-ui` directly | Import from `@/components/ui/` |
| `gap-[13px]` | `gap-3` (use the scale) |

---

## 6. Admin Panel Layout Pattern

```tsx
// app/(dashboard)/layout.tsx
import { Sidebar } from '@/components/sidebar'

export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen overflow-hidden">
      <Sidebar />
      <main className="flex-1 overflow-y-auto p-6">
        {children}
      </main>
    </div>
  )
}
```

The sidebar should be a Server Component. Only make it a Client Component if you need active link highlighting with `usePathname()`.
