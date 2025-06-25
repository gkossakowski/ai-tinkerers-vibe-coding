# Input Validation System Documentation

## Overview

The application implements a comprehensive, multi-layered validation system using Zod schemas that ensures data integrity, security, and consistent user experience across all forms and API endpoints. The system provides:

- **Client-side validation**: Real-time form validation with React Hook Form + Zod
- **Server-side validation**: Comprehensive API endpoint security with request sanitization
- **Inline editing validation**: Save-on-blur validation for editable components
- **XSS prevention**: Input sanitization and secure markdown rendering
- **Type safety**: Full TypeScript integration with shared schemas

## How It Works

### Architecture Flow

```
User Input → Client Validation → API Request → Server Validation → Database
    ↓              ↓                ↓              ↓                ↓
Forms/Inline → Zod Schemas → HTTP → Middleware → Sanitized Data
```

The validation system follows a clean separation of concerns:

- **Shared schemas** (`lib/zod-schemas/`) define validation rules once, used everywhere
- **Client components** import schemas for real-time validation feedback
- **API middleware** wraps endpoints with comprehensive security validation
- **Type safety** ensures validated data matches TypeScript interfaces

### Security Layers

1. **Request size limits**: 3MB maximum payload prevents abuse
2. **Content-Type validation**: Only `application/json` accepted for POST/PUT/PATCH
3. **UUID validation**: Path parameters validated as proper v4 UUIDs
4. **Input sanitization**: All strings trimmed, XSS-dangerous content removed
5. **Schema validation**: Structured field-level validation with clear error messages
6. **Markdown security**: User content rendered with whitelist-based ReactMarkdown config

## File Reference

### Core Validation Files

**`lib/zod-schemas/shared-schemas.ts`**

- Pure Zod schemas and validation rules
- Base validators: `uuidSchema`, `emailSchema`, `passwordSchema`, `nameSchema`
- Business logic schemas: `projectDescriptionSchema`, `pitchSchema`, `transcriptSchema`
- API request/response schemas: `createProjectRequestSchema`, `updateProjectRequestSchema`
- Path/query parameter schemas: `pathParamsSchema`, `slugPathParamsSchema`
- TypeScript type exports from schemas using `z.infer<>`

**`lib/zod-schemas/forms.ts`**

- Form-specific extensions of shared schemas
- Enhanced error messages for client-side forms (character overage counts)
- Composite schemas: `projectCreateSchema`, `interviewCreateSchema`, `authSignUpSchema`
- Confirm password validation with cross-field validation

**`lib/validations/api-validation.ts`**

- Server-side validation middleware and utilities
- Core functions: `withValidation()`, `withNextValidation()`, `validateRequestBody()`
- Error handling: `ValidationError`, `RequestSizeError`, `ContentTypeError` classes
- Response utilities: `createErrorResponse()`, `formatValidationError()`
- Convenience wrappers: `withBodyValidation()`, `withParamsValidation()`

### Client-Side Components

**`components/ui/form.tsx`**

- Reusable form components with validation integration
- `FormField`, `FormInput`, `FormTextarea` with error display and styling
- React Hook Form + Zod resolver integration

**`components/ui/editable-input.tsx` & `components/ui/editable-textarea.tsx`**

- Inline editing components with save-on-blur validation
- Optional `validationSchema` prop for Zod validation before save
- Real-time error display and save prevention on validation failure

**`components/security/markdown-security.tsx`**

- `SecureReactMarkdown` wrapper for safe user content rendering
- Whitelist-based approach allowing safe markdown elements
- Blocks dangerous elements: `script`, `style`, `iframe`, `object`, etc.

### API Routes (Examples)

All API routes use validation middleware for comprehensive security:

- **`app/api/projects/route.ts`**: Project creation/listing with query param validation
- **`app/api/projects/[id]/route.ts`**: Project CRUD with UUID path validation
- **`app/api/interviews/route.ts`**: Interview operations with project ID validation
- **`app/api/interviews/[id]/route.ts`**: Interview CRUD with comprehensive validation

## Implementation Summary

### What Was Accomplished

✅ **Comprehensive Schema System**

- 25+ validation schemas covering all forms and API endpoints
- Smart error messages with character overage counts
- Business logic validation (transcript size limits, duration formats)
- Cross-field validation (password confirmation)
- XSS prevention with input sanitization

✅ **Client-Side Validation**

- All forms converted to React Hook Form + Zod resolver pattern
- Real-time validation feedback (validate on blur, show on submit)
- Reusable form components with consistent error styling
- Inline editing with save-on-blur validation and error prevention

✅ **Server-Side Security**

- All API endpoints protected with validation middleware
- Request size limits (3MB) and Content-Type enforcement
- UUID validation for path parameters
- Structured error responses with field-level details
- Input sanitization preventing malicious content

✅ **Security Enhancements**

- User-generated markdown content secured with whitelist approach
- All text inputs sanitized to prevent XSS attacks
- Dangerous HTML/JS content stripped from user input
- Proper Content Security Policy for markdown rendering

### Character Limits & Business Rules

- **Project names**: 100 characters
- **Project descriptions**: 400 characters
- **Collaborators/Participants**: 500 characters
- **Startup pitches**: 2000 characters
- **Interview questions**: 5000 characters
- **Circleback notes**: 10000 characters
- **Transcripts**: 108000 characters (900 chars/min × 120 min max)
- **Passwords**: 8-128 characters with complexity requirements

## Usage Instructions

### Adding New Forms

**Step 1: Define Schema**

```typescript
// lib/zod-schemas/forms.ts
export const myNewFormSchema = z.object({
  name: nameSchema,
  description: projectDescriptionSchema,
  // ... other fields
});

export type MyNewFormData = z.infer<typeof myNewFormSchema>;
```

**Step 2: Create Form Component**

```typescript
// components/my-new-form.tsx
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { FormInput, FormTextarea } from '@/components/ui/form';
import { myNewFormSchema, type MyNewFormData } from '@/lib/zod-schemas/forms';

export function MyNewForm({ onSubmit }: { onSubmit: (data: MyNewFormData) => void }) {
  const form = useForm<MyNewFormData>({
    resolver: zodResolver(myNewFormSchema),
    defaultValues: { name: '', description: '' },
  });

  return (
    <form onSubmit={form.handleSubmit(onSubmit)}>
      <FormInput control={form.control} name="name" label="Name" />
      <FormTextarea control={form.control} name="description" label="Description" />
      <button type="submit">Save</button>
    </form>
  );
}
```

### Adding New API Endpoints

**Step 1: Define API Schema**

```typescript
// lib/zod-schemas/shared-schemas.ts
export const createMyResourceRequestSchema = z.object({
  name: nameSchema,
  description: createTextSchema(1, 500, "Description"),
});

export type CreateMyResourceRequest = z.infer<
  typeof createMyResourceRequestSchema
>;
```

**Step 2: Create API Route**

```typescript
// app/api/my-resource/route.ts
import { withValidation } from "@/lib/validations/api-validation";
import { createMyResourceRequestSchema } from "@/lib/zod-schemas/shared-schemas";

export const POST = withValidation(
  { body: createMyResourceRequestSchema },
  async (request, { validatedBody }) => {
    // validatedBody is fully typed and sanitized
    const { name, description } = validatedBody!;

    // Your business logic here

    return NextResponse.json({ success: true });
  },
);
```

**Step 3: Handle Path Parameters**

```typescript
// app/api/my-resource/[id]/route.ts
import { withNextValidation } from "@/lib/validations/api-validation";
import {
  pathParamsSchema,
  updateMyResourceRequestSchema,
} from "@/lib/zod-schemas/shared-schemas";

export const PUT = withNextValidation(
  {
    params: pathParamsSchema,
    body: updateMyResourceRequestSchema,
  },
  async (request, { validatedParams, validatedBody }) => {
    const { id } = validatedParams!; // Validated UUID
    const updateData = validatedBody!; // Sanitized and validated

    // Your business logic here

    return NextResponse.json({ success: true });
  },
);
```

### Adding Inline Editing

**Example: Project Name Editing**

```typescript
// components/project-overview.tsx (see actual implementation)
import { nameSchema } from '@/lib/zod-schemas/forms';

<EditableInput
  value={project.name || ''}
  onSave={async (value) => {
    await updateProject({ id: project.id, name: value });
  }}
  placeholder="Untitled Project"
  validationSchema={nameSchema} // Validates before save
  isSaving={updateMutation.isPending}
/>
```

### Security Best Practices

**Displaying User Content**

```typescript
// Always use SecureReactMarkdown for user-generated content
import { SecureReactMarkdown } from '@/components/security/markdown-security';

<SecureReactMarkdown>{userGeneratedContent}</SecureReactMarkdown>
```

**API Error Handling**

```typescript
// Use structured error responses
import { createErrorNextResponse } from "@/lib/validations/api-validation";

if (!found) {
  return createErrorNextResponse("Resource not found", 404);
}
```

## What Is Secured

### All User Input Vectors

- ✅ **Form submissions**: All forms validate with Zod before submission
- ✅ **Inline editing**: Save-on-blur validation prevents invalid data
- ✅ **API requests**: All endpoints validate payloads, params, and query strings
- ✅ **File uploads**: Size limits enforced (3MB maximum)
- ✅ **URL parameters**: UUID validation prevents injection attacks

### Data Integrity Protection

- ✅ **Type safety**: Validated data matches TypeScript interfaces
- ✅ **Sanitization**: All string inputs trimmed and XSS-cleaned
- ✅ **Character limits**: Prevents database constraint violations
- ✅ **Format validation**: Email, UUID, duration, slug format enforcement
- ✅ **Business rules**: Transcript size, password complexity, etc.

### XSS Prevention

- ✅ **Input filtering**: Dangerous HTML/JS content stripped from user input
- ✅ **Markdown security**: User content rendered with element whitelist
- ✅ **Safe rendering**: ReactMarkdown configured to block script execution
- ✅ **Content isolation**: User content never executed as code

### API Security

- ✅ **Request validation**: Size limits, Content-Type enforcement
- ✅ **Parameter validation**: Path and query parameters strictly validated
- ✅ **Error handling**: Structured responses prevent information leakage
- ✅ **Authorization**: Validation runs after auth middleware (middleware.ts)

## Example: Complete Project Validation Flow

**Client-Side (Form Creation)**

```typescript
// User fills out AddProjectModal form
// → React Hook Form validates with projectCreateSchema
// → Zod shows real-time validation errors
// → Form submits only if validation passes
```

**Server-Side (API Processing)**

```typescript
// POST /api/projects receives request
// → withValidation middleware validates request size & Content-Type
// → createProjectRequestSchema validates request body
// → Input sanitization trims strings and removes XSS content
// → Database receives clean, validated data
```

**Inline Editing (Updates)**

```typescript
// User edits project name in EditableInput
// → nameSchema validates on save attempt
// → Validation error shows if invalid (e.g., too long)
// → PUT /api/projects/[id] validates UUID and body
// → Database updated with validated data
```

## Future Improvements

The current validation system provides comprehensive security for the application's current scope. Future enhancements could include:

### Enhanced Type Safety

- Advanced type utilities bridging Zod schemas with TypeScript
- Runtime type guards for complex data structures
- Enhanced Supabase type integration and compatibility checking
- Automatic type generation from database schema

### Comprehensive Testing

- Unit tests for all validation schemas and edge cases
- Integration tests for API endpoint security
- End-to-end testing of form validation flows
- Accessibility testing for error states and screen readers

### Advanced Validation Features

- Conditional validation based on user roles or feature flags
- File upload validation with type checking and virus scanning
- Rate limiting integration with validation middleware
- Advanced query parameter validation for complex search/filter APIs

### Performance Optimizations

- Schema compilation caching for frequently used validators
- Lazy loading of validation schemas for better bundle size
- Optimized error message generation for better UX
- Advanced TanStack Query integration with validation-aware error handling

These improvements would be valuable for production-scale applications but represent over-engineering for the current project stage.
